---
title: 'Azure Quickstart Guide'
date: 2017-03-30
permalink: /posts/2017/03/Azure Quickstart Guide/
tags:
  - azure
  - vm
  - instances
  - guide
  - cloud computing
  - gpu
---

Hi everyone! In this post I will explain how to <a href="#create">create a VM instance</a>, 
how to <a href="#connect">connect</a> to it and how to <a href="#send">send files</a> to 
and from it, using <a href="https://azure.microsoft.com/">Microsoft Azure</a>.

<h2 id="create">Create a Virtual Machine</h2>

1. Click on **+** (New)

    <p align="center"><img src="https://dl.dropboxusercontent.com/s/um6tmjwe8zi9bao/new.png?dl=0" alt="new"/></p>
    
2. Choose **Ubuntu Server 16.04 LTS** from the **Compute** menu.
    
    <p align="center"><img src="https://dl.dropboxusercontent.com/s/bd1ultihxuyzlwb/ubuntu-server.png?dl=0" alt="ubuntu server"/></p>

3. Select **Resource Manager** as **Deployment Model** and click **Create**.

    <p align="center"><img src="https://dl.dropboxusercontent.com/s/c5bnsfcdawgth98/resource-manager.png?dl=0" alt="resource manager"/></p>

4. In the **Basic Settings** select a **Name** for the instance, the **disk type** (HDD for
more choice), a **username**, the **authentication type**, the **name of the resource group**
and the **location of the server** (some instances are available only on some servers, e.g.
NC series is not available in Europe at the time of writing this post). Once you're done, 
click on **OK**.

    <p align="center"><img src="https://dl.dropboxusercontent.com/s/og3misgx4kefiuv/basics.png?dl=0" alt="basics"/></p>

    On the **authentication type**: 
    - if you choose SSH, you can generate your key with
    ssh-keygen on Mac OS X and Linux or PuTTYGen on Windows; 
    - if you choose Password, it must contain 3 of the following: lowercase letter, 
    uppercase letter, number, special character. It must be also between 12 and 72 characters.

5. Choose your **virtual machine size** in the **Size settings**. Click on **View all** to
have more choice. In West Europe, for the subscription I'm using, the instances with one or
more graphic cards are **NV6** and **NV12**. It's visible in the specific, for example for
NV6 it's specified **1xM60 Graphics**, meaning that this instance has a NVIDIA Tesla M60 GPU.
Click on your choice and on **Select**

    <p align="center"><img src="https://dl.dropboxusercontent.com/s/ua4m2t5qzj0cnaq/machine-size.png?dl=0" alt="machine size"/></p>
    
6. On **Settings** leave everything on default and click on **Ok**

    <p align="center"><img src="https://dl.dropboxusercontent.com/s/j3q92rui7xabk0d/settings.png?dl=0" alt="settings"/></p>

7. Check that **Validation is passed** and confirm the creation by clicking **Ok** and wait
for the deployment of the model (it takes some time usually).
    
<h2 id="connect">Connect to the Virtual Machine</h2>

1. Go on **Resource Groups** (1), click on your **newly created one** (2) and on the **VM
instance** (3).

    <p align="center"><img src="https://dl.dropboxusercontent.com/s/zj1ddoyw07c5ftc/vm-instance.png?dl=0" alt="vm instance"/></p>

2. Click on **Connect** to see the command to connect to the machine. Copy it in the
terminal. You will be asked the password or the SSH key, enter it and you are in!

    **Remark**: you may be asked to add the IP as an authenticated address, type **yes** to confirm.

    <p align="center"><img src="https://dl.dropboxusercontent.com/s/j59qwhzvf1hl30l/ssh-command.png?dl=0" alt="ssh command"/></p>

    You will be prompted to something like this:
    
    <p align="center"><img src="https://dl.dropboxusercontent.com/s/zpe7v3vbi177ts2/ssh-prompt.png?dl=0" alt="ssh prompt"/></p>

<h2 id="send">Send files to and from the Virtual Machine</h2>

<h3> Send files to the VM</h3>

1. You have a command of the form `ssh <username>@<IPaddress>` to enter the VM. You just need to
navigate on your local machine to the location of the file you want to send and type

    `scp <filename> <username>@<IPaddress>:/home/<username>`
    
    If you want to send an entire repository, add the **recursive** option
    
    `scp -r <filename> <username>@<IPaddress>:/home/<username>`
    
    You will be asked to enter your password or SSH key.
    
    If for example I want to copy a repository called *test* on a machine at the IP address 1.1.1.1,
    where my username is *iacolippo*, the command will be
    
    `scp -r test iacolippo@1.1.1.1:/home/iacolippo`

<h3> Send files from the VM</h3>

1. You need again to use `scp`. The first argument is the path to the file on the remote
machine, the second argument is the relative path where you want to copy the file on your 
local machine.

    `scp <username>@<IPaddress>:/home/<username>/path/to/file local/path/where/I/want/to/copy`

    For example, if I want to copy something a file called *awesome-model.py* in the folder
    *DL* on the remote machine to my local folder *awesomeness*:
    
    `scp iacolippo@1.1.1.1:/home/iacolippo/DL/awesome-model.py awesomeness`
    
    You can use the recursive option for folders also in this case.



#### Footnote
<sub>This post is slightly changed from a guide written by my colleague 
<a href="https://www.linkedin.com/in/clément-gastaud-ab2a3298/">C. Gastaud</a>
at <a href="http://www.lighton.io">LightOn</a>.</sub>
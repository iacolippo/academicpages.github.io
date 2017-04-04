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

Hi everyone! In this post I will explain how to create a VM instance on the cloud using
from the Microsoft Azure Dashboard.

<h2>Create a Virtual Machine</h2>

1. Click on **+** (New)

    <p align="center"><img src="https://iacolippo.github.io/files/azure-quickstart-guide-img/new.png" alt="new"/></p>
    
2. Choose **Ubuntu Server 16.04 LTS** from the **Compute** menu.
    
    <p align="center"><img src="https://iacolippo.github.io/files/azure-quickstart-guide-img/ubuntu-server.png" alt="ubuntu server"/></p>

3. Select **Resource Manager** as **Deployment Model** and click **Create**.

    <p align="center"><img src="https://iacolippo.github.io/files/azure-quickstart-guide-img/resource-manager.png" alt="resource manager"/></p>

4. In the **Basic Settings** select a **Name** for the instance, the **disk type** (HDD for
more choice), a **username**, the **authentication type**, the **name of the resource group**
and the **location of the server** (some instances are available only on some servers, e.g.
NC series is not available in Europe at the time of writing this post). Once you're done, 
click on **OK**.

    <p align="center"><img src="https://iacolippo.github.io/files/azure-quickstart-guide-img/basics.png" alt="basics"/></p>

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

    <p align="center"><img src="https://iacolippo.github.io/files/azure-quickstart-guide-img/machine-size.png" alt="machine size"/></p>
    
6. On **Settings** leave everything on default and click on **Ok**

    <p align="center"><img src="https://iacolippo.github.io/files/azure-quickstart-guide-img/settings.png" alt="settings"/></p>

7. Check that **Validation is passed** and confirm the creation by clicking **Ok** and wait
for the deployment of the model (it takes some time usually).

    <p align="center"><img src="" alt="validation"/></p>
    
<h2>Connect to the Virtual Machine</h2>

1. 

2.

3.

4.

5.

<h2>Send files to and from the Virtual Machine</h2>

1.

2.

3.

4.

#### Footnote TODO: ADD LINKEDIN LINK
This post is slightly changed from a guide written by my colleague <a href="#">C. Gastaud</a>
at <a href="http://www.lighton.io">LightOn</a>
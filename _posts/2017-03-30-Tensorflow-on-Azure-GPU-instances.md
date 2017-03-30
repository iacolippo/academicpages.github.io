---
title: 'How to run Tensorflow and other DL frameworks on Azure GPU instances'
date: 2017-03-30
permalink: /posts/2017/03/Tensorflow-on-Azure-GPU-instances/
tags:
  - tensorflow
  - azure
  - gpu
  - cuda
---

If you can't get your code in your favorite DL framework to run on GPUs on Azure, you're
in the right place. What follows is the extensive guide you're looking for, result of 
direct experience and pain, a lot of pain.

In the following we assume the install is for an **Ubuntu Server 16.04 LTS** virtual 
machine with a graphic card (e.g. NV6, NV12, NC6, NC12). It's pretty straightforward that
you can't run code on a GPU, if you don't have it =)

You can check that you have available NVIDIA hardware by entering in the terminal:

`lspci | grep -i nvidia`

The output should be something like:

(example from NV6)

CUDA INSTALL
======

NVIDIA® CUDA® Toolkit is *a comprehensive development environment for C and C++ 
developers building GPU-accelerated applications*.

Download and scp the installation package
------

Download CUDA 8.0 deb package for your system frome [here](https://developer.nvidia.com/cuda-downloads).

You have to select:
- operating system
- architecture
- distribution
- version
- installer type

The correct choices are:
- OS: Linux
- architecture: x86_64 (you can check it by entering `uname -m` in the terminal)
- distribution: Ubuntu
- version: 16.04

For the **installer type**, I recommend **deb(network)**. It's fast to download and fast 
to scp to the remote machine. The *deb(local)* version is 1.8GB, vs 2.6K of the network one.

Now you can transfer this file from your local machine to the remote machine. Navigate
to the directory where the file is (using `cd`).
To transfer files to the remote, we will use `scp`, a command which works like this:

`scp <local-path-to-the-file-to-transfer> <remote-machine-address>`

The Azure portal gives you an SSH command to connect to the machine, which is something like:

`ssh [username]@[ipaddress]`

Take the second part, append `:/home/lighton/` and enter in the terminal:

`scp cuda-repo-ubuntu1604_8.0.61-1_amd64.deb [username]@[ipaddress]:/home/[username]/`

Where `[username]` and `[ipaddress]` are YOUR USERNAME and YOUR IP ADDRESS. You will now 
find your file in the home directory of the remote machine. You're ready to ssh into your
remote machine and start with the install:

`ssh [username]@[ipaddress]`

Install
------

1. First, to build CUDA you need **gcc**, which is not installed by default, so:

    `sudo apt install gcc`

2. Just to be sure we have the correct kernel headers:

    `sudo apt-get install linux-headers-$(uname -r)`

    This passage is sometimes needed, sometimes useless. Misteries of computer science.

3. Install the package

    ```bash
    sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb
    sudo apt-get update
    sudo apt-get install cuda
    ```
4. Add `/usr/local/cuda-8.0/bin` to `PATH` environment variable in `.profile` in home 
directory using `nano` or `vim`:

    `nano .profile`

    Append `:/usr/local/cuda-8.0/bin` to the content of the path variable, like from

    `PATH="$HOME/bin:$HOME/.local/bin:$PATH"`

    to

    `PATH="$HOME/bin:$HOME/.local/bin:$PATH:/usr/local/cuda-8.0/bin"`

5. Add `/usr/local/cuda-8.0/lib64` to `LD_LIBRARY_PATH` variable in `.profile`. If such 
variable doesn't exist, create it.

    `LD_LIBRARY_PATH="/usr/local/cuda-8.0/lib64"`

    To save in `nano`: Ctrl+X, Y, Enter.

6. Activate the changes using:

    `source .profile`

7. To make them effective, reboot the machine:

    `sudo reboot`

**Greetings dear reader, you have installed CUDA!**

CUDNN INSTALL
======

NVIDIA cuDNN is  *a GPU-accelerated library of primitives for deep neural networks*.

Download and scp the installation package
------

Download CUDNN 5.1 for CUDA 8.0 Linux from [here](). You may have to subscribe and wait to 
get accepted, but it's usually a quite fast process. Once logged in you have to agree to 
the cuDNN Software License Agreement. Now you can download **cuDNN v5.1 Library for Linux**
(update for cuDNN v6.0 coming soon...). It's a tar file of around 147MB.

As for CUDA deb file, transfer the cuDNN tar file to the remote machine through scp:

`scp cudnn-8.0-linux-x64-v5.1.tar [username]@[ipaddress]:/home/[username]/` 

Reconnect via SSH, we're going to install things! 

Install
------

1. extract the files from the tarball and enter in the cuda directory

    ```bash
    tar -xvf cudnn-8.0-linux-x64-v5.1.tar
    cd cuda
    ```
    
2. create symbolic links

    ```bash
    sudo cp -P include/cudnn.h /usr/include/
    sudo cp -P lib64/libcudnn* /usr/lib/x86_64-linux-gnu/
    ```
    
3. set permissions

    `sudo chmod a+r /usr/lib/x86_64-linux-gnu/libcudnn*`


**Aaaaand you have installed cuDNN!**

WHICH DL FRAMEWORK DO YOU WANT TO INSTALL?
======

|               |       |       |       |
| :-------------: | :-----: | :-----: | :-----: |
| <a href="#tensorflow">Tensorflow</a>  | <a href="#torch">Torch</a> | <a href="#theano">Theano</a>| <a href="#keras">Keras</a> |

Remember, if you don't have `pip` installed, you can get it using

`sudo apt-get install python-pip`

<span id="tensorflow">TENSORFLOW INSTALL AND CHECK</span>
------

1. You have to install another cuda library and the GPU-enabled version of tensorflow: 

    ```bash
    sudo apt-get install libcupti-dev
    sudo pip install tensorflow-gpu
    ```
    
2. check that GPU is being used running this python script:

    ```python 
    import tensorflow as tf

    # Creates a graph.
    with tf.device('/gpu:0'):a = tf.constant([1.0, 2.0, 3.0, 4.0, 5.0, 6.0], shape=[2, 3], name='a')
        b = tf.constant([1.0, 2.0, 3.0, 4.0, 5.0, 6.0], shape=[3, 2], name='b')
        c = tf.matmul(a, b)
    # Creates a session with log_device_placement set to True.
    sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))
    # Runs the op.
    print sess.run(c)
    ```
    
Now everytime you run a tensorflow script, it should be executed automatically on gpu, 
without modifying the code. To check on which device the code is being executed, run the 
session with option `log_device_placement=True`:

`sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))`

<span id="torch">TORCH INSTALL AND CHECK</span>
------

<span id="theano">THEANO INSTALL AND CHECK</span>
------

<span id="keras">KERAS INSTALL AND CHECK</span>
------

1. Install `keras`

    `sudo pip install keras`
    
2. If you are running on the TensorFlow backend, your code will automatically run on GPU 
if any available GPU is detected.

3. If you are running on the Theano backend, you can setup your .theanorc as in <a href="#theano">Theano
instructions</a>.



#### Footnote
This post is adapted from my [github repository](https://github.com/iacolippo/gpu-dnn-install)
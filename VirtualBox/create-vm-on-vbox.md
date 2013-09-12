Create a Base Virtual Machine in VirtualBox
===========================================

This document explains how to create a small virtual machine (VM) in VirtualBox to serve as the foundation for LAMP and LEMP clones. Building a base VM with just a clean, current version of the operating system gives you an easier option for creating new VMs and an simpler recovery path if your run into problems setting up a clone VM and need to reset to a clean starter. While this example walks through setting up an Ubuntu Server VM, but the same basic process applies for any guest operating system.

You'll need an Ubuntu install ISO, so go to http://www.ubuntu.com/download/server and choose an Ubuntu version. For the example, I'll be using Ubuntu 13.04 64-bit. You can download it directly from http://releases.ubuntu.com/13.04/ubuntu-13.04-server-amd64.iso or the 32-bit version from http://releases.ubuntu.com/13.04/ubuntu-13.04-server-i386.iso if you prefer. Download the ISO image and save it to your hard drive.

While it's downloading, let's create the VM we'll install it on.

Start the VirtualBox Manager program. For Windows, you may have an icon on your desktop or an item in the start menu. Other platforms will vary.

Before creating a VM, see *Choosing Virtual Machine Location in VirtualBox* and choose a location that works for you.

Click the New option on the toolbar. 

On the Name and Operating System page, give the VM a name that makes sense. For example, I'm going to setup an Ubuntu Server 13.04 base VM, so I'll name the VM `US1304-Base`. Choose "Linux" from the Type drop-down and "Ubuntu" or "Ubuntu (64 bit)" from the Version drop-down. Click Next.

On the Memory size page, define how much memory the VM can use. For development web server VMs, 1-1.5MB should be enough. You can use the slide bar or enter a number in the box. Click Next.

On the Hard drive page, choose Create a virutal hard drive now and click Create. Unless you want the virtual disk to be readable by VMWare, QEMU, or some other virtualization platform, choose VDI and click Next. I recommend setting the virutal disk to be fixed size. This improves performance and avoids the risk of running out of disk space unexpectedly mid-processing. Finally, specify the size of the virtual disk. For a basic development LAMP or LEMP server, 5GB is plenty. If you want the virtual disk files to be created in a location other than the VM folder, pick the directory. I recommend keeping everything together for easier moves if needed. Click Create. VirtualBox will allocate disk space. For a 5GB disk, this will take a minute or two depending on your computer.

When the virtual disk finishes creating, you'll see your new VM in the list of VMs in VirtualBox and general information about your VM on the right.

Now, it's time to install Ubuntu on the VM.

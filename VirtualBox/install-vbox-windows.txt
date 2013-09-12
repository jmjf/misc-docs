Install VirtualBox on Windows
=============================

VirtualBox lets you create virtual machines (VMs). With a VM, you can install Linux, Windows, or another operating system on the VM and use it without changing your computer's actual operating system and use both the physical machine and the VM at the same time. In my case, I run Linux virtual machines on Windows as web servers for web development testing.

In virtual machine speak, the host machine is the physical machine and the guest is the virtual machine. The host machine hosts the guest operating system in a virtual machine. So if you have a Windows computer and want to run a Linux virtual machine, you have a Windows host and a Linux guest. If you have a Windows 7 machine and want to run a Windows 8 virtual machine, you have a Windows 7 host and a Windows 8 guest.

VirtualBox is available for Windows, OS X, Linux, and Solaris hosts.

This document covers Windows hosts. Mac users will get a dmg file and need to install that. Files will probably be located in different directories than files for Windows. Linux users get a page listing install packages for different Linux distros. Pick, the appropriate installer package and use standard install procedure to install the package or check your distro's repository. They probably have a VirtualBox package available. Again, directories will probably not match Windows directories.

Detailed install instructions for different host operating systems are available at https://www.virtualbox.org/manual/ch02.html.

Go to https://www.virtualbox.org/wiki/Downloads. Download the appropriate VirtualBox package for Windows. If you have a 64-bit operating system, use the amd64 package if available (even if your CPU is Intel). If you aren't sure, use the x86 package.

Run the installer that downloads.

VirtualBox creates folders and files for each virtual machine including files for the VM's virtual disk. By default, VirtualBox for Windows creates the VM files in the  Users/username directory. I prefer to keep the VM files elsewhere. To change the default VM location, start VirtualBox. Go to File, Preferences and select the General item in the Settings dialog. Change the default machine folder to the directory of your choice. For example, I changed mine to d:\web\vm.
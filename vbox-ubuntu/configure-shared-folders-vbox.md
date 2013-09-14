Configure Shared Folders in VirtualBox
======================================

## Introduction
Shared folders make one or more host directories available in the guest VM. I'm developing WordPress, so my content replaces /var/www. I define a shared folder for www in my base VM, then edit it in any clones to point to the appropriate subdirectory. I also define a shared folder to exchange files between the host and guest so I can keep /var/www clean. This folder is the same for all VMs, which gives me an easy way to move files between VMs.

You can define shared folders while the VM is running, but I prefer to shut it down first. VMs usually won't recognize shared folders without a reboot.

## Define the Exchange Shared Folder
In the VirtualBox Manager in your host, select the base VM and click the Settings icon in the toolbar. Select the Shared Folders item.

On the right side of the window, click the +(folder) icon to add a folder. 

Enter the folder path. For example, I share D:\web\xfer as my exchange folder, so I'd enter D:\web\xfer for my folder path. I usually pick the path from the drop-down Other option because VirtualBox isn't exactly smart about typed path names and tries to insert extra backslashes. 

Assign the shared folder a name. This is the name the VM will use to mount the shared folder. I typically call it xfer (the default). It doesn't make much sense to make this folder read-only, and auto-mount mounts the shared folders in /media where I (mostly out of habit) prefer to mount to a mount point in /mnt where I can rely on the name and path of the mounted folder. Your mileage may vary. Click OK when done.

You'll see there's now a shared folder named xfer with path d:\web\xfer (or whatever you chose) in the Folders List.

## Define the www Shared Folder
Follow the same procedure to create the www shared folder. In my setup, I have d:\web\www with subdirectories for different projects under www. I mount www to a shared folder named www in the base VM so I can configure the mount points and mount commands correctly. When I edit the shared folder to point to d:\web\www\xyz-project, VirtualBox will change the shared folder name to xyz-project. I change it back to www and all my prebuilt mount code works with no other changes.

When done configuring shared folders, click OK.


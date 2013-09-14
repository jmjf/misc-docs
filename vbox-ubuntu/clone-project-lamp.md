Clone a Project LAMP Server from the Base LAMP Server
=====================================================

## Introduction
I could use a single LAMP server VM for different projects and edit the shared folder information each time I need to change it. Or, for a little disk space cost, I can give each project it's own VM, set the shared folder once, and forget it. I'm lazy, so I choose the latter approach.

We're going to use linked clones in VirtualBox. A linked clone uses the parent's virtual disk and a local difference log to produce the appearance of a separate virtual disk. 

If I were making a lot of changes to the project clone's disk, it would make sense to create a full clone with it's own virtual disk. The way I'm configuring my setup, I don't make many changes to the project clone, so I don't need the overhead of a full disk copy. Project archives are smaller too.

Another advantage of a linked clone is that updates happen on the parent--the base LAMP server. Updating one VM brings all my projects up-to-date, and changes on that one VM can propogate to all the project clones.

If I run into a situation where I think the MySQL database for a given project will be huge (the client has a million pages of content), I can always do a full clone for better performance. Then again, if the project is that big, I probably won't be working on it alone, so I'll set up a physical development server or a development VM on a physical server so multiple people can edit content at once.

## Create the Project Clone
I'll be creating a clone for the XYZ project. What you call the VM, the project folder, or even how you organize your projects on disk isn't particularly significant to this process as long as you can sort your projects out, have a folder for the project's www directory, and can find it to map the shared folder to it.

Before creating the clone, create a project folder in your local work directory. For example, /web/www/xyz.

In VirtualBox Manager on my host machine, select US1304-LAMPBase (my base LAMP server). From the menu, select Clone. 

Give the clone a name, for example, US1304-XYZ-LAMP. I like to designate the server stack in the VM name so I don't have to trust my memory. Also, it may be necessary to test the configuration on both LAMP and LEMP servers. Putting the server stack in the VM name makes it easier to sort out which is which.

Check "Reinitialize the MAC address...". Click Next.

Chose to create a Linked clone. Click Clone. The cloning process will take a few seconds because VirtualBox doesn't have to copy the 5GB virtual disk file.

## Configure the Project Clone
Start the project clone. As before, initial boot will take a while because the network connection has to fail completely. When the VM comes up, login and run fix-config.sh with the new hostname as a parameter. For example `sudo ./fix-config.sh XYZ-LAMP`.

After reboot, point your web browser to the project clone's IP address. Verify you get the "It works!" page. Also check PHP and that the phpMyAdmin login screen comes up.

Shutdown the project clone with `sudo shutdown -hP now`.

Select the project clone in the VirtualBox Manager and click Settings in the toolbar. Choose Shared Folders from the list of option sets, select the www shared folder, and click the edit icon (folder with a circle on it). Change the shared folder to point to the project directory. For example, \web\www\xyz.

VirtualBox will change the default shared folder name to match the project folder name. We don't want this because it will break our mount configuration in the VM. So change Folder Name back to www. 

Click OK. Click OK again. Start the project clone.

Login to the project clone. Check the contents of /mnt/www with `ls /mnt/www`. The contents should match your host-side project folder's contents.

## Next Steps
At this point, you're ready to install WordPress. Because the project clone's www folder is on your host machine, you can unzip and configure WordPress on your host machine. Use phpMyAdmin on the project clone to set up a database. Point your browser to the project clone's IP address, and do the famous five minute install and you're ready to go.

I'm assuming anyone developing with Roots knows how to install WordPress.

Future installments will look at options for setting up a WordPress-Skeleton based development server, integrating git into your workflow, etc.




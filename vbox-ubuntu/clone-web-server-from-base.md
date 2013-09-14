Clone a Base Web Server from the Base Virtual Machine
=====================================================

## Introduction
We put a lot of effort into configuring the base virtual machine for a reason. Once we have a solid foundation, we can clone it to make base Apache and Nginx web servers that we can then clone (linked) to develop different clients' sites. We'll get to linked cloning later.

Why would we need both Apache (LAMP) and Nginx (LEMP)? Some clients will use a virtual private server (VPS) or other hosting that lets them choose their server configuration including web server (Apache or Nginx). Other clients may choose to use shared hosting or other options where they have no choice about web server. Extremely cautious developers may want to become familiar with different Linux distros so they can set up a Linux VM that runs on the same version of Linux as their client's target environment.

For my purposes, I'm proposing that the differences in Linux distributions, while not insignificant, are less likely to affect a web developer--especially a WordPress developer--than the differences between Apache and Nginx. I suspect that the differences between Apache and Nginx for my purposes are also small, but I want to learn more about Nginx anyway, so this will be a good opportunity. I'll stick with Ubuntu for two reasons. First, as stated, I doubt the Linux differences are that significant to WordPress. Second, I tried to set up CentOS once and was pulling my hair out trying to find good instructions for installing packages.

If you do choose to set up different base web servers using different versions of Linux, I recommend following a similar approach--establish a working base, clone it to make LAMP and LEMP bases, then clone those bases for different clients.

## Cloning
Cloning a VM in VirtualBox is fairly simple. First, shut down the VM. From the command line

    sudo shutdown -hP now

You can shut down the VM from the menus, but letting Linux shut down is politer to the OS.

Select the VM you want to clone from the list of VMs. From the Machine menu, choose Clone.

Name the clone. In this case, I'm going to call it US1304-LAMPBase because it will become my base for Apache VMs. For the LEMP base, I'd call it US1304-LEMPBase.

Check the "Reinitialize the MAC address" option. The MAC address uniquely identifies the VM's virutal network adapter to the network. If it's the same as another running VM, there will be problems. Always reinitializing the MAC ensures your VMs can coexist peacefully.

For our LAMP (and LEMP) base, we're going to make a full clone. Linked clones share their parent VM's disk and track differences. We'll be doing linked clones for individual client VMs, so doing a full clone for the base LAMP/LEMP servers reduces the linking overhead. Since my base server only has a 5GB disk, two additional 5GB virtual disks isn't that much disk space on a modern hard drive. Linked clones for clients lets me avoid having dozens of 5GB virtual disk clones.

So choose full clone and click Clone. VirtualBox will start cloning the VM. It will take 5-10 minutes depending on the size of the virtual disk being cloned, hard drive performance, etc.

## Cleaning Up the Clone
When the clone is complete, you'll have a new VM in your list of VMs in VirtualBox. We aren't done yet, though.

Start the cloned VM. Be patient--the network setup has to fail because the MAC while Ubuntu wasn't looking. Login to the VM. The username and password will be the same as the base VM.

You should see the fix-clone.sh script in your directory. Use `ls` to verify it's there. If not, either you didn't put it in your base machine or something about your clone has gone awry.

Run the fix-clone script. Remember to pass the new hostname for the cloned host.

    sudo ./fix-clone.sh US1304-LAMPBase

The script should run and reboot the VM. When the VM reboots, it should come up faster because it will discover the correct MAC address and the network connection will succeed. If not, something is wrong with the fix-clone script. Check it out and fix it. (Note that shared host folders don't rely on the network connection, so you can use the /mnt/xfer folder to transfer files between host and guest if you need to edit the file. Be sure your text editor is using Unix/Linux/OSX end-of-line. Linux shells don't like scripts with extra carriage-returns.)

Now you're ready to install the AMP stack on your LAMP base server.


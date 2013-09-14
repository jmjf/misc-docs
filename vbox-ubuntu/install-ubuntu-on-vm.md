Install Ubuntu Server on the Base Virtual Machine
=================================================

**Settings, Settings, Settings**
After creating a virtual machine, select the VM and click Settings in the toolbar or right-mouse on the VM entry in the list of VMs and choose Settings. Choose System in the list of settings. In the Boot Order group, uncheck Floppy. Make sure CD/DVD-ROM is first in the boot order. Use the up and down arrow buttons on the right of the Boot Order list to move entries up and down as needed.

Choose Storage in the list of settings. Click on Controller: IDE and choose the + icon with a single circle under it to add a CD image. VirtualBox will ask if you'd like to choose a virtual CD/DVD disk. Click Choose disk. Navigate to Ubuntu Server ISO image you downloaded in **Create a Base Virtual Machine in VirtualBox** and choose it. Click Open to finish creating the virtual CD. You should now see an entry under Controller: IDE for the Ubuntu image you selected.

There is much debate about how best to set up virtual networks for VMs. For development, I prefer to use bridged connections. That lets me expose the VM to other devices on my local network--like a phone or tablet I might use to test a responsive web site design.

To configure bridged networking, choose Network in the list of settings. For Adapter 1, in the "Attached to" drop-down, choose Bridged Adapter. For "Name" choose the appropriate network adapter on your machine. If you have both wired and wireless network adapters, you may want to setup Adapter 1 as wired and Adapter 2 as wireless (and bridged).

Click OK to accept settings. Information on the virtual machine detail on the right will change to reflect the newly mounted CD image and other changes.

**Get This VM Started**
Finally, select the VM and click Start in the toolbar or right-mouse on the VM entry in the list of VMs and choose Start.

The VM will boot and ask you to choose a language. Pick whichever you prefer. From the menu (text menu, not drop-down) select Install Ubuntu Server. Use arrow keys and tab to navigate the menus throughout the install process.

The installer asks for a language. This is the language the operating system will use as its base language for localization. Pick whichever is appropriate. On the next screen, select your country, etc. For "Configure the keyboard" select No and pick your keyboard from the list. Ubuntu makes a guess based on your language choice. Usually the other likely suspects are near that guess. Finally, choose your keyboard layout. Again, Ubuntu guesses based on your earlier choices, but if you prefer an English Dvorak alternative international no dead keys layout to QWERTY, it's there with over a dozen others.

After you select the keyboard layout, the installer will run for a minute and ask you to configure the network. Usually, you want eth0 as your primary network interface. After selecting, the install will progress for a while.

The installer will ask for a hostname. You'll override this in clones, but I like to match hostname to the VM name, so I'll type US1304-Base and hit enter. Enter whatever you like for the user full name--Edogawa Conan, Tecumseh, or your real name--and hit enter. For username (the name you'll type to login), pick something. For development VMs, I'm usually not too worried about security, so favor short and simple. Hit enter after typing your choice. Enter your password twice. Again, for development I'm not too concerned about security. This runs on my local machine. The chances anyone else will be able to access this are slim. Finally, there's probably no need to encrypt your home directory, so choose No.

The installer chugs for a few seconds and asks you to verify your time zone. If it's wrong, select No and pick the correct time zone. Otherwise, select Yes.

Next stop will be disk partitioning. Ubuntu Server likes logical volumes managed by LVM. We don't need that. Choose "Guided - use entire disk" and hit enter. Pick the disk to partition (there's only one). And write the partitions to disk--which requires you to choose Yes. The default is No.

Finally the installer starts actually installing stuff. Sit back and wait a while.

If you use an HTTP proxy to connect to the Internet, you'll need to enter that information when asked. Otherwise, just hit enter.

The installer configures for a few seconds and starts retrieving files for apt, the package manager. Then it starts installing software. Lots of software.

If you want automatic security updates, choose that option. I prefer to do updates manually.

On the software selection screen, don't choose any of the options listed. We want this to be a clean base machine. We'll install LAMP or LEMP stacks as needed on clones of this machine. This is a small, development web server. We don't need a lot of overhead. Hit Tab to jump to Continue, then hit enter. Watch as more software is selected and installed.

Several minutes of installing and configuring later, the installer is ready to install GRUB into the master boot record (of the virtual disk). Select Yes.

When GRUB finishes installing, you'll get an Installation complete message. You can't easily eject the ISO, so just select Continue. After a little cleanup, the VM will reboot. You'll briefly see a menu that you can use to select various utility functions if needed. Ubuntu will boot up and present you with the login prompt in all it's glory.

`US1304-Base login:`

Enter your user name--the login one, not the full name one. Hit enter. Enter your password and hit enter. Above the command prompt you'll see how horribly out of date your software already is.

Now it's time to install updates and set up a script that will fix things that break when we clone a VM and assign it a new host name.

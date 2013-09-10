Installing a Apache, PHP5, and MySQL on Ubuntu
==============================================

Falko Timme's instructions at http://www.howtoforge.com/installing-apache2-with-php5-and-mysql-support-on-ubuntu-13.04-lamp works as a general solution for Ubuntu Server 13.04 with a couple of adjustments.

Falko uses the legacy init.d approach for restarting services (apache2). Ubuntu 13.04 uses Upstart, not init.d, so in Falko's instructions, replace `/etc/init.d/apache2 restart` with `service apache2 restart` for Ubuntu 13.04.

I prefer to replace /var/www with a symbolic link to another directory. I'm using virtual machines to run Linux AMP/EMP servers on my Windows machine for web development. Rather than rely on the VM's disk to store the site code, I keep the site code on Windows and use a shared folder in the VM to make the directory available to the AMP/EMP server. It's easier to link /var/www to the shared folder's mount than to set up Samba on Linux and share a folder. (Even on my physical Linux machine, I link /var/www because it lets me relocate the site files off the root partition, keeping the operating system and application core separate from the data.)

On my Windows host, I have a development directory. In that directory, the www subdirectory contains all web site development work. Different folders represent different sites or projects. I set up a default share named www in my base VM pointing to the www subdirectory on my Windows host. For each cloned server, I edit the www share to point to the appropriate subdirectory within the host's www directory.

I set up everything in my base VM for web servers before I install Apache or Nginx. The only thing I have to change on a clone is the actual subdirectory shared (defined in VirtualBox, etc., not Linux.)
`sudo mkdir /mnt/www`

I make the mount point writable to group and assigned to group www-data, the Apache server's group.
`sudo chmod g+w /mnt/www`
`sudo chgrp /mnt/www www-data`

Then I test mounting the shared folder. (I'm using VirtualBox. If you're using a VMWare Player, replace vboxsf with *WHAT*.
`sudo mount -t vboxsf www /mnt/www`

And do a simple test. If there is a file in the host folder I mounted, I should see it listed.
`ls /mnt/www`

Now that the mount is created and working, I link /var/www to it. WARNING: The following will delete all files in /var/www. If you've just installed Apache, all you're losing is the default index.html. If you have anything that matters there, copy it somewhere save before running these commands.
`sudo rm -R /var/www/*`
`sudo rmdir -R /var/www`
`sudo ln -s /mnt/www /var/www`

The mount doesn't run automatically on boot, so I add the mount information to /etc/fstab. Edit /etc/fstab with your editor of choice. NOTE: You must use sudo or be root/su to edit /etc/fstab. DO NOT change any existing mount lines unless you need to add a newline after the last line. Add the following line at the end of the file and save the file.
`www /mnt/www vboxsf`

Reboot.
`sudo reboot`

After reboot, you should be able to run the following and see whatever is in the host's shared folder.
`ls /mnt/www`
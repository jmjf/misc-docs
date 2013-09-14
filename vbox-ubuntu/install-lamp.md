Install Apache, PHP5, and MySQL on the Base Web Server
======================================================

## References
A couple of online sources have basic Ubuntu LAMP install instructions that may be worth refering to during the process. Falko Timme's instructions at http://www.howtoforge.com/installing-apache2-with-php5-and-mysql-support-on-ubuntu-13.04-lamp work as a general solution for installing LAMP on Ubuntu Server 13.04. Sourav K's instructions at http://www.wpexplorer.com/locally-install-wordpress-on-ubuntu/ narrow parts of the install to focus on what's required for WordPress. (Falko installs the kitchen sink with PHP5. You don't need all that for WordPress.)


## Commands to Use
Following is a commands-only version. As long as nothing fails, everything is fine. If something fails, check your spelling. (I had to retype the php5 line a couple of times due to typos. It happens to the best of us.)

    sudo apt-get install apache2
    sudo apt-get install mysql-server libapache2-mod-php5 php5-mysql
	sudo apt-get install php5 libapache2-mod-php5 php5-mcrypt php5-gd php5-xmlrpc php5-curl
    sudo apt-get install phpmyadmin
    sudo mysql_install_db

When you run the mysql line, you'll set up your MySQL root user password.

When you run the phpmyadmin install (optional) you'll need to select your web server, which is apache2. Highlight the apache2 entry, press space (will put a * in the selected entry) and hit enter to continue the install. When phpmyadmin asks about configuring the database with dbconfig-common, select yes. You'll need to enter the MySql root user password and a phpadmin application password

Sourav K refers to editing /etc/apache2/mods-enabled/dir.conf. When I ran the apt-get install lines above and looked at dir.conf, it was correct from the install. Check the file to be sure it contains.

    <IfModule mod_dir.c>
    DirectoryIndex index.php index.html index.cgi index.pl index.php index.xhtml index.htm
    </IfModule>
    
## Test Apache
Point your host web browser to the VM's IP address. If you aren't sure what that is, run ifconfig on the VM. The IP address you need is usually the inet addr for eth0. You should get the default Apache "It works!" page.

## Link /var/www to /mnt/www
On the VM, check the contents of /var/www with `ls /var/www`. It should contain index.html. Copy index.html to /mnt/www with `cp /var/www/index.html /mnt/www'.

Now delete /var/www. `sudo rm -R /var/www` where the rm command is "remove" and -R says "recursive". If you `ls /var`, you'll see /var/www is gone.

Now let's create a symbolic link from /var/www to /mnt/www. Symbolic links look like a file or directory in one directory, but point to a file or directory elsewhere on the machine.
    sudo ln -s /mnt/www /var/www

Now if you `ls /var/www` you'll see whatever is in /mnt/www, which is the www share we created in "Configure Shared Folders in VirtualBox." That should include index.html that we copied earlier

## Test Apache Again
Point your web browser to the VM's IP address again. You should get the "It works!" page, which confirms that our link is working as it should.

## Test PHP
Create a file called info.php that contains the following.

    <?php phpinfo(); ?>

Point your web browser to <VM ip address>/info.php. You should see a PHP info page with version and installed module information.

## Test phpMyAdmin
Point your web browser to <VM ip address>/phpmyadmin. You'll get the phpMyAdmin login page. Enter root for username and the MySQL root user's password for password. You should get the phpMyAdmin screen.

## Wrapup
Congratulations, you have a working base LAMP server for WordPress development. Reboot the machine with `sudo reboot` and test Apache, PHP, and phpMyAdmin again. If everything works, you're ready to clone project-specific VMs from the LAMP base.

Shutdown the server so we can clone it. `sudo shutdown -hP now`

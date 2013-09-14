Update/Upgrade Installed Software on Ubuntu
===========================================

Ubuntu is a Debian-derived Linux and Linuxes in the Debian family use APT (Advanced Packaging Tool) as their package manager. Other Linuxes use different package managers. For example, the Red Hat family uses RPM (Red Hat Package Manager).

Updates and upgrades on Ubuntu happen in two steps--update and upgrade.

First, update the list of packages and their versions. At the command line run `sudo apt-get update`. The `sudo` command is a prefix command that means, "Do as su (superuser/root)." When you run a command with sudo, it will ask you for your password and ask again after a period of inactivity.

The `apt-get update` command reads the list of packages from the various package repositories registered with it and updates it's list of what's available.

After updating the package list, upgrade the installed packages by running `sudo apt-get upgrade`. You may need to confirm that you want to install upgrades.

Installing software and upgrades over time can accumulate a lot of package archives on disk. If you find yourself running low on disk space, or just want to be proactive, run `sudo apt-get autoclean` to purge package archives for packages no longer on your system or `sudo apt-get clean` to purge all package archives. Note that apt-get clean does not uninstall any software, just deletes the install packages.

For those who prefer a prettier interface, aptitude is a text-GUI over apt-get. Run `sudo aptitude` and use arrow keys to navigate and Q to back out of a "window". After aptitude starts, Ctrl+space activates the menu, u updates the package list, U marks all the upgradable packages to be upgraded, and g runs any pending actions (like upgrades). When you've used U to tag upgrades, the first g gets you the list of what's upgrading. Press g again to actually upgrade.If you're searching for a particular package, aptitude is probably an easier interface to use than apt-get, but for simply running upgrades, apt-get involves less overhead.
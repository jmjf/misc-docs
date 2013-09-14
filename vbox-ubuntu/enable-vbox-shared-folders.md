Enable VirtualBox Shared Folders on the Base Virtual Machine
============================================================

My experience has been that the "pick Install Guest Additions from the menu" advice many sites give does not work for my VMs. My solution is as follows.

Run aptitude.

    sudo aptitude

Find virtualbox-guest-utils in the package list. To search the package list type / followed by the string to find. Once a string has been found, n (next) finds the next occurrence. 

Highlight the virtualbox-guest-utils package. Press + to flag it for install.

This package recommends other packages which aptitude will attempt to install by default. We need to deselect the packages we don't need.

Press g to preview the install. Scroll down the list of packages to install (down arrow) to virtualbox-guest-x11. This package adds the X11 window manager resources, which aren't needed on a server that isn't running a GUI. Highlight virtualbox-guest-x11 and press - to deselect it and its dependencies. You'll see a lot of packages change from green with a piA on the left to black-and-white with just a p on the left, indicating they won't be installed.

Scan the list to be sure no packages are not either green (okay) or black-and-white (not installed). If all is clear, press g to install the selected packages.

After aptitude finishes installing, you'll need to press return to get back to the aptitude screen. From aptitude, press Q then Y to exit.

Reboot the VM to ensure the changes are properly installed, configured, and recognized.

    sudo reboot
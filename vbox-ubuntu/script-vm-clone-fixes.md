Script Virtual Machine Clone Fixes
==================================

When we clone a virtual machine in VirtualBox, several settings in Ubuntu need to change. You'll want to change the host name to something meaningful for the clone. (Why did you create the clone in the first place?) You'll also need to fix the network configuration because you'll change the MAC (media access control) address when you clone the VM. The MAC address uniquely identifies the network interface. If it changes and Ubuntu tries to use the old MAC, the network connection won't happen.

The upshot of the last point is that the first time you start a cloned VM, it will take longer than usual because Ubuntu waits for the network to fail completely before it gives up. You also won't have a network connection until you fix the MAC address in Ubuntu.

Fortunately, both of these changes can be done with a simple shell script.

The script needs to do three things. First, it needs to accept a new hostname and reset the hostname for the machine. This involves changing /etc/hosts and /etc/hostname. Second, it needs to delete the file Ubuntu looks in to find the MAC address. Finally, it needs to reboot the VM so Ubuntu will recreate the MAC file.

Because changing all these files requires root privileges, run the script with sudo.

The script is below.

	# get old hostname from /etc/hostname
    oldname=$(cat /etc/hostname)
	# get new hostname from first parameter 
    newname=$1

	# I really should check to be sure newname isn't blank, but...

	# replace /etc/hostname with the new hostname
    cat "$newname" > /etc/hostname
    echo "Hostname changed from $oldname to $newname in /etc/hostname"
    
    # copy the old hosts file, just in case
    cp /etc/hosts oldhosts

	# generate newhosts replacing the old hostname with the new hostname
    cat /etc/hosts | sed s/"$oldname"/"$newname"/ > newhosts

	# replace /etc/hosts with newhosts
    mv newhosts /etc/hosts
    echo "The /etc/hosts file has been changed"

    # delete old MAC address
	rm /etc/udev/rules.d/70-persistent-net.rules

	reboot

Open an editor and put the code above in a file in your home directory. I'm calling it fix-clone.sh for this example. Save the file.

At the command line, in your home directory, set the file to be executable. The `chmod u+x` command says, "Add execute privileges for the user who owns the file." 

    chmod u+x fix-clone.sh

Now you can execute the script. The ~ is the shortcut for your home directory, regardless of what user you're logged in as.

    sudo ~/fix-clone.sh NewHostName

After the script runs, it reboots the VM. Networking should work and the VM should have the new hostname. Add this script in your base VM so any clones will have it.

## Note
You can create the script file above in your host machine's text editor, copy it to the xfer share, the copy it from the xfer share to the guest or just run it from the xfer share if you don't want to copy it. If you take this approach, be sure you set your text editor to use Unix-friendly end-of-line options or the script will fail.
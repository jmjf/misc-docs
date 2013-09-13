Mount Shared Folders on the Base Virtual Machine
================================================

## Configure VM to Mount Shared Folders on Boot
Now that we have the shared folders defined so the VM knows about them, we need to create mount points and mount the shared folders to them so we can use them in the VM. None of that is as hard or arcane as it might sound.

Start the VM and login to the command line.

## Create Mount Points
Mount points are just directories, so all we need to do is create a couple of directories. I prefer to mount my shared folders in /mnt, the mount directory, and name the mount points the same as the shared folders. Your mileage may vary.

Run the following commands to create mount points.
    sudo mkdir /mnt/xfer
    sudo mkdir /mnt/www

## Test Mounting Shared Folders
Next we'll manually mount the shared folders to be sure they work.

    sudo mount -t vboxsf xfer /mnt/xfer
    sudo mount -t vboxsf www /mnt/www

These commands mount the shared folders to the mount points we defined. We can test the mount by putting files in the directories and checking the directory contents. For example, I copy files into the host directories and then `ls` the guest mount (`/mnt/xfer` or `/mnt/www`) to see if the files are there. If they are, the shared folder setup is working.

## Make Mounts Automatic
Running mount commands every time you start the VM is a pain. Let's make the shared folders mount automatically.

Edit /etc/fstab. You'll need to run as root, so put sudo in front of whatever editor command you prefer.

Scroll to the end of the fstab file. DO NOT change anything already in the file. If you do, you'll create major problems for your VM. If you need to add a line break at the end of the last line, that's okay. Otherwise, don't touch the existing mounts.

Enter the following after the existing information in /etc/fstab.

    # mount shared folders
    www /mnt/www vboxsf
    xfer /mnt/xfer vboxsf

Save /etc/fstab when done and reboot the VM.

### Test Mount on Boot
After the VM reboots, login. You should be able to list the directories (e.g., `ls /mnt/www`) and see the files from the host.

## Conclusion
Now that the shared folders are mounting properly on boot, they'll mount for any cloned VM as well. If you need the cloned VM's www directory to point somewhere else, just edit the shared folder information in VirtualBox settings. Be sure the share is still named www when you're done. If the name stays the same, nothing needs to change on the VM to make the new www mount on boot.
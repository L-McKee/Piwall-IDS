# Piwall-IDS
Raspberry Pi project that configures the PI as a gateway firewall and IDS.
This document will be more of a step-by-step and notebook on the project.

Required Items:

    -Raspberry PI 3-B v1.2
    -HDMI cable
    -Ethernet cable
    -Micro-USB power adapter
    -16GB SD Card
    -Archlinux ARM image


-------------------------------------------------------Installing Archlinux ARM OS to Raspberry PI------------------------------------------------------

-Using Win32DiskManager or by following the commands given on the Archlinux ARM Installation guide, partition and install Archlinux ARM OS to the Raspberry PI.
After a day of attempts and the eventual bricking of my copy of Kali Linux being ran in a VirtualBox, I was finally able to get a working copy of Archlinux on my
Raspberry PI.
    
-Use the default login:

    user: root
    password: root
    
-Change the defualt password to root user to something a bit more secure.

    # passwd
    
-Enter new password twice to change.

-----------------------------------------------------------------Network Configuration------------------------------------------------------------------

-Still working on this bit... stay tuned.

-Known files that need to be edited:

    /etc/rc.conf
    /etc/hosts
    
-Then restart network:

    # rc.d restart network
    
---------------------------------------------------------------System Update and Packages--------------------------------------------------------------

-Update system and install required packages:

    # pacman -Syu
    # pacman-key --init
    (I used pacman-key --populate was also...not sure if that is required? Seems to work fine... for now)
    
-Update system again...

    # pacman -Syu
    
-Next, lets install a few packages:

    # pacman -S vim
    # pacman -S htop
    # pacman -S tcpdump
    
-Reboot to apply updates:

    # reboot
    
-To check how much memory is available (just a nice tool to have it seems):

    # htop
    
-------------------------------------------------------------------Adding Another User-------------------------------------------------------------------

-To add another user:

    # useradd -m -g users -G optical,storage,video,wheel,power -s /bin/bash USERNAME
    
-Create new password for user:

    # passwd USERNAME
    
-Install sudo package to enable running commands as root and allow members of the group "wheel" to execute as root:

    # pacman -S sudo
    # visudo
    
-Uncomment this line to allow root execution:
    
    %wheel ALL=(ALL) ALL
    
-Now we should be able to logout of root user for good and login to the new user.

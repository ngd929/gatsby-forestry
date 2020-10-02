---
date: 2020-10-01T05:00:00Z
title: Install Desktop GUI on Ubuntu 20.04 (Focal Fossa)
author: Ralph Waldo Emerson
hero_image: "/content/images/anomaly-oRskqiH7FNc-unsplash.jpg"

---
In this tutorial you will learn how to install GUI ( graphical user interface ) on [Ubuntu 20.04](https://linuxconfig.org/ubuntu-20-04-guide) Focal Fossa Server/Desktop.   
  
**In this tutorial you will learn:** 

* How to install `tasksel`
* How to select GUI from `tasksel` tasks
* How to install GUI
* How to login to newly installed GUI

 

[![Installed GUI on Ubuntu 20.04](https://linuxconfig.org/images/01-ubuntu-20-04-gui-installation.png)](https://linuxconfig.org/images/01-ubuntu-20-04-gui-installation.png "Installed GUI on Ubuntu 20.04") Installed GUI on Ubuntu 20.04

 

## Software Requirements and Conventions Used

 

| --- |
| Software Requirements and Linux Command Line Conventions |
| Category | Requirements, Conventions or Software Version Used |
| System | Installed or upgraded Ubuntu 20.04 Focal Fossa |
| Software | tasksel |
| Other | Privileged access to your Linux system as root or via the sudo command. |
| Conventions | # - requires given linux commands to be executed with root privileges either directly as a root user or by use of sudo command $ - requires given linux commands to be executed as a regular non-privileged user |

 

## Ubuntu 20.04 GUI installation step by step instructions

 

1. First step is to updated the `apt` package index and install `tasksel`. To do so execute the following [Linux commands](https://linuxconfig.org/linux-commands):

       $ sudo apt update
       $ sudo apt install tasksel
       
2. **_SUBSCRIBE TO NEWSLETTER_**_  
   Subscribe to Linux Career_ [_NEWSLETTER_](https://bit.ly/2X5D30q) _and receive latest Linux news, jobs, career advice and tutorials._
3. Next, select the GUI you wish to install. Below table shows main desktop environments available for installation via `tasksel`:

   | --- |
   | Main available Graphical User Interfaces (GUI) installations using tasksel's tasks |
   | Task | Description |
   | kubuntu-desktop | Kubuntu desktop ( KDE Desktop ) |
   | lubuntu-desktop | Lubuntu Desktop ( LXQt desktop ) |
   | ubuntu-budgie-desktop | Ubuntu Budgie desktop |
   | ubuntu-desktop | Ubuntu desktop ( default GNOME ) |
   | ubuntu-desktop-minimal | Ubuntu minimal desktop ( default GNOME ) |
   | ubuntu-mate-desktop | Ubuntu MATE desktop |
   | ubuntustudio-desktop | Ubuntu Studio desktop ( Xfce-based desktop ) |
   | ubuntustudio-desktop-core | Ubuntu Studio minimal DE installation ( Xfce-based desktop ) |
   | xubuntu-desktop | Xubuntu desktop ( Xfce desktop ) |

    For additional GUI selection execute the below command:

       $ tasksel --list-tasks
       
4. At this point you have selected GUI you wish to install and took a note of the relevant task name.   
     
   Next, use `tasksel` command to install your selected GUI. For example to install the default Ubuntu GNOME desktop execute:

       $ sudo tasksel install ubuntu-desktop
       
5. Reboot your system:

       $ reboot
6. At this point the GUI should start. You may need to select your desired desktop flavor on the login page before you login.   
     
    In case the GUI is not starting at all, make sure your system boots into the graphical target. To do so execute:

       $ sudo systemctl set-default graphical.target
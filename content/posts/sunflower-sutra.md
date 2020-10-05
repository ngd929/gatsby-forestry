---
date: 2020-10-01T05:00:00Z
title: Headless KVM Host with CentOS and virt-manager
author: Khai N
hero_image: "/content/images/adrien-olichon--aOsCcTJXWY-unsplash.jpg"

---
# Headless KVM Host with CentOS and virt-manager

1 minute read

I’m currently running [KVM](https://www.linux-kvm.org/page/Main_Page) on a single remote host. I have a bunch of virtual machines running services like DHCP/DNS, UniFi Controller and UniFi video.

When I intially set this up I wanted to keep the virtual host installation as minimal as possible. So off I went and did a minimal installation of CentOS 7, thinking I could remotely manage this server through File > Add Connection on my local Linux machine with virt-manager. Of course this was not as straightforward as I thought, so during my search for an answer I came across a suggestion to use SSH with X forwarding.

Below is a guide on setting up a KVM host with virt-manager that can be remotely managed through SSH with X forwarding.

I’m going to be using a CentOS 7 minimal installation that is fully patched.

To begin, install the virtualization host software.

    ~]# yum group install -y "Virtualization Host"

Start the libvirtd service and verify it is enabled on startup.

    ~]# systemctl start libvirtd
    ~]# systemctl is-enabled libvirtd

Install X Window System.

    ~]# yum install -y "@X Window System"

Install virt-manager.

    ~]# yum install -y virt-manager

The host setup is now complete. Now all we need to do is connect to the host through SSH with X Forwarding.

## Connecting with Linux[Permalink](https://blog.ricosharp.com/posts/2019/Headless-KVM-Host-with-CentOS-and-virt-manager#connecting-with-linux "Permalink")

Open a terminal and SSH to the KVM host. Once connected open virt-manager.

    ~]$ ssh -X rico@192.168.122.100
    ~]$ su
    ~]$ virt-manager

## Connecting with a Mac.[Permalink](https://blog.ricosharp.com/posts/2019/Headless-KVM-Host-with-CentOS-and-virt-manager#connecting-with-a-mac "Permalink")

Download and install [XQuartz](https://www.xquartz.org/) Open a terminal and SSH to the KVM host. Once connected open virt-manager.

    ~]$ ssh -X rico@192.168.122.100
    ~]$ su
    ~]$ virt-manager

## Connecting with a Windows System[Permalink](https://blog.ricosharp.com/posts/2019/Headless-KVM-Host-with-CentOS-and-virt-manager#connecting-with-a-windows-system "Permalink")

* Download, install, then open [xming](https://sourceforge.net/projects/xming/)
* Download and open putty
* Go to Connection > SSH > X11 and check Enable X11 forwarding
* Go back to Session and enter the IP/Hostname of your machine and click Open

## Using virt-manager as a non-root user[Permalink](https://blog.ricosharp.com/posts/2019/Headless-KVM-Host-with-CentOS-and-virt-manager#using-virt-manager-as-a-non-root-user "Permalink")

In the SSH examples above, I am SSH’ing as a non-root user, then changing to root to run virt-manager. This is because polkit blocks user accounts from accessing libvirtd.

To work around this and allow non-root users who are part of the wheel group access to run virt-manager, create this rule:

    ~]# vi /etc/polkit-1/rules.d/51-libvirt.rules
    
    /* Allow users in wheel group to manage the libvirt
    daemon without authentication */
    polkit.addRule(function(action, subject) {
        if (action.id == "org.libvirt.unix.manage" &&
            subject.isInGroup("wheel")) {
                return polkit.Result.YES;
        }
    });

## References[Permalink](https://blog.ricosharp.com/posts/2019/Headless-KVM-Host-with-CentOS-and-virt-manager#references "Permalink")

[https://wiki.archlinux.org/index.php/Libvirt#Using_polkit](https://wiki.archlinux.org/index.php/Libvirt#Using_polkit "https://wiki.archlinux.org/index.php/Libvirt#Using_polkit")
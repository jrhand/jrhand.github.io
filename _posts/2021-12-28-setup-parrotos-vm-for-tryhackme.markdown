---
layout: post
title:  "Tutorial: Set Up a Parrot OS VM in VirtualBox (For Use on TryHackMe Challenges)"
date:   2021-12-28 13:00:00 -0800
categories:
tags: tutorial
---

# Introduction

Using Linux virtual machines to complete challenges on platforms like [TryHackMe](https://tryhackme.com/) or [HackTheBox](https://www.hackthebox.com/) allows us to take advantage of (and learn) powerful, lightweight operating systems without altering our personal computers. Unlike the in-browser AttackBox provided by TryHackMe, which will revert to its original state when terminated, you will have to freedom to customize your virtual machine as needed, and more easily save the tools you use and document your progress.

Operating systems like Kali Linux and Parrot OS are both popular options for ethical hacking and pentesting, and both come with a variety of security and pentesting tools preinstalled. In this tutorial we'll be using Parrot OS.

**An important note:** These tools are meant for ethical and legal use. TryHackMe provides vulnerable machines to attack for the purpose of learning; you should never attack, perform intrusive reconnaissance, or conduct a penetration test on a real target unless you are authorized to do so.

In this tutorial we will...
- Download Parrot OS
- Install VirtualBox
- Create a new VM
- Install Parrot OS
- Connect to TryHackMe with OpenVPN

Versions used in this tutorial:
- VirtualBox 6.1.30
- Parrot Security 4.11.3

# Download Parrot OS

1. Visit https://parrotsec.org/download/ and select 'Get Security Edition'.
2. Select 'Download' under 'MATE Desktop', and save the .iso file in a folder dedicated to your VMs.

# Install VirtualBox

VirtualBox is a free hypervisor - a software application that allows us to deploy and manage virtual machines through an easy-to-use interface. VMWare Player is another free alternative.

For a more comprehensive resource on VirtualBox, visit https://www.virtualbox.org/manual/.

1. Visit https://www.virtualbox.org/ and select Downloads.
2. Select and download the VirtualBox platform package meant for your operating system.
3. You can check the integrity of the downloaded .exe by comparing its SHA256 hash with the checksum provided by VirtualBox. (A link to the SHA256 checksums can be found on the Downloads page.) If you are using Windows, you can compute the hash of file with the command: `certutil -hashfile <FILEPATH> SHA256` (where FILEPATH is the location of the .exe)
![Computing the hash of the .exe](/images/certutil.png)
4. Run the installer and start VirtualBox once the installation is complete.

# Create a new VM

1. Select 'New' to create a new VM.
![Select New](/images/vb1.png)
2. Name your VM so you can identify it later, select the type as 'Linux' and the version as 'Debian (64-bit)', then select 'Next'.

![New VM](/images/vb2.png)
3. Select the amount of memory to allocate, then select 'Next'. (In this example I allocate 8GB. Depending on your system and needs you may want more or less, and you can always adjust this later in your VM's settings in VirtualBox if you have any performance issues.)
![Allocate RAM](/images/vb3.png)
4. Select 'Create a virtual hard disk now', then select 'Create'
5. Select 'VDI', then select 'Next'
6. Select 'Fixed Size', then select 'Next'
7. Set the disk size to at least 15 GB, then select 'Create'
![Disk size](/images/vb4.png)
8. Select your new virtual machine, then select 'Settings'
9. In the 'Network' section, expand 'Advanced' and change the adapter type to 'PCnet-PCI II'
![Adapter type](/images/vb5.png)
10. Power on your new virtual machine by double clicking it in VirtualBox, or by selecting the machine and then clicking 'Start'


# Install Parrot OS

1. When you power on the VM, you will be asked to select a start up disk. Click the folder icon to open the Optical Disk Selector, click 'Add', and locate the .iso file you downloaded earlier
2. Make sure the Parrot OS .iso is selected, then select 'Choose'
3. Select 'Start', and wait for the OS to boot automatically or press your Enter key when you see the Try/Install option
4. Double click 'Install Parrot' on the desktop
5. In the Parrot OS Installer, select your timezone, select 'Erase Disk' in Partitions, and enter your desired username and password in the Users tab. Then select 'Install', 'Install Now', and 'Finish' once the installation is complete
6. Restart the VM and login!


# Connect to TryHackMe with OpenVPN

1. Open a browser, navigate to tryhackme.com and login.
2. Click on your user icon in the top right hand corner, and select 'Access' from the drop down menu.
3. Select a VPN server and click on 'Download My Configuration File'
4. Save `<YOUR USERNAME>.ovpn` in an easy to remember location
5. In a terminal, enter the command `sudo openvpn <FILEPATH>`, where FILEPATH is the location of your .ovpn file. You should see `Initialization Sequence Completed` if the connection is successful. Keep this terminal open in the background while you're interacting with TryHackMe's vulnerable machines, closing it will terminate the connection.
![OpenVPN command](/images/openvpn.PNG)


![OpenVPN connected](/images/openvpn2.PNG)

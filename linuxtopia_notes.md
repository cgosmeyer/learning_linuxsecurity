# PORTS

Computer sustems talk to each other through *ports*.

Linux systems have 65,535 ports.

PORTS
21 - FTP, file transfer
22 - SSH, secure remote login
25 - smtp, mail transfer and telnet, remote login
80 - httpd, web server

Once they obtain an IP address (by randomly trying all IP addresses ever), intruders will first try to look for any open ports.
Can check the firewall log file to see whether any attepts have been made to enter the network.


# FIREWALLS

A barrier between your system and the connection to the internet, filtering out anything not permitted to enter the internal network. It can be a software program on the computer system or built into the hardware such as the router.  

## Functions of a firewall

1. Discard *pings*.  A ping utility sends a data packet to the remote system represented by the IP address and waits for a reply. It there's a reply then the user knows that the system at that address is available on the network. It is a good idea NOT to repond to ping requests so that you remain anonymous to an attacker.

2. Forward and block ports. A firewall can block any ports that you do not want to be open to your systems inside the firewall. If, for example, you don't want anyone on the outside to have FTP access to your systems, you'll need to configure the firewall to block port 21. Can also configure the firewall to allow you to forward port 21 (telnet) connections to a system you want to access from the outside.

3. Filter packets. Data is transferred over networks and internet in *packets*. Each packet contains information about the nature of the data being transmitted (where it came from and where it is being sent, ie, the IP addresses.) You can then filter data packets using filtering rules. For example, can choose to block packets from a certain IP address or disallow all ftp packets. 

Close all ports that aren't being used. 

The Demiliterized Zone (DMZ) setting allows you to open all ports on a computer on your network. *Never do this.* 

# COMMUNICATION SERVICES

Httpd: Hyper Text Transfer Protocal Deamon. Activate if using a Linux system to host a web site. Make sure that port 80 is open on the Firewall and configured to forward requests to the IP address of the Linux system on your network that is running the web server.

Telnet: allows users to log into the Linux system from the outside. Recommended not to use this because transmits data in plain readable text - use SSH instead. 

SSH: also allows users to log into the Linux system from the outside, but using an encryption mechanism. 

FTP: protocol for exchanging files over the internet. The VSFTP (very secure ftp) server is recommended because more secure and faster.

SMTP: Simple Mail Transfer Protocal, protocal used for sending email messages between servers. Retrieve messages using an email client such as Evolution, KMail, or Balsa.

# CONFIGURING LINUX SERVICES AND RUNLEVELS

A typical Linux system can be configured to boot up into one of five *Runlevels*. During bootup, a process called *init* looks in the */etc/inittab* to find which runlevel the system should be booted to, and then it begins to execute the appropriate startup scripts to run the services required for the system. Both the runlevel and the services that get run at startup are configurable.

## Inits and Runlevels

A typical */etc/inittab* looks like this

	# Default runlevel. The runlevels used by RHS are:
	#   0 - halt (Do NOT set initdefault to this)
	#   1 - Single user mode
	#   2 - Multiuser, without NFS (The same as 3, if you do not have networking)
	#   3 - Full multiuser mode
	#   4 - unused
	#   5 - X11
	#   6 - reboot (Do NOT set initdefault to this)
	#
	id:3:initdefault:

The last line tells the init process that the default runlevel is 3. 

The different runlevels are

0 - The Halt Runlevel at which the system shuts down; unlikely this should be your default.

1 - The Single Runlevel. Causes system to start up in a single user moder under which only the root user can log in. Ideal for system admin to perform system maintenance or repair activities.

2 - Multi-user Runlevel with text-based console login capability. Does not start the network.

3 - Multi-user Runlevel with networking services started. Most common runlevel for server-based systems that do not require any kind of graphical desktop environment.

4 - Undefined runlevel, can be configured to provide a custom boot state.

5 - Boots the system into a networked, multi-user state with X Window System capability. By default the graphical desktop environment will start at the end of the boot. Most common runlevel for desktop or workstation use.  

6 - Reboots the system. Another unlikely default runlevel.

## Configuring Linux Services

*It's a good policy to disable any unused services on the Linux system.*

You can control which services you want started at boot time. 

To list all service settings and see whether or not they are started up at various runlevels:
	
	/sbin/chkonfig --list

To narrow down, for instance, the entry for the http daemon:

	/sbin/chkconfig --list | grep httpd

Or if you're interested in what gets started at runlevel 3:

	/sbin/chkconfig --list | grep '3:on'

To change settings, for example, to make HTTP service startup what at runlevel 5:

	/sbin/chkconfig --level 5 httpd on

# LINUX FIREWALL - SECOND LINE OF DEFENSE

The first line of defense is the firewall on your router or cable modem.

Now will learn how to configure security settings on your Linux system.

## lokkit

To change security settings of the Firewall installed on your stem, run *lokkit* command. But first must login as root or use the "su" command. If already super user, do:

	/usr/sbin/lokkit

If from a non-super user account:

	su -c "/usr/sbin/lokkit"

Based on your selections, *lokkit* will configure the firewall to allow access to the appropriate ports. Also provides option of specifying trusted devices on the "Configure" screen. You could then, for instance, disable the firewall settings for any connections coming from devices connected to the trusted or secure network while applying the firewall rules to devices connected to the untrusted network. 

# WIRELESS LINUX SECURITY

If wireless security is neglected, all your other precautions will be for nothing.

Wireless data is breadcast through radio waves; while an ethernet cable is almost impossible to intercept, a wifi network can potentially be snooped on by anyone.

Wireless networks are protected from attacks by using encryption. Breaking encryption can be so difficult that a hacker will likely just move on to the many unprotected networks and ignore yours. You can't keep the data from spreading out of the building, short of encasing the building in lead, so settle for encrypting that data; so although anyone can see the data, not just anyone can read it without the encryption key.

## Encryption

The encrypted form of the data is known as *cythertext*. 

Wireless networks use *symmetrical encryption* in which the same key is used at both ends of the network connection. The key is specified by you when you configure the encryption for your wireless network. 

WiFi wireless networks use a security standard called *Wired Equivalent Privacy (WEP)* whose aim is to provide the equivalent security of a wired network. In practice this is not always possible. 

Wireless encryption can be configured as either 64-bit or 128-bit. Refers to the lengh of the key; hence, 128-bit encryption is stronger. But stronger encryption can impact network performance because more time is spent encrypting and decrypting at each end of communication. In practice, the performance difference is small and 128-bits is encouraged.

Encryption keys are specified in *hexadecimal*, using a base of 16 (digits between 0-9 and A-F).

	64-bits: 10 digit key
	128-bits: 26 digit key

## Configuring Wireless Security

Once you have configured your wireless base station to use WEP encryptions, next will need to configure the wireless adaptor on your linux system to use the same encryption key.

On RedHat:

	redhat-config-network

On Fedora Core:

	system-config-network

To set up the encryption, enter the 26 digit key set up on your wireless base station.  

	Since hexadecimal, key should be prefixed with 0x















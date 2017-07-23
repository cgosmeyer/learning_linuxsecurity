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







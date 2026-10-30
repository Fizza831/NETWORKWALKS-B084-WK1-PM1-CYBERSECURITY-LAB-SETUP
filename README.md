# NETWORKWALKS-B084-WK1-PM1-CYBERSECURITY-LAB-SETUP
Week 1: Cybersecurity Lab Setup & Wireshark SOC Labs
This document covers my Week 1 work: building a cybersecurity testing lab (main task) and completing the extra Wireshark SOC project module
Cybersecurity Lab Setup (Main Task)
Requirements and result
Requirement	Status
VirtualBox as base (latest recommended version)	Done
Kali Linux as attacking machine	Done (Kali 2026.3 pre-built image)
NAT Network in subnet 10.0.0.0/24	Done (NatNetwork, DHCP enabled)
Shared clipboard and drag/drop enabled	Done (Bidirectional)
Shared folder from host machine	Done (Downloads, later a dedicated folder)
Kali IP address 10.0.0.2/24	Done (static, gateway 10.0.0.1)
Kali has full Internet access	Done (ping google.com works)
Snapshots taken	Done (two snapshots)

Steps I followed

1.	Installed 7-Zip and VirtualBox on Windows.
2.	Created the NAT Network NatNetwork with IPv4 prefix 10.0.0.0/24 (File > Tools > Network).
3.	Downloaded the Kali Linux VirtualBox image from kali.org and extracted the .7z archive with 7-Zip.
4.	Added the VM with Machine > Add and selected the .vbox file.
5.	Set Adapter 1 to NAT Network (NatNetwork) with Promiscuous Mode set to Allow All.
6.	Set Shared Clipboard and Drag'n'Drop to Bidirectional.
7.	Added a shared folder with Auto-mount and added my user to the vboxsf group.
8.	Set a static IPv4 address in Kali: 10.0.0.2/24, gateway 10.0.0.1, DNS 8.8.8.8.
9.	Applied the connectivity fix for VirtualBox 7 / Kali 2026.1+ (commands below).
10.	Verified the setup with ip a and ping google.com.
11.	Took VM snapshots.

Commands used:

sudo usermod -aG vboxsf kali
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
ip a
ping -c 3 google.com

Issues I ran into

•	The Kali download showed a Word icon. The file was a normal .7z archive; Windows showed the wrong icon because 7-Zip was not installed yet.
•	Import Appliance showed nothing. The Kali VirtualBox download is a .vbox and .vdi VM folder, so it is added with Machine > Add instead.
•	Security: I first shared my whole Downloads folder with Full access. I then switched to a dedicated folder so Kali can reach only that one folder.

Skills Practiced

•	Display filters such as ip.addr, tcp.flags.syn, tcp.port and http.request
•	Following TCP streams to read plain text conversations
•	Spotting a TCP SYN port scan and telling open ports (SYN, ACK) from closed ports (RST, ACK)
•	Finding credentials sent in clear text over HTTP
•	Recognising brute force login patterns
•	Analysing VoIP traffic

Main Takeaway

Unencrypted protocols such as HTTP, plain text chat, FTP and unencrypted VoIP expose passwords and conversations to anyone who can capture the traffic. The fix is encryption: HTTPS, SSH or SFTP, and SRTP for calls.
Practice Rules Followed
All traffic analysis was done inside the provided labs. The Kali VM is used only on my own isolated NAT Network, and I never tested or captured traffic on a network I do not own or have written permission to test.

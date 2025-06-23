# CyberSecurity Internship - Task 1
## Scanning My Local Network for Open Ports

### Environment Used
I performed this task using **Kali Linux** inside **Oracle VirtualBox**. I chose Kali because it’s purpose-built for cybersecurity — preloaded with tools like Nmap, Wireshark, and other network utilities. Kali gives deeper control over networking, and it's widely used in the industry for ethical hacking and penetration testing.

### Tools Used
- **Nmap** – For scanning IPs and open ports
- **Wireshark** – For optional packet capture and deep traffic analysis
- **Linux Terminal** – For command execution

Step 1: Identify My IP
I used the `ifconfig` command to find:
- **My IP address**: `192.168.1.2`
- **Subnet**: `255.255.255.0` → IP range: `192.168.1.0/24`
- **Interface**: `eth0`

Step 2: Run the Nmap Scan

with the help of **sudo nmap -sS 192.168.1.0/24 -oN scanResults.txt -oX result.xml** I was able to scan and see what host were open and closed. By -oN scanResults.txt I was able to store that result on a text format. By -oX result.xml I was to automate 
the result in xml later on I changed the .xml into .html by using this command **xsltproc result.xml -o result.html**. I have attached all three files.

### Hosts
In total it scanned 9 hosts. Some of them are:

| IP Address   | Ports Open             | Device Type (Likely) |
| ------------ | ---------------------- | -------------------- |
| 192.168.1.1  | 80, 443                | Router               |
| 192.168.1.3  | 8008, 8009, 8443, 9000 | Media device         |
| 192.168.1.10 | 8008, 9000, 9080       | Smart device         |
| 192.168.1.2  | None                   | My system,  Secure   |

### What I Observed and learned by using nmap?
I was able to see that my system with IP **192.168.1.2** firewalls are working fine with no open ports that makes it secure.
other than that there were 4 IP which was having open ports which can make there network vulnerable. No device exposed critical ports like FTP(21) and TELNET(23) which is a good thing. 
Some MAC gave us a hint that the particular device is manufactured by google for IP 192.168.1.8 which could be a media device. like google home.

- I learned that how we can covert a xml file into a html file.
- How imp nmap can be to see which IP have open, closed and filtered port.
- Like it is very important to limit the open ports to prevent from any threat.

## Going with Wireshark command.
After I used the nmap command I learned about wireshark that How important wireshark could be to capture the network packets. Alongside Nmap scanning, I used **Wireshark** to capture real-time packet data to understand what scanning looks like at the network level.

How I Used It
- Opened Wireshark on interface `eth0`
- Started packet capture
- Ran: `sudo nmap -sS 192.168.1.0/24` on terminal
- Stopped wireshark after the nmap scan and saved the capture as `wireshark.pcapng` 

What I Observed and Learned:
- TCP SYN packets sent to all IPs and ports in the subnet.
- SYN-ACK packets as replies from devices with open ports.
- RST (Reset) packets from devices with closed ports.
- ARP packets used for discovering live hosts.
- How Nmap's scanning behavior appears at the packet level.
- The difference between open and closed ports based on TCP responses.
- That scanning activity is easily visible and detectable by network defenders.

Practiced using filters in Wireshark:
- tcp.flags.syn == 1 && tcp.flags.ack == 0 — SYN packets
- tcp.flags.reset == 1 — RST packets (closed ports)
- arp — Host discovery packets

Saved the capture file as wireshark.pcapng and included it in the repository.







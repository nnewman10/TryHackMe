# [Day 7] Skilling Up Writeup
### Tags: `#Networking #Ports #NMAP`
#### [Machine Link](https://tryhackme.com/room/25daysofchristmas)

<img src='imgs/advent2019day7.png' width='200' align='center'>

## Walkthrough

1.) Lets download the machine task files and open the pcap file with the tool wireshark.

```bash
wireshark holidaythief.pcap
```

![](imgs/wireshark.png)

2.) By looking through the pcap file, we can see alot of packets using unencrypted protocols such as DNS and HTTP. These packets can be reconstructed and we can see all the data the packet contains. Lets reconstruct the DNS stream and see if any data looks interesting.

![](imgs/dnsstream.png)

3.) The subdomain string for holidaythief.com looks very out of place, it looks like the string is hex encoded. Using CyberChef, lets decode the string and see if any data was trying to be exfiltrated out of the network throught this packet.

![](imgs/cyberchef.png)

4.) Going back to the pcap file, lets take a look the the HTTP stream for all the HTTP packets and see if any data looks interesting. 

![](imgs/httpstream.png)

5.) The HTTP stream shows that two resources were requested, christmaslists.zip and TryHackMe.jpg. Since this stream was using the HTTP and not HTTPS we can use wireshark to download these resources by going to File -> Export Objects -> HTTP. If we try to unzip the christmaslists.zip file, we are prompted for a password. We can actually brute force zip files by using the tool fcrackzip and the rockyou.txt wordlist.

```bash
fcrackzip -b --method 2 -D -p /usr/share/wordlists/rockyou.txt -v christmaslists.zip
```

![](imgs/fcrackzip.png)

6.) Using Steganography, you can hide data within another message or physical object such as a image file. Using the tool steghide, we can try and extract any information hidden. Lets see if anything is hidden within the TryHackMe.jpg.

```bash
steghide extract -sf TryHackMe.jpg
```

![](imgs/steghide.png)

## Tasks
| Task | Question | Answer |
| --- | --- | --- |
| Task #1 | What data was exfiltrated via DNS? | Candy Cane Serial Number 8491 |
| Task #2 | What did Little Timmy want to be for Christmas? | PenTester |
| Task #3 | What was hidden within the file? | RFC527 |






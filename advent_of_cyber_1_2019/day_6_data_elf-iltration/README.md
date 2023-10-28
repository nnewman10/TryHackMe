# [Day 6] Data Elf-iltration Writeup
### Tags: `#Data Exfiltration #Steghide #fcrackzip`
#### [Machine Link](https://tryhackme.com/room/25daysofchristmas)

<img src='imgs/advent2019day6.png' width='200' align='center'>

## Walkthrough

1.) Lets download the machine task files and open the pcap file with the tool wireshark.

```bash
wireshark holidaythief.pcap
```

![](imgs/wireshark.png)

2.) By looking through the pcap file, we can see alot of packets using unencrypted protocols such as DNS and HTTP. These packets can be reconstructed and we can see all the data the packet contains. Lets reconstruct the DNS stream and see if any data looks interesting.

![](imgs/dnsstream.png)

3.) Using Google, lets try to see if this username is associated with any social media accounts. The first result shows that the username is connected to a twitter/X account.

![](imgs/username.png)

4.) The twitter account contains the user's DoB, occupation, location, and personal website. That is alot more data that is now available for OSINT research. 

![](imgs/twitter.png)

5.) Using the website The Wayback Machine, we can look at previous versions of the user's personal website.

![](imgs/wayback.png)

6.) We can look at the first version of the user's personal website, to see if there is any information disclosure.

![](imgs/firstwebsite.png)

7.) Using google image search and uploading a image file, we can search for all instances of that image on the web with all the related information.

![](imgs/googleimageserach.png)


## Tasks
| Task | Question | Answer |
| --- | --- | --- |
| Task #1 | What is Lola's date of birth? Format: Month Date, Year(e.g November 12, 2019) | December 29, 1900 |
| Task #2 | What is Lola's current occupation?| Santa's Helper |
| Task #3 | What phone does Lola make? | iPhone X |
| Task #4 | What date did Lola first start her photography? Format: dd/mm/yyyy | 23/10/2014 |
| Task #5 | HWhat famous woman does Lola have on her web page? | ada lovelace |





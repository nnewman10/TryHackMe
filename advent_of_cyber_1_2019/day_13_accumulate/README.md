# [Day 13] Accumulate Writeup
### Tags: `#Windows WebApp #Wordpress #JuicyPotato`
#### [Machine Link](https://tryhackme.com/room/25daysofchristmas)

<img src='imgs/advent2019day13.png' width='200' align='center'>

## Walkthrough

1.) Lets ping the machine ip and see if it is up and running. Im pretty sure this machine is ignoring ICMP.

```bash
ping 10.10.12.139
```
![](imgs/ping.png)

2.) Lets run a quick test nmap scan to double check that the machine is up and responding to other requests besides ICMP.

```bash
nmap 10.10.12.139
```
![](imgs/nmap1.png)

3.) Now that we confirmed that the machine is responding to a simple nmap scan, lets run a more in depth scan to enumerate all the running services on open ports.

```bash
nmap -A -p- 10.10.12.139
```
![](imgs/nmap2.png)

4.) Lets open the webapp running on port 80, we can see that it is a simple IIS default page.

![](imgs/webapp.png)

5.) Since we dont see anything on the default webpage, lets run a dirsearch to find hidden directories. 

```bash
dirsearch -u http://10.10.12.139 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```
![](imgs/dirsearch.png)

6.) The dirsearch scan came back with /retro as a code 200 for the webapp, lets take a look at the webpage.

![](imgs/retro.png)

7.) After looking around, we clicked on a recent comment from the user Wade. This post has what looks like a password that he wanted to save for later. Also under the META sub-menu we can see both a Log in and WordPress.org links.

![](imgs/password.png)

8.) Clicking on the Log in link, we are sent to a wordpress login page at /retro/wp-login.php. Lets try logging in with the username:password combo we found wade:parzival

![](imgs/wplogin.png)

9.) Looks like that was the correct admin creds as we are now logged into the wordpress admin dashboard. Upon looking at the dashboard we can see the wordpress version is 5.2.1

![](imgs/wpadmin.png)

## Tasks
| Task | Question | Answer |
| --- | --- | --- |
| Task #1 | What is the md5 hashsum of the encrypted note1 file? | 24cf615e2a4f42718f2ff36b35614f8f |
| Task #2 | Where was elf Bob told to meet Alice? | Santa's Grotto |
| Task #3 | Decrypt note2 and obtain the flag! | THM{ed9ccb6802c5d0f905ea747a310bba23} |











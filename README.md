<p align="center">
<a href="#"><img src="/Images/hs_gif_bg.gif" alt="bg" height="300 px" width="250px"></a>
</p>

<h1 align="Center"><b>Computer Forensics</b></h1>

<h3 align="Center">CFReDS's Hacking Case Walkthrough</h3>

## **Introduction**
> Here for the analysis of the scenario given below we will be using the <a href=https://www.autopsy.com/>Autopsy tool</a>. Autopsy® is the premier end-to-end open source digital forensics platform. Built by Basis Technology with the core features you expect in commercial forensic tools, Autopsy is a fast, thorough, and efficient hard drive investigation solution that evolves with your needs.

## **Scenario**

> On 09/20/04 , a Dell CPi notebook computer, serial # VLQLW, was found abandoned along with a wireless PCMCIA card and an external homemade 802.11b antennae. It is suspected that this computer was used for hacking purposes, although cannot be tied to a hacking suspect, G=r=e=g S=c=h=a=r=d=t. (The equal signs are just to prevent web crawlers from indexing this name; there are no equal signs in the image files.)  Schardt also goes by the online nickname of “Mr. Evil” and some of his associates have said that he would park his vehicle within range of Wireless Access Points (like Starbucks and other T-Mobile Hotspots) where he would then intercept internet traffic, attempting to get credit card numbers, usernames & passwords.

> Find any hacking software, evidence of their use, and any data that might have been generated. Attempt to tie the computer to the suspect, G=r=e=g S=c=h=a=r=d=t.

## Questions
### 1. What is the image hash? Does the acquisition and verification hash match?
```
MD5: aee4fcd9301c03b3b054623ca261959a
Acquition hash is not given in this scenario so we can't say that it will match or not with the verification hash.

Method: We find MD5 hash info by clicking on Data Source -> image file. Then in the file metadata, we find the MD5 Hash.
```
<p>
<a href="#"><img src="/Images/Ques1.png" alt ="Ques1"></a>
</p>

### 2. What operating system was used on the computer?
```
Windows XP

Method: We find OS info in Acquisition details which we find by clicking on Data Source -> image file. 
        Then in the file metadata, we find the Acquired OS.
```
<p>
<a href="#"><img src="/Images/Ques2.png" alt ="Ques2"></a>
</p>

### 3. When was the install date?
```
Thursday, August 19, 2004 10:48:27 PM GMT

Method: We will find the Install Date at “C:\Windows\system32\config\Software\Microsoft\Windows NT\CurrentVersion\InstallDate”.
        The Date we found is in UNIX format so we need to convert it in human readeable format.
        Just copy the number in the brackets and convert using any converter online.
```
<p>
<a href="#"><img src="/Images/Ques3.png" alt ="Ques3"></a>
</p>

### 4. What is the timezone settings?
```
Central Standard Time (CST) (GMT -6:00)

Method: We will find the timezone settings at “C:\windows\system32\config\system\CurrentControlSet\Control\TimeZoneInformation”.
        The timezone we found is CST which is 6 hours behind GMT.
```
<p>
<a href="#"><img src="/Images/Ques4.png" alt ="Ques4"></a>
</p>

### 5. Who is the registered owner?
```
Greg Schardt

Method: We will find the Registered Owner info at “C:\windows\system32\config\software\Microsoft\Windows NT\CurrentVersion\RegisteredOwner”
```
<p>
<a href="#"><img src="/Images/Ques5.png" alt ="Ques5"></a>
</p>

### 6. What is the computer account name?
```
Mr. Evil

Method: We will find the account name at “C:\windows\system32\config\SAM\Users\Names”
```
<p>
<a href="#"><img src="/Images/Ques6.png" alt ="Ques6"></a>
</p>

### 7. What is the primary domain name?
```
N-1A9ODN6ZXK4LQ

Method: We will find the Default Domain Name at “C:\windows\system32\config\software\Microsoft\Windows NT\CurrentVersion\Winlogon”
```
<p>
<a href="#"><img src="/Images/Ques7.png" alt ="Ques7"></a>
</p>

### 8. When was the last recorded computer shutdown date/time?
```
2004–08–27 10:46:33 AM

Method: We will get the last recorded computer shutdown at “C:\windows\system32\config\system\CurrentControlSet\Control\Windows\ShutdownTime”.
        We get the value C4 FC 00 07 4D 8C C4 01 which needs to be converted using DCode app which is time stamp decoder.
```
<p>
<a href="#"><img src="/Images/Ques8.png" alt ="Ques8"></a>
</p>

### 9. How many accounts are recorded (total number)?
```
5

Method: Total accounts can be found at  “C:\windows\system32\config\SAM\Users\Names”
```
<p>
<a href="#"><img src="/Images/Ques9.png" alt ="Ques9"></a>
</p>

### 10. What is the account name of the user who mostly uses the computer?
```
Mr. Evil

Method: We can find the Login count of the user click on Login Name in the OS Account section
```
<p>
<a href="#"><img src="/Images/Ques10.png" alt ="Ques10"></a>
</p>

### 11. Who was the last user to logon to the computer?
```
Mr. Evil

Method: We will find the default user at “C:\windows\system32\config software\Microsoft\Windows NT\CurrentVersion\Winlogon”
```
<p>
<a href="#"><img src="/Images/Ques11.png" alt ="Ques11"></a>
</p>

### 12. A search for the name of “G=r=e=g S=c=h=a=r=d=t” reveals multiple hits. One of these proves that G=r=e=g S=c=h=a=r=d=t is Mr. Evil and is also the administrator of this computer. What file is it? What software program does this file relate to?
```
The file is "irunin.ini" and the name of the software program is "Look@LAN".

Method: When we search for the word "Greg Schardt" we get 10 results and in that one of the file is "irunin.ini" and in that 
        we find it is mentioned that regowner is Greg Schardt while the LAN user is Mr. Evil which proves that both are same 
        and a program named "Look@LAN" is used for same.
```
<p>
<a href="#"><img src="/Images/Ques12.png" alt ="Ques12"></a>
</p>

### 13.  List the network cards used by this computer
```
The name of both the network cards is “Compaq WL110 Wireless LAN PC Card” & “Xircom CardBus Ethernet 100 + Modem 56 (Ethernet Interface)”

Method: We will find the name of the network cards at "C:\windows\system32\config\software\Microsoft\Windows NT\CurrentVersion\NetworkCards"
```
<p>
<a href="#"><img src="/Images/Ques13_1.png" alt ="Ques13_1"></a>
        
<a href="#"><img src="/Images/Ques13_2.png" alt ="Ques13_2"></a>
</p>

### 14. This same file reports the IP address and MAC address of the computer. What are they?
```
The IP address & MAC address of the computer are 192.168.1.111 & 0010a4933e09 respectively.

Method: We will find the IP and MAC Address at "C:\Program Files\Look@LAN\irunin.ini".
```
<p>
<a href="#"><img src="/Images/Ques14.png" alt ="Ques14"></a>
</p>

### 15. An internet search for vendor name/model of NIC cards by MAC address can be used to find out which network interface was used. In the above answer, the first 3 hex characters of the MAC address report the vendor of the card. Which NIC card was used during the installation and set-up for LOOK@LAN?
```
Xircom CardBus Ethernet 100 + Modem 56 (Ethernet Interface)

Method: The NIC Card had MAC Address "0010a4933e09" which we found in the previous question and using the first 3 hex 
        characters of the address and using OUI lookup website online we came to know about the vendor name.
```
<p>
<a href="#"><img src="/Images/Ques15_1.png" alt ="Ques15_1"></a>

<a href="#"><img src="/Images/Ques15_2.png" alt ="Ques15_2"></a>
</p>

### 16. Find 6 installed programs that may be used for hacking.

Sr No. | Program Name  | Usage
------ | ------------- | -------------
   1   | 123WASP | Used for storing Passwords
   2   | Anonymizer | Used to create a proxy
   3   | Cain | Used for Password cracking
   4   | Ethereal | Used for Packet Sniffing      
   5   | Look@LAN | Used for Networking Monitoring
   6   | NetStumbler | Used for hacking WiFi password

```
Method: This all programs can be found at "C:\Program Files"
```

### 17. What is the SMTP email address for Mr. Evil?
```
whoknowsme@sbcglobal.net

Method: We can find this mail by searching for SMTP in the Keyword search box and in that we find "NTUSER.DAT" file.
        This file has a submenu named Text that has the email address.
```
<p>
<a href="#"><img src="/Images/Ques17.png" alt ="Ques17"></a>
</p>

### 18. What are the NNTP (news server) settings for Mr. Evil?
```
Server name: news.dallas.sbcglobal.net
Username: whoknowsme@sbcglobal.net

Method: We can find this by searching for NNTP in the Keyword search box and in that we find "NTUSER.DAT" file.
        This file has a submenu named Text that has the Server name and the Username.
```
<p>
<a href="#"><img src="/Images/Ques18.png" alt ="Ques18"></a>
</p>

### 19. What two installed programs show this information?
```
MS Outlook Express & Forte

Method: We found 4 mail clients from that we need to find which 2 clients are used by Mr. Evil. After some search we find "Agent.ini" 
        which is the file Forte Client and in "C:/Documents and Settings/Mr. Evil/Local Settings/Application Data/Identities/{EF086998-1115-4ECD-9B13-9ADC067B4929}/Microsoft/" 
        we find the data for Outlook Express.
```
<p>
<a href="#"><img src="/Images/Ques19.png" alt ="Ques19"></a>

<a href="#"><img src="/Images/Ques19_1.png" alt ="Ques19_1"></a>
</p>

### 20. List 5 newsgroups that Mr. Evil has subscribed to?

The newsgroups are:
* Alt.binaries.hacking.utilities
* Alt.stupidity.hackers.malicious
* Free.binaries.hackers.malicious
* Free.binaries.hacking.talentless.troll_haven
* alt.dss.hack 
```
Method: We will find this all newsgroups at "C:\Document and Settings\Mr. Evil\Local Settings\Application Data\Identities\{EF086998–1115–4ECD-9B13 9ADC067B4929} \Microsoft\Outlook Express"
```
<p>
<a href="#"><img src="/Images/Ques20.png" alt ="Ques20"></a>
</p>

### 21. A popular IRC (Internet Relay Chat) program called MIRC was installed.  What are the user settings that was shown when the user was online and in a chat channel?
```
User Settings are "user=Mini Me, email=none@of.ya, nick=Mr, & anick=mrevilrulez"

Method: We will found this at "C:\Program Files\mIRC\mirc.ini"
```
<p>
<a href="#"><img src="/Images/Ques21.png" alt ="Ques21"></a>
</p>

### 22. This IRC program has the capability to log chat sessions. List 3 IRC channels that the user of this computer accessed.
```
Some IRC channnels are CyberCafe.UnderNet.log, Chataholics.UnderNet.log, Elite.Hackers.UnderNet.log

Methods: We will finds all the logs at "C:\Program Files\mIRC\logs"
```
<p>
<a href="#"><img src="/Images/Ques22.png" alt ="Ques22"></a>
</p>

### 23. Ethereal, a popular “sniffing” program that can be used to intercept wired and wireless internet packets was also found to be installed. When TCP packets are collected and re-assembled, the default save directory is that users \My Documents directory. What is the name of the file that contains the intercepted data?
```
"Interception" is the file name.

Method: We will find the recent intercepted file stored at the path "C:\Documents and Settings\Mr. Evil\Application Data\Ethereal\recent" 
        and it is named as "Interception".
```
<p>
<a href="#"><img src="/Images/Ques23.png" alt ="Ques23"></a>
</p>

### 24. Viewing the file in a text format reveals much information about who and what was intercepted. What type of wireless computer was the victim (person who had his internet surfing recorded) using?
```
The type of wireless computer used by the victim is "Microsoft Internet Explorer (MSIE) 4.01 with Windows CE (Pocket PC)"

Method: We will find this peice of information at "C:\Documents and Settings\Mr. Evil\interception"
```
<p>
<a href="#"><img src="/Images/Ques24.png" alt ="Ques24"></a>
</p>

### 25. What websites was the victim accessing?
```
The victim tried accessing "mobile.msn.com & MSN Hotmail" websites.

Method: We will the find this information at "C:\Documents and Settings\Mr. Evil\interception".
```
<p>
<a href="#"><img src="/Images/Ques25_1.png" alt ="Ques25_1"></a>

<a href="#"><img src="/Images/Ques25_2.png" alt ="Ques25_2"></a>
</p>

### 26. Search for the main users web based email address. What is it?
```
The main user's web based email address is mrevilrulez@yahoo.com

```
<p>
<a href="#"><img src="/Images/Ques26.png" alt ="Ques26"></a>
</p>

### 27. Yahoo mail, a popular web based email service, saves copies of the email under what file name?
```
"ShowLetter[1].htm" is the file in which yahoo saves copies of the email.

Method: We will find the required information by keyword searching the mail found in previous question.
```
<p>
<a href="#"><img src="/Images/Ques27.png" alt ="Ques27"></a>
</p>

### 28. How many executable files are in the recycle bin?
```
There are 4 executable files in the Recycle Bin.

Method: We will find the deleted executable files at "C:\RECYCLER\S-1–5–21–2000478354–688789844–1708537768–1003\"
```
<p>
<a href="#"><img src="/Images/Ques28.png" alt ="Ques28"></a>
</p>

### 29. Are these files really deleted?
```
No they are not really deleted, we can restore them as and when we require.
```

### 30. How many files are actually reported to be deleted by the file system?
```
1371 total files are deleted
```
<p>
<a href="#"><img src="/Images/Ques30.png" alt ="Ques30"></a>
</p>

### 31. Perform a Anti-Virus check. Are there any viruses on the computer?
```
Autopsy itself performs an antivirus check & it shows its result inside Interesting Items. On seeing that we find out one zip bomb.
```
<p>
<a href="#"><img src="/Images/Ques31.png" alt ="Ques31"></a>
</p>

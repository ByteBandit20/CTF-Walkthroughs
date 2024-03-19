# Meta

# Initial NMAP

# Enumeration

## SSH

SSH was a dead end here since the port was closed on nmap, and I confirmed it by trying to connect with my SSH client

(Editor's note: include text snippit of SSH being closed here)

## HTTP/S

The first step I took when enumerating the open web services was to open them in a browser. Ports 80 and 443 seemed to be hosting a Mr. Robot themed game that requires the player to type commands from a list into a terminal in the browser to learn more about the TV show. As a fan of the show, I thought the game was pretty cool, but I didn't find anything useful here.

(Editor's note: include picture of main webpage here)

I then decided to look at the /robots.txt file in order to see if it contained any other endpoints on the webpage I could explore manually before bruteforcing for files and directories. I ended up finding links for both a file called fsociety.dic, and a file called key-1-of-3.txt. Upon inspection, fsociety.dic is a wordlist that can be used to bruteforce passwords, and the key file contains the first of three keys that can be submitted to TryHackMe for credit. Congrats, you're 1337 now :)

(Editor's note: include picture of robots.txt directory here)

In order to more deeply explore the application, I ran a tool called feroxbuster that can recursively discover files and directories in a web application. The command I used is: ```feroxbuster -u http://10.10.233.74/ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt -x "txt,html,php,asp,aspx,jsp"```. The ```-u``` parameter specifies the url that the tool will target, the ```-w``` parameter specifies the wordlist to be used, and the ```-x``` parameter specifies which file extensions to search for.

(Editor's note: include snippit of output from feroxbuster here)

As we can see here, looking at the directory structure of this web application can give us some insight on how it functions. We are able to tell that the CMS being used is Wordpress. In order to see the verion of Wordpress running on this application, I looked at the license file, and was initially greeted by a joke indicating that there was no information on the page. After scrolling to the bottom however, we see a base64 encoded value which decodes to ```elliot:ER28-0652```. Since SSH is inaccessible as of now, I assumed that these credentials were for the Wordpress site.

(Editor's note: include picture of /license page here)

# Initial Foothold

In order to access the server, I decided to inject a php reverse shell in a theme file on the Wordpress application. 

# User Escelation

# Root Escelation

# Hacker's notes

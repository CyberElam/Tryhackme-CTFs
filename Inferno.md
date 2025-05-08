#Inferno CTF

Connect to your Openvpn file as usual Start the machine wait for the IP.
After getting the IP Address i ran rustscan **"rustscan -a <TargetIP> -r <Range of the ports> -- -A -oN <Output0>"**

It showed Alot of Open Ports and i wasnt in the mood to go through all of them so i just went to Port 80/Webserver
Nothing much showed up so used FFUF to brute force some files or directories
**"ffuf -u <URL>/FUZZ -w <Wordlist>**

You can choose a wordlist you want like Seclist or any other after that got a finding **"/inferno"** It required Credentials so i used hydra to Brute force the creds
**hydra -L /usr/share/wordlists/seclists/Usernames/cirt-default-usernames.txt  -P /usr/share/wordlists/rockyou.txt -f 10.10.138.42 http-get /inferno/**

You can choose your own Username wordlist and Password wordlist i manage to get the Username and Password **"Admin:dante1"**
then loged in saw that the website is running **"Codiad"** googled it and **"it is a web-based Integrated Development Environment (IDE) that allows developers to code from any web browser"** Then i looked around for exploits found one from exploit-db and github i chose the github one then kept it around on a new tab then looked for any other things like config files on the website found nothing so i used the github exploit then got RCE as www-data

#WWW-DATA
I manually looked around the files so find something Interesting then went to the **/home/** directory saw 2 users so checked **Dante** found the first flag but couldnt access it so i looked around dante's files found a interesting file on **/home/dante/Downloads/.download.dat**
so i cat the content of the file and i looked like some encoded stuff so used this website to decode ot **https://www.dcode.fr/ascii-code** then got dante's creds
**dante:V1rg1l10h3lpm3**

#Dante
Loged in using SSH as dante got the first flag now it was time for Privesc so i checked if dante has sudo permissions **(root) NOPASSWD: /usr/bin/tee**
looks like he can run tee as root without a password so i generated a passwd using openssl
**openssl passwd <password>** it will output a hash so place the hash like this
**hacker:<HASH>:0:0:root:/root:/bin/bash"**

on Dante machine run the command
**echo "hacker:<HASH>:0:0:root:/root:/bin/bash" | sudo tee -a /etc/passwd**
then switsh user a the user you entered then you have root privileges

#Root
Get the root flag then solve the lab

#Inferno CTF

Connect to your Openvpn file as usual Start the machine wait for the IP.
After getting the IP Address i ran rustscan **"rustscan -a <TargetIP> -r <Range of the ports> -- -A -oN <Output0>"**

It showed Alot of Open Ports and i wasnt in the mood to go through all of them so i just went to Port 80/Webserver
Nothing much showed up so used FFUF to brute force some files or directories
**"ffuf -u <URL>/FUZZ -w <Wordlist>**

You can choose a wordlist you want like Seclist or any other after that got a finding **"/inferno"** It required Credentials 


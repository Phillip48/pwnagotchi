# Pwnagotchi & Cracking The PCAP Files
[Pwnagotchi](https://pwnagotchi.ai/) is an A2C-based "AI" leveraging bettercap that learns from its surrounding WiFi environment to maximize the crackable WPA key material it captures (either passively, or by performing deauth and association attacks). This material is collected as PCAP files containing any form of handshake supported by hashcat. Pwnagotchi learns over time, the more access your pwnagotchi has to other wifi environments the more it will learn and better it will get. 

For more context the 4-way handshake is a process that happens behind the scenes when you connect to a Wi-Fi network with WPA/WPA2 security. This process consists of the exchange of four packets between the client device and the AP; these are used to derive session keys from the access point’s WiFi password. Once the packets have been successfully exchanged and the keys are generated, the client device is authenticated and can start sending and receiving data packets (now secured by encryption) to and from the wireless AP. Successful recovery of the WiFi key doesn’t necessarily even need all four packets! A half-handshake (containing only two of the four packets) can be cracked, too—and in some (most) cases, just a single packet is enough, even without clients.

## Table of Contents 
[Disclaimer](#disclaimer) <BR>
[Hardware](#hardware) <BR>
[Prerequisite](#prerequisite)<BR>
[Important links](#important-links)<BR>
[Steps](#steps)<BR>
[Steps to make your pwnagotchi better](#steps-to-make-your-pwnagotchi-better)<BR> 
[Crack PCAP Files](#crack-pcap-files)<BR> 
[How to protect yourself](#how-to-protect-yourself)<BR> 

## Disclaimer
Only use this on wifis you own. Although there is passive sniffing we don't recommend you use this on other people's wifi that you don't own. This is simply a tutorial to build a small cool device that helps you further your knowledge.

## Hardware
To build this there are a few things you'll need:
1. Raspberry PI Zero W.
2. Waveshare E-Ink Display.
3. Micro SD Card - 8GB Min.
4. Micro USB cord that supports data transfer.
5. Optionally, you can get a Pisugar2 Portable 1200 mAh UPS Lithium Battery so you can take your pwnagotchi with you.
6. If you'd like to make use of some awesome plugins like saving GPS coordinates whenever an handshake is captured then you'll need a GPS/GLONASS USB.
7. Lastly, if you like it to look more professional and not so bare bones you can either buy or 3d print a case for your pwnagotchi.

## Prerequisite 
You'll need to download a few things before getting started:
1. Filezila - to easily modify the files of your pwnagotchi
2. balenaEtcher - to flash your micro sd card with the pwnagotchi img.
3. Optionally, you could use a VPN with your pwnagotchi so if that's something you want to do then you can get that now. An option is Proton VPN since you can get the free version of that.

## Important links
* https://github.com/jayofelony/pwnagotchi
* https://pwnagotchi.ai/
* https://github.com/SHUR1K-N/Project-Pwnag0dchi
* https://etcher.balena.io/
* https://www.reddit.com/r/pwnagotchi/comments/jvh8hs/rndis_drivers/
* https://gist.github.com/fishd72/d3518ef40479a9272f2bd6c425b7af07

## Steps
1. Grab your micro sd card and plug it into your computer. You'll open [balenaEtcher](https://etcher.balena.io/)
2. Go to jayofelony Github page and download the latest pwnagotchi img release. You'll need to download the 32bit img, not 64bit. [Link here]([pwnagotchi](https://github.com/jayofelony/pwnagotchi)) - You can find the latest release on the right side of the page under the About Us.
3. Now in balenaEtcher you will first select "Flash from file" and select the img you downloaded from Github. Then, you'll select your micro sd card as the target. Finally, you'll select Flash to Flash the micro sd card.
* If the flash is failing you can try unzipping the the folder and selecting the img. That worked for me
4. Once the flash is completed you can remove the micro sd card form the computer and plug it into your Raspberry PI Zero W.
5. Connect your micro usb cable to your computer and the Raspberry PI Zero W. Open device manager and check to make sure it pops up as a network adapater. If it pops up as a port you'll need to download the following network adapter from reddit - [RNDIS Driver](https://www.reddit.com/r/pwnagotchi/comments/jvh8hs/rndis_drivers/)
6. Once downloaded unzip it and save it to your desktop. Right click the file called RNDIS.INF, hit install and that should install the driver. You can confirm it worked by going to your Ethernet adapter settings. You should find an option labeled something along the lines of 'USB Ethernet/RNDIS Gadget'.
7. Right click on the that option mentioned in the above step. Click "Properties" and select the "Use the following IP address" option and input the following:
* IP address: 10.0.0.1
* Subnet mask: 255.255.255.0
* Default gateway: 10.0.0.1(This is optional)
* You can also add a preferred DNS server. For some it helps and i personally did it. Here's what it would look like if you decide to add it:
* Preferred DNS server: 8.8.8.8
* Alternate DNS server: 1.1.1.1(Optional)
8. Click "OK" to close the tab.
9. Now you can connect the pwnagotchi to the internet either by using a VPN or your ethernet/wifi. You'll do this by right clicking either the VPN that shows up as an option in the network adapater settings or by selecting your working ethernet/wifi. Click "Properties" -> Sharing -> You'll want to make sure to check the box "Allow other network users to connect through this computers internet connection" and select the name of the pwnagotchi, usually something like Ethernet with a number.
10. Now you can open your terminal/powershell to ssh into the pwnagotchi. You'll input "ssh pi@10.0.0.2". If you get an error then you'll have too go to your folder -> local desk -> Users -> YourUser -> SSH -> Edir or delete the file called knownHosts.
11. Default password is: "raspberry".
12. You can now use the wizard to setup your pwangotchi if you'd like. Type "sudo pwnagotchi --wizard". *However we will be changing this in the better pwnagotchi part of the tutorial so ignore this if you want to go beyond the basic pwnagotchi.*
13. It will ask if you want to restore a previous config, Hit N because this is a new deivce.
14. Next hit Y to overwrite
15. Name your Pwnagotchi whatever you'd like.
16. Now you'll want to list the number of networks you have and white list them so the pwnagotchi doesn't deauth your networks. So first input how many networks you have.
17. Than the name of the network
18. If you know the Mac address you can enter it but if you don't you can just hit enter to skip this
19. It will ask if you want to enable bluetooth teather. Hit No for now we will update this later.
20. Hit Yes to use a display.
21. Specify what display you have. There is a link in the CLI that will help you find out what you have. Personally i used a wavehsare 3 so i inputted: "waveshare_3"
22. Next you can pick what color background you want. After this the config should be done.
23. You should start to see some signs of life now from pwnagotchi. (This is a basic start without plugins.

## Steps to make your pwnagotchi better
1. Once SSH into your pwnagotchi. Type "sudo nano /etc/ssh/sshd_config". Scroll down and uncomment PermitRootLogin and change it to yes. Saves and exit.
2. To set a root password. Type "sudo su" to be a superuser then type "passwd root". You can now select whatever password you want.
3. Now you can type "service ssh restart".
4. Go to SHUR1K-N Github and download the zip of the Project Pwnag0dchi repo and unzip the folder [Link Here](https://github.com/SHUR1K-N/Project-Pwnag0dchi)
5. Open Filezilla and connect to your pwnagotchi with it.
6. Navigate to User -> local -> share -> pwnagotchi -> custom-plugins.
7. Drag all the plugins from the unzipped folder from github to the custom plugins folder.
8. Navigate to etc -> pwnagotchi and backup the config.toml file. Then drag the config.toml file from the unzipped folder from github to overwrite the current one on your pwnagotchi.
9. Terminate and quit filezilla after this is done uipdating.
10. Reboot the pwnagotchi. You can go to the WEB UI by opening a browser and typing 10.0.0.2:8080 in the browser.
11. Default password should be pwnagotchi for both username and password.
12. Here you can enable or disable plugins easily and edit the config.toml file if needed - be careful doing that as you can break the pwnagotchi.
13. Lastly go to your shell/terminal and ssh into your pwnagotchi then type: "sudo nano /etc/pwnagotchi/config.toml"
14. Here you will need to update the SSID value to whitelist your wifi and do the same for grid exclude.
15. If you want to auto upload handshakes online and crack them you then you need an API Key but its easy and free. Go to [WPA-SEC.Stanev](https://wpa-sec.stanev.org/). Eneter your email. Get the API key from your email and add it to your config.toml file next to the line called: "main.plugins.wpa-sec.api_key". CTRL X to edit and restart the pwnagotchi. This can also be done using the WEBCFG Plugin rather then using a terminal.

## Crack PCAP Files
Here is a guide to how i used wordlists on Kalil Linux to crack PCAP files. This is one way to do it but probably not the best. This is just to check some common passwords. For example if the WPA2 key is "plRDQ48B" You are probably NEVER going to crack it with a wordlist. 
* For more info you can see this video on hashcat attacks: [Youtube](https://www.youtube.com/watch?v=RiX0zfWHS9k)
1. Open 2 terminals. 1 to ssh into and the other for your kali host.
2. On the kali terminal make a directory called handshakes in your desktop
3. SSH into your pwnagotchi through the Kali terminal.
4. Get into root
5. Copy the all PCAP handshakes directory to your pi as root
6. On you Kali host run the following command: sudo scp pi@10.0.0.2:*pcap /home/USERNAMEHERE/Desktop/handshakes
7. Enter password of the pwnagotchi
   * Basically in the command youre ssh into the pwangotchi and creating a secure copy of the pcap file to the handshakes directory that you created
8. On google search up hashcat converter and convert the PCAP you want to use with hashcat.
7. Make sure you have hashcat updated: sudo apt-get install hashcat then sudo apt-get upgrade
8. In the following steps you have the options you can take with getting the pcap files converted.<br>

![image](https://github.com/user-attachments/assets/cb8bf397-45ad-4195-b84b-ac38801918c5)<br>
![image](https://github.com/user-attachments/assets/9c7dbf9b-a2b6-40f7-8f09-1c2eb9febf46)

### Dict Attack
1. Run the following command: hashcat -m 22000 -a 0 -w 3 /FILPATHTOHH22000FILE/ /FILEPATHOFWORDLIST/
   * You can use locate and the file name to find the file path.
   * -m 22000: This specifies the hash type, in this case, Mode 22000 for WPA/WPA2 captures.
   * -a 0: This specifies a straight dictionary attack.
   * -w 3: This option is for workload tuning. It goes from 1 (low) to 4 (insane), where 3 is generally a safe option that performs well.
  
### Brute Force Attack
1. Run the following command: hashcat -m 22000 -a 3 /FILPATHTOHH22000FILE/ ?u?l?l?l?d?d
   * You can use locate and the file name to find the file path.
   * -a 3: This specifies a brute force attack
   * The end of the file is the

### [Association Attack](https://hashcat.net/forum/thread-9534-post-50281.html#pid50281)
This attack requires more knowledge on where the pcap file came from. For example lets say you the know the pcap came from a persons house wiifi. You search up the house using property appraiser and find the persons name is Jake Doe. You can gather information(OSINT) on words that can be used for the wifi. You find his name ofc which is Jake Doe but also he has a dog name Bud, a wife called Sally Doe and maybe you found his birthdate - 01/01/1996. Your word list can include: Jake, Doe, Sally, Bud, 1996, 1, 01, Etc... By doing this and applying rules you are more likely to crack the password than getting lucky on a brute force or dict attack. OFC the more info you gather on the person the better.
1. Run the following command: hashcat -m 22000 -a 9 /FILPATHTOHH22000FILE/ wordlist.txt -r /FILEPATHFORRULES.TXT/ -o results.txt
   * -o results.txt: Defines outfile for recovered hash
   * -a 9: Association attack
   * -m 22000: The hash type *You could also not include this and let it auto detect*
   * -r: Defines the rules file 

## How to protect yourself
Having a strong password is essential to protecting your home internet. Even if something like the pwnagotchi gets the handshake in a PCAP file if you have a strong password it will take a very long time to crack. For example there is a table by [oberlin](https://www.oberlin.edu/cit/bulletins/passwords-matter) on an article called "BeCyberSmart: How Fast Can a Hacker Break YOUR Password?" that shows how having, numbers, upper and lower case letters and synbols is so important. If you have that and the password is 11 characters long it can take up to 3 years to crack. If its 12 characters long it can take up to 226 years. This usually happens with a brute force attack.

Many people don't even change the default password from their router which make it even easier to crack assuming its on a word list(dictonary attack), which is easy to find out. Morale of the story use strong passwords not just for your home internet but any online accounts.

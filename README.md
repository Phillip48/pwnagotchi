# Pwnagotchi
[https://pwnagotchi.ai/](Pwnagotchi) is an A2C-based "AI" leveraging bettercap that learns from its surrounding WiFi environment to maximize the crackable WPA key material it captures (either passively, or by performing deauth and association attacks). This material is collected as PCAP files containing any form of handshake supported by hashcat. Pwnagotchi learns over time, the more access your pwnagotchi has to other wifi environments the more it will learn and better it will get. 

## Hardware
To build this there are a few things you'll need:
1. Raspberry PI Zero W.
2. Waveshare Ink Screen.
3. Micro SD Card - 8GB Min.
4. Optionally, a Pi Sugar battery so you can take your pwnagotchi with you.
5. If you'd like to make use of some awesome plugins like saving GPS coordinates whenever an handshake is captured then you'll need a GPS/GLONASS USB.
6. Lastly, if you like it to lok more professional and not so bare bones you can either buy or 3d print a case for your pwnagotchi.

## Prerequisite 
You'll need to download a dew things before getting started:
1. Filezila - to easily modify the files of your pwnagotchi
2. balenaEtcher - to flash your micro sd card with the pwnagotchi img.
3. Optionally, you could use a VPN with your pwnagotchi so if that's something you want to do then you can get that now. An option is Proton VPN since you can get the free version of that.

## Steps

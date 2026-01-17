# Raspberry Pi Network-Wide Adblocker

## Objective
This Project Objective was to create a network-wide ad-blocking solution using a Raspberry Pi Zero 2 W and Pi-hole. This solution is also taken a step further and paired with tailscale VPN to create ad-blocking functions even when away from home network, providing comprehensive protection regardless of location. The objective was also gain more understanding of DNS protocols, network security, and Linux system administration.


## Skills Learned
- DNS-based ad-blocking and network-level filtering techniques
- Raspberry Pi hardware configuration and Linux OS deployment
- Pi-hole installation and DNS server management
- SSH remote connection
- VPN integration with Tailscale for remote DNS routing\

## Tools Used
- Raspberry Pi Zero 2 W
- SSH (Secure Shell) - Remote terminal access
- Pi-hole - Network-wide ad blocker
- Tailscale - VPN service for remote access and DNS routing
- Raspberry Pi OS (Legacy, 64-bit) Lite - Lightweight Linux operating system without desktop environment
  
## Steps
I'm first going to connect my SD card into my MacBook. Then head over to the raspberry pi website and download the imager

<img width="384" height="400" alt="image" src="https://github.com/user-attachments/assets/62e505f8-01f3-4777-994d-2c0a051b31d6" /><img width="400" height="1000" alt="image" src="https://github.com/user-attachments/assets/ea1c1b93-fb15-4f51-b23a-a7b3f1ef412f" />

After I have downloaded the imager on my Macbook im going to open it and set it up. Im first going to select my raspberry device which is the Raspberry Pi zero 2W. Then I'm going to choose the OS which in this case is the legacy 64-bit lite.
<img width="450" height="800" alt="image" src="https://github.com/user-attachments/assets/0a881c2a-a5a8-4a5b-9835-9298b676bc49" /><img width="450" height="800" alt="image" src="https://github.com/user-attachments/assets/a5cbb7d0-c12e-4f9a-9b57-1aac5f8bd4a6" />

Then it will prompt me to select my WI-FI and enter in my credentials. I will continue with the setup process. The important part is to enable SSH so that im able to connect to the Raspberry Pi. Then I will continue and let write its image onto my SD card.
<img width="450" height="800" alt="image" src="https://github.com/user-attachments/assets/530e76a8-a922-4835-8b6f-6cbd5d76dd47" /><img width="450" height="800" alt="image" src="https://github.com/user-attachments/assets/7996b509-6e6d-423a-b129-a5f9289f7380" />

Now its finished writing to my SD card I'm going to plug the SD card into my raspberry pi then I'm also going to connect the raspberry pi to a power source with my micro USB cable 

<img width="300" height="512" alt="image" src="https://github.com/user-attachments/assets/b673b5a8-3582-48da-8ece-9c123a8a2f70" /><img width="300" height="512" alt="image" src="https://github.com/user-attachments/assets/741c859b-7b66-4720-a378-918cf326d687" /><img width="300" height="512" alt="image" src="https://github.com/user-attachments/assets/539cafe2-fb71-4ef6-a5ab-7bee35ca1405" />

Now I'm going open my terminal to SSH and connect to the pi hole running ``` SSH henry@pihole.local ``` Then i'm going to run the curl command I got from the official website to install pi-hole. Im then going to go through the set up process.
<img width="400" height="800" alt="image" src="https://github.com/user-attachments/assets/a610ca23-2ba6-424a-ae30-10449f993529" />
<img width="400" height="800" alt="image" src="https://github.com/user-attachments/assets/92f6a310-7457-4665-aecb-e94340120297" />

It will then prompt me to set a static ip address to my Pi hole. I will navigate to https://192.168.0.1/ to access my Wi-Fi settings and set a DHCP reservation for my pi server. After doing that I will hit continue.
<img width="600" height="800" alt="image" src="https://github.com/user-attachments/assets/409ca84f-83c1-4716-b21a-bb048f7d122e" />
<img width="618" height="51" alt="image" src="https://github.com/user-attachments/assets/8ac3291b-d92e-4f56-8bc2-3ebfcde9b46a" />

For my DNS provider I will choose Cloudflare. Then for the privacy mode I will select option 2: hide domains and clients
<img width="400" height="296" alt="image" src="https://github.com/user-attachments/assets/3a8159ca-6415-4083-ad33-58e5001acc38" /><img width="400" height="744" alt="image" src="https://github.com/user-attachments/assets/41854f69-04e6-46b9-a947-e76809f3b15d" />

Now its installed and I have to configure my Wi-Fi settings so that all traffic will use the Pi-hole as the DNS server. After I'm done with routing all requests through my Pi-hole. I will head over to my admin page my entering the static ip address assigned to my pi-hole followed with admin. It would look like ```IP-Address/admin```.

<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/2b2a7930-41f5-43a9-9f00-231dbd4cbb32" />
<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/d7f08149-34cf-4701-8b4a-0e35f0acc7fd" />

With the Dashboard ready I'm going to set a new password just to get it out of the way. In the terminal I make sure i connected via SSH and  run ```  sudo pihole setpassword ```. 
<img width="800" height="254" alt="image" src="https://github.com/user-attachments/assets/a34905e5-9bff-4e5c-8150-5471d618564b" />

I'm also going to add one more URL to the blocklist. I obtained this URL from the GitHub repo: https://github.com/hagezi/dns-blocklists?tab=readme-ov-file#pro. Now I'm going to paste it into my pi hole lists management.
<img width="500" height="600" alt="image" src="https://github.com/user-attachments/assets/f408e4b7-3d99-4461-8ecf-5ee128fad21e" />

I'm now going to take this a step further and install Tailscale so that I am able to have this adblocking function even when I'm away from home! I'm going to copy and paste the command to install Tailscale into my pi-hole. Using the command ``` curl -fsSL https://tailscale.com/install.sh | sh ```
It's going to tell me to run ``` sudo tailscale up ``` to finish intalling. Then it will tell me to visit the link given to authenticate.

<img width="1000" height="720" alt="image" src="https://github.com/user-attachments/assets/08611833-ee6a-4a59-8202-f5715a88c289" />
<img width="1000" height="288" alt="image" src="https://github.com/user-attachments/assets/9ef74d0d-7b31-4fb7-a4fe-85b52ac795e2" />

I will then create an account. In the Tailscale Dashboard I will copy my Pi-hole address and paste it into a new nameserver on the DNS section of Tailscale. With this connected I can download Tailscale on any platform such as Iphone, Macbook, Windows, and more. With Tailscale downloaded on the device I can connect on the app using VPN. This means that every  DNS request will pass through my Pi-hole server leading to ads and pop-ups being blocked even when im not on my home network!

<img width="801" height="327" alt="image" src="https://github.com/user-attachments/assets/82d5425a-ba1b-4f85-bb3e-9c5eb62f50a6" />


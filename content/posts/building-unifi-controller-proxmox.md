---
title: "Building the lastest version of UniFi Controller on Proxmox Container"
date: 2022-10-07T14:49:36-04:00
slug: 2022-10-07-building-unifi-controller-proxmox
type: posts
draft: false
categories:
  - How-To
tags:
  - ubiquiti
  - proxmox
  - unifi
---

I didn't want to buy a CloudKey to manage my Ubiquiti APs, and wanted something lightweight to run the controller. After some research and testing out different methods, I opted to install it directly on a Proxmox container. I found a super handy install script from [Glenn R](https://glennr.nl/) on the Ubiquiti forums which has worked great for me.

Here are the steps I use to install the controller.

1. Download an Ubuntu container template into your Proxmox VE
2. Create LXC container in Proxmox with the template you just downloaded. My current config:

    * Hostname: Unifi01
    * 1 vCPU
    * 1GB Memory
    * 32GB Storage
    * Static IPv4: `{chosen static IP, or use DHCP}`
    * MAC: `{MAC address if needed}`
3. Log into the container and update

    `sudo apt update && sudo apt upgrade -y`
4. Install CA certificates
 
     `sudo apt-get install ca-certificates wget -y`
5. Download install script -versions available [here](https://community.ui.com/questions/UniFi-Installation-Scripts-or-UniFi-Easy-Update-Script-or-UniFi-Lets-Encrypt-or-UniFi-Easy-Encrypt-/ccbc7530-dd61-40a7-82ec-22b17f027776), or download the lastest version

    `rm unifi-latest.sh &> /dev/null; wget https://get.glennr.nl/unifi/install/install_latest/unifi-latest.sh && bash unifi-latest.sh`
    
    **Optional/Troubleshooting: make script executable chmod +x {script}.sh*
6. Run the script and follow the install prompts
    <br>`bash {script}.sh --skip --fqdn {FQDN}:www.{FQDN}`


Congratulations! You should now have a fully functional UniFi controller running on a Proxmox LXC container. Go to https://{address}:8443/ to finish setup.
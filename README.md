# orange-pi-hole
Setting up pi hole on an orange pi zero 3

## Prerequisites:
- know how to get on the admin page of your router
- know how to unzip files
- know the difference between website urls and shell commands

## Get an OS on the board:
- download debian from the official orange website: http://www.orangepi.org/
  - take note of exact type of board, including the RAM size.
  - verify download with powershell: `Get-FileHash [FILENAME] -Algorithm SHA256`
- flash it on the SD card with "Balena Etcher": https://etcher.balena.io/
- HARDWARE: connect the orange-pi to your router (ethernet) and give it power (usb-c)
  - you should see it show up in your routers admin page, take note of the ip adress
- log into the device with powershell: `ssh orangepi@ipadress`
  - optional: change password with `passwd`

## Install pihole on the device:
- while logged into the device, command: `curl -sSL https://install.pi-hole.net | bash`
  - source: https://docs.pi-hole.net/main/basic-install/
  - requires root access, so either sudo or login with root
- end0 for wired connection (which i did), wlan0 for wireless connection
- Upstream DNS provider:
  - I used my default DNS provider
    - in a new cmd window, type `ipconfig /all`, note the adresses under "DNS servers".
    - fill those in under the "custom dns" option of the pihole installation.

## Configure router:
- login, user rights seem enough
- Give the orange pi a static IP:
  - Local Network > LAN > DHCP Binding
  - create a new binding, copy the MAC and IP adresses of the connected orangepi
- Use the orange pi as DNS:
  - Local Network > LAN > DHCP Server
    - ISP DNS: Off
    - Primary DNS: ip adress of orangepi.
- When the orangepi is disconnected, the ads come back; when it is reconnected, the ads go away
      

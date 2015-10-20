# WR841N-VPN
OpenWrt image and configuration for TL-WR841N router with VPN server

The TP-Link TL-WR841N device is a cheap router (16E delivered) that has some limited out-of-the box capabilities.
An OpenWRT build exists for it but, unfortunately, because of the limited 4MB Flash memory, a lot of options are not available.

I wanted to configure a drop-box that allows you to give this router to anyone in the world and have an out-of-the-box VPN server. This way you can get rid of most YouTube ads (especially prevalent in Germany), connect to a home network or bypass hotel/corporate/country firewalls.

What the image includes:
- LuCi web-based configuration for the usual tasks: WiFi, firewall, trafic monitoring, backup/flash, interfaces, DHCP
- Dynamic DNS with web-based configurator
- dropbear ssh server to allow remote ssh connection
- nano editor for the command line
- PPTP VPN server

What it does not include:
- **ipv6 - most of the support removed because of security and space concerns**
 
L2TP was chosen because of space concerns. If you are worried about privacy and 3rd parties intercepting your traffic you should not use this image. This is intended only for casual browsing.

The image has been running for a few months now with no issues.

**Because of the limited flash space you cannot install any addons - you would have to compile a new firmware yourself.**

Install procedure and general information: http://wiki.openwrt.org/toh/tp-link/tl-wr841nd#installing_via_web_interface

**Example configuration file:**
See the release folder for an example configuration which adds VPN server support.
The WiFi SSID is "MYWIRELESSNET" and the password for that is "WirelessPassword".

There are 3 VPN users set up: 'user1' with 'password1', user2/password2, user3/password3. These are editable in /etc/config/pptpd . The other options are in /etc/ppp/options.pptpd.

Remote web port is set to 4443. The SSH port you will have to find out.

To flash the example configuration, go to the LuCi interface (port 80, 443 or 4443), choose the System menu, "Backup/Fflash firmware", "Restore backup" and choose the my example file.
*You can check or edit the options before uploading by unpacking the backup .tar.gz file, editing the files and then repacking it. Most file commanders or archivers are able to handle that.*

The root ssh password has been deleted, I have not tested if you can restore it via LuCi. If not, you need to edit the /etc/shadow file to add an encrypted password instead of '*', before uploading.

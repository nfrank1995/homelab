# homelab
Everything regarding my private homelab setup
## Server Setup
### Laptops
To keep the server running even when the lid is closed add the following lines to /etc/systemd/logind.conf 
```shell
HandleLidSwitch=ignore
HandleLidSwitchExternalPower=ignore
HandleLidSwitchDocked=ignore
```
To turn the screen off after some time change the following line to /etc/default/grub
```shell
GRUB_CMDLINE_LINUX_DEFAULT="quiet consoleblank=60"
```
reference [Laptop runnind as a server](https://gist.github.com/tankibaj/71547848decdd7cc3bf0c6df68935c8f)
### Activation ethernet interface if not available
after setting up ubuntu server with a wlan connection the ethernet interface was not active, to change this configure the interface in the config file found in /etc/netplan/ folder. An example Netplan Configuration looksl ike this
``` shell
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: true  # Get IPv4 from DHCP on Ethernet
      dhcp6: false # Disable IPv6 for this example
  wifis:
    wlan0:
      dhcp4: true  # Get IPv4 from DHCP on Wi-Fi
      dhcp6: false # Disable IPv6 for this example
      access-points:
        "Your_WiFi_SSID": # Replace with your Wi-Fi network name
          password: "Your_WiFi_Password" # Replace with your Wi-Fi password
```

to get the names of the interfaces used in the configs run 

```shell
ip link show
```

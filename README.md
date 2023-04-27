## **linux_networking**

## IP INTERFACE COMMANDS
```
sudo apt install net-tools    > **If ifconfig command not found.**

ip link
ip -c r | column -t
ip -br a
ip -j a 
sudo apt install jq -y
ip -j a | jq
ip -o -4
ip a s | sed -ne 's,^ *inet6* \([^ /]*\)/.*$,\1,p' | sort -u
ip a s | awk -ne 's, ^ *inet6* \([^ /]*\)/.*$,\,p' | sort -u
ip -o -4 a
ip -o -4 a | awk '{print $4}'
ip a | grep inet | sort -n
cd /sys/class/net/                             > **To check network interface**

nano /etc/network/interfaces
----change form static to dhcp---
ifdown <interface name>
ifup <interface name>

nano /etc/network/interfaces
----change form dhcp to static---
iface ens3 inet static
        address 10.0.0.12/24
        gateway 10.0.0.1
ifdown <interface name>
ifup <interface name>
dhclient
ifquery <interface-name>
```
## IP ROUTE COMMANDS
```
ip route show
ip r
ip -c r | column -t
sudo ip r delete default
sudo ip r add default via 10.0.2.1
ip r
sudo ip r add 192.168.1.0/24 dev ens3         > **To add route to the interface**       
ip r
```
## HOSTNAME AND DNS
```
hostname
hostnamectl
hostnamectl set-hostname pt1.example.com 
hostnamectl set-hostname --pretty "This System used Development purpose"
hostnamtctl set-location building3
```
# NETWORK MANAGER CLI
```
nmcli                                         > Displays the network configuration
cat /etc/resolv.conf                          > To check the DNS server, Domain 
cat /etc/systemd/resolved.conf                > Ohter way in the different Linux distors
cat /etc/hosts                                > To check DNS mapped to and changing nano instead of cat
10.0.0.3   webserver.example.com  webserver   > Format to mention DNS mapping to the IP
nmcli con show                                > Displays the available NetworkManager connections
nmcli con mod <network-interface>            > Modifies the connection without the shell
nmcli con down <network-interface>            > Brings the network interface down
nmcli con up <network-interface>              > Brings the network interface up
nmcli con edit <network-interface>            > Opens the nmcli shell  
nmcli c m "Wired connection 1" ipv4.method manual ipv4.address 10.0.0.12/24 ipv4.gateway 10.0.0.1 ipv4.dns 8.8.8.8
nmcli c m "Wired connection 1" ipv4.method manual ipv4.address 10.0.0.12/24,10.0.0.13/24 ipv4.gateway 10.0.0.1 ipv4.dns 8.8.8.8
nmcli connection down "Wired connection 1"
nmcli connection up "Wired connection 1"
nmcli con show
nmcli con mod "Wired connection 1" ipv4.dns-search "example.local"
nmcli conneciton mod "Wired connection 1" ipv4.method auto
nmcli connection down "Wired connection 1"
nmcli connection up "Wired connection 1"
nmcli con show
nmcli c m "Wired connection 1" -ipv4.address 10.0.0.12/24        > To delete the IP
nmcli c m "Wired connection 1" 
nmcli > remove ipv4.address 10.0.0.12/24
nmcli > set ipv4.address 10.0.0.13/24
nmcli > save
nmcli > activate
nmcli > quit
```
## NETWORKING SERVICES
```
sudo systemctl status networking.service
service networking status
/etc/init.d/networking status
cat /etc/network/interfaces
```

## Ubuntu Specific Arch linux distros
```
sudo systemctl status systemd-networkd
netplan try
networkctl
networkctl status
journalctl -u systemd-networkd
networkctl down <interface-name>
networkctl up <interface-name>
resolvectl status
ubuntu: /etc/netplan
other distros : /etc/systemd/network
```

## Network manager Most widely used in the industry maily in fedora Redhat Centos Desktop Environment
```
systemctl status NetworkManager
Can be configured with a variety of tools:
1. Settings 2. nm-connection-editor 3. nmtui 4. nmcli 4. cockpit and configuration files (not recommended).

sudo systemctl status cockpit.socket         (**This Opens Port 9090 to access GUI from the Browser not recommended**)
sudo systemctl --now disable  cockpit.socket
```
## NETWORK PORT SCANNING
```
sudo apt install nmap
sudo namp 10.0.0.3 -P            > Scanning the Open ports on this IP
```

## READING SPECIFIC LOGS FOR THE SERVICE
```
journal -u NetworkManager | tail -10 | less
```

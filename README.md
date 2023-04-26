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

cd /sys/class/net/                             > **To check network interface**
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
nmcli                                         > to check the DNS SERVER
cat /etc/resolv.conf                          > To check the DNS server, Domain 
cat /etc/systemd/resolved.conf                > Ohter way in the different Linux distors
cat /etc/hosts                                > To check DNS mapped to and changing nano instead of cat
10.0.0.3   webserver.example.com  webserver   > Format to mention DNS mapping to the IP
nmcli con show 
nmcli con show <network-interface>
nmcli con down <network-interface>
cmcli con edit <network-interface>




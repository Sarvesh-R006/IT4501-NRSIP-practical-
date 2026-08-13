# Experiment 10 - Network Troubleshooting with Wireshark and CLI

Cisco CLI configuration and verification files extracted from the supplied NRSIP Lab Manual. Formatting has been cleaned so commands can be copied into Packet Tracer/GNS3 consoles.

## Files
- `Router1.cfg`
- `Router2.cfg`
- `VPCS_IP_Configuration.txt`
- `verification.txt`
- `wireshark_filters.txt`

> Packet Tracer `.pkt` and GNS3 project files are not included; this repository contains the source/configuration commands from the manual.


## `Router1.cfg`

```cisco
enable
configure terminal
interface gigabitEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
exit
interface gigabitEthernet0/1
 ip address 10.0.12.1 255.255.255.252
 no shutdown
exit
ip route 192.168.2.0 255.255.255.0 10.0.12.2
end
```


## `Router2.cfg`

```cisco
enable
configure terminal
interface gigabitEthernet0/0
 ip address 10.0.12.2 255.255.255.252
 no shutdown
exit
interface gigabitEthernet0/1
 ip address 192.168.2.1 255.255.255.0
 no shutdown
exit
ip route 192.168.1.0 255.255.255.0 10.0.12.1
end
```


## `VPCS_IP_Configuration.txt`

```text
PC1: 192.168.1.2 /24
PC2: 192.168.2.2 /24
```


## `verification.txt`

```text
show ip interface brief
show interfaces
show ip route
show arp
show running-config
show cdp neighbors
show ip protocols

PC1:
ping 192.168.2.2
traceroute 192.168.2.2

PC2:
ping 192.168.1.2
```


## `wireshark_filters.txt`

```text
icmp
arp
ip.addr==192.168.1.2
ip.addr==192.168.2.2
icmp || arp
```

# Experiment 3 - IPv4 Subnetting and VLSM Design

Cisco CLI configuration and verification files extracted from the supplied NRSIP Lab Manual. Formatting has been cleaned so commands can be copied into Packet Tracer/GNS3 consoles.

## Files
- `Router1.cfg`
- `Router2.cfg`
- `IP_Addressing.txt`
- `verification.txt`

> Packet Tracer `.pkt` and GNS3 project files are not included; this repository contains the source/configuration commands from the manual.


## `IP_Addressing.txt`

```text
PC1: 192.168.10.2 /26, gateway 192.168.10.1
PC2: 192.168.10.66 /27, gateway 192.168.10.65
PC3: 192.168.10.98 /28, gateway 192.168.10.97

R1 G0/0: 192.168.10.1 /26
R1 G0/1: 192.168.10.65 /27
R1 S0/0/0: 192.168.10.113 /30
R2 S0/0/0: 192.168.10.114 /30
R2 G0/0: 192.168.10.97 /28

VLSM:
LAN1 192.168.10.0/26
LAN2 192.168.10.64/27
LAN3 192.168.10.96/28
WAN  192.168.10.112/30
```


## `Router1.cfg`

```cisco
enable
configure terminal
interface gigabitEthernet0/0
 ip address 192.168.10.1 255.255.255.192
 no shutdown
exit
interface gigabitEthernet0/1
 ip address 192.168.10.65 255.255.255.224
 no shutdown
exit
interface serial0/0/0
 ip address 192.168.10.113 255.255.255.252
 clock rate 64000
 no shutdown
exit
ip route 192.168.10.96 255.255.255.240 192.168.10.114
end
write memory
```


## `Router2.cfg`

```cisco
enable
configure terminal
interface serial0/0/0
 ip address 192.168.10.114 255.255.255.252
 no shutdown
exit
interface gigabitEthernet0/0
 ip address 192.168.10.97 255.255.255.240
 no shutdown
exit
ip route 192.168.10.0 255.255.255.192 192.168.10.113
ip route 192.168.10.64 255.255.255.224 192.168.10.113
end
write memory
```


## `verification.txt`

```text
show ip interface brief
show ip route
show running-config
show interfaces

ping 192.168.10.98
ping 192.168.10.2
ping 192.168.10.66
```

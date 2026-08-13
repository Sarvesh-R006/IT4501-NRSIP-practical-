# Experiment 1 - VLAN Configuration and Inter-VLAN Routing

Cisco CLI configuration and verification files extracted from the supplied NRSIP Lab Manual. Formatting has been cleaned so commands can be copied into Packet Tracer/GNS3 consoles.

## Files
- `Switch0.cfg`
- `Router0.cfg`
- `PC_IP_Configuration.txt`
- `verification.txt`

> Packet Tracer `.pkt` and GNS3 project files are not included; this repository contains the source/configuration commands from the manual.


## `PC_IP_Configuration.txt`

```text
PC0: 192.168.10.2 /24, gateway 192.168.10.1
PC1: 192.168.10.3 /24, gateway 192.168.10.1
PC2: 192.168.20.2 /24, gateway 192.168.20.1
PC3: 192.168.20.3 /24, gateway 192.168.20.1
```


## `Router0.cfg`

```cisco
enable
configure terminal
interface gigabitEthernet0/0
 no shutdown
exit
interface gigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
exit
interface gigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
exit
end
```


## `Switch0.cfg`

```cisco
enable
configure terminal
vlan 10
 name SALES
exit
vlan 20
 name HR
exit
interface range fa0/1-2
 switchport mode access
 switchport access vlan 10
exit
interface range fa0/3-4
 switchport mode access
 switchport access vlan 20
exit
interface fa0/24
 switchport mode trunk
exit
end
```


## `verification.txt`

```text
show vlan brief
show interfaces trunk
show ip interface brief

PC0:
ping 192.168.10.3
ping 192.168.10.1
ping 192.168.20.2

PC2:
ping 192.168.20.3
ping 192.168.20.1
ping 192.168.10.2
```

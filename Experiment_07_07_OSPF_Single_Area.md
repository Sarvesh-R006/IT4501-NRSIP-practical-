# Experiment 7 - OSPF Single-Area Configuration

Cisco CLI configuration and verification files extracted from the supplied NRSIP Lab Manual. Formatting has been cleaned so commands can be copied into Packet Tracer/GNS3 consoles.

## Files
- `Router1.cfg`
- `Router2.cfg`
- `Router3.cfg`
- `VPCS_IP_Configuration.txt`
- `verification.txt`

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
router ospf 1
 network 192.168.1.0 0.0.0.255 area 0
 network 10.0.12.0 0.0.0.3 area 0
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
 ip address 10.0.23.1 255.255.255.252
 no shutdown
exit
interface gigabitEthernet0/2
 ip address 192.168.2.1 255.255.255.0
 no shutdown
exit
router ospf 1
 network 10.0.12.0 0.0.0.3 area 0
 network 10.0.23.0 0.0.0.3 area 0
 network 192.168.2.0 0.0.0.255 area 0
end
```


## `Router3.cfg`

```cisco
enable
configure terminal
interface gigabitEthernet0/0
 ip address 10.0.23.2 255.255.255.252
 no shutdown
exit
interface gigabitEthernet0/1
 ip address 192.168.3.1 255.255.255.0
 no shutdown
exit
router ospf 1
 network 10.0.23.0 0.0.0.3 area 0
 network 192.168.3.0 0.0.0.255 area 0
end
```


## `VPCS_IP_Configuration.txt`

```text
PC1: 192.168.1.2 /24, gateway 192.168.1.1
PC2: 192.168.2.2 /24, gateway 192.168.2.1
PC3: 192.168.3.2 /24, gateway 192.168.3.1
```


## `verification.txt`

```text
show ip interface brief
show ip ospf neighbor
show ip route
show ip protocols
show ip ospf database
show running-config

PC1:
ping 192.168.2.2
ping 192.168.3.2

PC2:
ping 192.168.1.2
ping 192.168.3.2

PC3:
ping 192.168.1.2
ping 192.168.2.2
```

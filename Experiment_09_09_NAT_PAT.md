# Experiment 9 - NAT and PAT Configuration

Cisco CLI configuration and verification files extracted from the supplied NRSIP Lab Manual. Formatting has been cleaned so commands can be copied into Packet Tracer/GNS3 consoles.

## Files
- `Router1_Dynamic_NAT.cfg`
- `Router1_PAT_Overload.cfg`
- `PC_Server_IP_Configuration.txt`
- `verification.txt`

> Packet Tracer `.pkt` and GNS3 project files are not included; this repository contains the source/configuration commands from the manual.


## `PC_Server_IP_Configuration.txt`

```text
PC1: 192.168.1.2 /24, gateway 192.168.1.1
PC2: 192.168.1.3 /24, gateway 192.168.1.1
Server: 200.1.1.2 /24, gateway 200.1.1.1
```


## `Router1_Dynamic_NAT.cfg`

```cisco
enable
configure terminal
interface gigabitEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 ip nat inside
 no shutdown
exit
interface gigabitEthernet0/1
 ip address 200.1.1.1 255.255.255.0
 ip nat outside
 no shutdown
exit
ip route 0.0.0.0 0.0.0.0 200.1.1.2
access-list 1 permit 192.168.1.0 0.0.0.255
ip nat pool NATPOOL 200.1.1.10 200.1.1.20 netmask 255.255.255.0
ip nat inside source list 1 pool NATPOOL
end
write memory
```


## `Router1_PAT_Overload.cfg`

```cisco
enable
configure terminal
interface gigabitEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 ip nat inside
 no shutdown
exit
interface gigabitEthernet0/1
 ip address 200.1.1.1 255.255.255.0
 ip nat outside
 no shutdown
exit
ip route 0.0.0.0 0.0.0.0 200.1.1.2
access-list 1 permit 192.168.1.0 0.0.0.255
ip nat inside source list 1 interface gigabitEthernet0/1 overload
end
write memory
```


## `verification.txt`

```text
show ip nat translations
show ip nat statistics
show ip interface brief
show running-config
show access-lists

PC1:
ping 200.1.1.2

PC2:
ping 200.1.1.2
```

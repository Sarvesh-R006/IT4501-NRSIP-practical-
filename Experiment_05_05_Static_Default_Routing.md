# Experiment 5 - Static and Default Route Configuration

Cisco CLI configuration and verification files extracted from the supplied NRSIP Lab Manual. Formatting has been cleaned so commands can be copied into Packet Tracer/GNS3 consoles.

## Files
- `Router1.cfg`
- `Router2.cfg`
- `Router3.cfg`
- `PC_IP_Configuration.txt`
- `verification.txt`

> Packet Tracer `.pkt` and GNS3 project files are not included; this repository contains the source/configuration commands from the manual.


## `PC_IP_Configuration.txt`

```text
PC1: 192.168.1.2 /24, gateway 192.168.1.1
PC2: 192.168.2.2 /24, gateway 192.168.2.1
PC3: 192.168.3.2 /24, gateway 192.168.3.1
```


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
ip route 192.168.3.0 255.255.255.0 10.0.12.2
end
write memory
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
ip route 192.168.1.0 255.255.255.0 10.0.12.1
ip route 192.168.3.0 255.255.255.0 10.0.23.2
end
write memory
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
ip route 0.0.0.0 0.0.0.0 10.0.23.1
end
write memory
```


## `verification.txt`

```text
show ip interface brief
show ip route
show running-config
show ip protocols
show interfaces

ping 192.168.1.2
ping 192.168.2.2
ping 192.168.3.2
traceroute 192.168.3.2
```

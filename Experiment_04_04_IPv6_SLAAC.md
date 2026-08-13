# Experiment 4 - IPv6 Configuration and SLAAC

Cisco CLI configuration and verification files extracted from the supplied NRSIP Lab Manual. Formatting has been cleaned so commands can be copied into Packet Tracer/GNS3 consoles.

## Files
- `Router1.cfg`
- `Router2.cfg`
- `PC_SLAAC.txt`
- `verification.txt`

> Packet Tracer `.pkt` and GNS3 project files are not included; this repository contains the source/configuration commands from the manual.


## `PC_SLAAC.txt`

```text
PC1: Desktop -> IP Configuration -> IPv6 Auto Config (SLAAC)
PC2: Desktop -> IP Configuration -> IPv6 Auto Config (SLAAC)
```


## `Router1.cfg`

```cisco
enable
configure terminal
ipv6 unicast-routing
interface gigabitEthernet0/0
 ipv6 address 2001:DB8:1:1::1/64
 no shutdown
exit
interface gigabitEthernet0/1
 ipv6 address 2001:DB8:1:12::1/64
 no shutdown
exit
ipv6 route 2001:DB8:1:2::/64 2001:DB8:1:12::2
end
write memory
```


## `Router2.cfg`

```cisco
enable
configure terminal
ipv6 unicast-routing
interface gigabitEthernet0/0
 ipv6 address 2001:DB8:1:12::2/64
 no shutdown
exit
interface gigabitEthernet0/1
 ipv6 address 2001:DB8:1:2::1/64
 no shutdown
exit
ipv6 route 2001:DB8:1:1::/64 2001:DB8:1:12::1
end
write memory
```


## `verification.txt`

```text
show ipv6 interface brief
show ipv6 route
show ipv6 interface
show ipv6 neighbors
show running-config
ping 2001:DB8:1:12::2
ping 2001:DB8:1:1::1

PCs:
ipconfig
ping
```

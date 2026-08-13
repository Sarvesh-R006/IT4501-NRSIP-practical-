# Experiment 2 - STP Verification and Root Bridge Election

Cisco CLI configuration and verification files extracted from the supplied NRSIP Lab Manual. Formatting has been cleaned so commands can be copied into Packet Tracer/GNS3 consoles.

## Files
- `S1_Root_Bridge.cfg`
- `S2.cfg`
- `S3.cfg`
- `PC_IP_Configuration.txt`
- `verification.txt`

> Packet Tracer `.pkt` and GNS3 project files are not included; this repository contains the source/configuration commands from the manual.


## `PC_IP_Configuration.txt`

```text
PC1: 192.168.1.2 /24, gateway 192.168.1.1
PC2: 192.168.1.3 /24, gateway 192.168.1.1
PC3: 192.168.1.4 /24, gateway 192.168.1.1
```


## `S1_Root_Bridge.cfg`

```cisco
enable
configure terminal
spanning-tree vlan 1 priority 4096
end
write memory
```


## `S2.cfg`

```cisco
enable
show spanning-tree
```


## `S3.cfg`

```cisco
enable
show spanning-tree
```


## `verification.txt`

```text
show spanning-tree
show spanning-tree vlan 1
show spanning-tree summary
show interfaces status
show mac address-table
show running-config

PC1:
ping 192.168.1.3
ping 192.168.1.4
```

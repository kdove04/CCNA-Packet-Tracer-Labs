# Day 18 Lab: VLANs (Part 3)

Completed Cisco Packet Tracer lab from Jeremy's IT Lab CCNA 200-301 course (Day 18, VLANs Part 3).

## What I practiced

- Configuring the native VLAN on a router-on-a-stick subinterface
- Inter-VLAN routing on a multilayer (Layer 3) switch with SVIs
- Enabling routing on the switch with `ip routing`
- Turning a switch port into a routed port with `no switchport`
- Verifying with `show ip interface brief` and `show ip route`

## Key commands

```
interface g0/0.99
 encapsulation dot1q 99 native
!
ip routing
interface vlan 10
 ip address <gateway-ip> <mask>
 no shutdown
interface g0/1
 no switchport
 ip address <ip> <mask>
!
show ip route
```

## Files

| File | Description |
|---|---|
| `.pkt` file in this folder | My completed lab. Open it with Cisco Packet Tracer 8.x. |

## Credit

Lab topology and tasks are from [Jeremy's IT Lab](https://www.youtube.com/@JeremysITLab) free CCNA course. The configuration in the file is my own work.

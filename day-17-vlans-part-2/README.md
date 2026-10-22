# Day 17 Lab: VLANs (Part 2)

Completed Cisco Packet Tracer lab from Jeremy's IT Lab CCNA 200-301 course (Day 17, VLANs Part 2).

## What I practiced

- Configuring 802.1Q trunk links between switches and to a router
- Controlling which VLANs are allowed on a trunk
- Setting the native VLAN on a trunk
- Routing between VLANs with router-on-a-stick (one subinterface per VLAN)
- Verifying with `show interfaces trunk` and `show vlan brief`

## Key commands

```
interface g0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
 switchport trunk native vlan 1001
!
interface g0/0.10
 encapsulation dot1q 10
 ip address <gateway-ip> <mask>
!
show interfaces trunk
```

## Files

| File | Description |
|---|---|
| `.pkt` file in this folder | My completed lab. Open it with Cisco Packet Tracer 8.x. |

## Credit

Lab topology and tasks are from [Jeremy's IT Lab](https://www.youtube.com/@JeremysITLab) free CCNA course. The configuration in the file is my own work.

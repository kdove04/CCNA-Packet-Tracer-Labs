# Day 16 Lab: VLANs (Part 1)

Completed Cisco Packet Tracer lab from Jeremy's IT Lab CCNA 200-301 course (Day 16, VLANs Part 1).

## What I practiced

- Creating and naming VLANs on a Cisco switch
- Assigning switch ports to VLANs as access ports
- Keeping each department in its own broadcast domain
- Routing between VLANs through the router
- Verifying the setup with `show vlan brief`

## Key commands

```
vlan 10
 name <VLAN-NAME>
interface range f0/1 - 2
 switchport mode access
 switchport access vlan 10
show vlan brief
```

## Files

| File | Description |
|---|---|
| [Day 16 Lab - VLANs (Part 1) kd .pkt](Day%2016%20Lab%20-%20VLANs%20%28Part%201%29%20kd%20.pkt) | My completed lab. Open it with Cisco Packet Tracer 8.x. |

## Credit

Lab topology and tasks are from [Jeremy's IT Lab](https://www.youtube.com/@JeremysITLab) free CCNA course. The configuration in the file is my own work.

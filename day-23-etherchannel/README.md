# Day 23 Lab: EtherChannel

Completed Cisco Packet Tracer lab from Jeremy's IT Lab CCNA 200-301 course (Day 23, EtherChannel).

## What I practiced

- Bundling multiple physical links into one logical port-channel
- Negotiating EtherChannels with LACP (`active` / `passive`) and PAgP (`desirable` / `auto`), and static `on` mode
- Matching member port settings (speed, duplex, switchport mode, allowed and native VLANs)
- Configuring the port-channel interface as a trunk
- Checking and changing load balancing with `port-channel load-balance`
- Verifying with `show etherchannel summary`

## Key commands

```
interface range g0/1 - 2
 channel-group 1 mode active
!
interface port-channel 1
 switchport mode trunk
!
port-channel load-balance src-dst-ip
!
show etherchannel summary
show etherchannel load-balance
```

## Files

| File | Description |
|---|---|
| [Day 23 Lab - EtherChannel - kd.pkt](Day%2023%20Lab%20-%20EtherChannel%20-%20kd.pkt) | My completed lab. Open it with Cisco Packet Tracer 8.x. |

## Credit

Lab topology and tasks are from [Jeremy's IT Lab](https://www.youtube.com/@JeremysITLab) free CCNA course. The configuration in the file is my own work.

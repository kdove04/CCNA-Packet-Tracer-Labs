# Day 22 Lab: Rapid STP

Completed Cisco Packet Tracer lab from Jeremy's IT Lab CCNA 200-301 course (Day 22, Rapid Spanning Tree Protocol).

## What I practiced

- Switching the STP mode to Rapid PVST+ with `spanning-tree mode rapid-pvst`
- Controlling root bridge placement with `spanning-tree vlan <id> root primary` and `root secondary`
- Identifying RSTP port roles: root, designated, alternate and backup
- Reading RSTP port states (discarding, learning, forwarding) and link types (edge, point-to-point, shared)
- Making end-host ports edge ports with `spanning-tree portfast`
- Verifying with `show spanning-tree`

## Key commands

```
spanning-tree mode rapid-pvst
spanning-tree vlan 1 root primary
!
interface f0/1
 spanning-tree portfast
!
show spanning-tree
show spanning-tree vlan 1
```

## Files

| File | Description |
|---|---|
| Packet Tracer file (uploading) | My completed lab. Open it with Cisco Packet Tracer 8.x. |

## Credit

Lab topology and tasks are from [Jeremy's IT Lab](https://www.youtube.com/@JeremysITLab) free CCNA course. The configuration in the file is my own work.

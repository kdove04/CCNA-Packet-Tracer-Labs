# Lab 02 Solution: Three-Site Static Routing

> Try the lab first. Open this only after you've finished and verified.

## R1

```
enable
configure terminal
hostname R1
interface GigabitEthernet0/0
 ip address 10.1.1.1 255.255.255.0
 no shutdown
interface GigabitEthernet0/1
 ip address 10.0.12.1 255.255.255.252
 no shutdown
 exit
! Task 1: one route covers everything (stub router)
ip route 0.0.0.0 0.0.0.0 10.0.12.2
end
copy running-config startup-config
```

## R2

```
enable
configure terminal
hostname R2
interface GigabitEthernet0/0
 ip address 10.0.12.2 255.255.255.252
 no shutdown
interface GigabitEthernet0/1
 ip address 10.0.23.1 255.255.255.252
 no shutdown
interface GigabitEthernet0/2
 ip address 10.2.2.1 255.255.255.0
 no shutdown
 exit
! Task 2: specific routes with next-hop IPs
ip route 10.1.1.0 255.255.255.0 10.0.12.1
ip route 10.3.3.0 255.255.255.0 10.0.23.2
! Task 3: everything else toward R3
ip route 0.0.0.0 0.0.0.0 10.0.23.2
end
copy running-config startup-config
```

## R3

```
enable
configure terminal
hostname R3
interface GigabitEthernet0/0
 ip address 10.0.23.2 255.255.255.252
 no shutdown
interface GigabitEthernet0/1
 ip address 10.3.3.1 255.255.255.0
 no shutdown
interface GigabitEthernet0/2
 ip address 203.0.113.2 255.255.255.252
 no shutdown
 exit
! Task 4: fully specified route to LAN 1, next-hop route to LAN 2
ip route 10.1.1.0 255.255.255.0 GigabitEthernet0/0 10.0.23.1
ip route 10.2.2.0 255.255.255.0 10.0.23.1
! Task 5: unknown traffic to the ISP
ip route 0.0.0.0 0.0.0.0 203.0.113.1
end
copy running-config startup-config
```

## ISP (setup)

```
enable
configure terminal
hostname ISP
interface GigabitEthernet0/0
 ip address 203.0.113.1 255.255.255.252
 no shutdown
interface Loopback0
 ip address 8.8.8.8 255.255.255.255
 exit
ip route 10.0.0.0 255.0.0.0 203.0.113.2
end
```

## Part A verification answers

1. **The /24 static route.** Routers use the longest prefix match, and /24 is more specific than /0.
2. **`*` marks the candidate default route.** R1 also shows *"Gateway of last resort is 10.0.12.2 to network 0.0.0.0."*
3. **4 hops:** 10.1.1.1 (R1), 10.0.12.2 (R2), 10.0.23.2 (R3), then 8.8.8.8 (ISP).
4. **Yes, it's redundant right now,** because the default route sends LAN 3 traffic to R3 anyway. Engineers often keep specific routes so internal traffic still goes the right way if the default route is later changed, for example to point at a second ISP.

## Part B answers

**Ticket 1: B.** A static route is installed only if the router can reach its next hop. 10.0.21.2 isn't in any connected subnet (the link is 10.0.12.0/30), so the route stays in the config but never reaches the routing table. The next hop was mistyped as 21 instead of 12.

**Ticket 2: C.** R3 has no route to 10.1.1.0/24, so the reply to 10.1.1.10 matches R3's default route and goes to the ISP. The ISP's 10.0.0.0/8 route sends it straight back to R3, and the packet bounces between them until the TTL reaches 0. Fix: `ip route 10.1.1.0 255.255.255.0 GigabitEthernet0/0 10.0.23.1`.
*Why not B?* There's no 10.0.0.0/8 route on R3. "10.0.0.0/8 is variably subnetted" is only a heading for the subnets listed under it, not a route.

**Ticket 3: A.** `255.255.255.255` makes this a host route that matches only 10.2.2.0. Fix:
```
no ip route 10.2.2.0 255.255.255.255 10.0.23.1
ip route 10.2.2.0 255.255.255.0 10.0.23.1
```

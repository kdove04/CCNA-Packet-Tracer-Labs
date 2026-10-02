# Lab 01 Solution: Branch Office Bring-Up

> Try the lab first. Open this only after you've finished and verified.

## Part 1: Subnetting

Four equal subnets need **2 borrowed bits** (2² = 4), so /24 becomes **/26**.
Mask: **255.255.255.192** · Block size: 256 − 192 = **64**

| Subnet | Network | First usable | Last usable | Broadcast |
|---|---|---|---|---|
| 1st (reserved) | 192.168.50.0 | .1 | .62 | .63 |
| 2nd (Sales) | 192.168.50.64 | .65 | .126 | .127 |
| 3rd (Admin) | 192.168.50.128 | .129 | .190 | .191 |
| 4th (reserved) | 192.168.50.192 | .193 | .254 | .255 |

## Addressing plan

| Device | Interface | IP address | Mask | Gateway |
|---|---|---|---|---|
| R1-BRANCH | G0/0 | 192.168.50.65 | 255.255.255.192 | — |
| R1-BRANCH | G0/1 | 192.168.50.129 | 255.255.255.192 | — |
| PC-A1 | NIC | 192.168.50.126 | 255.255.255.192 | 192.168.50.65 |
| PC-A2 | NIC | 192.168.50.125 | 255.255.255.192 | 192.168.50.65 |
| SW1 | VLAN 1 | 192.168.50.124 | 255.255.255.192 | 192.168.50.65 |
| PC-B1 | NIC | 192.168.50.190 | 255.255.255.192 | 192.168.50.129 |

## R1-BRANCH

```
enable
configure terminal
hostname R1-BRANCH
enable secret Cisc0Lab!
service password-encryption
banner motd # Authorized access only #
!
line console 0
 password ConsoleLab1
 login
 exit
!
interface GigabitEthernet0/0
 description LAN-SALES
 ip address 192.168.50.65 255.255.255.192
 no shutdown
 exit
!
interface GigabitEthernet0/1
 description LAN-ADMIN
 ip address 192.168.50.129 255.255.255.192
 no shutdown
 end
!
copy running-config startup-config
```

## SW1

```
enable
configure terminal
hostname SW1
interface vlan 1
 ip address 192.168.50.124 255.255.255.192
 no shutdown
 exit
ip default-gateway 192.168.50.65
end
copy running-config startup-config
```

## SW2

```
enable
configure terminal
hostname SW2
end
copy running-config startup-config
```

## Verification answers

1. **62.** A /26 has 6 host bits: 2⁶ = 64 − 2 (network and broadcast) = 62.
2. **2 C routes and 2 L routes.** The C routes are 192.168.50.64/26 and 192.168.50.128/26. The L routes are **/32**, one for each of the router's own addresses (.65 and .129). The table header reads *"192.168.50.0/24 is variably subnetted, 4 subnets, 2 masks."*
3. **7.** It's Cisco type 7 encryption, which is weak and easy to reverse. That's why the enable password uses `enable secret` (type 5 hash) instead.
4. **`ip default-gateway 192.168.50.65`.** Without it, SW1 can receive PC-B1's ping but has no way to send the reply to a different subnet.
5. **192.168.50.127 is the Sales broadcast address.** The next block starts at .128, so .127 is the last address in .64/26.

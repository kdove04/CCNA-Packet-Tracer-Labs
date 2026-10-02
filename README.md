# CCNA 200-301 Lab Portfolio

Hands-on labs I built and completed while preparing for the Cisco CCNA 200-301 exam. Each lab is written in the style of a CCNA simulation item: a scenario, a topology, a numbered task list with constraints, and verification questions. Labs are built and tested in Cisco Packet Tracer.

**Exam target:** December 2026

## Labs

| # | Lab | Topics | Status |
|---|-----|--------|--------|
| 00 | [VLAN Lab](vlan-lab/) | VLANs, access ports, trunking | 🚧 In progress |
| 01 | [Branch Office Bring-Up](lab-01-branch-bring-up/) | Subnetting, IPv4 addressing, device hardening, switch management | ⬜ Not started |
| 02 | [Three-Site Static Routing](lab-02-static-routing/) | Static routes, default routes, longest-prefix match, troubleshooting | ⬜ Not started |

## How each lab is organized

```
lab-XX-name/
├── README.md       # Scenario, topology, tasks and verification questions
├── solution.md     # Reference configuration and answers
└── my-work/        # My Packet Tracer file, configs and screenshots
```

## How to use these labs

1. Read the lab `README.md` and build the topology in Packet Tracer.
2. Complete every task **without** opening `solution.md`.
3. Run the verification commands and answer the questions.
4. Check against `solution.md`, then save your `.pkt` file and `show running-config` output in `my-work/`.

## Tools

- Cisco Packet Tracer 8.x
- Devices: Cisco 2911 routers, Cisco 2960 switches, generic PCs

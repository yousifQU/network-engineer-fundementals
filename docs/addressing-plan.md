# Addressing Plan

Each project built or rebuilt its environment, so addresses are scoped per project and are not meant to be globally unique. Public-side addresses use the documentation range `203.0.113.0/24` (RFC 5737). Private ranges use RFC 1918. Original VLAN IDs, hostnames, and team-specific octets were replaced with generic values.

## Project 1: Cabling and switching (flat network)

| Item | Value |
|------|-------|
| LAN | 10.0.1.0/24, gateway 10.0.1.1 |
| PCs | PC1–PC9 at 10.0.1.3 – 10.0.1.11 (static) |
| Switches | SW1, SW3 (Cisco 3650), SW2 (Cisco 2960) |

## Project 2: VLANs and router-on-a-stick

| VLAN | Subnet | Gateway (R1 subinterface) | DHCP range | Switch management |
|------|--------|---------------------------|------------|-------------------|
| 1 (native) | 10.0.1.0/24 | 10.0.1.1 (Gi0/0.1) | .100 – .200 | — |
| 2 | 10.0.2.0/24 | 10.0.2.1 (Gi0/0.2) | .100 – .200 | SW1 .99, SW2 .98, SW3 .97 |
| 3 | 10.0.3.0/24 | 10.0.3.1 (Gi0/0.3) | .100 – .200 | — |

## Project 3: Wireless

| Item | Value |
|------|-------|
| Wireless router WAN | 203.0.113.254/24, gateway 203.0.113.1 |
| LAN | 192.168.1.0/24, router 192.168.1.1 |
| DHCP | 192.168.1.100 – 192.168.1.200 |
| Switch management (VLAN 1) | SW1 .99, SW2 .98, SW3 .97 |
| Wi-Fi | 2.4 GHz and 5 GHz, WPA2-Personal (AES), SSID `<SSID>` |

## Projects 4 and 5: Two routers, three VLANs

| VLAN | R1 subnet (gateway .1) | R2 subnet (gateway .1) | Primary router |
|------|------------------------|------------------------|----------------|
| 10 | 10.1.1.0/24 | 10.1.2.0/24 (Project 5) | R2 |
| 20 | 10.2.1.0/24 | 10.2.2.0/24 (Project 5) | R1 |
| 30 | 10.3.1.0/24 | 10.3.2.0/24 (Project 5) | R1 |

DHCP pools hand out .100 – .200 in each subnet. In Project 4 both routers used the R1 subnets; in Project 5, R2 moved to its own subnets.

| Item | Value |
|------|-------|
| R1 uplink (to the campus/internet) | 203.0.113.254/24, gateway 203.0.113.1 |
| R1 ↔ R2 transit link (Project 5) | 192.168.0.0/30 (R1 .1, R2 .2) |
| VLAN 40: R1 ↔ VyOS wired link (Project 5) | 172.30.0.0/25 (R1 .1, SW1 .3, VyOS eth0 .2) |
| VyOS wireless access point (Project 5) | 172.30.0.128/25, gateway .129, DHCP .130 – .254 |
| OSPF router IDs (Project 5) | R1 1.1.1.1, R2 2.2.2.2, VyOS 3.3.3.3, all in area 0 |

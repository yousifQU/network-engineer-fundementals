# Addressing Plan

Each project built or rebuilt its environment, so addresses are scoped per project and are not meant to be globally unique. Public-side addresses use the documentation range `203.0.113.0/24` (RFC 5737). Private ranges use RFC 1918. Original VLAN IDs, hostnames, and team-specific octets were replaced with generic values.

## Project 3: Wireless

| Item | Value |
|------|-------|
| Wireless router WAN | 203.0.113.254/24, gateway 203.0.113.1 |
| LAN | 192.168.1.0/24, router 192.168.1.1 |
| DHCP | 192.168.1.100 – 192.168.1.200 |
| Switch management (VLAN 1) | SW1 .99, SW2 .98, SW3 .97 |
| Wi-Fi | 2.4 GHz and 5 GHz, WPA2-Personal (AES), SSID `<SSID>` |

## Project 5: Routing, NAT, and ACLs

| VLAN | R1 subnet (gateway .1) | R2 subnet (gateway .1) |
|------|------------------------|------------------------|
| 10 | 10.1.1.0/24 | 10.1.2.0/24 |
| 20 | 10.2.1.0/24 | 10.2.2.0/24 |
| 30 | 10.3.1.0/24 | 10.3.2.0/24 |

DHCP pools hand out .100 – .200 in each subnet.

| Item | Value |
|------|-------|
| R1 uplink (to the campus/internet) | 203.0.113.254/24, gateway 203.0.113.1 |
| R1 ↔ R2 transit link | 192.168.0.0/30 (R1 .1, R2 .2) |
| VLAN 40: R1 ↔ VyOS wired link | 172.30.0.0/25 (R1 .1, SW1 .3, VyOS eth0 .2) |
| VyOS wireless access point | 172.30.0.128/25, gateway .129, DHCP .130 – .254 |
| OSPF router IDs | R1 1.1.1.1, R2 2.2.2.2, VyOS 3.3.3.3, all in area 0 |

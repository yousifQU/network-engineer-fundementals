# Plain-English Glossary

Short definitions of the terms used in this repository, written for non-specialist readers.

| Term | What it means |
|------|---------------|
| **Switch** | A box that connects computers in the same office so they can talk to each other. |
| **Router** | A device that connects different networks together, including your network to the internet. |
| **IP address** | A device's address on the network, like a street address for mail. |
| **MAC address table** | The switch's list of which device is plugged into which port. |
| **VLAN** | A virtual network. One physical switch can be split into several separate networks, for example one per department. |
| **Trunk / 802.1Q** | A single cable that carries traffic for several VLANs, with each frame labelled (tagged) with its VLAN. |
| **Router-on-a-stick** | One router connected by one trunk cable that routes traffic between all the VLANs. |
| **DHCP** | Hands out IP addresses automatically, so nobody has to type them in by hand. |
| **SSH** | An encrypted way to log in to and manage a network device remotely. |
| **WPA2 / AES** | The security standard and encryption that protect a Wi-Fi network from eavesdropping. |
| **Spanning Tree (STP / MSTP)** | Lets you add backup cables between switches without creating loops that would flood the network. MSTP does this per group of VLANs, so different VLANs can prefer different paths. |
| **OSPF** | A routing protocol. Routers share what networks they know about and automatically pick the best path. |
| **NAT / PAT** | Lets many internal devices share one public internet address. |
| **ACL (access control list)** | A list of allow/deny rules on a router, used to control who can reach what. |
| **VyOS** | An open-source router and firewall operating system that runs on ordinary PC hardware. |
| **TFTP** | A very simple file-transfer service, often used to copy configurations and firmware to network devices. |
| **Wireshark** | A tool that captures and shows network traffic, used to prove things work as designed. |
| **Running vs startup configuration** | The running configuration is what a device is doing now. The startup configuration is what it loads after a reboot. Changes are lost unless saved from one to the other. |
| **ROMmon** | A Cisco recovery mode used to reset or repair a device that cannot boot normally. |

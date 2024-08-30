# Lab 01 - The Redundant Network

This lab includes essential networking concepts for the CCNA certification. It covers a range of topics including VLAN configuration, Hot Standby Router Protocol (HSRP) for gateway redundancy, Rapid Spanning Tree Protocol (RSTP) for Layer 2 loop prevention, Link Aggregation Groups (LAG) for increased bandwidth and redundancy, and OSPF for dynamic routing.
The network topology features multiple VLANs, redundant links, and point-to-point connections, simulating a real-world environment that requires both Layer 2 and Layer 3 networking knowledge. Through this lab, users will gain practical experience in configuring and troubleshooting these technologies, ensuring a solid understanding of how they interoperate to create a resilient and efficient network.

## Difficulty

This lab covers several intermediate topics for the CCNA curriculum, including VLAN configuration, HSRP, RSTP, OSPF, and LAG. These are critical topics for network design and redundancy, which require a solid understanding of both Layer 2 and Layer 3 concepts. The integration of multiple technologies in a single lab environment increases complexity, especially with features like HSRP for redundancy, RSTP for fast spanning-tree convergence, and OSPF for dynamic routing.

**Difficulty Rating:** 6/10

## Prerequisites

Before starting this lab, ensure you are comfortable with the following topics and networking concepts:

- Network Segmentation at Layer 3
- Network Segmentation at Layer 2
- Link Aggregation Group Protocols
- First Hop Redundancy Protocols (FHRP) for multiple gateways
- Static Routing
- Dynamic Routing (OSPF)
- Per-VLAN Spanning Tree (PVST) and Rapid Per-VLAN Spanning Tree (Rapid-PVST)

If you are following [Jeremy's IT LAB](https://www.youtube.com/playlist?list=PLxbwE86jKRgMpuZuLBivzlM8s2Dk5lXBQ), you will likely know all these concepts by the end of day 29.

## Lab Instructions

The following instructions may help you address the lab:

**The goal is to allow all computers to communicate with each other and also with the remote server.**

Consider the following order to configure the devices, which can help you simplify the process:

1. **Link Aggregation Group (LAG):** Start by configuring the grouped links in the network. I recommend taking notes about the group numbers on a piece of paper or directly in Packet Tracer.

2. **End Device Configuration:** Although not critical at this stage, you may want to configure the end devices now. Assign the appropriate IP addresses and gateways. Make sure that you configure the appropriate Virtual IP addresses for the relevant devices, as FHRP will not work without these configurations.

3. **VLANs:** Configure the VLANs on all switches. Ensure that links are set as trunks or access ports as required. Change the native VLAN to an unused VLAN to enhance security.

4. **RSTP:** Enable Rapid Per-VLAN Spanning Tree Protocol (Rapid-PVST) and configure Root Bridges to ensure that each VLAN uses a different switching route. Enable PortFast and BPDU Guard on the appropriate ports.

5. **FHRP:** Configure the Multilayer Switch and the Router to use an FHRP like Hot Standby Routing Protocol (HSRP). Ensure you set up the correct Virtual IP addresses for the corresponding VLANs. Use Switch Virtual Interfaces (SVIs) on the Layer 3 Switch and "Router On A Stick" (ROAS) on the Router. Configure the physical interface to handle VLAN 10 as native by setting up its IP address.

6. **Routing:** Configure static and default routes on the routers connected directly to the LANs. Test connectivity to ensure that computers using the router as their default gateway can reach the remote server.

7. **Dynamic Routing with OSPF:** Configure OSPF on all routers. On routers that have static and default routes, ensure the appropriate commands are used to share that information via OSPF. Finally, configure passive interfaces where necessary to prevent unnecessary OSPF advertisements.

## Step-by-Step Guide

(TODO)
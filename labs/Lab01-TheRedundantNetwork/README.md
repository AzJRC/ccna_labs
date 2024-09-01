# Lab 01 - The Redundant Network

![Screenshoot of the Packet Tracer Lab](LAB_PREVIEW.png "The Redundant Network")

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

## Commands You Should Known

Here you have all the commands you will need to complete this lab.

### General Commands

| **Command** | **Config Mode** | **Description** |
|-------------------------------------------|-------------------------|---------------------------------------------------------------------------------------------------|
| **channel-group {ethc-num} mode {mode}** | Interface Configuration | Creates an EtherChannel interface for Link Aggregation. |
| **ip address {address} {netmask}** | Interface Configuration | Assigns an IP address and subnet mask to an interface. |
| **interface Loopback{number}** | Global Configuration | Creates a loopback interface. |

### Router-specific Commands

| **Command** | **Config Mode** | **Description** |
|----------------------------------------------------|-------------------------|---------------------------------------------------------------------------------------------------|
| **encapsulation ppp** | Interface Configuration | Configures the interface to use PPP (Point-to-Point Protocol) for encapsulation. Used in serial links. |
| **clock rate {speed}** | Interface Configuration | Sets the clock rate on a serial interface. |
| **interface {interface}.{subinterface}** | Global Configuration | Creates a subinterface on a physical interface for a specific VLAN. It is recommended to match the subinterface value with the VLAN ID. |
| **encapsulation dot1Q {vlan-id}** | Subinterface Configuration | Configures the subinterface to use 802.1Q encapsulation for inter-VLAN routing. |
| **standby {group number} ip {ip address}**| Interface Configuration | Configures HSRP (Hot Standby Router Protocol) by assigning a virtual IP address. |
| **standby {group number} priority {priority value}** | Interface Configuration | Sets the HSRP priority for determining the active router. |
| **standby {group number} preempt** | Interface Configuration | Allows the router to take over as the active router if it has a higher priority. |
| **ip route {destination network} {subnet mask} {next-hop address} [administrative distance]** | Global Configuration | Configures a static route to a specific destination network. |
| **router ospf {process-id}** | Global Configuration | Enters OSPF router configuration mode. |
| **ip ospf {process-id} area {area-id}** | Interface Configuration | Enables OSPF routing on the interface in a specific area. |
| **passive-interface {interface}** | OSPF Router Configuration | Configures a specific interface as a passive OSPF interface, preventing it from sending OSPF hello packets. |
| **auto-cost reference-bandwidth {bandwidth}** | OSPF Router Configuration | Adjusts the OSPF cost calculation to accommodate higher-speed interfaces. |

### Switch-specific Commands

| **Command** | **Config Mode** | **Description** |
|--------------------------------------------------|-------------------------|---------------------------------------------------------------------------------------------------|
| **ip routing** | Global Configuration | Enables IP routing on the device, allowing it to route packets between different networks. Particularly used in Multilayer Switches |
| **switchport trunk encapsulation dot1q** | Interface Configuration | Configures the interface to use 802.1Q encapsulation for VLAN tagging on a trunk port. |
| **switchport mode trunk** | Interface Configuration | Configures the interface as a trunk port (tagged port), allowing it to carry multiple VLANs. |
| **switchport mode access** | Interface Configuration | Configures the interface as an access port (untagged port), allowing it to access a VLAN. |
| **switchport trunk native vlan {vlan-id}**| Interface Configuration | Sets the native VLAN for the trunk. |
| **switchport trunk allowed vlan {vlan-list}** | Interface Configuration | Specifies which VLANs are allowed on the trunk link. |
| **switchport access vlan {vlan-id}** | Interface Configuration | Assigns the port to a specific VLAN for untagged traffic on an access port. |
| **spanning-tree mode {mode}** | Global Configuration | Sets the spanning tree mode. |
| **spanning-tree portfast** | Interface Configuration | Configures the interface access ports to immediately transition to the forwarding state, bypassing the transitional states. |
| **spanning-tree portfast default** | Global Configuration | Configures all interface access ports to immediately transition to the forwarding state, bypassing the transitional states. |
| **spanning-tree portfast bpduguard default** | Global Configuration | Enables BPDU Guard on all PortFast-enabled ports, automatically disabling a port if a BPDU is received. |
| **spanning-tree vlan {vlan-id} root primary** | Global Configuration | Sets the spanning tree priority for VLAN {vlan-id} to a lower value than the current root bridge, influencing the election of the root bridge. |

## Known errors and bugs

1. When enabling Rapid Spanning Tree Protocol (RSTP), Packet Tracer seems to behave strangely, blocking interfaces that it shouldn't. To solve this issue save and close the application and open it again.

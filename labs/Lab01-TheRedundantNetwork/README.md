# Lab 01 - The Redundant Network

![Screenshoot of the Packet Tracer Lab](LAB_PREVIEW.png "The Redundant Network")

This lab includes essential networking concepts for the CCNA certification. It covers a range of topics including VLAN configuration, Hot Standby Router Protocol (HSRP) for gateway redundancy, Rapid Spanning Tree Protocol (RSTP) for Layer 2 loop prevention, Link Aggregation Groups (LAG) for increased bandwidth and redundancy, and OSPF for dynamic routing.
The network topology features multiple VLANs, redundant links, and point-to-point connections, simulating a real-world environment that requires both Layer 2 and Layer 3 networking knowledge. Through this lab, users will gain practical experience in configuring and troubleshooting these technologies, ensuring a solid understanding of how they interoperate to create a resilient and efficient network.

## Relevant CCNA Exam Topics

(TODO)

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

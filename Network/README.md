# WIP
This folder is a WIP of public documentation of my home network.

# Home Network
This folder contains documentation and config for my home network.

## Topology
![Network Topology Diagram](NetworkTopology.png)

### Networks
- MGMT		    192.168.0.0/24 - For management of network devices.
- Devices		192.168.1.0/24 - For wired household devices such as printers, TVs, media devices, smarthome devices, IoT devices, etc.
- NVR			192.168.2.0/24 - For the security camera system.
- Hypervisor	192.168.3.0/24 - For any VMs and services operating on the HV01 [hypervisor](../Hypervisor).
- WiFi		    10.1.0.0/16 - For standard household WiFi users.
- WiFiGuest	    10.2.0.0/24 - For guests. Isolated to prevent access to any other local networks.

### VLANs
- 10    Devices
- 20    WiFi
- 25    WiFiGuest
- 30    Hypervisor
- 4000  Management

## Devices
### R01
Mikrotik L009UiGS-RM
Hardware offloading disabled to allow practice implementation of OSPF routing.

#### R01 Interfaces
- E01		DHCP from ISP
- E02		192.168.2.1/24
- E03
  - VLAN 30		192.168.3.1/24
  - VLAN 4000	192.168.0.1/28
- E08 	192.168.0.9/28
- SFP01
  - VLAN 10		192.168.1.1/24
  - VLAN 20		10.1.0.1/16
  - VLAN 25		10.2.0.1/24
  - VLAN 4000	192.168.129.1/25

#### OSPF
TBC

### SW01
TP-Link TL-SG1210MPE
Managed switch handling VLANs via 802.11Q.

#### SW01 802.1Q VLAN Ports
- SFP01	- 10, 20, 25, 4000
- E02 - 20, 25, 4000
- E03 - 20, 25, 4000
- E04 - 20, 25, 4000
- E05 - 10 (untagged)
- E06 - 10 (untagged)
- E08 - 20 (untagged)
- E09 - 10 (untagged)

### SW02 & SW03
TBA
These will be small PoE powered, unmanaged switches to allow ethernet connectivity of multiple media devices in the home theatre and living room.

### AP01, AP02, & AP03
TP-Link EAP-615 wall-mounted PoE access points.
These are controlled by an Omada Software Controller hosted on HV01 in a Docker container.
Configured to serve several WiFi networks that all support fast roaming via 802.11k/v/r.
A primary WLAN supports the majority of users accross both 2.4GHz and 5GHz bands.
A secondary 2.4GHz WLAN supports household legacy devices that only support older 2.4GHz protocols.
A third guest WLAN is configured as a copy of the first with a different SSID, and isolated on a separate network.

### HV01
Mini PC hypervisor running Proxmox.
See [hypervisor docs](../Hypervisor) for details.

### NVR
Network Video Recorder, i.e., security camera system.

### PC01
Home desktop workstation.

### P01
Printer.
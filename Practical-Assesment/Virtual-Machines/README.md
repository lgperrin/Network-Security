# About the Virtual Machines

In order to complete the Practical Assesment, we will use two virtual machines (VMs) in VirtualBox to provide a Linux environment within which to experiment
with `nmap`, `hping3`, and firewalls. This handout does not assume any prior knowledge of Linux as we just need to follow instructions carefully. The specific 
pipeline is:

![alt text](https://github.com/lgperrin/Network-Security/blob/main/Practical-Assesment/Images/Captura%20de%20pantalla%202024-02-26%20115128.png)

1. **Setup**: Installation and configuration of VirtualBox and VMs.
2. **Network Configuration**: Static IP assignment and network interface setup.
3. **Connectivity Testing**: Using `ping` and `traceroute` to test VM connectivity.
4. **Security Tools Exploration**: Scanning and packet crafting with `nmap` and `hping3`.
5. **Firewall Configuration**: Implementing and testing firewall rules with UFW.
6. **Shutdown procedure**.

## 1. Instructions and Setup

In this initial phase, you will prepare your virtual environment for the network security exercises. This involves setting up two Xubuntu virtual machines (VMs) in VirtualBox, configuring their network interfaces, and ensuring they can communicate within a shared Local Area Network (LAN). Follow these steps to get started:

1.1 **Importing VMs into VirtualBox**. Locate the Xubuntu1.ova and Xubuntu2.ova files provided in this Github repository. Import each VM by double-clicking on the respective files. Accept the default settings during the import process. Once imported, start each VM by double-clicking on their names in the VirtualBox interface.
The default password for both VMs is `csc3064`. Use this whenever prompted.

1.2 **Configuring VM Network Interfaces**. Both VMs will be set up with static IP addresses to communicate over a virtual LAN. We'll do this manually. For Xubuntu1 (VM1) open a terminal and execute the following commands to configure the network interface named `enp0s8`:

* Disable the interface: `sudo ifconfig enp0s8 down`
* Assign IP address and network settings: `sudo ifconfig enp0s8 192.168.1.1 netmask 255.255.255.0 broadcast 192.168.1.255`

For Xubuntu2 (VM2) we repeat the steps for VM1, but assign the IP address `192.168.1.2` to `enp0s8`.

1.3 **Validation and Troubleshooting**. Ensure both VMs' network configurations are correctly set up by checking their IP settings with `ifconfig`. We should see the new configuration information added. Be mindful of a potential bug where the interface configuration might reset, indicated by a lost network connection and a spinning icon on the screen. If this occurs, reapply the `sudo ifconfig enp0s8 192.168.1.x` command as needed.

<u>Important</u>: Both VMs must have their network configurations correctly set to the specified IP addresses and subnet mask for successful communication within the shared LAN (subnet `192.168.1.0/24`).

## 2. VM Configuration:

* Assign static IP addresses to both VMs (`192.168.1.1` for VM1 and `192.168.1.2` for VM2) using `ifconfig` commands.
* Be aware of a bug that might require re-entering IP configuration commands.

## 3. Network Testing

* Verify network connectivity between VMs using `ping`.
* Explore traceroute from both VMs to understand packet routing in a LAN setup.


## 4. Network Scanning 

* Perform a local IP range scan to identify active hosts.
* Use Wireshark to capture and analyze packets during the scan.
* Experiment with TCP SYN scans and OS detection scans.

## 5. Packet Crafting 

* Craft and send packets to analyze responses and test firewall rules.
* Experiment with spoofing source addresses and setting flags.

## 6. Firewall Configuration and Testing

* Use UFW (Uncomplicated Firewall) to enable, configure, and test firewall rules.
* Allow and deny access to specific ports and IPs to understand firewall behavior.

## 7. Shutdown

* Properly log out and shut down each VM.









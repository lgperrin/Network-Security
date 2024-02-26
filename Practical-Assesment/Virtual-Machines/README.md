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

- [x] Use VirtualBox with Xubuntu VMs on either CSB desktops or personal computers.
- [x] Download and import two VMs from the Github repository.
- [x] Within the VMs, whenever you are asked for a password it is `csc3064`. 

_Note_. Once configured, the two VMs, called Xubunut1 (VM1) and Xubuntu2 (VM2), will share a network connection that is provided by VirtualBox. This is like having 
two hosts on the same LAN. Neither host is configured with internet connectivity, so it is safe to experiment with tools such as nmap and hping3 within this 
virtual environment.

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









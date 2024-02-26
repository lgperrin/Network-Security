# About the Virtual Machines

In order to complete the Practical Assesment, we will use two virtual machines (VMs) in VirtualBox to provide a Linux environment within which to experiment
with `nmap`, `hping3`, and firewalls. This handout does not assume any prior knowledge of Linux as we just need to follow instructions carefully. The specific 
pipeline is:

![alt text](https://github.com/lgperrin/Network-Security/blob/main/Practical-Assesment/Images/Captura%20de%20pantalla%202024-02-26%20115128.png)

1. **Setup and Network Configuration**: Installation and configuration of VirtualBox and VMs. Manually assign static IP assignment and network interface setup.
2. **Connectivity Testing**: Using `ping` and `traceroute` to test VM connectivity.
3. **Security Tools Exploration**: Scanning and packet crafting with `nmap` and `hping3`.
4. **Firewall Configuration**: Implementing and testing firewall rules with UFW.
5. **Shutdown**.

## 1. Setup and Network Configuration

In this initial phase, you will prepare your virtual environment for the network security exercises. This involves setting up two Xubuntu virtual machines (VMs) in VirtualBox, configuring their network interfaces, and ensuring they can communicate within a shared Local Area Network (LAN). Follow these steps to get started:

1.1 **Importing VMs into VirtualBox**. Locate the Xubuntu1.ova and Xubuntu2.ova files provided in this Github repository. Import each VM by double-clicking on the respective files. Accept the default settings during the import process. Once imported, start each VM by double-clicking on their names in the VirtualBox interface.
The default password for both VMs is `csc3064`. Use this whenever prompted.

1.2 **Configuring VM Network Interfaces**. Both VMs will be set up with static IP addresses to communicate over a virtual LAN. We'll do this manually. For Xubuntu1 (VM1) open a terminal and execute the following commands to configure the network interface named `enp0s8`:

* Disable the interface: `sudo ifconfig enp0s8 down`
* Assign IP address and network settings: `sudo ifconfig enp0s8 192.168.1.1 netmask 255.255.255.0 broadcast 192.168.1.255`

For Xubuntu2 (VM2) we repeat the steps for VM1, but assign the IP address `192.168.1.2` to `enp0s8`.

1.3 **Validation and Troubleshooting**. Ensure both VMs' network configurations are correctly set up by checking their IP settings with `ifconfig`. We should see the new configuration information added. Be mindful of a potential bug where the interface configuration might reset, indicated by a lost network connection and a spinning icon on the screen. If this occurs, reapply the `sudo ifconfig enp0s8 192.168.1.x` command as needed.

<ins>Important</ins>: Both VMs must have their network configurations correctly set to the specified IP addresses and subnet mask for successful communication within the shared LAN (subnet `192.168.1.0/24`).

## 2. Connectivity Testing

2.1 **Verify network connectivity between VMs using `ping`**. This part aims to validate the network connection between the two VMs by sending and observing ping packets. The VM2 is going to be the sender and VM1 is going to be the observer.

* <ins>Sending Ping Packets</ins>. Open a terminal in VM2. To send a specified number of ping packets to VM1, use the command: `ping -c [number] 192.168.1.1`. Replace `[number]` with the number of ping packets you wish to send. If you don't specify a number with `-c`, the ping command will run indefinitely. Use `Ctrl+c` to stop it.
  
* <ins>Steps for VM1 (Observer)</ins>. We'll need to setup Wireshark in order to observe ping packets sent by VM2. First, open a terminal and launch Wireshark with administrative privileges: `sudo wireshark`. In Wireshark, double-click on the `enp0s8` interface to begin capturing packets. Close the terminal window as it's no longer needed for input. While Wireshark is capturing, return to VM2 and send ping packets to VM1 again. In Wireshark on VM1, you should observe the ICMP request and reply packets indicating a successful ping operation.

2.2 **Explore `traceroute` from both VMs to understand packet routing in a LAN setup**. This provides insight into the path packets take across the network, even in a simplified environment like the one created by VirtualBox. Again, VM2 is the sender and VM1 the observer. Open a terminal in VM2 and then perform a traceroute to VM1 with the command: `traceroute 192.168.1.1`. To force traceroute to use ICMP (Internet Control Message Protocol) packets instead of the default UDP (User Datagram Protocol), run: `traceroute -I 192.168.1.1`. Traceroute is a diagnostic tool that traces the route packets take to reach a host. By default, it uses UDP packets, but options like `-I` can force it to use ICMP.


## 3. Security Tools Exploration

3.1 **Network and Host Scan**. This can be done by using `namp`. The objective is to identify active hosts and attempt to determine the operating system of a target host.

* <ins>Network Scan</ins>. On VM1, open a terminal. To scan the local IP range for active hosts, execute: `sudo nmap -sn 192.168.1.0/24`. This scan, known as a ping scan, quickly identifies live hosts on the network without sending any packets to high-numbered ports.
* <ins>Host Scan for OS Detection</ins>. Execute: `sudo nmap -O 192.168.1.2` to attempt OS detection on VM2. This scan sends a series of TCP and UDP packets to the host to analyze responses and attempt to determine the operating system based on these responses. During the host scan, use Wireshark on VM1 to capture and observe the packets being sent and received. Now we can analyze the captured packets to understand how nmap's OS detection technique works, noting the variety of packets used and the responses they provoke.

_Note_. `-sn` flag is used for a simple network scan to identify active hosts, while the `-O` flag attempts OS detection by analyzing responses to various probes. The OS detection scan is more sophisticated, sending various probes to analyze how the target system responds. This can provide clues about the target's operating system but may not always be accurate, especially in controlled environments or with customized configurations.

3.2 **Packet Crafting**. This can be done by using `hping3` as it's is a powerful tool for manual packet crafting and analysis, providing insights into the lower-level workings of network protocols. The objective is to use `hping3` on VM1 to craft and send TCP ACK packets to VM2 and observe these packets with Wireshark running on VM2. By crafting specific types of packets, like TCP ACK, you can learn about the behavior of network devices and protocols in response to different conditions.

* Start Wireshark on VM2. Begin capturing packets on the `enp0s8` interface, which is the network interface used by VM2.
* Open a terminal on VM1. To send a sequence of 4 TCP ACK packets to VM2 on port 80, use the command: `sudo hping3 -A -c 4 192.168.1.2 -p 80`.
  * The `-A` flag specifies that the packets should be ACK packets.
  * The `-c 4` option indicates the number of packets to send, which is 4 in this case.
  * The `-p 80` option specifies the destination port, which is port 80 (commonly used for HTTP).

## 4. Firewall Configuration and Testing


<ins>Initial Setup and Basic Testing</ins>. 

* Use `sudo ufw status verbose` to check if UFW is active in VM2. It's likely to be disabled by default.
* Activate UFW with `sudo ufw enable`. Check the status again to confirm that it's active and that by default, all incoming traffic is denied.
* From VM1, attempt to send TCP packets to VM2 on port 80 using `sudo hping3 -S -c 5 192.168.1.2 -p 80`.
* Disable UFW on VM2 (`sudo ufw disable`), repeat the hping3 command from VM1, and observe the difference.

<ins>Allowing Specific Ports</ins>. 

* Enable UFW again on VM2.
* Conduct a scan using hping3 from VM1 targeting ports 20 to 90: `sudo hping3 -8 20-90 192.168.1.2 -S`. With UFW enabled, this should result in no responses due to the firewall blocking the packets.
* On VM2, allow incoming connections on port 22 with `sudo ufw allow 22`.
* Verify the new rule with `sudo ufw status verbose`.
* Optionally, remove any unnecessary rules (e.g., an IPv6 rule) with `sudo ufw delete [rule number]`.
* Test again from VM1 with hping3 targeting port 22. This time, you should observe responses indicating that the port is open.

<ins>Fine-tuning Firewall Rules</ins>. 
* To deny access to port 22 from a specific IP (e.g., `192.168.1.1`), first create a deny rule for that IP, then allow general access to the port. This demonstrates the importance of rule order, as rules are processed top-down.







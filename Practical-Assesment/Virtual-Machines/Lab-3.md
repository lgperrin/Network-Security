# Lab 3: Introduction to Intrusion Detection with Snort in a Virtual Network

In Lab 3, we continue using the VMs from Practice Lab 2 to explore the basics of configuring rules in the network intrusion detection tool, Snort. This lab requires no prior knowledge of Linux, and step-by-step instructions are provided. The specific pipeline is:

![alt text](https://github.com/lgperrin/Network-Security/blob/main/Practical-Assesment/Images/Captura%20de%20pantalla%202024-02-26%20132306.png)

1. **Setup**. Continue using the VMs from Practice Lab 2, ensuring VirtualBox and the necessary VMs are ready for use. Confirm network interface configurations from Lab 2 are applied, setting the groundwork for Snort monitoring.
2. **Introduction to Snort Configuration**. Review the Snort configuration file (`snort.conf`) to understand the `HOME_NET` setting, which is crucial for rule definition and packet analysis within the specified network range.
3. **Rule Configuration**. Access and modify the `local.rules` file to input custom Snort rules. This involves understanding and applying the syntax for rule creation, focusing on:
   * Rule 1: Generating alerts for ICMP traffic directed at `HOME_NET`.
   * Rule 2: Alerting on TCP packets from `HOME_NET` on port 80.

4. **Running Snort and Generating Alerts**. Execute Snort with specific parameters to actively monitor network traffic on VM1, applying the configured rules. Engage in practical testing to trigger alerts defined by the rules, using ICMP pings for Rule 1 and Crafted TCP packets for Rule 2.
   
5. **Custom Rule Creation and Testing**. Stop Snort to update rules, demonstrating the importance of managing an IDS in dynamic network environments. Craft and add a new rule to detect telnet (port 23) traffic, showcasing the flexibility and customization possible with Snort rule syntax. Restart Snort and validate the effectiveness of the new rule through crafted packet testing, reinforcing the iterative process of rule creation, testing, and refinement.
   
6. **Advanced Packet Crafting and Detection**. Explore advanced packet crafting with hping3, including data payload manipulation, to simulate more sophisticated attack scenarios. Propose a scenario to detect a specific threat pattern (Night Dragon attack), applying knowledge of Snort rule writing and packet crafting to address emerging threats.


## 1.  Snort Network Setup

Set up a network intrusion detection system (IDS) using Snort in a controlled virtual environment with two VMs. VM1 will run Snort to monitor and generate alerts based on network traffic sent from VM2.

### 1.1 Network Configuration

Ensure both VMs are configured with static IP addresses within the same subnet to facilitate communication and monitoring. Follow the configuration steps as outlined in Lab 2.

* **For VM1**:
  * Disable the network interface: `sudo ifconfig enp0s8 down`
  * Assign IP address and network parameters: `sudo ifconfig enp0s8 192.168.1.1 netmask 255.255.255.0 broadcast 192.168.1.255`

* **For VM2**: Assign a similar configuration with an IP address of `192.168.1.2`.

### 1.2 Snort Configuration Review:

Without making changes, examine the Snort configuration file to understand how the `HOME_NET` variable is set up.

* Open a terminal in VM1 and navigate to the Snort configuration directory: `cd /etc/snort`
* Use the mousepad text editor to open the configuration file: `mousepad snort.conf`
* Locate the `HOME_NET` variable set to `192.168.1.0/24`, which defines the network range Snort will monitor.


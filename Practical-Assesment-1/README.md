# Practical Assesment 1 -- Packet Capture Analysis and Security Measures

## Requirements

- [x] Wireshark
- [x] Virtual Machine (VM) 
- [x] Assesment-1.pcap

## Part 1: Basic Analysis

### A. Transport Layer Protocol Analysis

Objective: Provide a quick overview of the packet capture's composition and involved IP addresses. You'll need to identify the percentage of bytes belonging to each transport layer protocol (e.g., TCP, UDP) in relation to the entire capture. This can be done by analyzing the pcap file to count bytes for each protocol.

  1. Open the packet capture file with Wireshark.
  2. Use "_Protocol Hierarchy_" under the statistics tools to view the percentage of bytes for each protocol, giving an idea of the traffic composition.
  3. Summarize these statistics in a PowerPoint slide, focusing on main transport layer protocols like TCP, UDP, etc.

### B. Identification of IP Addresses

Objective: Identify all IP addresses involved in the capture in order to understand the network's structure and the potential targets of the malware.

  1. Use the "_Endpoints_" tool under the "_Statistics_" menu to list all IP addresses involved in the capture.
  2. Highlight these IP addresses on your slide, noting any frequent addresses or address ranges that might indicate a network segment.

### C. Host and Network Insight

Objective: Deduce the capturing host's IP address by identifying the most common local address or based on the capture file's context. Also, provide insights into the IP addresses, such as potential local network ranges or external addresses that may indicate command and control servers or other relevant entities.

## Part 2: Advanced Analysis

Objective: Dive deeper into the packet capture to identify Mirai-specific activities and Indicators of Compromise (IOCs). In this section, you'll delve deeper into the pcap file using Wireshark to identify network activity and Indicators of Compromise (IOC) associated with Mirai. Focus on:

1. Timeline and Communications: Construct a timeline based on packet timestamps to understand the sequence of malicious activities.
2. Evidence of Mirai Activity: Look for signatures of Mirai, such as attempts to exploit specific vulnerabilities, the use of default credentials in Telnet access attempts, and unusual outbound traffic patterns.
3. Key Pieces of Evidence: Highlight specific packets, IP addresses, and payloads that indicate malicious activity.

### Evidence of Malware Activity
- **Method:**
  1. Look for patterns typical of Mirai, such as attempts to exploit known vulnerabilities, brute-force attacks over Telnet, and specific payloads or commands.
  2. Use Wireshark's filtering capabilities to isolate and examine these activities, e.g., `tcp.port == 23` for Telnet.

### Timeline and Key Evidence
- Construct a timeline of malicious activities by noting the timestamps of critical packets.
- Present specific packets or sequences that demonstrate malware behavior, including any payloads decoded from hexadecimal or ASCII.

## Part 3: Demonstrate Network Security Measures

Objective: Utilize VMs to replicate packet features observed in the analysis and test security measures. Based on the identified IOCs, you'll use hping3 to simulate similar traffic and then implement network security measures to detect or block such activity. Discuss the effectiveness of each measure and demonstrate them using the VM environment.

### Replicating Packet Features with hping3
- **Method:** Use hping3 to create packets that mirror those identified as malicious, including specific flags, payload sizes, or rate limiting.

### Implementing and Testing Security Measures
- Configure network security tools (e.g., IDS/IPS, firewalls) within the VMs based on the identified IOCs and behaviors.
- Demonstrate the effectiveness of these measures by showing how they identify or stop the test packets.

### Evaluation of Security Measures
- Discuss the strengths and potential weaknesses of each security measure, considering factors like false positives/negatives, resource consumption, and evasion techniques complexity.

## Video Report Tips
- Ensure clarity in both audio and visual elements. Use zooming or highlighting in Wireshark to make details easily viewable.
- Practice concise communication to stay within the time limit, focusing on the most critical elements of your analysis and recommendations.
- While presenting, imagine explaining your findings to someone with a technical understanding but who may not be familiar with network security analysis details.

## Final Notes
- Familiarize yourself with the specific tools and files (Wireshark, hping3, the packet capture file) required for practical execution.
- The goal is not just to identify malicious activity but also to demonstrate understanding by replicating behaviors and testing security measures effectively.

# Network Security


# University Course Information

| Attribute           | Details                       |
|---------------------|-------------------------------|
| **University**      | Queen's University of Belfast |
| **Module**          | Malware Analysis              |
| **Teacher**         | Dr Niall McLaughlin           |
| **Author of Notes** | Laura García Perrín           |


# Practical Assesment 1 -- Packet Capture Analysis and Security Measures

## Part 1: Basic Analysis

### Objective
Provide a quick overview of the packet capture's composition and involved IP addresses.

### Analysis of Protocols
- **Tool Used:** Wireshark
- **Method:**
  1. Open the packet capture file with Wireshark.
  2. Use "Protocol Hierarchy" under the statistics tools to view the percentage of bytes for each protocol, giving an idea of the traffic composition.
  3. Summarize these statistics in a PowerPoint slide, focusing on main transport layer protocols like TCP, UDP, etc.

### Identification of IP Addresses
- **Tool Used:** Wireshark
- **Method:**
  1. Use the "Endpoints" tool under the "Statistics" menu to list all IP addresses involved in the capture.
  2. Highlight these IP addresses on your slide, noting any frequent addresses or address ranges that might indicate a network segment.

### Host and Network Insight
- Deduce the capturing host's IP address by identifying the most common local address or based on the capture file's context.
- Provide insights into the IP addresses, such as potential local network ranges or external addresses that may indicate command and control servers or other relevant entities.

## Part 2: Advanced Analysis

### Objective
Dive deeper into the packet capture to identify Mirai-specific activities and Indicators of Compromise (IOCs).

### Evidence of Malware Activity
- **Method:**
  1. Look for patterns typical of Mirai, such as attempts to exploit known vulnerabilities, brute-force attacks over Telnet, and specific payloads or commands.
  2. Use Wireshark's filtering capabilities to isolate and examine these activities, e.g., `tcp.port == 23` for Telnet.

### Timeline and Key Evidence
- Construct a timeline of malicious activities by noting the timestamps of critical packets.
- Present specific packets or sequences that demonstrate malware behavior, including any payloads decoded from hexadecimal or ASCII.

## Part 3: Demonstrate Network Security Measures

### Objective
Utilize VMs to replicate packet features observed in the analysis and test security measures.

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

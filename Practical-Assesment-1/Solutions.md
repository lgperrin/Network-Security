# Solutions to the Exercises

## Part 1: Basic Analysis

### A. Transport Layer Protocol Analysis

From the _Statistics_ $>$ _Protocol Hierarchy_ section we get:

![alt text](https://github.com/lgperrin/Network-Security/blob/main/Practical-Assesment-1/Images/Captura%20de%20pantalla%202024-02-22%20114059.png)

Based on the Protocol Hierarchy statistics provided from Wireshark, here's what we can derive for task 1.A:

1. **Transmission Control Protocol (TCP)**: This is the dominant transport layer protocol in the capture, accounting for 83.2% of the total bytes. This suggests that most of the network activity in the capture was TCP-based. Given that TCP is a connection-oriented protocol, this indicates a prevalence of established sessions, which could include web traffic, file transfers, or other application data that requires reliable communication.

2. **User Datagram Protocol (UDP)**: UDP accounts for 16.8% of the total bytes. This is significantly less than TCP, indicating less UDP-based activity. Since UDP is connectionless and often used for services that require fast delivery such as DNS or streaming, the presence of UDP could be related to domain resolution activities or possibly streaming or real-time communication services.

3. **Telnet**: Within the TCP traffic, Telnet is specifically highlighted, accounting for 17.7% of the packets and 59.6% of the TCP bytes. This is a substantial portion of the traffic, which is particularly significant given that Telnet is an unencrypted protocol commonly exploited by malware like Mirai for command and control or lateral movement within a network due to its use of default or weak credentials.

4. **Hypertext Transfer Protocol (HTTP)**: HTTP traffic makes up 5.7% of the total bytes. While it's a smaller portion, HTTP traffic could be indicative of web browsing, web-based file transfers, or potentially web-based command and control communications.

5. **Domain Name System (DNS)**: DNS traffic, which uses UDP, accounts for 16.8% of the packets but only 2.9% of the total bytes, which aligns with the typical behavior of DNS traffic being frequent but small in size.

| Protocol      | Percentage of Packets | Percentage of Bytes | Observations                                         |
|:-------------:|:---------------------:|:-------------------:|-----------------------------------------------------|
| **TCP**       | 83.2%                 | 83.7%               | Majority of the traffic, suggesting reliable sessions|
| **UDP**       | 16.8%                 | 16.8%               | Used for services requiring fast delivery, like DNS  |
| **Telnet**    | 17.7% of TCP packets  | 59.6% of TCP bytes  | Significant, possibly indicating Mirai activity      |
| **HTTP**      | Not Applicable        | 5.7%                | Web activity or potential web-based C2 communications|
| **DNS**       | 16.8% of UDP packets  | 2.9%                | Frequent but small packets typical for DNS           |

Given this data, for task 1.A we could state that the network traffic captured is predominantly TCP-based with a significant amount of Telnet traffic, which could be indicative of Mirai malware activity since Mirai is known to exploit Telnet. The presence of substantial HTTP traffic suggests regular web activity or potential web-based C2 mechanisms. The relatively high number of DNS packets compared to their byte size is consistent with normal network behavior, as DNS queries are generally frequent but small in packet size.

### B. Identify All IP Addresses

To complete task 1B, where we need to identify all IP addresses involved in the packet capture, we need to follow these steps in Wireshark:

1. Open Wireshark and load the pcap file.
2. Go to the "_Statistics_" menu at the top.
3. Select "Endpoints" from the drop-down menu.
4. In the Endpoints window, click on the "_IPv4_" tab to list all the unique IPv4 addresses. If there is IPv6 traffic, you can also click on the "_IPv6_" tab.
We can export this information by clicking the "_Copy_" button at the bottom of the Endpoints window and select "_… as CSV_" to copy the details in a CSV format that can be pasted into a spreadsheet or other document.

This will give you a list of all IP addresses that have sent or received packets during the capture. If you want to narrow it down to only certain types of traffic, you can apply a display filter before opening the Endpoints window. For example, if you want to identify the IP addresses involved in Telnet traffic, you could apply a filter such as `tcp.port == 23` before opening the Endpoints statistic.


### C. Host and Network Insights






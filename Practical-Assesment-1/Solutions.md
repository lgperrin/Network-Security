# Solutions to the Exercises

## Part 1: Basic Analysis

### A. Transport Layer Protocol Analysis

From the _Statistics_ $>$ _Protocol Hierarchy_ section we get:

![alt text](https://github.com/lgperrin/Network-Security/blob/main/Practical-Assesment-1/Images/Captura%20de%20pantalla%202024-02-22%20114059.png)

Based on the Protocol Hierarchy statistics provided from Wireshark, here's what we can derive for task 1.A:

1. **Transmission Control Protocol (TCP)**: This is the dominant transport layer protocol in the capture, accounting for $83.2$% of the total bytes. This suggests that most of the network activity in the capture was TCP-based. Given that TCP is a connection-oriented protocol, this indicates a prevalence of established sessions, which could include web traffic, file transfers, or other application data that requires reliable communication.

2. **User Datagram Protocol (UDP)**: UDP accounts for $16.8$% of the total bytes. This is significantly less than TCP, indicating less UDP-based activity. Since UDP is connectionless and often used for services that require fast delivery such as DNS or streaming, the presence of UDP could be related to domain resolution activities or possibly streaming or real-time communication services.

3. **Telnet**: Within the TCP traffic, Telnet is specifically highlighted, accounting for $17.7$% of the packets and $59.6$% of the TCP bytes. This is a substantial portion of the traffic, which is particularly significant given that Telnet is an unencrypted protocol commonly exploited by malware like Mirai for command and control or lateral movement within a network due to its use of default or weak credentials.

4. **Hypertext Transfer Protocol (HTTP)**: HTTP traffic makes up $5.7$% of the total bytes. While it's a smaller portion, HTTP traffic could be indicative of web browsing, web-based file transfers, or potentially web-based command and control communications.

5. **Domain Name System (DNS)**: DNS traffic, which uses UDP, accounts for $16.8$% of the packets but only $2.9$% of the total bytes, which aligns with the typical behavior of DNS traffic being frequent but small in size.

| Protocol      | Percentage of Packets | Percentage of Bytes | Observations                                         |
|:-------------:|:---------------------:|:-------------------:|-----------------------------------------------------|
| **TCP**       | 83.2%                 | 83.7%               | Majority of the traffic, suggesting reliable sessions|
| **UDP**       | 16.8%                 | 16.8%               | Used for services requiring fast delivery, like DNS  |
| **Telnet**    | 17.7% of TCP packets  | 59.6% of TCP bytes  | Significant, possibly indicating Mirai activity      |
| **HTTP**      | Not Applicable        | 5.7%                | Web activity or potential web-based C2 communications|
| **DNS**       | 16.8% of UDP packets  | 2.9%                | Frequent but small packets typical for DNS           |

Given this data, for task 1.A we could state that the network traffic captured is predominantly TCP-based with a significant amount of Telnet traffic, which could be indicative of Mirai malware activity since Mirai is known to exploit Telnet. The presence of substantial HTTP traffic suggests regular web activity or potential web-based C2 mechanisms. The relatively high number of DNS packets compared to their byte size is consistent with normal network behavior, as DNS queries are generally frequent but small in packet size.

### B. Identify All IP Addresses

To complete task 1B, where we need to identify all IP addresses involved in the packet capture, we will follow these steps in Wireshark:

1. Open Wireshark and load the pcap file.
2. Go to the "_Statistics_" menu at the top.
3. Select "_Endpoints_" from the drop-down menu.
4. In the Endpoints window, we can click on the "_IPv4_" tab to list all the unique IPv4 addresses. This information can be exported by clicking the "_Copy_" button at the bottom of the Endpoints window and select "_… as CSV_" to copy the details in a CSV format that can be pasted into a spreadsheet or other document. This will give us a list of all IP addresses that have sent or received packets during the capture. If we want to narrow it down to only certain types of traffic, we can apply a display filter before opening the Endpoints window.

![alt text](https://github.com/lgperrin/Network-Security/blob/main/Practical-Assesment-1/Images/Captura%20de%20pantalla%202024-02-23%20101902.png)

**Comments**. From the screenshot we can see there are six unique IPv4 addresses in our `Assessment-1.cap` file along with associated data, such as the number of packets, bytes transmitted and received, and in some cases, additional information like country, city, latitude, longitude, AS number, and organization. Interesting facts we can get from this:

| IP Address       | Description |
|------------------|-------------|
| `8.8.8.8`        | This is a public DNS server provided by Google. It's widely used for resolving domain names to IP addresses. |
| `13.51.81.207`   | This address belongs to the Amazon Web Services (AWS) range. It could be hosting services or applications. |
| `13.51.81.212`   | This address belongs to the Amazon Web Services (AWS) range. It could be hosting services or applications. |
| `65.222.202.53`  | Without additional context, it's not clear what this IP is used for. However, it could be related to a service provider or a private entity based on the network infrastructure. |
| `109.184.144.30` | This is likely an IP address located in Europe based on the numeric range, but without additional data or context, its use is not clear. |
| `192.168.2.56`   | This is a private IP address, commonly used within private networks. This address is not routable on the public internet and is typically used for local network devices. |


### C. Host and Network Insights






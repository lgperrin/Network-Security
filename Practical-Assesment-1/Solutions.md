# Solutions to the Exercises

## Part 1: Basic Analysis

### A. Transport Layer Protocol Analysis

![alt text](https://github.com/lgperrin/Network-Security/blob/main/Practical-Assesment-1/Images/Captura%20de%20pantalla%202024-02-22%20114059.png)

Based on the Protocol Hierarchy statistics provided from Wireshark, here's what we can derive for task 1.A:

1. **Transmission Control Protocol (TCP)**: This is the dominant transport layer protocol in the capture, accounting for 83.2% of the total bytes. This suggests that most of the network activity in the capture was TCP-based. Given that TCP is a connection-oriented protocol, this indicates a prevalence of established sessions, which could include web traffic, file transfers, or other application data that requires reliable communication.

2. **User Datagram Protocol (UDP)**: UDP accounts for 16.8% of the total bytes. This is significantly less than TCP, indicating less UDP-based activity. Since UDP is connectionless and often used for services that require fast delivery such as DNS or streaming, the presence of UDP could be related to domain resolution activities or possibly streaming or real-time communication services.

3. **Telnet**: Within the TCP traffic, Telnet is specifically highlighted, accounting for 17.7% of the packets and 59.6% of the TCP bytes. This is a substantial portion of the traffic, which is particularly significant given that Telnet is an unencrypted protocol commonly exploited by malware like Mirai for command and control or lateral movement within a network due to its use of default or weak credentials.

4. **Hypertext Transfer Protocol (HTTP)**: HTTP traffic makes up 5.7% of the total bytes. While it's a smaller portion, HTTP traffic could be indicative of web browsing, web-based file transfers, or potentially web-based command and control communications.

5. **Domain Name System (DNS)**: DNS traffic, which uses UDP, accounts for 16.8% of the packets but only 2.9% of the total bytes, which aligns with the typical behavior of DNS traffic being frequent but small in size.

Given this data, for task 1.A we could state that the network traffic captured is predominantly TCP-based with a significant amount of Telnet traffic, which could be indicative of Mirai malware activity since Mirai is known to exploit Telnet. The presence of substantial HTTP traffic suggests regular web activity or potential web-based C2 mechanisms. The relatively high number of DNS packets compared to their byte size is consistent with normal network behavior, as DNS queries are generally frequent but small in packet size.

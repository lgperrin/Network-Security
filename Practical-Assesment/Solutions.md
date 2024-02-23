# Solutions to the Exercises

## Table of Contents

- [Part 1: Basic Analysis](#part-1-basic-analysis)
  - [1.1 Transport Layer Protocol Analysis](#a-transport-layer-protocol-analysis)
  - [1.2 Identify All IP Addresses](#b-identify-all-ip-addresses)
  - [1.3 Host and Network Insights](#c-host-and-network-insights)
- [Part 2: Advanced Analysis](#part-2-advanced-analysis)
  - [2.1 Capture File Properties](#21-capture-file-properties)
  - [2.2 TCP Port](#22-tcp-port)
  - [2.3 HTTP GET Request](#23-http-get-request)
  - [2.4 Detecting TCP SYN Floods Attacks](#24-detecting-tcp-syn-floods-attacks)
  - [2.5 DNS Traffic](#25-dns-traffic)
- [Part 3: Demonstrate Network Security Measures](#part-3-demonstrate-network-security-measures)
- [Conclusions](#conclusions)


## Part 1: Basic Analysis

### 1.1 Transport Layer Protocol Analysis

From the _Statistics_ $>$ _Protocol Hierarchy_ section we get:

![alt text](https://github.com/lgperrin/Network-Security/blob/main/Practical-Assesment-1/Images/Captura%20de%20pantalla%202024-02-22%20114059.png)

Based on the Protocol Hierarchy statistics provided from Wireshark, here's what we can derive for task 1.A:

1. **Transmission Control Protocol (TCP)**: This is the dominant transport layer protocol in the capture, accounting for $83.2$% of the total bytes. This suggests that most of the network activity in the capture was TCP-based. Given that TCP is a connection-oriented protocol, this indicates a prevalence of established sessions, which could include web traffic, file transfers, or other application data that requires reliable communication.

2. **User Datagram Protocol (UDP)**: UDP accounts for $16.8$% of the total bytes. This is significantly less than TCP, indicating less UDP-based activity. Since UDP is connectionless and often used for services that require fast delivery such as DNS or streaming, the presence of UDP could be related to domain resolution activities or possibly streaming or real-time communication services.

3. **Telnet**: Within the TCP traffic, Telnet is specifically highlighted, accounting for $17.7$% of the packets and $59.6$% of the TCP bytes. This is a substantial portion of the traffic, which is particularly significant given that Telnet is an unencrypted protocol commonly exploited by malware like Mirai for command and control or lateral movement within a network due to its use of default or weak credentials.

4. **Hypertext Transfer Protocol (HTTP)**: HTTP traffic makes up $5.7$% of the total bytes. While it's a smaller portion, HTTP traffic could be indicative of web browsing, web-based file transfers, or potentially web-based command and control communications.

5. **Domain Name System (DNS)**: DNS traffic, which uses UDP, accounts for $16.8$% of the packets but only $2.9$% of the total bytes, which aligns with the typical behavior of DNS traffic being frequent but small in size.

<ins>**Comments**</ins>. Given this data, we could state that the network traffic captured is predominantly TCP-based with a significant amount of Telnet traffic, which could be indicative of Mirai malware activity since Mirai is known to exploit Telnet. The presence of substantial HTTP traffic suggests regular web activity or potential web-based C2 mechanisms. The relatively high number of DNS packets compared to their byte size is consistent with normal network behavior, as DNS queries are generally frequent but small in packet size.

### 1.2 Identify All IP Addresses

In order to identify all IP addresses involved in the packet capture, we will follow these steps in Wireshark:

1. Open Wireshark and load the pcap file.
2. Go to the "_Statistics_" menu at the top.
3. Select "_Endpoints_" from the drop-down menu.
4. In the Endpoints window, we can click on the "_IPv4_" tab to list all the unique IPv4 addresses. This information can be exported by clicking the "_Copy_" button at the bottom of the Endpoints window and select "_… as CSV_" to copy the details in a CSV format that can be pasted into a spreadsheet or other document. This will give us a list of all IP addresses that have sent or received packets during the capture. If we want to narrow it down to only certain types of traffic, we can apply a display filter before opening the Endpoints window.

![alt text](https://github.com/lgperrin/Network-Security/blob/main/Practical-Assesment-1/Images/Captura%20de%20pantalla%202024-02-23%20101902.png)

<ins>**Comments**</ins>. From the screenshot we can see there are six unique IPv4 addresses in our `Assessment-1.cap` file along with associated data, such as the number of packets, bytes transmitted and received, and in some cases, additional information like country, city, latitude, longitude, AS number, and organization. Interesting facts we can get from this:

| IP Address       | Description |
|------------------|-------------|
| `8.8.8.8`        | This is a public DNS server provided by Google. It's widely used for resolving domain names to IP addresses. |
| `13.51.81.207` and `13.51.81.212`   | This address belongs to the Amazon Web Services (AWS) range. It could be hosting services or applications. |
| `65.222.202.53`  | Without additional context, it's not clear what this IP is used for. However, it could be related to a service provider or a private entity based on the network infrastructure. |
| `109.184.144.30` | This is likely an IP address located in Europe based on the numeric range, but without additional data or context, its use is not clear. |
| `192.168.2.56`   | This is a private IP address, commonly used within private networks. This address is not routable on the public internet and is typically used for local network devices. |


### 1.3 Host and Network Insights

**How can we identify the host IP?** By looking for the IP address with the most packets sent and received, as this is often the host machine where the capture was taken. In network captures, the host typically has the most traffic because it communicates with multiple external IP addresses. In the provided data, the IP address `192.168.2.56` has the highest number of packets, which suggests it could be the host of the capture.

**Are there any other IPs in the same network which might be interesting?** We can seek for any other IPs which are part of the subnet from the host IP. For example, private IP addresses like `192.168.x.x` are typically on the same subnet and belong to the same local network. However, there aren't any other private addresses which follow that IP structure, so we can state that `192.168.2.56` is the only local network IP address captured.

**Can we state any insights that might be inferred about other host IP addresses which might be useful in understanding the behaviour of the malware?** Of course, concretely:

* The connections to `8.8.8.8` indicate that the host is using Google’s DNS, which is common for both benign and malicious activities.
* The AWS IPs (`13.51.81.207` and `13.51.81.212`) could be significant if they are not expected within the network's normal traffic; they might be related to C2 communication or there might be hosting a service that interacts with the malware.
* The absence of additional context about the addresses `65.222.202.53` and `109.184.144.30` makes it difficult to draw definitive conclusions, but their interactions with the host may warrant further investigation, especially if the traffic volume is anomalous or if there are connections on unusual ports.

## Part 2: Advanced Analysis

In this section, we have to identify a diverse range of features from the capture that provide clear evidence of network activity and network Indicators of Compromise (IOC) associated with Mirai network activity.

### 2.1 Capture File Properties 

The Capture File Properties provide information about the packet capture (pcap) file. We can get this info by opening _Statistics -> Capture File Properties_:

![alt text](https://github.com/lgperrin/Network-Security/blob/main/Practical-Assesment-1/Images/Captura%20de%20pantalla%202024-02-23%20104930.png)

<ins>**Comments**</ins>. The path shows that the file is stored in the `OneDrive/Documents/Network Security` directory, indicating it may be related to a network security assessment or exercise. The file is $508$ KB, which suggests a moderate amount of captured data, and it's also "_hashed_" as it appears some cryptographic hash functions, like SHA256 and SHA-1, which might be used to verify the integrity of the file. On the other hand, the file is in standard Wireshark format (`.pcap`) and the data it contains is encapsulated using Ethernet, indicating that the capture was taken from a network using Ethernet technology. The maximum packet size that was captured is $65535$ bytes, which is the maximum Ethernet frame size and the capture duration was about 30 minutes, starting from `19:18:31` and ending at `19:48:42` on September 30, 2016. Some other statistics are:

* A total of $1753$ packets were captured.
* The capture spanned $1810.887$ seconds.
* The average packets per second (`pps`) is $1.0$, indicating that, on average, one packet was captured per second.
* The average packet size is $274$ bytes.
* The total number of bytes captured is $480379$.
* The average bytes per second is $265$, which could be considered low, indicating not a very high traffic volume during the capture period.
* The bit rate is $2129$ bits per second, which again suggests a <ins>low traffic volume</ins>.

### 2.2 TCP Port 

In the top pane, we can select the first packet and expand the TCP information in the middle pane.

![alt text](https://github.com/lgperrin/Network-Security/blob/main/Practical-Assesment-1/Images/Captura%20de%20pantalla%202024-02-23%20110704.png)

<ins>**Comments**</ins>. The source TCP port is `55392`, meanwhile the destination port is `23`, which is commonly used for Telnet, a protocol used to provide a command-line interface for communication with a remote device. The use of port $23$ could suggest that the packet is part of an attempt to establish a Telnet connection, which is often not secure because it transmits data, including passwords, in plaintext. Now, we can apply the source port of the first packet as a filter in order to see how many packets are displayed when the filter is applied. There are 28 packets.

On the other side, and in the context of a network capture file analyzed with Wireshark, TCP conversations represent the back-and-forth communication between two endpoints over the Transmission Control Protocol (TCP). Each conversation is a distinct stream of packets sharing a common source and destination IP address, as well as a pair of ports – one for the source (Port A) and one for the destination (Port B). We can get this information by opening _Statistics -> Conversations -> TCP_.

![alt text](https://github.com/lgperrin/Network-Security/blob/main/Practical-Assesment-1/Images/Captura%20de%20pantalla%202024-02-23%20122204.png)

<ins>**Comments**</ins>. We can see that there are 61 TCP conversations, most of them having the port `80` as the most frequent for the field _Port B_. Port $80$ being the most common Port B indicates that the majority of these conversations are directed towards a web server, as Port $80$ is the default port for HTTP traffic, which is unencrypted web traffic. The presence of other conversations where Port B is $23$ indicates that there are a few instances of communication with a Telnet service. Telnet operates on Port $23$ and is used for remote command-line interface access and it is generally considered insecure (as we mentioned before) because it transmits data in plaintext, without encryption.

So, **what can be said about the TCP conversations?** In the context of a network security assessment or an analysis for malicious activity, the numerous communications on Port $80$ indicate a predominance of web traffic within the network, whereas communications on Port $23$, used for Telnet, could signify potential security concerns, as Telnet is inherently insecure and its use may imply attempts at unauthorized access or device control within the network.

### 2.3 HTTP GET Request 

**What URL does the attack attempt to use?** To find out which URL an attack is attempting to use in a pcap file, we'll need to look for an HTTP GET request, as this is the method used by web browsers and other clients to request data from servers. One approach is to use the "_Filter_" bar at the top of the main Wireshark window to filter the displayed packets and enter the filter expression `http.request.method == "GET"` to show only the HTTP GET requests. Then, expand the '_Hypertext Transfer Protocol_' field to view the full HTTP request, including the requested URL. After that, we can select the menu item _Analyze → Follow → TCP Stream_. The only HTTP Get Request packet we get is the following:

![alt text](https://github.com/lgperrin/Network-Security/blob/main/Practical-Assesment-1/Images/Captura%20de%20pantalla%202024-02-23%20111756.png)

<ins>**Comments**</ins>. The HTTP GET request is attempting to access a resource at the URL path `/bins/mirai.arm7`. The destination IP address is `13.51.81.212`, which previously was identified as belonging to the Amazon Web Services (AWS) range. This suggests that the requested resource is hosted on a server within AWS. On the other hand, the specific path `/bins/mirai.arm7` indicates that the request is for a file named `mirai.arm7` located in a directory named "_bins_". The `.arm7` suffix suggests that this file is compiled for ARMv7 architecture, which is commonly used in mobile devices and embedded systems. The name "_mirai_" is associated with a well-known malware strain that targets IoT devices. Once infected, devices are conscripted into a botnet that can be used for various malicious activities, including large-scale distributed denial-of-service (DDoS) attacks.

The fact that a GET request for `mirai.arm7` is present in the network traffic may indicate that the host with IP address `192.168.2.56` is involved in downloading malware or could be part of it. Given the context of the capture, this GET request could be a significant indicator of compromise or an attempt to infect or control a device within the network. 

### 2.4 Detecting TCP SYN Floods Attacks

These attacks try to fill the state table in a firewall or try to overwhelm a server's buffer. To detect SYN floods using Wireshark, we can apply the following steps:

1. **Identify Excessive SYN Packets**. Apply the display filter `tcp.flags.syn == 1 && tcp.flags.ack == 0` to view only the SYN packets that do not have the ACK flag set. These packets represent connection initiation requests. There are $111$ packets that areattempting to establish new connections, which could be legitimate traffic or could be part of a SYN flood attack if these attempts are not completing the TCP three-way handshake.
   
3. **Examine Responses**. Next, we'll want to identify the server's responses with the filter `tcp.flags.syn == 1 && tcp.flags.ack == 1`. This filter shows SYN/ACK packets, which are the server's way of acknowledging the SYN requests. There are $36$ packets that are responses to the initial connection attempts.

In a SYN flood attack, we would expect to see a large number of SYN packets compared to SYN/ACK packets because the attacker does not complete the TCP handshake. Since the number of SYN-ACK Packets is significantly less than the number of initial SYNs, it suggests that some initial SYNs did not receive a response, possibly due to the server being overwhelmed or a filtering mechanism in place, as it happens in SYN flood attacks. Finally and based on the information from the SYN and SYN-ACK packets:

* The most common destination IP address for the initial SYN packets (indicative of outgoing connection attempts) is `65.222.202.53`.
* The most common source IP address for the SYN-ACK packets (indicative of responses to connection attempts) is also `65.222.202.53`.

This suggests that the <ins>IP address being targeted by the attempted DoS (Denial of Service)</ins> is `65.222.202.53` as it is receiving numerous SYN packets from an internal IP address (`192.168.2.56`) but is only able to send back a smaller number of SYN-ACK packets in response.

### 2.5 DNS Traffic

Finally, we could inspect the DNS traffic by applying the filter `dns`on Wireshark, from which we get:

![alt text](https://github.com/lgperrin/Network-Security/blob/main/Practical-Assesment-1/Images/Captura%20de%20pantalla%202024-02-23%20125422.png)

<ins>**Comments**</ins>. The source IP address `192.168.2.56` is making repeated DNS queries to the Google DNS server `8.8.8.8`. The domain being queried is `network.santasbigcandycane.cx`. This domain name is unusual and does not appear to be associated with any legitimate service or website. Such domains can often be linked to malicious activities. Finally, the repeated queries for the same domain could indicate automated behavior, possibly from a malware-infected device that is trying to communicate with a control server.


## Part 3: Demonstrate Network Security Measures

For Part 3 we are required to use the two VMs that were used for Labs 2 and 3. This task involves leveraging the network activity and Indicators of Compromise (IoCs) identified in Part 2 to craft and send test packets between the VMs. Here’s a summarized plan of action:

1. **Creating Test Packets**: Utilize `hping3` to generate test packets that mimic the key characteristics of the network activity observed in Part 2. These packets should simulate the malicious traffic patterns or IoCs identified during your analysis, such as specific TCP/UDP ports used, packet sizes, or frequency.

2. **Implementing Security Measures**: Choose appropriate network security tools available within the VMs to demonstrate how we would detect and protect a real network against the Mirai variant observed. This could involve configuring firewalls, intrusion detection systems, or other security mechanisms to identify and mitigate the simulated attack traffic.

3. **Evaluation of Security Measures**: Discuss the advantages and disadvantages of the security measures we've implemented. Consider their effectiveness against the Mirai malware, potential impacts on network performance, false positives/negatives, and any limitations they may have in a real-world scenario.


## Conclusions

From the Parts 1 and 2, we can state that the network traffic analysis uncovers substantial evidence of potentially malicious activities, including significant Telnet traffic that might indicate Mirai malware activity, attempts to download malware, and potential SYN flood attack signs. Also, the usage of AWS IPs and repeated DNS queries to an unusual domain suggest potential command and control activities. 




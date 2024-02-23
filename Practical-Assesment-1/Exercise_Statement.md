# Practical Assesment 1 -- Packet Capture Analysis and Security Measures

## Requirements

- [x] Wireshark
- [x] Virtual Machine (VM) 
- [x] Assesment-1.pcap

## Part 1: Basic Analysis

You are required to concisely present the following information at the start of your video. No other introduction or summary is necessary. You may wish to summarise information answering parts 1.a, 1.b, and 1.c in a single PowerPoint slide. This part of the video should take you less than 1 minute to present.

a. For all protocols encapsulated by the transport layer, identify the percentage of bytes belonging to each protocol relative to the entire capture.

b. Identify all IP addresses involved in the capture.

c. State the IP address of the host where the capture was taken, as well as any other IP addresses that you think belong to the same network. Briefly, state any insights that might be inferred about other host IP addresses that you think is useful in understanding the behaviour of the malware.

## Part 2: Advanced Analysis

Identify a diverse range of features from the capture that provide clear evidence of network activity and network Indicators of Compromise (IOC) associated with Mirai network activity. This part of the video should take you 2-3 minutes to present.

* Use Wireshark to present your analysis. You are required to demonstrate that you can effectively use the Wireshark tool for packet analysis.
* Provide a verbal and visual explanation of what you think happened in the network. You may want to consider a timeline of the communications that took place and walk through the evidence using Wireshark.
* Be sure to clearly show on screen the observable features or network Indicators of Compromise that you think are key pieces of evidence.
* Discuss and display specific individual packets, protocol information, headers, IP addresses, payloads, etc. (anything you think is relevant), with commentary about how the information supports your discussion.

## Part 3: Demonstrate Network Security Measures

For Part 3 you are required to use the two VMs that were used for Labs 2 and 3. This part of the video should take you 2-3 minutes to present.

* Using the network activity and Indicators of Compromise identified in your answer for Part 2, use hping3 to create test packets that replicate those key features. hping3 will allow you to send created packets from one VM to the other.
* Using whatever network security tools that you think are appropriate within the existing VM environment, propose and demonstrate network security measures that you would implement in a real network to provide protection and detection against the version of Mirai that you observed in the packet capture.
* Briefly explain any pros or cons of your proposed network security measures, i.e. how effective you think each of your proposed measures would be against Mirai.
* For guidance, the test packets you create with hping3 do not have to perfectly replicate the packets seen in the original packet capture. The expectation is that you create packets with features that are sufficiently similar to allow for meaningful testing of your security measures.
* You should present a diverse set of security measures against various network indicators that you believe would be effective, i.e. several different measures and IOCs should be covered by your answer.
* Provide a verbal and visual explanation to demonstrate and prove that your test packets and security measures work as expected.

Note that for Part 3 you must create test packets that replicate features of interest that you found in the pcap. You do not need to use the Assessment-1.pcap file within the VM environment. You should not create your own alternative VM environment. You do not need to modify the VMs, apart from using the tools as covered in Labs 2 and 3.

## Video Report Tips
- Ensure clarity in both audio and visual elements. Use zooming or highlighting in Wireshark to make details easily viewable.
- Practice concise communication to stay within the time limit, focusing on the most critical elements of your analysis and recommendations.
- While presenting, imagine explaining your findings to someone with a technical understanding but who may not be familiar with network security analysis details.

## Final Notes
- Familiarize yourself with the specific tools and files (Wireshark, hping3, the packet capture file) required for practical execution.
- The goal is not just to identify malicious activity but also to demonstrate understanding by replicating behaviors and testing security measures effectively.

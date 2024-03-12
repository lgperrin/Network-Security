# 1. Background Information

ADVRTS is a small to medium sized company that started 5 years ago and has quickly grown to 25 employees. They serve 100s of clients by developing online adverts that are seen on websites and social media across the world. The company is constantly producing new media (images, videos, catchy jingles, marketing text, etc.) for their clients. These creations can produce significant intellectual property that is very valuable to the company and to the clients.

The company is split into a few teams dealing with separate functions of the business, primarily a sales team, content creators, and a business management and finance team. Employees of ADVRTS often split their time between the head office and working from home. Sometimes they also visit their bigger clients. Due to these remote working scenarios, they have a number of software platforms that staff are required to access remotely. After a disagreement about the highly questionable nature of online advertisements tracking and monetizing the personal data of the unsuspecting public, the person who was managing the IT systems at ADVRTS suddenly left the company. Consequently, the management have called in your consultancy firm to report on the state of their IT systems.

The ADVRTS staff have provided the following information related to their company network and various IT systems:

* The company is based at a single site with office space for staff. The office space contains several PCs and various other hosts, including a few servers used by different groups in the company, including a media database server which hosts advert related media files that the company has created.

* The company is provided with two static IPv4 public IP addresses by its business broadband provider. A Fortinet 40F has been used to set up a DMZ and a separate office LAN that uses private IP addressing. The Fortinet is also occasionally used to provide SSL VPN access for remote users to access a ‘Docuware’ server.

* The DMZ is home to a ‘Qlik Sense’ server, which is on-premises software used by the company for data analytics to process information related to the performance of adverts, user interactions, and so on. The DMZ allows access to both the internal LAN, and to remote staff via the second static IP address.

* According to initial discussions with staff, the Fortinet device and the Qlik server were set up around 18 months ago. However, it is not known how long ago other networked devices were set up, and there appears to be no clear policy for update and patch management, so the status of systems on the network in this respect is uncertain.

* For internal networking, a UniFi USW-Pro-48 switch is used to create a single LAN. Hosts across the company share the 192.168.1.0/24 address range, with internet access provided via one of the static IP addresses provided by the ISP.

* The LAN hosts a server running ‘Docuware’ on-premises software that allows for processing and storage of financial data related to sales and clients.

* The previous network administrator configured the network so hosts generally use Google’s 8.8.8.8 public DNS service as a default.
Most hosts are connected by physical ethernet cables to the switch. Additionally, a NETGEAR WAC104 Dual Band wireless access point, connected to the switch, provides WiFi connectivity for laptops and mobile devices.


In addition to the information about the network, given above, your manager is particularly concerned about a new ransomware threat called Cactus Ransomware. As part of your report, you must consider how ADVRTS might be vulnerable to Cactus Ransomware. According to the guidance on the next page, you therefore must also propose a set of network security solutions that could be used to detect the specific presence of Cactus Ransomware activities across the ADVRTS network, focussing on network IOCs related to the malware.

Where information about the current network configuration is not known, in your report you can state your own (reasonable) assumptions and work from there.

# 2. Report Requierements

You must submit a report of 1,800 to 2,000 words in total, which includes any references. Your report must have two sections that address the requirements listed below:

## Part 1: Analysis of Network Security Threats – General Issues and Cactus Related Issues

 - [x] Consider the background information about the network and its usage. Accordingly, present an analysis that identifies key network security issues of concern at the company.

 - [x] Based on the information provided and your own research, you should explain any threats to the company from the Cactus Ransomware.
Your analysis should include justifications to explain why each issue you identify poses a security threat. For example, don’t just say that something is bad, or an obvious problem. Concisely explain what could happen as a consequence of each threat.

 - [x] For all threats you identify, you must consider their relative severity, and rank which issues you would prioritise as highest risk. You must justify your analysis with some discussion of the relative risks. (This is not an exact science. The intention is for you to demonstrate judgement in evaluating the threats).

## Part 2: Network Security Recommendations

 - [x] Propose solutions to improve the security of the network, based on general best practice and your analysis of issues and threats from part 1. In particular, explain how you would apply detection and protection measures to address network security issues that you have identified.

 - [x]  Your recommendations should consider specific network indicators of compromise (IOCs) and propose how they can be used to detect the presence of Cactus malware in the company network. Focus on network-based IOCs. There may well be published information that discusses encryption, file hashes, etc. which are not applicable or useful from a networking perspective.

 - [x] Draw a network diagram to illustrate how you would propose to configure the network to improve its security. Be sure to discuss key points about the diagram in your text.

 - [x] Assuming long-term changes will take time to implement, highlight any short-term mitigations that should be applied as a priority to lessen risks to the current network.

 - [x] Evaluate how effective you think your proposed security measures would be. Consider any trade-offs or pros and cons.



# 3. Dos and Don’ts

* Do independent research into the issues presented in the Background Information.

* Do provide technical depth about specific details in your answers.
* Do explain why you are recommending a specific solution, and what the effect will be.
* Don’t provide generic or superficial advice.

  * For example: “Use a network IDS to detect attacks and a firewall to block scanning” does not meaningfully address the case study.

  * Generic advice can be provided by a chatbot. You need to go beyond this and provide meaningful insight related to the technical details in the case study.

* Do not spend time on issues that cannot be addressed by networking technologies. For example:

  * Discussing executables is not generally related to networking (unless, for example, an executable can somehow cause activity that is observable on the network).
  * Don’t recommend data back-ups, good passwords, etc. – unless for example you discover the company has a router that uses default passwords, these are not networking issues. A concise technical report is required, not an essay.
  * Aim for concise detail, clear reasoning, and clear advice, which can be quickly digested.


# 4. Format

You may use any word processor to produce your document, but the submission must be a PDF.

* Your document style should be clear, uncomplicated, and professional.
* Font: Calibri, Arial, Times, or similar, using font size 11 or 12
* Do not use 1.5 or double line spacing to make the document seem longer.

# 5. Referencing

You should include a small number of references to support key recommendations.

* References count towards your total word count.
* Provide references as a footnote as shown in this sentence 1. It is unlikely you will need to cite academic papers. If you do, use a footnote with the APA or Harvard style.
* It is unlikely you will need more than 5-6 references, so choose references related to key technical issues. For example, you might refer to a source that provides significant instructions on how to configure a particular device, which would be useful to someone carrying out this task. Summarise the key points and add a footnote.

* Using external material to learn about an issue does not mean you need to reference every single source of information that you used to form your judgements.

* The content of your report should be able to stand on its own. In real life your manager will not want to have to follow a bunch of references to understand your discussion!






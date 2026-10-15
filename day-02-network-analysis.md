day-02-network-analysis.md
Day 2: Network Traffic Analysis with Wireshark

Lab Overview

In this lab, I used Wireshark to capture and analyze network traffic from my computer. The goal was to develop foundational packet analysis skills and better understand how devices communicate across networks.

Tools Used

* Wireshark
* Visual Studio Code
* macOS
* GitHub (for lab documentation)

Lab Objectives

* Identify private and public IPv4 addresses
* Analyze DNS queries and responses
* Examine TCP three-way handshakes
* Identify UDP traffic and IPv6 addresses
* Understand the security relevance of network traffic analysis

Lab Environment

Capture Interface: Wi-Fi (en0)

Capture File: day-02-network-capture.pcapng

Analysis Method: Wireshark display filters and packet inspection

## Step 3: IPv4 Address Analysis
**Protocol:** TCP
**Source IP Address:** 192.168.1.106
**Source IP Type:** Private
**Destination IP Address:** 89.43.104.212
**Destination IP Type:** Public

### Observations
I selected packet number 8 in Wireshark and examined the source and destination IP addresses. The source address was 192.168.1.106, which is a private IP address commonly used within home networks. The destination address was 89.43.104.212, which is a public IP address.

This packet demonstrates communication from a private network address to a public internet address. I also identified TCP as the protocol used for this packet.

**What I Learned**
I learned how to identify source and destination IP addresses in Wireshark and determine whether they are private or public. This skill is important in cybersecurity because it helps analysts understand where network traffic originates and where it is going.

## Step 4: DNS Traffic Analysis
Protocol: DNS

Domain Queried: mask.apple-dns.net

Query Type: HTTPS (65)

Transaction ID: 0x80eb

DNS Class: IN (Internet)

**Observations**

While analyzing DNS traffic in Wireshark, I identified a DNS query for mask.apple-dns.net, a domain associated with Apple’s networking and privacy services.

The query used record type HTTPS (65), which requests information about connecting to an HTTPS service.

The packet contained one DNS question and zero answers because it was a request rather than a response.

**What I Learned**

I learned how to identify and examine DNS queries in Wireshark, including the domain name, query type, transaction ID, and DNS flags. I also learned that DNS queries can request different types of information beyond IPv4 and IPv6 addresses.

### DNS Response Analysis

Domain Queried: mask.apple-dns.net

Query Type: HTTPS (65)

Response Code: No error

Answer Records: 0

**Observations**

I examined the DNS response associated with my original query. The DNS server returned a response code of “No error,” indicating that the request was processed without a DNS error.

However, the response contained zero answer records. This demonstrates that a DNS response can indicate no error without necessarily returning the requested information.

**What I Learned**

I learned how to match DNS queries with their responses and interpret DNS response codes and answer counts in Wireshark.

### DNS Authority Record Analysis

Domain: mask.apple-dns.net

Requested Record Type: HTTPS (65)

Response Code: No error

Answer Records: 0

Authority Record Type: SOA (Start of Authority)

**Observations**

I examined the authoritative nameservers section of the DNS response and identified an SOA record.

The DNS response returned no error but contained zero answer records for the requested HTTPS record type. This is consistent with a NOERROR/NODATA response.

**What I Learned**

I learned that a successful DNS response does not always contain the requested DNS record. I also learned that SOA records provide administrative information about DNS zones and can appear in the Authority section of DNS responses.

## Step 5: TCP Three-Way Handshake Analysis

Protocol: TCP (Transmission Control Protocol)

TCP Stream Index: 6

Client Source Port: 52969

Server Destination Port: 443 (HTTPS)

Handshake Status: Complete

**Observations**

While analyzing TCP traffic in Wireshark, I identified a complete TCP three-way handshake.

1. SYN: The client initiated a connection with the server.
2. SYN-ACK: The server acknowledged the connection request.
3. ACK: The client acknowledged the server’s response, completing the handshake.

After the TCP handshake, I observed TLS 1.3 traffic, including Client Hello and Server Hello messages, followed by encrypted application data.

**What I Learned**

I learned how TCP establishes reliable connections through the three-way handshake. I also learned how to use TCP stream filters in Wireshark to isolate individual connections and examine their communication.

**Security Relevance**

Cybersecurity analysts examine TCP handshakes to identify connection attempts, troubleshoot networking problems, and investigate potentially suspicious communication patterns.

## Step 6: UDP and IPv6 Traffic Analysis

Packet Number: 411

Network Protocol: IPv6

Transport Protocol: UDP

Source IPv6 Address: 2600:1700:5790:7770:6dbf:d365:e357:7b59

Destination IPv6 Address: 2600:1700:5790:7770::1

Source Port: 9201

Destination Port: 53 (DNS)

**Observations**

While analyzing UDP traffic in Wireshark, I identified packet 411, which used IPv6 for network addressing and UDP for transport.

The packet originated from source port 9201 and was sent to destination port 53, which is commonly associated with DNS services.

Unlike TCP, UDP does not require a three-way handshake before sending data.

**What I Learned**

I learned how to identify UDP traffic, examine source and destination ports, recognize IPv6 addresses, and understand how DNS can operate over UDP.

**Security Relevance**

Cybersecurity analysts monitor DNS traffic to understand network activity, investigate unusual domain requests, and identify potentially suspicious communication patterns.

### UDP DNS Query Investigation

Packet Number: 411

Network Protocol: IPv6

Transport Protocol: UDP

Source Port: 9201

Destination Port: 53

Domain Queried: mobile.events.data.microsoft.com

DNS Query Type: HTTPS (65)

DNS Class: IN (Internet)

**Observations**

I identified a DNS query transmitted over UDP using IPv6.

The query requested HTTPS service information for mobile.events.data.microsoft.com, a domain associated with Microsoft’s event and diagnostic data services.

The DNS request contained one question and zero answer records.

I also identified a linked DNS response in packet 414.

**What I Learned**

I learned how DNS operates over UDP, how to examine IPv6 traffic, and how to identify domain names and DNS record types in Wireshark.

I also learned that DNS queries can request HTTPS service information rather than only IPv4 or IPv6 addresses.

### DNS Response Verification

Query Packet: 411

Response Packet: 414

Domain: mobile.events.data.microsoft.com

Query Type: HTTPS (65)

Response Code: No error

Answer Records: 2

**Observations**


I examined the DNS response associated with packet 411 and identified the corresponding response in packet 414.

The DNS server returned a response code of “No error” and included two answer records.

Earlier in my analysis, I observed another DNS response that returned no error but contained zero answer records.

Comparing these responses helped me understand that DNS responses can contain different amounts of information depending on the request and the server’s response.

**What I Learned**

I learned how to match DNS queries with their responses, interpret response codes, and examine the number of answer records returned by a DNS server.

## Lab Summary

During this lab, I captured and examined network traffic using Wireshark. I analyzed source and destination IP addresses, DNS queries and responses, TCP connection establishment, and UDP communication over IPv6.

I successfully identified a complete TCP three-way handshake and observed TLS 1.3 traffic following the establishment of the connection.

I also investigated DNS responses that contained different numbers of answer records and learned how to interpret DNS response codes.

## Cybersecurity Skills Demonstrated

* Network packet analysis
* TCP/IP protocol fundamentals
* DNS traffic investigation
* IPv4 and IPv6 address identification
* Network troubleshooting fundamentals
* Technical documentation

## Security Takeaways

Network traffic analysis helps cybersecurity professionals understand communication patterns, identify unusual connections, and investigate potential security incidents.

This lab strengthened my ability to interpret packet-level information and document findings in a structured manner.

## Conclusion

This exercise provided hands-on experience with networking concepts relevant to entry-level cybersecurity and Security Operations Center (SOC) analyst roles.
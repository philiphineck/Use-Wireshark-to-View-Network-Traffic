# Wireshark Activity: # Unmasking Network Traffic with a Packet Sniffer

## Project Overview

Welcome to the fascinating world of network traffic analysis! This project plunges into the core of how data moves across a network, utilizing **Wireshark**, a powerful software protocol analyzer. Often referred to as a "packet sniffer" application, Wireshark is used for network troubleshooting, analysis, software and protocol development, and education. As data streams travel back and forth over the network, the sniffer "captures" each protocol data unit (PDU) and can decode and analyze its content according to the appropriate RFC or other specifications. This hands-on lab is designed to demystify the journey of data, from your local machine to remote servers across the Internet, by focusing on **ICMP (Ping) traffic**.

My role in this project was to actively engage with the Wireshark tool, capturing and analyzing live network data. This involved configuring filters, interpreting packet headers, and discerning the intricate details of how data is encapsulated and addressed at different layers of the network model.

**Key Technologies Used:**

* **Wireshark:** The primary tool for packet capture and analysis.
* **Command Prompt (Windows):** Used for executing `ipconfig` and `ping` commands.
* **Local Area Network (LAN):** The environment for capturing local traffic.
* **Internet Control Message Protocol (ICMP):** The protocol specifically examined for network diagnostics (ping).
* **TCP/IP Protocol Suite:** The foundational model guiding data transmission.

## The Journey Begins: Diving into Local Traffic

My initial exploration focused on understanding how basic communication happens within our immediate network. By sending simple "ping" requests to another computer on the same Local Area Network (LAN), we could observe the fundamental exchange of data packets. This analysis helped clarify how packet headers are used to transport data to their destination.

### How I Unveiled Local ICMP Data:

1.  **Preparation is Key:** Before capturing, we retrieved our PC's vital network statistics using `ipconfig /all` in the command prompt. This provided us with our PC IP address, its network interface card (NIC) description, and its MAC (physical) address.
2.  **Launching the Sniffer:** Wireshark was launched, and we double-clicked the desired interface to start the packet capture. We ensured the desired interface had traffic.
3.  **Focusing the Lens (Filtering):** Networks are bustling places! To avoid information overload, we applied an `icmp` filter in Wireshark by typing `icmp` in the Filter box and pressing Enter or clicking the Apply button. This ensured that only ICMP (ping) PDUs were displayed, allowing us to concentrate on our specific test traffic.
4.  **Generating the Traffic:** From the command prompt, we initiated a ping to a teammate's PC on the LAN. As the ping requests and replies occurred, Wireshark's top window, previously empty due to the filter, began to populate with live ICMP packets.
5.  **Stopping the Flow:** Once enough data was captured, we halted the capture process by clicking the Stop Capture icon.

### Insights from Local ICMP Capture:

Examining the captured data revealed fascinating details about local network communication. Wireshark data is displayed in three sections: the top section lists captured PDU frames with IP packet information; the middle section details PDU information for the selected frame, separated by protocol layers; and the bottom section displays the raw data of each layer in both hexadecimal and decimal form.

* **PDU Structure:** As described above, Wireshark's interface facilitates detailed analysis.
* **Source and Destination IPs:** Clicking the first ICMP request PDU frame showed our PC's IP address in the Source column and the teammate PC's IP address in the Destination column.
* **MAC Address Revelation:** With the PDU frame selected, navigating to the middle section and clicking the plus sign next to the Ethernet II row allowed us to view the destination and source MAC addresses. We verified that the source MAC address matched our PC interface.
* **ARP's Role:** A significant observation was understanding how the MAC address of the pinged PC is obtained by our PC. This typically involves the Address Resolution Protocol (ARP), which resolves IP addresses to MAC addresses on a local network.
* **Encapsulation in Action:** The captured ICMP request showed that ICMP data is encapsulated inside an IPv4 packet PDU (IPv4 header), which is then encapsulated in an Ethernet II frame PDU (Ethernet II header) for transmission on the LAN. This visual confirmation solidified the layered approach of network protocols.

## Beyond the Local Network: Probing Remote Hosts

The next phase involved exploring communication with hosts *outside* our local network – hosts on the Internet. This allowed us to highlight key differences in how packets are handled when they need to cross a router.

### How I Tracked Remote ICMP Data:

1.  **Fresh Start:** We started the data capture again. A prompt appeared to save previously captured data, but it was not necessary, so we clicked "Continue without Saving".
2.  **Pinging the World:** With the capture active, we pinged three website URLs from a Windows command prompt: `www.yahoo.com`, `www.cisco.com`, and `www.google.com`.
3.  **DNS in Action:** When pinging the URLs, we noticed that the Domain Name Server (DNS) translated the URL to an IP address, and we noted the IP address received for each URL.
4.  **Capture Complete:** Once the ping operations finished, the capture was stopped by clicking the Stop Capture icon.

### Distinctions in Remote ICMP Capture:

Reviewing the captured data in Wireshark for the three remote locations  revealed a critical difference compared to local traffic:

* **Destination IP vs. Destination MAC:** While we could clearly see the *destination IP address* for `www.yahoo.com`, `www.cisco.com`, and `www.google.com`, the *destination MAC address* consistently belonged to our **Default Gateway Router**, not the remote host itself.

This fundamental difference highlights how routing works: when sending traffic to a remote network, our PC doesn't know the remote host's MAC address directly. Instead, it sends the packet to its **default gateway** (the router), which is responsible for forwarding the packet closer to its final destination. The MAC address we see is always that of the *next hop* device on the local network.

## Reflection and Key Takeaways

This activity provided a powerful visual demonstration of network communication principles.

**Why Wireshark shows local MAC addresses but not remote ones:**
Wireshark captures traffic on your local network interface. When you communicate with a local host, that host is directly accessible on your LAN, and its MAC address can be discovered using ARP. Therefore, Wireshark can show the actual MAC address of the local destination.

However, when you communicate with a remote host (e.g., a server on the Internet), that host is not on your local network. Your computer doesn't know its MAC address directly. Instead, your computer sends the packet to its **default gateway router**. The router then takes responsibility for forwarding the packet across the Internet. Therefore, the destination MAC address seen in Wireshark for remote traffic will *always* be the MAC address of your **default gateway router**, which is the next hop on your local network, not the MAC address of the final remote destination.

This lab reinforced the critical roles of both IP addresses (for logical addressing across networks) and MAC addresses (for physical addressing on a local segment), and how they interact to facilitate communication, whether local or global. It truly brought the abstract concepts of networking to life by showing the packets in action.

---
## Author

**Philiphine Cheptanui**


---
**Connect with Me:** &emsp;&emsp;
[LinkedIn](http://linkedin.com/in/philiphinecheptanui) &emsp;&emsp;
[PortFolio Website](https://compnetworksecurity.blogspot.com/) &emsp;&emsp;
[Repository](https://github.com/philiphineck/Use-Wireshark-to-View-Network-Traffic) &emsp;&emsp;
[Email](koimaphilipine@gmail.com) &emsp;&emsp;
---

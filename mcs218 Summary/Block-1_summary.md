Summary of Block-1.pdf:

This academic text provides a comprehensive introduction to data communication and computer networks, covering fundamental concepts from the Internet's structure to data transmission, encoding, multiplexing, and switching.

Here's a summary of the main ideas, key points, and conclusions:

---

### Unit 1: Introduction to Internet

*   **Definition of Computer Networks and Internet:**
    *   A computer network is two or more computing devices connected to share information, resources, and messages, regardless of geographical location.
    *   The Internet is the largest global computer network, a "network of networks," connecting billions of people and organizations worldwide.
    *   ARPANET was the world's first general-purpose computer network (1969), with Bob Taylor credited as the "father of the Internet."
    *   End systems (hosts) are computing devices (desktops, mobiles, etc.) that connect to the Internet using applications like web browsers and email.
*   **Internet Service Providers (ISPs) and Internet Backbone:**
    *   ISPs transport Internet traffic and are hierarchically organized into a 3-tier model:
        *   **Tier-1 ISPs:** Form the Internet backbone, have global coverage, connect directly to other Tier-1 ISPs, and handle the majority of traffic with very high-speed links (e.g., Sprint, AT&T).
        *   **Tier-2 ISPs:** Have regional/national coverage, connect to a few Tier-1 ISPs, and often peer with other Tier-2 ISPs.
        *   **Tier-3 ISPs (Access ISPs):** At the bottom of the hierarchy, connect end systems to the Internet via Tier-2 or Tier-1 ISPs.
    *   **Points of Presence (POPs):** Routers where ISPs connect to other ISPs or customer networks.
*   **Network Taxonomy (Classification):**
    *   **By Physical Area:**
        *   **Personal Area Network (PAN):** Few meters (e.g., Bluetooth, USB).
        *   **Local Area Network (LAN):** Small geographical area (e.g., single building, campus).
        *   **Metropolitan Area Network (MAN):** City-wide (e.g., TV cable network, broadband).
        *   **Wide Area Network (WAN):** Large geographical area (cities, states, countries). The Internet is the largest WAN.
    *   **By Architecture:** Peer-to-peer, Client-server.
    *   **By Transmission Technology:** Broadcast networks (shared channel, message to all), Point-to-point/Switched networks.
*   **Standard Internet Protocols:**
    *   Protocols are rules enabling devices to communicate. The Internet Protocol Suite is layered:
        *   **Application Layer:** Facilitates user access to services (HTTP, SMTP).
        *   **Transport Layer:** End-to-end data delivery (TCP for reliable, UDP for unreliable).
        *   **Network Layer:** Routes data, assigns IP addresses (IPv4, IPv6).
        *   **Data Link Layer:** Node-to-node data delivery (Ethernet for wired, IEEE 802.11 for wireless).
*   **Public vs. Private Networks (Intranet):**
    *   **Public Network:** Open access (e.g., Internet), uses public IP addresses, less secure.
    *   **Private Network (Intranet):** Managed/controlled by an authority, restricted access (e.g., school network), uses private IP addresses, often requires Network Address Translator (NAT) for Internet access.
*   **Accessing the Internet:**
    *   **Telephone Network:**
        *   **Dial-Up Lines:** Slow (max 56kbps), temporary connection, ties up phone line.
        *   **Dedicated Lines:** Always-on, higher quality.
            *   **ISDN (Integrated Services Digital Network):** Faster than dial-up, uses telephone lines, limited range (3.5 miles).
            *   **DSL (Digital Subscriber Line):** Fast, uses existing telephone lines, "always-on," allows simultaneous voice/data. ADSL (Asymmetric DSL) is popular for higher download speeds.
    *   **Cable Network:** Uses television cable infrastructure, faster (up to 1 Gbps) than dial-up/DSL, but can be less secure and costlier.
    *   **Wireless Network:** Cheaper to install/maintain, uses radio waves (e.g., Wi-Fi, Bluetooth, Infrared). Wi-Fi has typical range ~90 meters.
*   **Internet Services:**
    *   **Communication Services:** Email, Telnet, Internet Relay Chat (IRC), Voice over IP (VoIP), Instant Messaging (IM).
    *   **Information Retrieval Services:** File Transfer Protocol (FTP).
    *   **Web Services:** Applications interacting with each other.
    *   **World Wide Web (WWW):** System for retrieving linked documents (text, audio, visuals, graphics) via hyperlinks.
*   **Network Topology:**
    *   Defines the physical and logical arrangement of nodes. Affects performance and cost.
    *   **Bus Topology:** Nodes connected to a common backbone link. Simple, cheap, but single point of failure (backbone), prone to collisions, insecure.
    *   **Star Topology:** All devices connect to a central hub/switch. Easy to install/extend, robust (if central node is fine), but central node is a single point of failure.
    *   **Ring Topology:** Each device connected to two others, forming a ring. Low collision chances (token message), cheap. Difficult fault diagnosis and extension.
    *   **Mesh Topology:** Each device directly connected to every other device. Highly robust, easy fault diagnosis, secure. Most costly and difficult to manage for large networks.
*   **Network Models (OSI and TCP/IP):**
    *   Hierarchical, layered approach to simplify network understanding and enable interoperability.
    *   **OSI (Open System Interconnection) Model (7 Layers):** Reference model, conceptual.
        1.  **Physical Layer:** Hardware standards, signaling, bit transmission (Hub).
        2.  **Data Link Layer (DLL):** Node-to-node delivery, framing, physical (MAC) addressing, flow/error control, access control (Switch, Bridge).
        3.  **Network Layer:** IP addressing, routing (best path selection), packetizing (Router).
        4.  **Transport Layer:** Process-to-process delivery (port numbers), segmentation/reassembly, connection-oriented (TCP) or connectionless (UDP) services, end-to-end flow/error control.
        5.  **Session Layer:** Manages communication sessions (establish, maintain, synchronize).
        6.  **Presentation Layer:** Data formatting (translation, encryption/decryption, compression/decompression).
        7.  **Application Layer:** User interface to network services (HTTP, FTP, SMTP).
    *   **TCP/IP Model (4 Layers):** More practical, reflects actual working.
        *   **Application Layer:** Combines OSI Session, Presentation, Application layers.
        *   **Transport Layer:** Same as OSI Transport layer.
        *   **Internet Layer:** Same as OSI Network layer.
        *   **Link Layer:** Combines OSI Data Link and Physical layers.

---

### Unit 2: Data Transmission Basics & Transmission Media

*   **Data Communication Terminology:**
    *   **Channel:** Medium for data transmission (wired/wireless), has capacity.
    *   **Baud:** Unit of symbol rate (signals changes per second). Bit rate = Baud rate × bits per Baud.
    *   **Bandwidth:** Data carrying capacity per unit time (bits/s for digital, Hz for analog). Higher bandwidth means higher throughput.
    *   **Frequency:** Rate of repetition of an event per second (Hz).
*   **Modes of Data Transmission:**
    *   **Directional Modes:**
        *   **Simplex:** One-way communication (e.g., radio broadcast, keyboard to computer).
        *   **Half-Duplex:** Two-way communication, but one direction at a time (e.g., walkie-talkie).
        *   **Full-Duplex:** Two-way communication simultaneously (e.g., telephone).
    *   **Bit Transfer Modes:**
        *   **Serial Communication:** Bits sent one after another over a single channel. Suitable for long distances, slower.
        *   **Parallel Communication:** Multiple bits sent simultaneously over multiple channels. Faster, suitable for short distances.
    *   **Synchronization in Serial Communication:**
        *   **Synchronous Communication:** Data transmitted in frames/blocks, regulated by an external clock. Faster, expensive, uses CRC for error control.
        *   **Asynchronous Communication:** Data transmitted character by character, uses start/stop bits. Slower, economical, uses parity bit for error control.
        *   **Isochronous Communication:** Hybrid of synchronous and asynchronous; uses start/stop bits but transmits characters at fixed intervals.
*   **Analog and Digital Data Transmission:**
    *   **Analog Signals:** Continuous, represented by sine waves (e.g., voice, video). Signal strength decreases over distance, amplifiers boost signal *and* noise, leading to error accumulation.
    *   **Digital Signals:** Discrete pulses, represented by square waves (e.g., computer data). Repeaters regenerate original signal levels, effectively removing noise. Less prone to errors over distance.
*   **Transmission Impairments:** Factors that degrade signal quality.
    *   **Attenuation:** Loss of signal energy/strength over distance due to medium resistance. Measured in dB.
    *   **Delay Distortion:** Different frequency components of a composite signal travel at different speeds, causing signal distortion.
    *   **Noise:** Unwanted signals mixing with the original signal. Types include thermal, induced, impulse, and crosstalk noise.
    *   **Signal to Noise Ratio (SNR):** Measures signal quality (ratio of signal power to noise power). Higher SNR indicates better quality.
    *   **Concept of Delays:** Time taken for a packet to reach its destination.
        *   **Transmission Delay:** Time to put the entire packet onto the transmission medium (Packet Size / Bandwidth).
        *   **Propagation Delay:** Time for the signal to travel across the physical medium (Distance / Speed of Signal).
*   **Transmission Media:**
    *   **Guided Media (Wired):** Physical conduits that guide signals.
        *   **Twisted-Pair Cable:** Copper wires twisted to reduce interference (UTP - unshielded, STP - shielded). Cheapest, easiest to install, used in LANs.
        *   **Coaxial Cable:** Two concentric conductors. Higher bandwidth than twisted-pair, used in TV cable networks.
        *   **Fiber Optic Cable:** Transmits data as light pulses through thin glass fibers (total internal reflection). Very high speed, huge bandwidth, immune to electromagnetic interference, but costly to install/maintain. Can be multimode (multiple light paths) or single mode (single light path).
    *   **Unguided Media (Wireless):** Broadcast signals through air (electromagnetic waves).
        *   **Ground Propagation:** Low frequency radio waves close to Earth's surface, omnidirectional.
        *   **Sky Propagation:** Radio waves (2-30 MHz) reflected by the ionosphere for long distances.
        *   **Line-of-Sight Propagation:** High frequency signals travel in a straight line between antennas.
*   **Wireless Transmission Methods:**
    *   **Microwave Transmission:** High frequency (1-300 GHz), narrow focused, line-of-sight. Used for terrestrial (Earth-based antennas) and satellite communication. Affected by environmental factors at lower frequencies.
    *   **Radio Transmission:** Lower frequency (3 KHz-1 GHz), omnidirectional. Can penetrate walls, but prone to interference. Used in AM/FM radio, TV.
    *   **Infrared and Millimeter Waves:** Very high frequency (300 GHz-400 THz), short-range, line-of-sight. Used in remote controls.
*   **Wireless LAN (WLAN):** Uses radio waves for wireless connectivity in a local area (e.g., Wi-Fi).

---

### Unit 3: Data Encoding and Multiplexing (Focus on Encoding)

*   **Encoding Necessity:** To transform information signals into a format suitable for transmission over physical media, especially over long distances. This involves "modulation," where a low-frequency information signal modifies a high-frequency "carrier" signal.
*   **Four Basic Combinations of Encoding:**
    *   **Analog-to-Analog Modulation:** Encoding analog data as an analog signal (e.g., radio broadcasting).
        *   **Amplitude Modulation (AM):** Varies carrier amplitude. Vulnerable to noise (static).
        *   **Frequency Modulation (FM):** Varies carrier frequency. Less susceptible to noise, higher quality, requires more bandwidth.
        *   **Phase Modulation (PM):** Varies carrier phase. Similar to FM in noise immunity.
    *   **Analog-to-Digital Modulation:** Encoding analog data as a digital signal (e.g., digitizing voice for digital media).
        *   **Pulse Code Modulation (PCM):** High quality. Involves:
            1.  **Pulse Amplitude Modulation (PAM):** Sampling the analog signal at fixed intervals (Nyquist's theorem: sample rate >= 2 * highest frequency).
            2.  **Quantization:** Converting sampled analog amplitudes into discrete digital values.
            3.  **Encoding:** Converting discrete values into binary digits.
        *   **Delta Modulation:** Simpler, lower quality method; encodes only the direction of change in amplitude (1 for increase, 0 for decrease).
    *   **Digital-to-Analog Modulation:** Encoding digital data as an analog signal (e.g., modems over telephone lines).
        *   **Bit Rate:** Number of individual bits transmitted per second.
        *   **Baud Rate:** Number of signal transitions per second.
        *   **Amplitude Shift Keying (ASK):** Varies carrier amplitude to represent bits. Vulnerable to noise. Bandwidth equals baud rate.
        *   **Frequency Shift Keying (FSK):** Varies carrier frequency. Less susceptible to noise than ASK, but higher bandwidth.
        *   **Phase Shift Keying (PSK):** Varies carrier phase. Robust against amplitude noise. Allows multiple bits per symbol (e.g., 4-PSK, 8-PSK) for increased efficiency.
        *   **Quadrature Amplitude Modulation (QAM):** Combines ASK and PSK. Most efficient, achieves high bit rates with the same bandwidth as ASK/PSK by using multiple amplitude and phase levels.
    *   **Digital-to-Digital Encoding:** Encoding digital data as a digital signal (e.g., computer to printer, LANs).
        *   **Unipolar Encoding:** Uses a single polarity (e.g., positive voltage for 1, zero for 0). Problems: synchronization issues with long strings of same bit, and a DC (direct current) component.
        *   **Polar Encoding:** Uses both positive and negative voltage levels. Reduces DC component.
            *   **Non-Return to Zero (NRZ):** NRZ-L (level-based), NRZ-I (inversion-based). NRZ-I is better for synchronization with 1s.
            *   **Return to Zero (RZ):** Signal returns to zero midway through each bit, ensuring synchronization, but requires higher bandwidth.
            *   **Biphase Encoding (Manchester/Differential Manchester):** Transitions mid-bit (Manchester) or at the beginning of the bit (Differential Manchester) for synchronization.
        *   **Bipolar Encoding:** Uses three levels (zero for 0, alternating positive/negative for 1s). Eliminates DC component, helps synchronize 1s.
            *   **Alternate Mark Inversion (AMI):** Problem with long strings of 0s.
            *   **High Density Bipolar 3 (HDB3) & 8-Zero Substitution (B8ZS):** Techniques to address long strings of 0s by introducing controlled "violations" of the AMI rule to maintain synchronization.

---

### Unit 4: Multiplexing and Switching

*   **Multiplexing:**
    *   **Purpose:** To enable simultaneous transmission of multiple data streams over a single shared communication channel due to bandwidth scarcity and economic efficiency.
    *   **Multiplexer:** Combines multiple inputs into one output.
    *   **Demultiplexer:** Separates the combined signal back into original inputs.
    *   **Frequency Division Multiplexing (FDM):**
        *   Divides the available frequency spectrum into multiple smaller, non-overlapping frequency bands.
        *   Each data stream is assigned a dedicated frequency band, allowing simultaneous transmission.
        *   Uses "guard bands" to prevent interference (crosstalk) between adjacent channels.
        *   Can suffer from "intermodulation noise" due to non-linear equipment.
        *   Inefficient if channels are idle as their dedicated frequency band remains unused.
    *   **Time Division Multiplexing (TDM):**
        *   Divides the transmission time into discrete time slots, allowing each data stream to use the entire bandwidth for a brief period.
        *   **Synchronous TDM:** Fixed time slots are reserved for each input, regardless of whether there is data to transmit. Simpler to implement but can be inefficient due to wasted idle slots. Requires frame synchronization (e.g., by adding a fixed bit pattern) and pulse stuffing (to handle clock variations).
        *   **Statistical TDM:** Time slots are dynamically allocated only when an input device has data to send. More efficient as it utilizes available bandwidth better during periods of inactivity. Requires addressing information in each frame to identify the source and buffering for peak loads. More complex than synchronous TDM.
*   **Digital Subscriber Lines (DSL):**
    *   **ADSL (Asymmetric DSL):** A popular DSL technology that uses existing telephone lines to provide high-speed Internet access.
    *   **Asymmetric Nature:** Dedicates more bandwidth/channels for downstream (downloading) traffic than for upstream (uploading) traffic, reflecting typical user behavior.
    *   **Limitations:** Speed heavily depends on the distance from the subscriber's premises to the provider's nearest termination point.
    *   **Implementation:** Requires a splitter and ADSL modem at the user's end.
*   **ADSL vs. Cable Internet:**
    *   **ADSL:** Offers a dedicated connection, leading to predictable speeds and higher security (no shared channel). Limited by distance.
    *   **Cable Internet:** Uses shared coaxial cable infrastructure (shared among many users), leading to variable speeds and potential security risks (though often mitigated by encryption). Offers higher potential bandwidth generally.
*   **Switching:**
    *   **Purpose:** To connect any two desired nodes in a large network for communication, as direct physical links between all possible pairs are impractical.
    *   **Circuit Switching:**
        *   Establishes a dedicated, physical communication path (circuit) between two devices for the entire duration of their conversation.
        *   Involves three phases: circuit setup, data transmission, and circuit dismantling.
        *   **Space Division Switches:** Create separate physical paths (e.g., crossbar switches). No delays once the path is established. Pure crossbar is impractical due to the high number of "crosspoints." Multistage switching reduces crosspoints but introduces the possibility of "blocking" (no available path).
        *   **Time Division Switches (TSI):** Achieves switching by reordering time slots in a TDM stream. Involves buffering and introduces delays.
        *   **Combination Switches (e.g., TST):** Combine space and time division stages to optimize cost (crosspoints) and performance (delays).
        *   **Suitability:** Ideal for voice communication due to its continuous nature, low delay tolerance, and stable data rates. Inefficient for bursty data traffic as resources are wasted during idle periods.
    *   **Packet Switching:**
        *   Data is broken into self-contained units called "datagrams" (packets), each containing destination address and control information.
        *   No dedicated path is established; each packet is routed independently by intermediate network nodes.
        *   **Advantages over Circuit Switching for Data:**
            *   **Efficiency:** Optimizes resource utilization for "bursty" data traffic, as channels are not held idle.
            *   **Flexibility:** Allows for prioritization of data, and alternate routes can be used if a link fails or congestion occurs.
            *   **Robustness:** Can recover from link failures by re-routing.
        *   **Datagram Approach:** Packets are routed independently and may arrive out of sequence at the destination.
        *   **Virtual Circuit Approach:** A logical "virtual circuit" is established at the beginning of a session, and all packets for that session follow the same pre-determined route.
            *   **Permanent Virtual Circuits:** Dedicated logical paths, always available.
            *   **Switched Virtual Circuits:** Logical paths set up on demand for a limited duration.
            *   Offers reliability by re-routing if a part of the virtual circuit fails, without disrupting the session. Can still experience congestion at switches due to multiplexing.

---

**Conclusion:**
The text emphasizes that efficient and reliable data communication relies on a complex interplay of network infrastructure, standardized protocols, various transmission media, and sophisticated encoding/multiplexing/switching techniques. Each component is designed to address specific challenges related to distance, speed, noise, security, and the diverse nature of data and communication demands. The evolution from simple analog transmission to complex digital and hybrid systems reflects the continuous effort to optimize bandwidth utilization, minimize errors, and enhance user experience in a globally interconnected world.
Summary of Block-2.pdf:

This academic text provides a comprehensive overview of the Data Link Layer (DLL) in computer networks, covering its fundamental functions, error and flow control mechanisms, media access control protocols for both wired and wireless environments, and data link layer switching devices.

Here's a summary of the main ideas, key points, and conclusions:

**I. Data Link Layer Fundamentals (Unit 1)**

*   **Role of Data Link Layer (DLL):**
    *   Second layer of the OSI model.
    *   Takes raw data from the Physical layer and transforms it into an "error-free" line for the Network layer.
    *   Converts data packets into frames for transmission.
    *   Divided into two sublayers:
        *   **Media Access Control (MAC) Layer:** Controls how a computer gains access to link resources and permission to transmit.
        *   **Logical Link Control (LLC) Layer:** Controls frame synchronization, flow control, and error checking.
*   **Key Functions of DLL:**
    *   **Framing:**
        *   Process of converting bit streams into discrete units called frames, explicitly marking their beginning and end.
        *   Methods:
            *   **Character Count:** Header specifies frame size; susceptible to desynchronization if count is corrupted.
            *   **Character Patterns (Character Stuffing):** Uses special ASCII sequences (DLE STX, DLE ETX) to mark frame boundaries; DLE stuffing handles embedded DLEs in data. Less suitable for non-character-oriented streams.
            *   **Bit Patterns (Bit Stuffing):** Uses a specific bit flag (01111110) for frame boundaries; inserts a '0' after five consecutive '1's in data to prevent flag imitation. More flexible for arbitrary bit streams.
            *   **Framing by Illegal Code (Code Violation):** Uses bit patterns not used for data (e.g., Manchester encoding's all-low/all-high codes) as markers.
    *   **Error Detection:**
        *   Ensures accurate data delivery by detecting alterations during transmission.
        *   **Types of Errors:**
            *   **1-bit error:** Single bit flipped (0 to 1, or 1 to 0).
            *   **Burst error:** Two or more bits altered, within a defined "burst" size.
            *   **Lost message (frame):** Frame sent but not received.
        *   **Detection Methods (using Redundancy):**
            *   **Parity Check:** Adds a single parity bit to make the count of 1s even or odd; weak, only detects single-bit errors.
            *   **Block Sum Check:** Extension of parity, adding row and column parity bits; detects up to two-bit errors and increases burst error detection probability.
            *   **Cyclic Redundancy Check (CRC):** Treats bit strings as polynomials; sender divides data by a generator polynomial and appends the remainder (checksum/FCS). Receiver divides by the same polynomial; a zero remainder indicates error-free data. Highly effective for burst errors.
            *   **Checksum:** Divides data into segments, sums them using one's complement arithmetic, and appends the complemented sum. Receiver recalculates; all 1s (complement all 0s) indicates error-free.
    *   **Forward Error Correction (FEC):**
        *   Enables the receiver to correct errors without requiring retransmission, by identifying the exact location of the error.
        *   Requires `2^r >= n + r + 1` redundant bits (`r`) for `n` data bits to identify all possible error locations (including no error).
        *   **Hamming Code:** An example of FEC that inserts redundant bits at specific positions to create parity checks that pinpoint error locations.
    *   **Flow Control:**
        *   Manages the rate of data transmission to prevent a faster sender from overwhelming a slower receiver's buffer.
        *   **Basic Strategies:**
            *   **Stop-and-Wait:** Sender transmits one frame and waits for an acknowledgment (ACK) before sending the next. Simple but inefficient, leading to idle channel time.
            *   **Sliding Window Protocol:** Allows the sender to transmit multiple frames (within a defined "window" size) without waiting for individual ACKs. A single ACK can acknowledge multiple frames, significantly improving channel utilization. Uses sequence numbers to track frames.

**II. Retransmission Strategies (Unit 2)**

*   **Automatic Repeat Request (ARQ):**
    *   A set of rules for retransmitting frames when errors (lost/damaged frames or ACKs) are detected.
    *   ACK (positive acknowledgment), NAK/REJ (negative acknowledgment).
*   **ARQ Protocols (building on Flow Control):**
    *   **Stop-and-Wait ARQ:**
        *   Sender sends a frame and waits for ACK. If ACK is lost/damaged or timeout occurs, the frame is retransmitted.
        *   Uses sequence numbers (0 or 1) to prevent duplicate processing if an ACK is lost and the sender retransmits.
        *   Still inefficient due to waiting.
    *   **Go-Back-N ARQ:**
        *   Sender can transmit multiple frames (up to a window size 'N') without waiting for ACKs.
        *   Receiver only accepts frames in sequential order; discards out-of-order or corrupted frames.
        *   If an error occurs or a timeout expires for a frame, the sender retransmits *that frame and all subsequent frames* in its window.
        *   More efficient than Stop-and-Wait, but can be inefficient if the error rate is high (many frames retransmitted).
    *   **Selective Repeat ARQ:**
        *   Most efficient ARQ strategy.
        *   Sender retransmits *only* the specific frame that was lost or corrupted.
        *   Receiver buffers out-of-order frames and delivers them to the Network layer once all preceding frames are received.
        *   Requires more complex buffering and logic at the receiver.
        *   Window sizes for sender and receiver are typically half of the sequence number range (2^k / 2) to prevent ambiguities.
*   **Pipelining:**
    *   Concept of starting a new task before the previous one is completed.
    *   Implemented in Go-Back-N and Selective Repeat ARQ (by sending multiple frames concurrently), improving bandwidth utilization.
*   **Piggybacking:**
    *   A technique where an acknowledgment (ACK) for a received frame is appended to an outgoing data frame from the receiver to the sender.
    *   Increases efficiency for bidirectional data flow by reducing the number of separate control frames.

**III. Contention-Based Media Access Protocols (Unit 3)**

*   **Media Access Control (MAC) for Broadcast Links:**
    *   Addresses the challenge of multiple nodes sharing a single transmission medium (e.g., in a LAN).
    *   **Channel Allocation Techniques:**
        *   **Static:** Fixed allocation (e.g., FDM, TDM); simple but inefficient for bursty traffic or many users.
        *   **Dynamic:** On-demand allocation for large numbers of users with bursty traffic.
*   **Random Access Protocols (for Dynamic Allocation):**
    *   **Pure ALOHA:**
        *   Stations transmit frames whenever they are ready.
        *   Collisions occur if frames overlap in time.
        *   Sender retransmits if no acknowledgment is received within a timeout.
        *   **Vulnerable period:** 2 * (frame transmission time).
        *   Maximum theoretical throughput: 18%. Highly inefficient.
    *   **Slotted ALOHA:**
        *   Time is divided into discrete slots; transmissions must begin at the start of a slot.
        *   Reduces the vulnerable period to 1 * (frame transmission time).
        *   Maximum theoretical throughput: 36%. More efficient than Pure ALOHA, but still prone to collisions.
    *   **Carrier Sense Multiple Access (CSMA):**
        *   "Listen before talk" protocols: Stations sense the channel before transmitting.
        *   **Variants:**
            *   **1-Persistent CSMA:** Transmits immediately if idle; continuously senses and transmits immediately when idle if busy (greedy, high collision risk).
            *   **Non-Persistent CSMA:** Transmits immediately if idle; if busy, waits a random time before re-sensing (reduces collisions, but can introduce longer delays).
            *   **p-Persistent CSMA:** For slotted channels; transmits with probability 'p' if idle, defers with (1-p).
    *   **CSMA with Collision Detection (CSMA/CD):**
        *   Stations sense the channel, and if idle, begin transmitting.
        *   Crucially, stations *continue sensing while transmitting*. If a collision is detected, transmission is immediately aborted.
        *   Saves time and optimizes bandwidth by stopping corrupted transmissions early.
        *   Requires a minimum frame length (e.g., 64 bytes for Ethernet) to ensure a collision can be detected before the entire frame is sent.
        *   **Backoff Algorithm (Binary Exponential Backoff):** After a collision, stations wait a random amount of time (doubling the range of random delay after each successive collision) before attempting retransmission.
*   **Ethernet Frame Format (IEEE 802.3):**
    *   A widely used MAC sublayer protocol for wired LANs, employing 1-persistent CSMA/CD.
    *   Defines various cabling types (e.g., 10Base5, 10BaseT) and their characteristics.
    *   **Frame Structure:** Includes Preamble (synchronization), Start Delimiter, Destination and Source Addresses (48-bit MAC addresses), Length of Data Field, Data, Pad (for minimum frame length), and Frame Check Sequence (CRC-32 for error detection).

**IV. Wireless LAN and Datalink Layer Switching (Unit 4)**

*   **Wireless LAN (WLAN) Introduction:**
    *   Addresses mobility, ad-hoc networking, and difficult-to-wire locations.
    *   Challenges: Not all stations are within range of each other, leading to unique problems.
*   **WLAN Architecture (IEEE 802.11):**
    *   **Basic Service Set (BSS):** A cell controlled by an Access Point (AP).
    *   **Distribution System (DS):** Connects multiple APs (e.g., an Ethernet backbone).
    *   **Ad hoc Networks:** Stations form networks directly without central control or APs.
*   **Unique Problems in WLANs:**
    *   **Hidden Station Problem:** A station cannot detect another transmitting station because it's out of range, leading to collisions at the common receiver.
    *   **Exposed Station Problem:** A station hears a transmission (from a distant sender) and falsely concludes the medium is busy, unnecessarily deferring its own transmission to another distant receiver.
    *   CSMA/CD is not suitable for WLANs due to these problems and the half-duplex nature of most radios.
*   **Wireless LAN Protocols:**
    *   **MACA (Multiple Access with Collision Avoidance):**
        *   Uses a **RTS (Request to Send) / CTS (Clear to Send)** handshake mechanism.
        *   RTS/CTS frames contain the expected duration of data transmission, causing other nodes to defer. Addresses some hidden/exposed station issues.
    *   **MACAW (MACA for Wireless):**
        *   Extends MACA with **RTS-CTS-DS (Data Sending)-Data-ACK** handshake.
        *   Adds **Data Link Layer Acknowledgments** to improve retransmission efficiency.
        *   Incorporates **Carrier Sensing** to reduce initial RTS collisions.
        *   Introduces an **improved backoff mechanism** (per-data-stream) for fairness.
        *   Uses the **DS message** to inform neighbors of successful RTS/CTS, ensuring deferral.
*   **IEEE 802.11 Protocol Stack:**
    *   **Physical Layer (PHY):** Supports Infrared, Frequency Hopped Spread Spectrum (FHSS), and Direct Sequence Spread Spectrum (DSSS) in the 2.4 GHz ISM band. Spread spectrum techniques improve resistance to noise and jamming.
    *   **MAC Sub-layer Protocol:**
        *   Does not use CSMA/CD.
        *   **Distributed Coordination Function (DCF):** Uses **CSMA/CA (CSMA with Collision Avoidance)**.
            *   Combines **physical channel sensing** with **virtual channel sensing** (using RTS/CTS and **NAV - Network Allocation Vector** to indicate busy periods).
            *   Employs **fragmentation** (splitting large frames into smaller pieces) to improve reliability on noisy channels, as only smaller fragments need retransmission.
        *   **Point Coordinated Function (PCF) (Optional):** Centralized control where the base station polls stations for data, eliminating collisions. Supports Quality of Service (QoS).
        *   Both DCF and PCF can coexist.
*   **Switching at Data Link Layer:**
    *   **Repeaters (Layer 1):** Regenerate and propagate signals, extending LAN segments. Connect networks with the *same* physical layer.
    *   **Bridges (Layer 2):** Connect multiple LANs, potentially with different physical and MAC layers (e.g., Ethernet to Token Ring).
        *   **Characteristics:** Store-and-forward devices (perform error detection via CRC); susceptible to broadcast storms.
        *   **Reasons for Use:** Connecting departmental LANs, spanning geographical distances, load distribution, overcoming distance limitations, improving reliability and security by segmenting networks.
        *   **Challenges in Bridging Different 802 LANs:** Different frame formats (requiring reformatting, checksum recalculation), different data rates (requiring buffering), different frame lengths (may require discarding larger frames), loss of security (encryption) and QoS features when crossing incompatible segments.
    *   **Types of Bridges:**
        *   **Transparent Bridges:** "Plug and play" devices that are invisible to network devices. They operate in promiscuous mode, learning source MAC addresses to build a "backward address table." They forward frames based on destination MAC address, flooding if the destination is unknown, and discard if source and destination are on the same segment.
        *   **Spanning Tree Bridges:** Used in networks with multiple bridges to prevent network loops (where frames circulate indefinitely). They communicate using the IEEE 802.1d Spanning Tree Algorithm to establish a loop-free logical topology (a "spanning tree").
        *   **Source Routing Bridges:** (Used in Token Ring networks). The sending machine is responsible for determining the frame's path across different networks and includes this routing information directly in the frame's header.
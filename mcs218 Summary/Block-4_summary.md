Summary of Block-4.pdf:

This academic text is divided into four units, covering Transport Services and Mechanisms, TCP/UDP protocols, and two units on Network Security.

### Unit 1: Transport Services & Mechanism

This unit introduces the transport layer as the core of the OSI model, responsible for end-to-end data delivery between application programs, shielding them from underlying network complexities.

*   **Core Function:** Provides end-to-end data transport, making the underlying physical network appear as a homogeneous, reliable entity to upper layers.
*   **Key Services Provided to Upper Layers:**
    *   **Types of Services:**
        *   **Connection-oriented:** Establishes, maintains, and terminates a logical connection (handshaking). Generally reliable, including flow control, error control, and sequence delivery (e.g., TCP).
        *   **Connectionless (Datagram):** No prior handshaking, faster, but unreliable (no flow/congestion control, no acknowledgments) (e.g., UDP).
    *   **Quality of Service (QoS):** Allows users to specify transmission quality (e.g., expedited delivery, acceptable error/loss levels, desired delay, throughput, priority levels). The transport layer optimizes resource use based on these specifications, limited by network layer capabilities.
    *   **Data Transfer:** Oversees the delivery of an entire sequence of packets for a message, unlike the network layer's hop-by-hop packet delivery. Provides full-duplex service.
    *   **Connection Management:** Responsible for establishing and terminating connections (abrupt or graceful).
    *   **Expedited Delivery:** Prioritizes certain data for rapid transmission, often interrupting the receiving application.
*   **Elements of Transport Layer Protocols (Mechanisms to support services):**
    *   **Addressing:** Uses "transport addresses" or "ports" (TSAPs) to identify specific application processes on hosts. Methods include initial connection protocols, well-known addresses, and name servers.
    *   **Multiplexing:**
        *   **Upward Multiplexing:** Multiple transport connections share a single network connection (e.g., for cost efficiency on virtual circuits).
        *   **Downward Multiplexing (Splitting):** A single transport connection is split across multiple lower-level connections to enhance bandwidth.
    *   **Flow Control & Buffering:** Regulates data flow to prevent the sender from overwhelming the receiver.
        *   Similarities with data link layer: Uses sliding window protocols.
        *   Differences: More complex at transport layer due to variable/long transmission delays and interaction of TS users, transport entities, and network service.
        *   Mechanisms: Fixed sliding-window protocol and credit schemes (decouples acknowledgment from flow control, giving receiver more control).
        *   Buffering: Dynamic allocation based on traffic type (sender-side for bursty, receiver-side for high-bandwidth).
    *   **Connection Establishment:** Uses a "3-way handshake" procedure (SYN, SYN-ACK, ACK) to ensure both ends exist, negotiate parameters (e.g., segment size, window size), allocate resources, and handle delayed/duplicate packets by synchronizing initial sequence numbers.
    *   **Crash Recovery:** Mechanisms to recover from host or virtual circuit crashes, often involving retransmission of unacknowledged data.

### Unit 2: TCP/UDP

This unit provides a detailed examination of the two primary Internet transport protocols: Transmission Control Protocol (TCP) and User Datagram Protocol (UDP).

*   **Internet Transport Service Models:**
    *   **TCP (Transmission Control Protocol):**
        *   **Connection-Oriented:** Establishes a full-duplex connection via a handshake procedure.
        *   **Reliable Transport Service:** Guarantees delivery of all data, without error, in the proper order, using acknowledgments and retransmissions.
        *   **Congestion-Control Mechanism:** Manages network load to prevent congestion.
        *   *Does NOT guarantee a minimum transmission rate or provide any delay guarantee.*
    *   **UDP (User Datagram Protocol):**
        *   **Connectionless:** No handshaking before data transfer.
        *   **Unreliable Data Transfer:** No guarantee that messages will reach the destination or in order.
        *   **No Congestion Control:** Sender can pump data at any rate.
        *   **Advantages:** No connection establishment delay, less connection state to maintain on servers, smaller packet header overhead (8 bytes vs. TCP's 20 bytes).
        *   **Use Cases:** Suited for applications that can tolerate some data loss but require speed (e.g., Internet telephony, video conferencing, DNS, network management, routing protocols). Reliability can be built at the application layer, but this increases complexity.
*   **TCP Segment Header:** A single, comprehensive header format (minimum 20 octets) used for all TCP mechanisms, including:
    *   Source and Destination Ports (16 bits each).
    *   Sequence Number (32 bits): For first data octet in segment.
    *   Acknowledgement Number (32 bits): Next byte expected.
    *   Data Offset (4 bits): Header length in 32-bit words.
    *   Flags (6 bits): URG (urgent data), ACK (ACK field valid), PSH (push data to application), RST (reset connection), SYN (synchronize sequence numbers), FIN (no more data from sender).
    *   Receive Window (16 bits): For credit-based flow control (bytes receiver is willing to accept).
    *   Checksum (16 bits): For reliability, covers header, data, and pseudo-header.
    *   Urgent Data Pointer (16 bits): Points to end of urgent data.
    *   Options (Variable): E.g., maximum segment size.
*   **TCP Connection Establishment:**
    *   Uses a "3-way handshake" (SYN, SYN-ACK, ACK) to ensure both transport entities exist, agree on initial sequence numbers (must be different), and negotiate optional parameters. This procedure is robust against delayed packets.
*   **TCP Connection Termination:**
    *   Provides a "graceful close" involving independent termination of each direction of the connection. Requires explicit FIN packets from each side to be acknowledged by the other.
*   **TCP Flow Control:**
    *   Regulates traffic to prevent receiver buffer overflow.
    *   Uses a "sliding window with credit scheme," decoupling acknowledgments from credit granting (unlike data link layer's fixed sliding window).
    *   **Nagle's Algorithm:** Improves efficiency for interactive applications by buffering small outgoing segments until an ACK for previously sent data arrives, or a full segment can be sent.
    *   **Silly Window Syndrome:** A problem where the receiver continuously advertises small window updates. Clark's solution prevents the receiver from advertising a window until it's sufficiently large (e.g., half buffer size or maximum segment size).
*   **TCP Congestion Control:**
    *   Uses an end-to-end mechanism (as IP doesn't provide congestion support).
    *   Limits data rate based on perceived network congestion using a "congestion window." The effective transmission window is `min(advertised window, congestion window)`.
    *   **Algorithm Phases:**
        *   **Slow Start:** Exponential growth of the congestion window (doubling per ACK) until a `congestion threshold` is reached.
        *   **Congestion Avoidance:** Linear growth of the congestion window (one segment per round-trip time) after the threshold is met.
        *   **Congestion Occurrence:** Triggered by a timeout (segment loss) or duplicate acknowledgments. The congestion threshold is halved, and the window is adjusted (reset to one for timeout, or decreased for duplicate ACKs).
*   **Remote Procedure Call (RPC) and Network File System (NFS):**
    *   RPC allows programs to call procedures located on remote machines, abstracting network communication details.
    *   NFS is a file access protocol that makes remote file systems appear local, relying on RPC services.

### Unit 3: Network Security-I

This unit delves into the fundamental principles and practices of cryptography, distinguishing between symmetric and asymmetric key systems and detailing prominent algorithms.

*   **Introduction to Cryptography:**
    *   **Definition:** The science of writing in secret code, protecting transmitted information from unauthorized access.
    *   **Purpose:** Secure communication in the presence of adversaries.
    *   **Modern Uses:** Access control, digital signatures, email security, password authentication, data integrity, copyright protection.
    *   **Classification Dimensions:** Type of operation (substitution, transposition), Key Used (symmetric/asymmetric).
    *   **Security Requirements for Application-to-Application Communication:** Authentication, Privacy/Confidentiality, Integrity, Non-repudiation.
    *   **Cryptographic Schemes:** Secret key (symmetric) cryptography, Public key (asymmetric) cryptography, and Hash functions.
*   **Symmetric Key Cryptography (Secret Key/Conventional Encryption):**
    *   Uses a single, shared secret key for both encryption and decryption.
    *   **Challenge:** Secure distribution of the key.
    *   **Types:**
        *   **Stream Ciphers:** Operate on single bytes/bits, with a constantly changing key (e.g., RC4, SEAL, A5/1).
        *   **Block Ciphers:** Encrypt fixed-size blocks of data (e.g., 64-bit or 128-bit).
            *   **DES (Data Encryption Standard):** Developed in 1970s, 56-bit key, 64-bit blocks, 16 rounds. Vulnerable to brute-force attacks due to short key length.
            *   **DES Variants:**
                *   **Double-DES:** Uses two keys, but vulnerable to "Meet-in-the-middle" attack.
                *   **Triple-DES (3DES):** Applies DES three times (Encrypt-Decrypt-Encrypt) with one, two, or three keys, offering effective key lengths up to 168 bits. More secure but slower than single DES.
                *   **DESX:** XORs plaintext/ciphertext with additional key bits to increase brute-force resistance.
            *   **AES (Advanced Encryption Standard):** Successor to DES, based on the Rijndael algorithm. Supports 128, 192, or 256-bit keys with a 128-bit block size. Designed for efficient hardware/software implementation. Involves transformations like SubBytes, ShiftRows, MixColumns, and AddRoundKey.
            *   **Other Symmetric Ciphers:** Blowfish, CAST-128, IDEA, Rabbit, RC4.
    *   **Modes of Operation for Block Ciphers:**
        *   **ECB (Electronic Code Book):** Encrypts each block independently; identical plaintext blocks yield identical ciphertext blocks.
        *   **CBC (Cipher Block Chaining):** XORs plaintext block with the previous ciphertext block before encryption, providing chaining.
        *   **CFB (Cipher Feedback):** Encrypts previous ciphertext block and XORs with plaintext. Self-synchronizing.
        *   **OFB (Output Feedback Block):** Generates a key-stream by iterative encryption, XORed with plaintext.
    *   **The One-Time Pad (OTP):** The only cipher proven unconditionally secure if the key is truly random, same length as message, and used only once. Practical challenge lies in key distribution.
*   **Public Key Cryptography (Asymmetric Key/Two-Key Encryption):**
    *   Uses two mathematically related keys: a public key (advertised) for encryption and a private key (kept secret) for decryption. Knowledge of one does not easily reveal the other.
    *   Based on "one-way functions" (easy to compute, hard to reverse, e.g., multiplication vs. factorization, exponentiation vs. logarithms).
    *   **Most Common Implementations:**
        *   **RSA (Rivest-Shamir-Adelman):** Most common, used for key exchange, digital signatures, and encryption. Security relies on the difficulty of factoring large integers.
        *   **Diffie-Hellman (D-H):** Used for secret-key key exchange only. Security based on the discrete logarithm problem.
        *   **Digital Signature Algorithm (DSA):** Specified in NIST's DSS, provides digital signature capability for message authentication.
        *   **Elliptic Curve Cryptography (ECC):** Based on the Elliptic Curve Discrete Logarithm Problem (ECDLP). Offers comparable security to RSA with significantly shorter key sizes, making it efficient for resource-constrained devices.
        *   **Public-Key Infrastructure (PKI):** A framework for managing public keys, including Certifying Authorities (CAs) that issue and manage digital certificates (e.g., India's CCA, RCAI).
*   **Mathematical Background:** Explains core mathematical operations used in cryptography:
    *   **Exclusive OR (XOR):** A Boolean operation where the output is TRUE (1) if exactly one input is TRUE (1), otherwise FALSE (0). Critical for encryption/decryption as `(P XOR K) XOR K = P`.
    *   **Modulo Function:** Returns the remainder of a division (X mod Y). Useful for limiting numbers within a specific range for computational purposes.

### Unit 4: Network Security-II

This unit focuses on practical aspects of network security, discussing cyber threats, various attack types, system vulnerabilities, counter-measures, and an introduction to computer forensics.

*   **Cyber Threats, Attacks, and Counter Measures:**
    *   **Cyber Threat:** The *possibility* of a malicious attempt to damage, disrupt, or gain unauthorized access to a computer network or system, or steal data. Sources include nation states, terrorists, industrial spies, organized crime, hacktivists, business competitors, and disgruntled insiders.
    *   **Cyber Attack:** An actual malicious event that has occurred, aiming to compromise data integrity, confidentiality, or availability.
    *   **Counter Measures:**
        *   Staff training against fraudulent emails and information sharing.
        *   Regularly updated systems and software (patch management).
        *   Endpoint protection for remote devices.
        *   Firewalls to prevent unauthorized access.
        *   Regular data backup.
        *   Access management for systems and networks (physical and logical).
        *   Enabling Wi-Fi security options.
        *   Securing employee personal information (unique credentials).
        *   Using strong, unique, and frequently changed passwords.
*   **Taxonomy of Cyber Attacks:** Attacks are classified by type, behavior, impact, possible attackers, motives, consequences, and defense mechanisms.
*   **Specific Cyber Attacks:**
    *   **Virus:** Self-replicating malicious programs that infect other programs, files, or systems, aiming to gain administrative rights or steal sensitive information. Categories include boot sector, browser hijacker, web scripting, resident, polymorphic, file infector, and macro viruses.
    *   **Worm:** A self-replicating type of malware that spreads through networks by exploiting OS vulnerabilities, often without human intervention. Aims to infect as many systems as possible. Categories include email, file sharing, crypto-worms, internet, and instant messaging worms.
    *   **Trojan (Trojan Horse):** Malware that disguises itself as legitimate software. Once installed, it can steal information, open backdoors, or download other malware. Sources include file sharing websites, email attachments, spoofed messages, unsecured websites, and hacked Wi-Fi networks.
    *   **Denial of Service (DoS) Attack:** A single system attacking another to reduce or restrict authorized user access.
        *   **Flooding Services:** Overwhelming the target with traffic (e.g., Buffer Overflow, ICMP Flood/Smurf Attack, SYN Flood).
        *   **Crashing Services:** Exploiting bugs to cause system/service crashes.
    *   **Distributed Denial of Service (DDoS) Attack:** Multiple compromised systems (a "botnet" of "zombies" controlled by a "command and control" server) simultaneously attack a single target.
    *   **Phishing Attack:** Uses social engineering to trick specific users via fraudulent communications (e.g., emails) to obtain sensitive information (financial, login details) or install malware.
    *   **Malware (Malicious Software):** A generic term for software designed to breach cybersecurity, gain unauthorized access, or steal personal information. Includes viruses, spyware, ransomware, trojan horses.
        *   **Exploit Kit:** Toolkits used by attackers to find and exploit system vulnerabilities.
        *   **Malicious Websites and Drive-by-Downloads:** Websites designed to host exploit kits and automatically inject malware.
        *   **Malvertising:** Malicious code embedded in online advertisements.
        *   **Man in the Middle (MitM) Attack:** An attacker intercepts communication between two parties, often on poorly secured networks.
        *   **Man in the Browser (MiTB) Attack:** Malware injected into a browser to collect information directly from the user's browser without intercepting network traffic.
    *   **Ransomware:** Encrypts data or blocks system access, demanding a ransom for release.
        *   **Locker Ransomware:** Blocks system functionalities.
        *   **Crypto Ransomware:** Encrypts files, making them inaccessible.
*   **Vulnerabilities:** Flaws or weaknesses within a system that can be exploited by attackers.
    *   **Network Vulnerabilities:** Flaws in network hardware (routers, switches) or software (firewalls).
    *   **Operating System (OS) Vulnerabilities:** Flaws in the OS itself (e.g., default admin accounts, RDC/RDG client/server vulnerabilities).
    *   **Human Vulnerabilities:** Lack of user awareness or poor security practices.
    *   **Process Vulnerabilities:** Flaws in specific system processes (e.g., login mechanisms).
    *   **Specific Examples:**
        *   **Buffer Overflow:** A process vulnerability where excess data overwrites defined memory space, potentially causing system crashes or allowing arbitrary code execution.
        *   **SQL Injection:** A web application vulnerability where malicious SQL code is injected into input fields to manipulate backend databases.
        *   **Browser Vulnerabilities:** Exploiting browser features (cookies, plugins) or malicious websites to compromise user systems.
*   **Basic Computer Forensics:**
    *   **Definition:** The preservation, identification, extraction, documentation, and interpretation of digital data from digital artifacts (e.g., computers, mobile phones) for legal investigations.
    *   **Phases:** Acquisition, Examination, Analysis, Report Preparation.
    *   **Techniques:** Cross-Drive Analysis, Live Analysis, Analysis by Recovery (file carving for deleted files), Stochastic Forensics, Stenography Analysis (detecting hidden data in images).
*   **Recent Cyber Attacks:** Examples include data breaches at Facebook (2019), Canva (2019), MGM Hotel (2020), a ransomware attack on California University (2020), email hacks at WHO (2020), and Zoom bombing (2020).
*   **Firewalls and Intrusion Detection Systems (IDS):**
    *   **Firewall:** A software or hardware device that filters network traffic, blocking unauthorized access between a local network and the internet. Acts as a "watchman" at the network's entry point.
    *   **Intrusion Detection System (IDS):** A software or hardware installed on a network (NIDS) or host (HIDS) to detect and report intrusion attempts *within* the network. Acts as "security cameras" inside, alerting to suspicious activity but not blocking it.

**Conclusion:**
The provided units offer a comprehensive overview of how data is transmitted reliably and efficiently across networks (Transport Layer, TCP/UDP) and the critical security measures required to protect this data and the systems involved (Network Security I & II). They move from foundational network protocols to advanced cryptographic techniques and practical cyber defense strategies, emphasizing the constant evolution of threats and the need for continuous vigilance and education in cybersecurity.
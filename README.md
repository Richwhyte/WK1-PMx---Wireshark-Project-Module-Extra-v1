# 🕵️‍♂️ Networkwalks SOC Analyst Internship: Wireshark Project Module

Building a network analysis framework to investigate attackers, recover hidden data, and secure unencrypted communication channels.

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/NetworkWalks-404040?style=flat-square&labelColor=C00000" />
   <img src="https://img.shields.io/badge/OKON%20Inemesit%20Udo-C00000?style=flat-square" />
</p>

---

## 📝 Project Overview

This project focuses on executing advanced packet forensics and traffic analysis inside a simulated Security Operations Center (SOC) environment. 

The purpose of this module is to investigate live network captures, reconstruct multi-layered communications, isolate malicious footprints, and extract operational intelligence from unencrypted data packages. The entire series was completed with an **Outstanding 100/100 marks** evaluation.

<p align="center">
  <img src="Lab 8 Result - Okon Inemesit Udo.png" alt="Lab 8 Completion Certificate 100% Score" width="60%">
</p>

---

## 🔬 Investigated SOC Labs

The training module consists of six distinct, objective-driven live laboratory environments:

* **Identify the Attacker’s IP (Lab 3):** Isolating malicious external source addresses attempting network penetration.
* **Follow TCP Stream 1 (Lab 4):** Rebuilding data conversations to read cleartext packet exchanges.
* **Follow TCP Stream, Part 2 (Lab 5):** Performing stream reassembly on complex captures to uncover hidden payloads.
* **HTTP Plain Text Credentials (Lab 6):** Detecting application-layer vulnerabilities revealing unencrypted usernames and passwords.
* **Catch the Brute Force Attacker (Lab 7):** Tracking systematic high-frequency authentication loops and identifying the origin IP.
* **Catch the Call Scammer (Lab 8):** Parsing VoIP signaling, decoding telephony codecs, and replaying unauthorized voice captures.

---

## 🔍 Case Study: Lab 8 – VoIP Call Replay

### 1. Signaling Interception (SIP)
Using the explicit network display filter `sip`, the transport layer data was isolated to review session initiation workflows. As demonstrated in the telemetry, **Packet 51** executes a direct `SIP INVITE` handshake from host `192.168.10.45` to `192.168.10.52`. 

Inspecting the packet details inside the message header revealed the explicit identification tags of the target entities:
* **Caller Identity:** Ali Raza (`sip:101@192.168.10.45`)
* **Recipient Target:** Sara (`sip:202@192.168.10.52`)

<p align="center">
  <img src="images/sip_analysis.png" alt="Wireshark SIP Display Filter and Message Header Analysis" width="90%">
</p>

### 2. Stream Audio Reconstruction (RTP)
To audit the voice data transmitted after session confirmation, the Real-time Transport Protocol (RTP) packet framework was reviewed via the integrated **Wireshark RTP Player** console. 

The call utilizes the standard `G.711 PCMU` audio codec distributed over two concurrent directional paths:
* **Forward Stream:** `192.168.10.45:16384` ➔ `192.168.10.52:18000`
* **Reverse Stream:** `192.168.10.52:18000` ➔ `192.168.10.45:16384`

<p align="center">
  <img src="images/rtp_player.png" alt="Wireshark RTP Player Audio Stream Playback" width="90%">
</p>

### 3. Exfiltrated Evidence Extraction
Synchronous audio playback of both discrete streams enabled real-time vocal analysis of the underlying invoice transaction. Auditing the verbal exchange successfully confirmed the last four digits of the fraudulent credit card profile used: **`2394`**.

---

## 🛠️ Technical Competencies Developed

* **Advanced Display Filtering:** Architecting targeted filters (`sip`, `rtp`, `http.request.method=="POST"`) to isolate critical traffic subsets instantly.
* **Stream Carving & Reassembly:** Extracting plain text strings and multi-part data pieces from underlying TCP streams.
* **Incident Behavioral Diagnostics:** Evaluating volumetric handshake patterns to distinguish standard connection anomalies from active brute-force scripts.
* **Telephony Packet Forensics:** Navigating the relationship between SIP setup sequences and raw RTP data packets to analyze voice traffic.

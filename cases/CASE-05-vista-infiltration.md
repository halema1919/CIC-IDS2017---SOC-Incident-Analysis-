 Splunk: Infiltration flow identification
This search isolates flows carrying the ground-truth Infiltration label from the Thursday-afternoon flow dataset. Splunk identified 108 malicious flows, all sharing the same source-destination pair: victim host 192.168.10.8 (the Windows Vista machine) communicating with external host 205.174.165.73 on destination port 444. Unlike the Thursday-morning web attacks, which spanned three distinct labels (brute force, XSS, SQL injection), the afternoon dataset contains a single attack category, consistent with the incident being one continuous C2 session rather than several attack types. The narrow five-tuple (one source, one destination, one port) and the multiplicity of source ports (53966, 54119, 54131, 54573, etc.) indicate the same channel being repeatedly re-established over roughly 90 minutes rather than 108 independent attacks. These are flow-level records, so Wireshark was used afterward to confirm what this channel actually carried at the packet level.
<img width="1904" height="744" alt="Screenshot 2026-08-04 at 7 57 06 PM" src="https://github.com/user-attachments/assets/e2ee0d29-9abd-4c7c-ac6b-60d1c2a8edf2" />

 Wireshark: C2 channel packet capture
This filter (ip.addr == 192.168.10.8 && ip.addr == 205.174.165.73 && tcp.port == 444) isolates the packet-level traffic corresponding to the flows identified in Evidence 1. The capture shows repeated, complete TCP handshakes (SYN → SYN/ACK → ACK) between the two hosts, each followed by a short exchange of PSH/ACK data packets before an orderly FIN/ACK or RST teardown. This handshake-data-teardown pattern repeating across multiple source ports confirms the flow labels are not artifacts of misclassification — each session is a genuine, independently negotiated TCP connection to the same destination and port, consistent with a backdoor or listener periodically checking in rather than a single long-lived session. This established that port 444 traffic was a live, functioning channel, which raised the question of what was actually being transmitted inside it.




<img width="1512" height="946" alt="Screenshot 2026-08-04 at 8 15 45 PM" src="https://github.com/user-attachments/assets/9ba8fa9c-af6e-42d4-be38-374fa1420c1d" />


Wireshark: Follow TCP Stream (command shell)
Following the TCP stream on one of the port-444 sessions reveals the payload behind the channel identified in Evidence 2. After an initial block of encoded/encrypted handshake bytes, the stream resolves into plaintext: a Windows command interpreter banner (Microsoft Windows [Version 6.0.6002]) followed by an active shell prompt (C:\Users\cic2\Downloads>). Version 6.0.6002 corresponds to Windows Vista SP2, matching the victim host identified in the flow and packet evidence. This is the point in the investigation where the incident moves from suspected to confirmed compromise: the attacker at 205.174.165.73 held interactive command-line access to 192.168.10.8, not merely a probing connection. This finding directly supports the "Confirmed compromise" impact rating on the summary slide and establishes the pivot point from which subsequent internal activity originated.

<img width="1512" height="946" alt="Screenshot 2026-08-04 at 8 13 50 PM" src="https://github.com/user-attachments/assets/cf0cdf6a-55df-466f-be6d-75e5387cc011" />

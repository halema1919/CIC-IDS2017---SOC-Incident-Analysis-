For that same Friday afternoon, we can see that over 128k flows of traffic were part of a DDoS attack (using LOIC). 
<img width="2916" height="726" alt="Screenshot 2026-08-04 at 10 49 35 AM" src="https://github.com/user-attachments/assets/123b4179-9b7a-48f2-a285-cf21b5f44945" />

Here we can see that once the attacker is within the network, they continue to use 172.16.0.1 as their IP due to the firewall. This IP spikes multiple times in the line chart below. These packets spike to the thousands, representing the amount HTTP requests made and the flooding on ports 80 and 8080. They use the other victim machines to continue the attack as well.
<img width="2376" height="656" alt="Screenshot 2026-08-04 at 2 08 43 PM" src="https://github.com/user-attachments/assets/006f3107-b074-4d47-bafd-a064d08eed15" />

With Wireshark, we can follow the HTTP streams on GET packets and analyze their statistics on an I/O Graph. The earlier red spikes on the graph actually indicate the earlier botnet and port scan attacks but later the large red spikes reach up to 8k-10k packets/second. This marks where the DDoS attacked sent an overwhelming amount of traffic that triggered mass server dropouts, TCP retransmissions, and hindering the networks functionality. 
<img width="2390" height="1262" alt="Screenshot 2026-08-04 at 2 09 50 PM" src="https://github.com/user-attachments/assets/418e3f1a-fca9-463c-a8be-cb44643dd482" />

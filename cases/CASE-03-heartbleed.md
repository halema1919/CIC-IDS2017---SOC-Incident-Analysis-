This search provides an overview of all traffic in the Wednesday dataset by counting the number of flows for each attack label. It shows that DoS Hulk is the most common attack with 231,073 flows, while Heartbleed appears only 11 times. This screenshot establishes the scope of the investigation by confirming that both DoS attacks and the Heartbleed exploit are present. It also demonstrates that DoS attacks generate a much larger volume of traffic, whereas Heartbleed consists of only a few targeted connections.
<img width="1710" height="663" alt="Screenshot 2026-08-01 at 12 02 51 AM" src="https://github.com/user-attachments/assets/92646b16-86e0-4576-a1f6-ee71beb52a34" />

This search compares the average duration of network flows for each attack type. Heartbleed has the longest average flow duration (about 110 million), which is significantly higher than the DoS attacks. This indicates that Heartbleed maintains longer-lived connections while exploiting the vulnerable server, making its network behavior very different from traffic flooding attacks.
<img width="1710" height="551" alt="Screenshot 2026-08-01 at 12 13 25 AM" src="https://github.com/user-attachments/assets/a08b7f31-461e-4cf5-a64e-4e57bd434511" />

This search compares the average number of packets sent from the client to the server (forward) and from the server back to the client (backward). Most DoS attacks average only 5–6 forward packets per flow, while Heartbleed averages over 2,500 forward packets and nearly 1,900 backward packets. This unusually large exchange of packets reflects the exploit's extended communication with the server rather than simple flooding behavior.
<img width="1710" height="559" alt="Screenshot 2026-08-01 at 12 14 11 AM" src="https://github.com/user-attachments/assets/1199180d-f472-473d-b15b-be20fce04573" />

This search identifies the largest packet observed for each attack type. Heartbleed reaches a maximum packet length of 17,376 bytes, considerably larger than the DoS attacks. Larger packets are consistent with the behavior of the Heartbleed vulnerability, where the attacker can receive unexpectedly large amounts of server memory in response to crafted requests. This distinguishes Heartbleed from the smaller, repetitive packets used in DoS attacks.
<img width="1709" height="491" alt="Screenshot 2026-08-01 at 12 14 43 AM" src="https://github.com/user-attachments/assets/709d8ffd-04c8-41aa-a831-66a4e0dcd9fe" />



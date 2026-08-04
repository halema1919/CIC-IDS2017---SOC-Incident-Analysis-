On Friday morning, a Botnet attack occurred. Using the csv file for the morning working hours, it displayed the most common attack as Bot. In this investigation we were able to see what the Botnet did and what other IPs were involved and made victims. Below shows 1966 traffic flows for this part of the attack.
<img width="2926" height="690" alt="Screenshot 2026-08-04 at 10 48 38 AM" src="https://github.com/user-attachments/assets/072feaa4-5272-47c7-8118-8f9ecfe42921" />

This snapshot shows the IPs that were used in the internal attack along with the attackers IP (205.174.165.73). These machines were used as bots to infiltrate the network. Each compromised IP shows when their first and last contact with the attacker was made. Victim devices sent frequent status updates to the attacker over port 8080 within 1 or 2 hours in the morning.
<img width="2394" height="512" alt="Screenshot 2026-08-04 at 1 56 38 PM" src="https://github.com/user-attachments/assets/7dd340dc-f4fe-4130-8816-622a3ff3b02a" />

On wireshark, whilst filtering the attacker’s IP and the specific port used during the attack, we can take a closer look and follow the TCP stream between one of the internal IPs and the attacker. This stream displayed information such as the method of attack (python malware scripts), its host server name (Ares), and the unique identifier the attacker used to contact the infected IP.
<img width="1426" height="474" alt="Screenshot 2026-08-04 at 1 58 24 PM" src="https://github.com/user-attachments/assets/e203e7ae-bf1c-4b16-a55d-fb8530904145" />

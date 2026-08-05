On Friday afternoon, one of the two attacks were PortScan attacks. Below splunk displays 158,930 flows of traffic for this one attack.
<img width="2922" height="806" alt="Screenshot 2026-08-04 at 10 49 05 AM" src="https://github.com/user-attachments/assets/9722c9e5-e893-4d4c-98f5-1db97f210ec5" />

Here we can see 172.16.0.1 (attacker hiding behind a firewall) targeting 192.168.10.50. 1000 unique ports were probed over 158k flows of traffic on that one victim server. This indicates a NMAP Port Sweep. This attack checked ports across multiple computers on the network and flooded the system with traffic amongst different victims as well. 
<img width="2380" height="612" alt="Screenshot 2026-08-04 at 2 02 08 PM" src="https://github.com/user-attachments/assets/b111277e-293c-48b6-834c-68d238924cc6" />

Wireshark paints the same picture. Now that we can track two IPs for the same attack, we can filter both of them and view the packet behavior amongst those connections. This snapshot shows the beginning of the port scan attack. TCP resets display across multiple ports within fractions of seconds. The red section shows SYN scans hitting closed ports or receiving RSP(reset) responses.
<img width="1582" height="1018" alt="Screenshot 2026-08-04 at 2 03 23 PM" src="https://github.com/user-attachments/assets/310a2d5c-1a73-4567-bd02-d02f0799d26d" />

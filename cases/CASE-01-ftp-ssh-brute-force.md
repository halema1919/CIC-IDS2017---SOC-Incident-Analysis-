This search pulls the traffic going to the web server at 192.168.10.50 to show which machines were connecting to it and what services they were using. The two top sources showed unusual activity. The first source had 7,937 connections to port 21 (FTP) and the second had 5,897 to port 22 (SSH). Normal machines on the network had much less connections to those same ports all day, showing that it wasn't regular use. Both of those ports are login services, where they'd ask for a username and password. One source making thousands of connections to two login services on one machine is the pattern of a brute force attack.
<img width="2430" height="1290" alt="image" src="https://github.com/user-attachments/assets/9edee744-affe-4852-bd01-44f4e049bb4f" />


All 13,835 attack connections came from this IP: 172.16.0.1. That's the firewall's inside interface, not the attacker's real address. The traffic was captured inside the network, so by the time it reached the sensor the firewall had already replaced the original source. The dataset documentation lists the real attacker as 205.174.165.73, but that address never appears in the data. 
<img width="2428" height="484" alt="image" src="https://github.com/user-attachments/assets/025f522a-353b-4c6d-8790-50832222d2ff" />


This search checks whether anything else on the network was attacked. Every one of the 13,835 malicious connections went to the same server. No other machines were attacked so the incident was contained to a single  machine.
<img width="2398" height="410" alt="image" src="https://github.com/user-attachments/assets/1b758e1c-e33e-486c-8816-39aa5fe43be0" />


This search shows both attacks on a timeline. The chart shows two separate spikes with nothing in between, which shows the attacker ran the attack, stopped, and came back later. The FTP attack (purple) ran in one continuous block, about an hour long from 9:20-10:20 am, at about 150 connections per minute. The SSH attack (pink) had the same pattern, also about an hour from 2:00-3:00 pm, also at a steady rate. A person wouldn't keep up that pace of attempting to login for an hour, so this shows that it was automated. Note: The SSH attack displays as 2:00 AM here due to an AM/PM parsing error. 
<img width="2408" height="732" alt="image" src="https://github.com/user-attachments/assets/20a071c0-50c3-4035-a7e2-ae19d9a4d8c7" />


FTP sends passwords as readable text, so the captured traffic would have the passwords that were tried and how the server answered each one. Filtering the capture for FTP traffic between the attacker and the server shows the same loop of unsuccessful login attempts. However, one response returned "230 Login successful" (packet no. 461741, highlighted in blue)
<img width="2222" height="1506" alt="image" src="https://github.com/user-attachments/assets/1fa6d25d-e5b7-4206-8ced-750de9c7174d" />


Following the TCP stream for the successful login, we see that the attacker logged in with the username iscxtap and the password 1234, and the server accepted it. The attacker then ran command SYST which asks the server what operating system it's running, and the session timed out after that. The brute force worked, but this session shows no files being accessed or downloaded.
<img width="734" height="660" alt="image" src="https://github.com/user-attachments/assets/8e83dc3c-145d-44c6-97e6-e459867976bc" />


Filtering the capture for SSH traffic between the attacker and the server shows many connections being opened at the same time and getting abandoned immediately. The client identifies itself as paramiko, which is a Python library used to automate SSH connections, which confirms the attempts were automated.
<img width="2854" height="1274" alt="image" src="https://github.com/user-attachments/assets/3446f989-dda4-42b7-9e6c-9f796ae18298" />


SSH is encrypted, so the packet capture can't show whether a login worked, and confirming it would require the server's login records, which the dataset doesn't include. Sorting the connections by how long each one lasted shows two that stand out. Most attempts lasted about 18 seconds, sent around 32 packets, and got 40 to 43 packets back. These two lasted about two minutes but sent only 14 to 16 packets and got just 16 back. The connections stayed open longer while both sides sent less. A successful login would normally show the server sending more data back, so these are more consistent with connections that stalled or timed out. Nothing in the network data suggests the SSH attack succeeded, though it can't be completely ruled out because of encryption
<img width="2420" height="1252" alt="image" src="https://github.com/user-attachments/assets/dd7b3360-f07e-49a4-81a9-64f98989438e" />



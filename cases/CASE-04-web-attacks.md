This search counts the Thursday-morning malicious flow records by published attack label. Splunk identified 2,180 malicious flows: 1,507 labelled brute force, 652 XSS, and 21 SQL injection. This establishes that the investigation contains three separate web-attack categories. These values are flow counts rather than individual HTTP requests, so Wireshark was used afterward to verify the actual application activity.

<img width="3205" height="217" alt="Destination Port" src="https://github.com/user-attachments/assets/4e0848c7-3d36-4cd9-b3b2-822a40504da3" />

This search compares the flow behavior of the three web-attack categories. Brute force produced the most labelled flows at 1,507 and had the highest average number of forward and backward packets, supporting the pattern of repeated communication with the login service. XSS produced 652 flows and had a similar average duration but lower packet and byte rates. SQL injection appeared in only 21 flows and had the shortest average duration and fewest packets per flow, but it had the highest average bytes-per-second and packets-per-second rates. This suggests that the SQL-injection traffic was smaller in volume but shorter and more concentrated. 

<img width="1655" height="336" alt="Evidence 3" src="https://github.com/user-attachments/assets/a92a434e-4a1a-40e5-a3d9-80df485ac933" />

# CIC-IDS2017 — SOC Incident Analysis

A SOC analysis and incident-response writeup of the **CIC-IDS2017** intrusion-detection dataset (Canadian Institute for Cybersecurity). This repo doubles as our case-management system: each incident is tracked as a case file with triage, impact, ATT&CK mapping, and IOCs.

> **Note:** CIC-IDS2017 is a synthetic lab dataset. All attacks were run by the dataset authors from a Kali host against their own testbed, so there is **no real threat actor** to attribute and IOCs are lab artifacts, not live intelligence.

## Case Log

| Case | Incident | Day | Tactic | ATT&CK | Severity | Status |
|------|----------|-----|--------|--------|----------|--------|
| [CASE-01](cases/CASE-01-ftp-ssh-brute-force.md) | FTP/SSH Brute Force (Patator) | Tue | Credential Access | T1110 | Medium | Triage |
| [CASE-02](cases/CASE-02-dos-floods.md) | DoS Floods (Slowloris/Hulk/etc.) | Wed | Impact | T1498/T1499 | Availability | Impact |
| [CASE-03](cases/CASE-03-heartbleed.md) | Heartbleed | Wed | Credential Access | T1212 | High | Impact |
| [CASE-04](cases/CASE-04-web-attacks.md) | Web Attacks (BF/XSS/SQLi) | Thu | Initial Access | T1190/T1189/T1110 | High | Impact |
| [CASE-05](cases/CASE-05-vista-infiltration.md) | Infiltration — Vista Compromise | Thu | Execution | T1203/T1204 | Critical | Confirmed |
| [CASE-06](cases/CASE-06-internal-portscan.md) | Internal Port Scan from Vista | Thu | Discovery | T1046 | High | Confirmed |
| [CASE-07](cases/CASE-07-botnet-ares.md) | Botnet ARES | Fri | Command & Control | T1071 | High | Triage |
| [CASE-08](cases/CASE-08-port-scan.md) | Port Scan | Fri | Discovery | T1046/T1595 | Medium | Triage |
| [CASE-09](cases/CASE-09-ddos-loit.md) | DDoS LOIT | Fri | Impact | T1498 | Availability | Impact |

## Incident Summary

**Arc:** clean baseline (Mon) → steal credentials (Tue) → deny service (Wed) → exploit the app & infiltrate (Thu) → command bots, scan, and flood (Fri).

**Scope:** started as external attacks against two servers (192.168.10.50, .51), then spread inside the network once Windows Vista (192.168.10.8) was compromised and began scanning internal clients. Confirmed impact: 2 servers + at least 6 internal machines.

**Key finding:** the Vista pivot — one machine changing from victim to attacker — is the point the incident crossed from perimeter attacks into internal compromise. It is also the **only confirmed break-in** (proven by the host's behavior change).

## Repo Structure

```
cicids2017-soc/
├── README.md          <- this dashboard / case log
├── cases/             <- one markdown ticket per incident
└── evidence/          <- screenshots (Wireshark, packet captures, charts)
```

## Environment / Assets

| Role | Host |
|------|------|
| Attacker (Kali) | 205.174.165.73 |
| DDoS sources (Win 8.1 x3) | 205.174.165.69–71 |
| Firewall (NAT) | 205.174.165.80 → 172.16.0.1 |
| Web/FTP Server (Ubuntu) | 192.168.10.50 |
| Ubuntu 12 Server | 192.168.10.51 |
| Windows Vista (compromised) | 192.168.10.8 |
| DNS + Domain Controller | 192.168.10.3 |

## Team

- Analyst: Team Members
- Dataset: [CIC-IDS2017](https://www.unb.ca/cic/datasets/ids-2017.html)

## References

- Sharafaldin, Lashkari, Ghorbani (2018), *Toward Generating a New Intrusion Detection Dataset and Intrusion Traffic Characterization*, ICISSP.
- [MITRE ATT&CK](https://attack.mitre.org/)
- [DistriNet CIC-IDS2017 labeling audit](https://intrusion-detection.distrinet-research.be/CNS2022/CICIDS2017.html)

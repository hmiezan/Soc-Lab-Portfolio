# Lab 01 - Windows Password Spray Investigation

Simulate a password spray attack from a Kali Linux attacker against a Windows 11 endpoint monitored by Elastic Agent and Security Onion.

### Lab Environment
- Kali Linux 10.161.170.22
- Windows 11 10.161.200.x 
- Security Onion SIEM
- Elastic Agent Installed

### Attack Simulation
Using Kali Linux, multiple authentication attempts were performed against Windows accounts to generate failed and successful authentication logs.

Command Attack ran : crackmapexec smb 10.161.200.x -u user.txt -p passwords.txt

Observed accounts
victim.user,
finance.jane

<img width="656" height="265" alt="Spraying" src="https://github.com/user-attachments/assets/a1e87a49-cccc-455a-9edf-01111fd2ee5b" />


### Detection
Failed Logons

<img width="1609" height="676" alt="Detection from kali" src="https://github.com/user-attachments/assets/63a825f2-b3f7-41fd-aee8-ecdcf9b2fe4e" />
<img width="1676" height="521" alt="Failed Login" src="https://github.com/user-attachments/assets/c028aa94-b6d1-4b81-9600-8bb74582403f" />



### Successful Authentication
<img width="1649" height="676" alt="Succeed" src="https://github.com/user-attachments/assets/a3e7c133-5033-42de-8f6b-158e919a64d9" />
<img width="1601" height="468" alt="Succeed 2" src="https://github.com/user-attachments/assets/7a65fb82-d8a8-4a3d-b903-e9fabd5a403d" />


### Investigation findings

Source IP : 10.161.170.22
Target Accounts victim.user and finance.jane

Observations

- Multiple authentication failures detected
- Successful authentication observed
- Evidence consistent with Password Spraying
- No persistence detected

#### MITRE ATT&CK Mapping
- IDPassword Spraying :	T1110.003 
- Valid Accounts: T1078

#### Timeline
- Nov 4, 2026 @ 12:17:23.189	Authentication Failures Begin
- Nov 4, 2026 @ 12:26:26.574	Additional Failed Authentication Attempts
- Nov 4, 2026 @ 12:26:26.923	Successful Authentication Detected
- 12:28	SOC Investigation Started

#### Impact Assessment

Successful authentication was observed after multiple failed attempts. Potential account compromise could not be ruled out.

#### Recommendations
- Enable MFA
- Review account lockout policies
- Monitor authentication activity
- Investigate post-login actions
- Restrict SMB access where possible

#### Lessons Learned

This lab demonstrated how Security Onion and Elastic can be used to identify credential attacks against Windows endpoints and how Event IDs 4625 and 4624 can be correlated to identify potential account compromise.

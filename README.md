## Objective
To develop hands-on expertise in Windows penetration testing, focusing on key attack vectors such as LLMNR poisoning, SMB relay attacks, IPv6 exploitation, Pass The Password/Hash, and Kerberoasting. The goal is to understand and apply practical techniques for identifying and exploiting security vulnerabilities in Windows environments, ultimately enhancing the ability to secure and defend corporate networks.

### Skills Learned
- LLMNR Poisoning
  - Understanding of network name resolution protocols (LLMNR and NetBIOS).
  - Ability to perform poisoning attacks to intercept and redirect traffic for credential capture.
  - Recognizing misconfigurations in network settings that enable this vulnerability.
- SMB Relay Attacks
  - Expertise in exploiting SMB protocols to relay authentication requests.
  - Ability to conduct man-in-the-middle attacks to access systems.
  - Practical application of techniques to escalate privileges in Windows environments.
- IPv6 Attacks
  - Understanding IPv6-specific attack vectors and potential security risks in hybrid IPv4/IPv6 networks.  
  - Hands-on experience with exploiting IPv6-related vulnerabilities in Windows environments.
- Pass The Password/Hash Attacks
  - Knowledge of attacking Windows authentication protocols by using cached credentials or hash values.
  - Practical knowledge of lateral movement techniques, such as using Pass The Hash to escalate privileges.  
- Kerberoasting
  - Proficiency in exploiting service account misconfigurations in Active Directory.
  - Ability to request service tickets and perform offline cracking to recover service account passwords.
  - Knowledge of how to leverage Kerberos authentication weaknesses for privilege escalation.

### Tools Used
- Kali Linux: Penetration testing tool to perform attacks on a vulnerable machine.
- Windows Server 2022 Eval: Act as an Active Directory service.
- Windows 10 Eval: End-user workstation.
- VMWare Workstation: Isolated environment for testing and simulation.

## Practical Exercises

- LLMNR Poisoning
<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/01_First, run the Responder.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>First, run the Responder to capture network traffic, wait for responses, and capture hashes.</b>
<br/>

<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/02_To generate traffic, configure one of the Windows.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>To generate traffic, configure one of the Windows machines to point to the attacker's machine.</b>
<br/>

<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/03_On the attacker's machine.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>On the attacker's machine, it retrieves the IP address of the target, along with the user, domain, and hash.</b>
<br/>

<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/04_Copy and save the hash.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>Copy and save the hash to crack later.</b>
<br/>

<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/05_Retrieve_1_edited.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/05_Retrieve_2_edited.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>Crack the hash by using a tool called Hashcat. The speed at which Hashcat can crack the password depends on the length and complexity of the password.</b>
<br/>

- SMB Relay Attacks
<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/01_SMB_Relay_Run responder.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>Run the Responder to capture network traffic, wait for responses, and capture hashes.</b>
<br/>

<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/02_SMB_Relay_Run ntlmrelay.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>Run the ntlmrelay, wait for responses, and capture hashes.</b>
<br/>

<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/03_SMB_Relay_Let's trigger the connection.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>Let's trigger the connection. On one of the machines, let's point it to the attacher's machine just to generate traffic.</b>
<br/>

<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/04_SMB_Relay_On the attacker's machine.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>On the attacker's machine, it receives a connection from 192.168.10.7, then proceeds to attack the target at 192.168.10.8. It successfully authenticates using the TFC020308 account, which is a local administrator on 192.168.10.8. Since it's an administrator on that machine, it is able to dump the SAM hashes. Now, we have the hashes.</b>
<br/>

<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/05_SMB_Relay_Copy and save the hash.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>Copy and save the hash to crack later.</b>
<br/>

- IPv6 Attacks
<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/01_IPv6_run the tool.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>To begin, run the tool, let it spin up, and start receiving replies from devices on the network.</b>
<br/>

<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/02_IPv6_run the tool.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b> At this point, we configure a relay attack and allow it to run in the background.</b>
<br/>

<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/03_IPv6_To speed up the process.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>To speed up the process, reboot one of the Windows machines. This will allow the attacker to observe the action: the machine will send out an IPv6 request. It will then attempt to authenticate as the IT-011A$ machine. You will see it enumerate the relayed user's privileges and dump the domain information into the lootdir.</b>
<br/>

<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/04_IPv6_Since the domain information_1.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/04_IPv6_Since the domain information_2.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>Since the domain information is dumped into the lootdir, examine its contents, as it provides important details about the domain. Open the domain_users_by_group.html file in a web browser to review key information.</b>
<br/>

<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/05_IPv6_If a Domain Administrator logs_1.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/05_IPv6_If a Domain Administrator logs_2.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>If a Domain Administrator logs in to one of the Windows machines, the attack succeeds. It targets LDAP, and then attempts to create a new user. When we check the Domain Controller in Active Directory Users and Computers, we can confirm that the new user was successfully created.</b>
<br/>
  
- Pass the Password and Hash Attacks
<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/01_Pass the pass_run the tool_1.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/01_Pass the pass_run the tool_2.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>To begin, run the tool and issue the command using the domain account we cracked earlier. The tool will then attempt to attack local machines on the network. We observed that it connected and attempted to use the username and password on workstations IT-011A and IT-012A. Let's try connecting to IT-012A — it successfully obtained a shell.</b>
<br/>

<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/02_Pass the hash_Next, let's attempt to dump hashes_1.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/02_Pass the hash_Next, let's attempt to dump hashes_2.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>Next, let's attempt to dump hashes on workstations IT-011A and IT-012A, then run the tool.</b>
<br/>

<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/03_Pass the hash_Copy the hashes.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>Copy the hashes and perform a quick check for password reuse.</b>
<br/>

<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/04_Pass the hash_Run the tool.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>Run the tool and issue the command. A green plus sign indicates that it worked and attempted to pass the hash to other machines on the network.</b>
<br/>

- Kerberoasting
<p align="center">
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/01_Kerberoasting_1.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<img src="https://github.com/edgonzalesjr/Windows-Penetration-Testing/blob/main/images/01_Kerberoasting_2.png" height="90%" width="90%" alt="Device Specification"/>
<br/>
<b>Run the tool and issue the command. Provide the domain name, the domain user account, and specify the domain controller's IP address along with the request. It will obtain the Ticket Granting Service (TGS) ticket, which contains the hash that is encrypted. Copy and save the hash to crack it later.</b>
<br/>

## Outcome
- Gained practical experience in identifying and exploiting vulnerabilities within Windows-based environments.
- Developed the ability to execute LLMNR poisoning to intercept network traffic and capture credentials in misconfigured networks.
- Proficient in having used SMB relay attacks to bypass authentication mechanisms and escalate privileges.
- Gained proficiency in exploiting IPv6 attacks to compromise network defenses in mixed IPv4/IPv6 environments.
- Acquired expertise in Pass The Password/Hash techniques for lateral movement within compromised networks.
- Developed a deep understanding of Kerberoasting for extracting service account credentials via Active Directory misconfigurations.
- Built proficiency with industry-standard penetration testing tools to simulate real-world attacks and identify weaknesses in systems.
- Strengthened the ability to apply attack methods in realistic scenarios, preparing to effectively assess, detect, and mitigate security risks.
- Enhanced readiness to contribute to incident response, vulnerability assessments, and network defense strategies in a professional setting.

## Acknowledgements
This project combines ideas and methods from various sources, such as the Real World Windows Pentest by David Bombal and TCM Security and my IT experience. These resources provided the fundamental information and techniques, which were then modified in light of practical uses. 
 - [David Bombal](https://www.youtube.com/watch?v=BsS7VITiUXo)
 - [TCM Security](https://academy.tcm-sec.com/)
 - [Kali Linux](https://www.kali.org/) 
 - [Windows Server 2022 Eval](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022)
 - [Windows 10 Eval](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-10-enterprise)
 - [VMWare Workstation](https://www.vmware.com/products/desktop-hypervisor/workstation-and-fusion)

## Disclaimer
The sole goals of the projects and activities here are for education and ethical cybersecurity research. All work was conducted in controlled environments, such as paid cloud spaces, private labs, and online cybersecurity education platforms. Online learning and cloud tasks adhered closely to all usage guidelines. Never use these projects for improper or unlawful purposes. It is always prohibited to break into any computer system or network. Any misuse of the provided information or code is not the responsibility of the author or authors.

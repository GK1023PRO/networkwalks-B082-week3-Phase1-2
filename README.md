# PASSWORD SECURITY & PASSWORD CRACKING PHASE

### W3-PM-FINAL | CYBERSECURITY | NETWORKWALKS

| Field | Details |
|---|---|
| **Pentester Name (Cybersecurity Professional)** | Georges Khoury |
| **Program/Batch** | B082 – NetworkWalks |
| **Week** | 03 |
| **Modules / Activities** | W3-PM1 – Password Cracking with John the Ripper (JTR)<br>W3-PM2 – Password Cracking with NetworkWalks Tools<br>W3-OPTIONAL1 – z. Optional Module Lab - JTR Password Cracking Lab v1 (AI-version)<br>W3-OPTIONAL2 – Mediroza Hospital Web Authentication Security Assessment |
| **Operating Environment** | Kali Linux |
| **Status** | W3-PM1 – Completed<br>W3-PM2 – Completed<br>W3-OPTIONAL1 – Completed<br>W3-OPTIONAL2 – In Progress |
| **Topics Covered** | Password Security, Password Recovery, Hash Extraction, Dictionary Attacks, Authentication Testing, Web Security & Troubleshooting |
| **Purpose** | Authorized cybersecurity training and educational security assessment |

---

## 1. Liability Disclaimer

I performed the activities documented in this report strictly within authorized cybersecurity training, educational laboratory, and approved security-assessment environments. The password-recovery exercises were performed against files supplied for the NetworkWalks Week 3 practical modules, while the local authentication testing documented in the optional laboratory was performed against a web application hosted on my own Kali Linux system.

W3-OPTIONAL2 remains in progress. Only activities and observations that were actually performed or observed are documented. An observation is not treated as a confirmed vulnerability unless sufficient evidence has been collected and the result has been appropriately validated.

Password cracking, credential testing, reconnaissance, vulnerability assessment, and penetration-testing techniques must only be performed against files, systems, applications, accounts, and networks for which explicit authorization has been obtained. Unauthorized access or testing may violate applicable laws and organizational policies.

---

## 2. Introduction

This report documents the practical cybersecurity activities completed and currently in progress during Week 3 of the NetworkWalks Cybersecurity & Ethical Hacking Program.

Week 3 focuses primarily on password security and password-recovery techniques. The practical exercises demonstrate how password-protected information can be assessed using password-auditing tools, how password-verification information can be extracted from protected files, how dictionary-based password recovery operates, and why strong and unique passwords are important security controls.

The Week 3 work consists of four activities:

1. **W3-PM1 – Password Cracking with John the Ripper (JTR)**
2. **W3-PM2 – Password Cracking with NetworkWalks Tools**
3. **W3-OPTIONAL1 – z. Optional Module Lab - JTR Password Cracking Lab v1 (AI-version)**
4. **W3-OPTIONAL2 – Mediroza Hospital Web Authentication Security Assessment**

For W3-PM1, I used Kali Linux and John the Ripper to perform the assigned password-recovery exercise against a password-protected PDF. The practical demonstrated the relationship between a protected document, extracted password-verification information, candidate-password testing, password recovery, and manual verification.

For W3-PM2, I used the NetworkWalks browser-based Hash Calculator and Password Cracker. The protected PDF was processed to obtain a `$pdf$...` hash, which was then used for password-recovery testing before the result was verified against the original document.

For W3-OPTIONAL1, I completed the additional **z. Optional Module Lab - JTR Password Cracking Lab v1 (AI-version)**. The Week 3 optional work also included a controlled authentication laboratory hosted locally on Kali Linux, where a deliberately weak test credential was successfully identified and manually verified.

W3-OPTIONAL2 extends the Week 3 activities into web-authentication security assessment involving the Mediroza Hospital web application. This activity is still in progress. During the current stage, the web service became unavailable and network troubleshooting was performed to determine whether the issue originated from the Kali Linux environment or from service availability.

Together, these exercises demonstrate the importance of password strength, secure authentication controls, result validation, troubleshooting methodology, accurate cybersecurity documentation, and explicit authorization.

---

## 3. Tools Used

The following tools and technologies were used during the Week 3 practical activities.

| Tool | Purpose |
|---|---|
| **Kali Linux** | Primary operating system used for the Week 3 cybersecurity practicals |
| **John the Ripper (JTR)** | Password auditing and password recovery |
| **PDF Hash Extraction Utility** | Extract password-verification information from password-protected PDF files in a JTR-compatible format |
| **Wordlists / Dictionaries** | Provide candidate usernames and passwords during authorized dictionary-based testing |
| **NetworkWalks Hash Calculator** | Extract password-verification information from an assigned protected PDF |
| **NetworkWalks Password Cracker** | Perform browser-based password recovery against the extracted PDF hash |
| **THC Hydra** | Perform automated credential testing against the controlled localhost authentication laboratory |
| **Apache HTTP Server** | Host the controlled local web application |
| **PHP** | Provide server-side authentication functionality for the local laboratory |
| **Firefox** | Access browser-based tools and manually verify authentication results |
| **cURL** | Inspect HTTP/HTTPS responses and test web-service connectivity |
| **Netcat (`nc`)** | Verify TCP connectivity to specific destination ports |
| **ping** | Verify basic Internet connectivity |
| **getent** | Verify hostname and DNS resolution |

---

## 4. Activities Performed

### Week 3 Protected PDF / Hash Mapping

The same three password-protected PDF files and their corresponding hash files are used across **W3-PM1, W3-PM2, and W3-OPTIONAL1**.

| Protected PDF | Extracted Hash |
|---|---|
| `My Locked PDF1.pdf` | `hash1.txt` |
| `My Locked PDF2.pdf` | `hash2.txt` |
| `My Locked PDF3.pdf` | `hash3.txt` |

Therefore, each of the three password-cracking modules uses all three pairs:

```text
My Locked PDF1.pdf → hash1.txt
My Locked PDF2.pdf → hash2.txt
My Locked PDF3.pdf → hash3.txt
```

The difference between the modules is the **password-recovery method**, not the files being tested:

| Module | Password-Recovery Method |
|---|---|
| **W3-PM1** | John the Ripper (JTR) directly on Kali Linux |
| **W3-PM2** | NetworkWalks Hash Calculator + NetworkWalks Password Cracker |
| **W3-OPTIONAL1** | Claude + HexStrike AI + John the Ripper on Kali Linux |

These PDF/hash pairs are **not part of W3-OPTIONAL2**, which is a separate web-authentication assessment activity.

---

### 4.1 W3-PM1 – Password Cracking with John the Ripper (JTR)

**Protected files used:** `My Locked PDF1.pdf`, `My Locked PDF2.pdf`, `My Locked PDF3.pdf`  
**Corresponding hash files:** `hash1.txt`, `hash2.txt`, `hash3.txt`

All three protected PDFs were included in the W3-PM1 John the Ripper exercise:

```text
My Locked PDF1.pdf → hash1.txt
My Locked PDF2.pdf → hash2.txt
My Locked PDF3.pdf → hash3.txt
```

Each hash file contains the password-verification information extracted from its corresponding protected PDF and is used during the JTR password-auditing workflow.

I performed the W3-PM1 practical using **John the Ripper** directly within Kali Linux. The objective of the exercise was to recover the password protecting the supplied `My Locked PDF1.pdf` file and then verify the recovered password against the original protected document.

The protected PDF could not be supplied directly to John the Ripper as a normal password string. Instead, password-verification information first had to be extracted from the PDF and converted into a format that John the Ripper could process.

The practical followed the general workflow:

```text
Password-Protected PDF
        ↓
PDF Password-Verification Extraction
        ↓
JTR-Compatible Hash
        ↓
John the Ripper
        ↓
Candidate-Password Testing
        ↓
Recovered Password
        ↓
Manual PDF Verification
```

After the password-verification information was prepared, John the Ripper was used to test candidate passwords. The recovered password was then entered into the original PDF to confirm that the password-recovery result was valid.

This exercise demonstrated that strong encryption alone does not compensate for a weak password. If the password protecting an encrypted document is predictable or appears in an attacker's candidate-password list, it may be recovered using automated password-auditing techniques.

**W3-PM1 Status:** ✅ Completed

---

### 4.2 W3-PM2 – Password Cracking with NetworkWalks Tools

**Protected files used:** `My Locked PDF1.pdf`, `My Locked PDF2.pdf`, `My Locked PDF3.pdf`  
**Corresponding hash files:** `hash1.txt`, `hash2.txt`, `hash3.txt`

All three protected PDFs were included in the W3-PM2 NetworkWalks password-recovery exercise:

```text
My Locked PDF1.pdf → hash1.txt
My Locked PDF2.pdf → hash2.txt
My Locked PDF3.pdf → hash3.txt
```

The same three PDF/hash pairs were processed through the NetworkWalks Hash Calculator and Password Cracker workflow.

I performed the second Week 3 practical using the browser-based **NetworkWalks Hash Calculator** and **NetworkWalks Password Cracker**.

The assigned protected PDF was first provided to the Hash Calculator. The tool extracted password-verification information from the PDF and returned it in a format beginning with:

```text
$pdf$...
```

The complete hash was required for the next stage because removing or truncating any portion of the value could prevent the password-recovery tool from correctly processing it.

The extracted hash was then supplied to the NetworkWalks Password Cracker. The password-recovery tool performed dictionary-based candidate-password testing against the hash.

The workflow was:

```text
Protected PDF
      ↓
NetworkWalks Hash Calculator
      ↓
Complete $pdf$... Hash
      ↓
NetworkWalks Password Cracker
      ↓
Candidate-Password Testing
      ↓
Recovered Password
      ↓
Manual PDF Verification
```

After a matching password was identified, the recovered password was manually entered into the original protected PDF. Successful access confirmed that the recovered password was correct.

This exercise reinforced the same password-security concept demonstrated in W3-PM1 while using browser-based tools instead of a command-line password-auditing workflow.

**W3-PM2 Status:** ✅ Completed

---

### 4.3 W3-OPTIONAL1 – z. Optional Module Lab - JTR Password Cracking Lab v1 (AI-version)

**Protected files used:** `My Locked PDF1.pdf`, `My Locked PDF2.pdf`, `My Locked PDF3.pdf`  
**Corresponding hash files:** `hash1.txt`, `hash2.txt`, `hash3.txt`

All three protected PDFs were included in the W3-OPTIONAL1 AI-assisted password-cracking exercise:

```text
My Locked PDF1.pdf → hash1.txt
My Locked PDF2.pdf → hash2.txt
My Locked PDF3.pdf → hash3.txt
```

Claude and HexStrike AI were used to assist the workflow on Kali Linux, while John the Ripper remained the underlying password-auditing tool.

I completed the additional Week 3 optional practical titled:

**z. Optional Module Lab - JTR Password Cracking Lab v1 (AI-version)**

The purpose of this optional activity was to extend the password-security and password-cracking concepts practiced during W3-PM1 and W3-PM2 by introducing an **AI-assisted password-auditing workflow using Claude and HexStrike AI on Kali Linux**.

While W3-PM1 demonstrated password cracking directly with **John the Ripper (JTR)** and W3-PM2 demonstrated password recovery using the **NetworkWalks Hash Calculator and Password Cracker**, W3-OPTIONAL1 demonstrated how an AI assistant can interact with cybersecurity tools running inside a Kali Linux environment.

The main technologies used during this optional practical were:

- **Kali Linux** – operating environment used for the cybersecurity laboratory.
- **Claude** – AI assistant used to interact with and assist the password-cracking workflow.
- **HexStrike AI** – security-tool integration layer used to connect the AI-assisted workflow with tools available in Kali Linux.
- **John the Ripper (JTR)** – password-auditing tool used to perform the underlying password-recovery operations.
- **Wordlists / candidate passwords** – candidate values used during the authorized password-auditing process.

The AI-assisted architecture used during the exercise can be represented as:

```text
Claude
   ↓
HexStrike AI
   ↓
Kali Linux
   ↓
John the Ripper
   ↓
Password-Recovery Operation
```

The password-cracking methodology followed the same fundamental process demonstrated during the previous Week 3 practical activities:

```text
Password-Protected Lab Resource
        ↓
Extract Password-Verification Information
        ↓
Prepare JTR-Compatible Hash
        ↓
Claude + HexStrike AI
        ↓
John the Ripper
        ↓
Candidate-Password Testing
        ↓
Recovered Password
        ↓
Manual Verification
```

First, the required cybersecurity environment was prepared on **Kali Linux**. HexStrike AI was configured to provide the integration layer between the AI-assisted workflow and the security tools available within Kali Linux.

Claude was then used as the AI interaction layer. Through HexStrike AI, the password-auditing workflow could interact with the tools running in the Kali Linux environment while John the Ripper remained responsible for the underlying password-recovery operation.

An important concept demonstrated during this activity was the separation between the AI assistant, the integration layer, and the underlying security tool:

```text
Claude          → AI interaction and assistance
HexStrike AI    → Security-tool integration and orchestration
Kali Linux      → Security-tool execution environment
John the Ripper → Password-auditing and password-recovery engine
```

The password-verification information associated with the protected laboratory resource was prepared in a John the Ripper-compatible format. Candidate passwords could then be evaluated by the password-auditing process.

After the password-recovery operation completed, the resulting output was reviewed and the recovered password was verified against the original protected laboratory resource.

The final verification workflow was:

```text
Password-Recovery Result
        ↓
Recovered Password
        ↓
Original Protected Resource
        ↓
Manual Verification
        ↓
Confirmed Result
```

Manual verification was an important part of the exercise because automated and AI-assisted security-tool output should be validated before being documented as a confirmed result.

The three Week 3 password-cracking activities can be compared as follows:

| Module | Password-Cracking Approach | Main Tools | Environment |
|---|---|---|---|
| **W3-PM1** | Direct password cracking | John the Ripper (JTR) | Kali Linux |
| **W3-PM2** | Browser-based password cracking | NetworkWalks Hash Calculator + Password Cracker | Web Browser |
| **W3-OPTIONAL1** | AI-assisted password cracking | Claude + HexStrike AI + John the Ripper | Kali Linux |

W3-PM1 demonstrated the traditional command-line password-auditing workflow. W3-PM2 demonstrated a browser-based password-recovery workflow. W3-OPTIONAL1 demonstrated how Claude and HexStrike AI could be integrated with the Kali Linux environment to assist the same general password-auditing process while John the Ripper performed the underlying technical operation.

The optional practical reinforced several important concepts:

- Password strength directly affects resistance to password-cracking attacks.
- Weak and predictable passwords may be susceptible to dictionary-based password recovery.
- Password-verification information must be prepared correctly before it can be processed by John the Ripper.
- Claude provides an AI interaction layer for the workflow.
- HexStrike AI provides the security-tool integration layer.
- John the Ripper remains the underlying password-auditing engine.
- AI assistance does not replace the need to understand the tools and commands being executed.
- Automated and AI-assisted results should be reviewed and manually verified.
- Strong and unique passwords provide greater resistance to password-recovery attacks.
- AI-assisted cybersecurity activities must remain within an explicitly authorized scope.

Overall, W3-OPTIONAL1 provided hands-on experience combining **Claude, HexStrike AI, Kali Linux, and John the Ripper** within an AI-assisted password-auditing laboratory.

All password-cracking activities documented in this optional module were performed as part of an authorized educational cybersecurity exercise.

**W3-OPTIONAL1 Status:** ✅ Completed

---

### 4.4 W3-OPTIONAL2 – Web Authentication Password Testing & Mediroza Hospital Security Assessment

**Status: 🟡 In Progress**

W3-OPTIONAL2 extends the Week 3 practical activities from offline password auditing into **web-authentication password testing and security assessment using Kali Linux**.

This optional activity currently consists of two clearly separated stages:

1. A controlled localhost web-authentication laboratory used to validate the authentication-testing methodology.
2. The Mediroza Hospital web-authentication assessment, which remains in progress.

#### Stage 1 – Controlled Local Web-Authentication Laboratory

Before continuing with the external assessment, I created and tested a controlled authentication application on my own Kali Linux system.

The local application was available at:

```text
http://127.0.0.1/patient/login.php
```

Because `127.0.0.1` is the loopback address, all credential-testing activity performed during this stage remained inside my locally controlled laboratory environment.

The local patient-login page contained username and password fields. An unsuccessful login attempt returned:

```text
Invalid credentials
```

This response was used as the failure condition during the controlled automated authentication test.

Two small laboratory wordlists were prepared:

```text
6 usernames
7 passwords
42 possible credential combinations
```

THC Hydra was then used to test the candidate credentials against the local HTTP POST authentication form.

The command used was:

```bash
hydra -L ~/users.txt -P ~/passwords.txt 127.0.0.1 \
http-post-form "/patient/login.php:username=^USER^&password=^PASS^:F=Invalid credentials" \
-V -f
```

Hydra processed the 42 possible username/password combinations and identified the deliberately configured laboratory credential:

```text
Username: hydra-lab
Password: kali
```

The terminal reported:

```text
[80][http-post-form] host: 127.0.0.1   login: hydra-lab   password: kali
1 of 1 target successfully completed, 1 valid password found
```

The automated result was then manually verified through the local patient-login page. The identified username and password were entered into the application, which returned:

```text
Login successful
```

The manual verification confirmed that Hydra had identified a genuine valid laboratory credential rather than a false positive.

The `hydra-lab / kali` credential belongs **exclusively to the deliberately configured localhost laboratory**. It is not presented as a credential or finding associated with the external Mediroza Hospital application.

This controlled exercise demonstrated how weak credentials can be susceptible to dictionary-based authentication testing when candidate values are predictable. It also reinforced the importance of strong password policies, authentication monitoring, rate limiting, and manual verification of automated findings.

#### Stage 2 – Mediroza Hospital Web Authentication Security Assessment

After validating the authentication-testing methodology in the controlled localhost laboratory, I proceeded with the Mediroza Hospital web-authentication assessment.

The external web application observed during this activity is:

```text
https://www.medirozahospital.com/
```

A patient authentication interface was observed at:

```text
/patient/login.php
```

The interface presented username and password fields. An unsuccessful authentication attempt produced:

```text
Invalid credentials
```

During the ongoing assessment, the external website subsequently became inaccessible from the Kali Linux environment. I therefore performed connectivity troubleshooting before continuing the assessment.

#### Internet Connectivity Verification

The following command was executed:

```bash
ping -c 4 8.8.8.8
```

The result showed:

```text
4 packets transmitted
4 received
0% packet loss
```

This confirmed that Kali Linux retained basic Internet connectivity.

#### DNS Resolution Verification

DNS resolution was then verified using:

```bash
getent hosts www.medirozahospital.com
```

The hostname successfully resolved to:

```text
199.188.201.16  medirozahospital.com www.medirozahospital.com
```

This confirmed that DNS resolution remained functional.

#### HTTP Connectivity Verification

TCP connectivity to HTTP port 80 was tested using:

```bash
nc -vz -w 5 www.medirozahospital.com 80
```

The result was:

```text
Connection refused
```

#### HTTPS Connectivity Verification

TCP connectivity to HTTPS port 443 was tested using:

```bash
nc -vz -w 5 www.medirozahospital.com 443
```

The result was:

```text
Connection refused
```

#### HTTPS Request Verification

An HTTPS request was attempted using cURL:

```bash
curl -I --connect-timeout 10 https://www.medirozahospital.com/
```

The result was:

```text
curl: (7) Failed to connect to www.medirozahospital.com port 443:
Could not connect to server
```

#### Kali Linux Restart

Kali Linux was restarted to determine whether the connectivity condition originated from the virtual machine.

After restarting:

```text
Internet Connectivity: Working
DNS Resolution: Working
HTTPS Connectivity: Still unavailable
```

The restart did not change the observed condition.

#### Host Computer Restart

The host computer was subsequently restarted as an additional troubleshooting measure.

After the restart, Kali Linux again had working Internet connectivity and DNS resolution, but the external HTTP/HTTPS service remained unavailable during testing.

#### Current Troubleshooting Summary

| Test | Result |
|---|---|
| Internet connectivity | ✅ Working |
| Packet loss | 0% |
| DNS resolution | ✅ Working |
| Resolved address | `199.188.201.16` |
| TCP port 80 | ❌ Connection refused |
| TCP port 443 | ❌ Connection refused |
| HTTPS cURL request | ❌ Connection could not be established |
| Kali Linux restart | No change |
| Host-computer restart | No change |

The available evidence establishes that the Kali Linux environment retained Internet connectivity and successfully resolved the target hostname while the tested HTTP and HTTPS connections were not being accepted at that time.

The available evidence does not establish the underlying reason for the external service's unavailability. Therefore, the connectivity condition is documented as a **troubleshooting observation rather than a confirmed vulnerability**.

#### W3-OPTIONAL2 Current Result

The controlled localhost authentication laboratory was completed successfully and demonstrated that the authentication-testing methodology functioned correctly within the locally controlled environment.

The Mediroza Hospital assessment has not yet reached a final result because the external web service became unavailable during the ongoing activity.

Additional evidence and findings will be documented only after they are actually observed and validated.

**W3-OPTIONAL2 Status:** 🟡 In Progress

---


## 5. Risk Analysis / Impact

Based on the Week 3 practical activities, I identified the following password-security and authentication observations.

| # | Risk / Finding | Evidence / Observation | Potential Impact | Risk Level |
|---:|---|---|---|---|
| 1 | Weak passwords may be susceptible to dictionary attacks | Password-recovery exercises demonstrated candidate-password testing | Predictable passwords may be recovered using automated password-auditing techniques | **High** |
| 2 | Password-protected documents depend heavily on password strength | W3-PM1 and W3-PM2 demonstrated password recovery from protected PDFs | Weak passwords may significantly reduce the practical protection provided by encryption | **High** |
| 3 | Password-verification data can support offline password testing | PDF password information can be converted into a password-auditing format | Candidate passwords can potentially be evaluated without repeatedly interacting with the original document | **Medium** |
| 4 | Weak authentication credentials may be susceptible to automated guessing | The controlled localhost laboratory recovered `hydra-lab / kali` | Weak credentials may increase the likelihood of unauthorized authentication | **High** |
| 5 | Insufficient authentication throttling can increase guessing risk | The controlled local application accepted repeated authentication attempts | Automated password testing becomes more practical without rate limiting or equivalent controls | **High** |
| 6 | Automated findings require validation | The Hydra result was manually verified through the browser | Unvalidated automated findings may result in inaccurate security conclusions | **Medium** |
| 7 | Password reuse increases potential impact | Password-security principles demonstrated throughout Week 3 | Compromise of a reused password may expose multiple accounts or services | **High** |
| 8 | DNS resolution does not guarantee application availability | W3-OPTIONAL2 resolved successfully while HTTP/HTTPS connections were unavailable | Troubleshooting must distinguish DNS, network, transport, and application-layer conditions | **Low** |

The findings above represent observations from educational and authorized cybersecurity exercises. A security observation should not automatically be interpreted as a confirmed exploitable vulnerability without sufficient supporting evidence.

---

## 6. Recommendations

Based on the Week 3 practical activities, I recommend the following security improvements:

1. **Use long and unique passwords**  
   Passwords should be sufficiently long, unpredictable, and unique for each account or protected resource.

2. **Avoid common dictionary passwords**  
   Common passwords, names, dates, keyboard patterns, and predictable numerical sequences should not be used to protect sensitive information.

3. **Avoid password reuse**  
   A different password should be used for every important account and system.

4. **Use a reputable password manager**  
   Password managers can generate and securely store long, random, and unique passwords.

5. **Enable multi-factor authentication where available**  
   MFA provides an additional authentication layer if a password becomes compromised.

6. **Protect encrypted documents with strong passwords**  
   Encryption should be combined with strong password selection and appropriate access controls.

7. **Implement authentication rate limiting**  
   Web applications should restrict excessive authentication attempts to reduce automated password guessing.

8. **Use progressive delays or temporary restrictions**  
   Increasing delays or temporary restrictions after repeated authentication failures can reduce automated guessing effectiveness.

9. **Monitor authentication activity**  
   Repeated failed logins and unusual authentication patterns should be logged, monitored, and investigated.

10. **Perform authorized password-security audits**  
    Organizations should periodically assess password strength and authentication controls within a clearly defined authorized scope.

11. **Validate automated findings**  
    Results generated by automated security tools should be independently verified before being reported as confirmed findings.

12. **Maintain clear testing boundaries**  
    Local laboratories, educational targets, and external systems should remain clearly separated in cybersecurity documentation.

13. **Document unsuccessful tests and troubleshooting**  
    Failed tests and troubleshooting activities provide useful technical evidence and should be documented accurately.

14. **Do not infer vulnerabilities from connectivity failures alone**  
    Service availability problems require additional evidence before their underlying cause can be established.

---

## 7. Conclusion

During Week 3 of the NetworkWalks Cybersecurity & Ethical Hacking Program, I completed practical activities covering password security, password cracking, password-verification information, dictionary attacks, authentication testing, result validation, and basic web-service troubleshooting.

In W3-PM1, I used John the Ripper within Kali Linux to perform password recovery against an assigned password-protected PDF. The exercise demonstrated how password-verification information can be extracted from an encrypted document and tested against candidate passwords.

In W3-PM2, I used the NetworkWalks Hash Calculator and Password Cracker to perform the same general password-recovery workflow through browser-based tools. The exercise reinforced the relationship between an encrypted document, its password-verification information, candidate-password testing, and manual verification.

In W3-OPTIONAL1, **z. Optional Module Lab - JTR Password Cracking Lab v1 (AI-version)**, I reinforced the password-security and password-auditing concepts introduced in the main Week 3 modules. The additional controlled localhost authentication laboratory demonstrated automated credential testing against a deliberately configured weak account. Hydra tested 42 candidate combinations and identified the `hydra-lab / kali` credential pair. Manual browser authentication returned `Login successful`, confirming the automated finding.

W3-OPTIONAL2 remains in progress. During its current stage, the Mediroza patient authentication interface was observed before the external web service became unavailable. Troubleshooting demonstrated that Kali Linux retained Internet connectivity and DNS resolution while HTTP and HTTPS connections were not being accepted during the subsequent tests. No unsupported conclusion regarding the cause of the remote service condition has been made.

Overall, Week 3 demonstrated that password security depends heavily on password strength, uniqueness, authentication controls, and appropriate defensive measures. The practical activities also reinforced the importance of authorization, controlled testing, manual verification of automated findings, accurate reporting, and distinguishing observations from confirmed vulnerabilities.

---

## 8. Evidences Collected

### 8.1 W3-PM1 – Password Cracking with John the Ripper

**Protected PDFs:** `My Locked PDF1.pdf`, `My Locked PDF2.pdf`, `My Locked PDF3.pdf`  
**Hash files:** `hash1.txt`, `hash2.txt`, `hash3.txt`

Evidence collected during W3-PM1 documents the complete password-recovery workflow performed with John the Ripper on Kali Linux.

The evidence includes:

- The assigned password-protected PDF.
- Kali Linux environment.
- John the Ripper.
- PDF password-verification extraction.
- JTR-compatible hash preparation.
- Password-recovery activity.
- Recovered-password result.
- Manual verification against the original protected PDF.

The documented workflow is:

```text
My Locked PDF1.pdf
        ↓
PDF Hash Extraction
        ↓
JTR-Compatible Hash
        ↓
John the Ripper
        ↓
Password Recovery
        ↓
Manual PDF Verification
```

#### Screenshot Placement

Place the W3-PM1 screenshots in chronological order under:

```text
screenshots/W3-PM1/
```
![W3-PM1 Evidence 1](screenshots/W3-PM1/1.png)
![W3-PM1 Evidence 2](screenshots/W3-PM1/2.png)
![W3-PM1 Evidence 3](screenshots/W3-PM1/3.png)
![W3-PM1 Evidence 4](screenshots/W3-PM1/4.png)
![W3-PM1 Evidence 5](screenshots/W3-PM1/5.png)
![W3-PM1 Evidence 6](screenshots/W3-PM1/6.png)
![W3-PM1 Evidence 7](screenshots/W3-PM1/7.png)
![W3-PM1 Evidence 8](screenshots/W3-PM1/8.png)
![W3-PM1 Evidence 9](screenshots/W3-PM1/9.png)
![W3-PM1 Evidence 10](screenshots/W3-PM1/10.png)
![W3-PM1 Evidence 11](screenshots/W3-PM1/11.png)
![W3-PM1 Evidence 12](screenshots/W3-PM1/12.png)
![W3-PM1 Evidence 13](screenshots/W3-PM1/13.png)
![W3-PM1 Evidence 14](screenshots/W3-PM1/14.png)
![W3-PM1 Evidence 15](screenshots/W3-PM1/15.png)
![W3-PM1 Evidence 16](screenshots/W3-PM1/16.png)
![W3-PM1 Evidence 17](screenshots/W3-PM1/17.png)
![W3-PM1 Evidence 18](screenshots/W3-PM1/18.png)
![W3-PM1 Evidence 19](screenshots/W3-PM1/19.png)
![W3-PM1 Evidence 20](screenshots/W3-PM1/20.png)
![W3-PM1 Evidence 21](screenshots/W3-PM1/21.png)
![W3-PM1 Evidence 22](screenshots/W3-PM1/22.png)
![W3-PM1 Evidence 23](screenshots/W3-PM1/23.png)
![W3-PM1 Evidence 24](screenshots/W3-PM1/24.png)
![W3-PM1 Evidence 25](screenshots/W3-PM1/25.png)
![W3-PM1 Evidence 26](screenshots/W3-PM1/26.png)
![W3-PM1 Evidence 27](screenshots/W3-PM1/27.png)
![W3-PM1 Evidence 28](screenshots/W3-PM1/28.png)
![W3-PM1 Evidence 29](screenshots/W3-PM1/29.png)
![W3-PM1 Evidence 30](screenshots/W3-PM1/30.png)
![W3-PM1 Evidence 31](screenshots/W3-PM1/31.png)
![W3-PM1 Evidence 32](screenshots/W3-PM1/32.png)
![W3-PM1 Evidence 33](screenshots/W3-PM1/33.png)
![W3-PM1 Evidence 34](screenshots/W3-PM1/34.png)
![W3-PM1 Evidence 35](screenshots/W3-PM1/35.png)
![W3-PM1 Evidence 36](screenshots/W3-PM1/36.png)
![W3-PM1 Evidence 37](screenshots/W3-PM1/37.png)
![W3-PM1 Evidence 38](screenshots/W3-PM1/38.png)
![W3-PM1 Evidence 39](screenshots/W3-PM1/39.png)


Use the shared hash files stored under:

```text
outputs/password-hashes/hash1.txt
outputs/password-hashes/hash2.txt
outputs/password-hashes/hash3.txt
```

**Status:** ✅ Completed

---

### 8.2 W3-PM2 – Password Cracking with NetworkWalks Tools

**Protected PDFs:** `My Locked PDF1.pdf`, `My Locked PDF2.pdf`, `My Locked PDF3.pdf`  
**Hash files:** `hash1.txt`, `hash2.txt`, `hash3.txt`

Evidence collected during W3-PM2 documents the browser-based password-recovery process.

The evidence includes:

- NetworkWalks Hash Calculator.
- Protected PDF upload.
- `$pdf$...` hash extraction.
- Complete hash copied for password recovery.
- NetworkWalks Password Cracker.
- Password-recovery result.
- Manual verification against the original PDF.

The documented workflow is:

```text
Protected PDF
      ↓
Hash Calculator
      ↓
$pdf$... Hash
      ↓
Password Cracker
      ↓
Recovered Password
      ↓
Manual Verification
```

#### Screenshot Placement

Place the W3-PM2 screenshots in chronological order under:

```text
screenshots/W3-PM2/
```

Recommended filenames:

```text
01-PDF1-Protected-File.png
02-PDF1-NetworkWalks-Hash-Calculator.png
03-PDF1-Hash1-Result.png
04-PDF1-Password-Cracker.png
05-PDF1-Recovered-Password.png
06-PDF1-Password-Verification.png

07-PDF2-Protected-File.png
08-PDF2-NetworkWalks-Hash-Calculator.png
09-PDF2-Hash2-Result.png
10-PDF2-Password-Cracker.png
11-PDF2-Recovered-Password.png
12-PDF2-Password-Verification.png

13-PDF3-Protected-File.png
14-PDF3-NetworkWalks-Hash-Calculator.png
15-PDF3-Hash3-Result.png
16-PDF3-Password-Cracker.png
17-PDF3-Recovered-Password.png
18-PDF3-Password-Verification.png
```

Use the shared hash files stored under:

```text
outputs/password-hashes/hash1.txt
outputs/password-hashes/hash2.txt
outputs/password-hashes/hash3.txt
```

**Status:** ✅ Completed

---

### 8.3 W3-OPTIONAL1 – z. Optional Module Lab - JTR Password Cracking Lab v1 (AI-version)

**Protected PDFs:** `My Locked PDF1.pdf`, `My Locked PDF2.pdf`, `My Locked PDF3.pdf`  
**Hash files:** `hash1.txt`, `hash2.txt`, `hash3.txt`

Evidence collected during W3-OPTIONAL1 documents the additional password-security practical work performed in Kali Linux.

The optional evidence includes password-auditing activities and the additional controlled localhost authentication laboratory.

The local authentication target was:

```text
http://127.0.0.1/patient/login.php
```

The unsuccessful authentication indicator was:

```text
Invalid credentials
```

The controlled candidate set contained:

```text
6 usernames × 7 passwords = 42 combinations
```

The Hydra command used in the localhost laboratory was:

```bash
hydra -L ~/users.txt -P ~/passwords.txt 127.0.0.1 \
http-post-form "/patient/login.php:username=^USER^&password=^PASS^:F=Invalid credentials" \
-V -f
```

Hydra identified:

```text
Username: hydra-lab
Password: kali
```

The terminal reported:

```text
1 valid password found
```

Manual browser verification returned:

```text
Login successful
```

The result was therefore independently validated.

#### Screenshot Placement

Place the W3-OPTIONAL1 screenshots in chronological order under:

```text
screenshots/W3-OPTIONAL1/
```

Recommended filenames:

```text
01-HexStrike-AI-Kali-Environment.png
02-Claude-HexStrike-Integration.png

03-PDF1-Protected-File.png
04-PDF1-Hash1-Preparation.png
05-PDF1-AI-Assisted-JTR.png
06-PDF1-Recovered-Password.png
07-PDF1-Password-Verification.png

08-PDF2-Protected-File.png
09-PDF2-Hash2-Preparation.png
10-PDF2-AI-Assisted-JTR.png
11-PDF2-Recovered-Password.png
12-PDF2-Password-Verification.png

13-PDF3-Protected-File.png
14-PDF3-Hash3-Preparation.png
15-PDF3-AI-Assisted-JTR.png
16-PDF3-Recovered-Password.png
17-PDF3-Password-Verification.png
```

Use the shared hash files stored under:

```text
outputs/password-hashes/hash1.txt
outputs/password-hashes/hash2.txt
outputs/password-hashes/hash3.txt
```

**Status:** ✅ Completed

---

### 8.4 W3-OPTIONAL2 – Mediroza Hospital Web Authentication Security Assessment

**Status: 🟡 In Progress**

The external application observed during the current stage of the activity was:

```text
https://www.medirozahospital.com/
```

The patient authentication interface was observed at:

```text
/patient/login.php
```

The observed unsuccessful authentication response was:

```text
Invalid credentials
```

During subsequent testing, the external web service became unavailable.

Internet connectivity was verified using:

```bash
ping -c 4 8.8.8.8
```

Result:

```text
4 packets transmitted
4 received
0% packet loss
```

DNS resolution was verified using:

```bash
getent hosts www.medirozahospital.com
```

Result:

```text
199.188.201.16  medirozahospital.com www.medirozahospital.com
```

HTTP connectivity was checked using:

```bash
nc -vz -w 5 www.medirozahospital.com 80
```

Result:

```text
Connection refused
```

HTTPS connectivity was checked using:

```bash
nc -vz -w 5 www.medirozahospital.com 443
```

Result:

```text
Connection refused
```

The HTTPS service was also checked using:

```bash
curl -I --connect-timeout 10 https://www.medirozahospital.com/
```

Result:

```text
curl: (7) Failed to connect to www.medirozahospital.com port 443:
Could not connect to server
```

The current evidence can therefore be summarized as:

```text
Internet Connectivity : Working
DNS Resolution        : Working
Resolved IP           : 199.188.201.16
HTTP/80               : Connection refused
HTTPS/443             : Connection refused
Assessment Status     : IN PROGRESS
```

Additional evidence will be appended as W3-OPTIONAL2 progresses.

---

## 9. Problems Encountered & Solutions

### 9.1 W3-OPTIONAL2 – External Web-Service Connectivity

#### Problem Encountered

During the ongoing W3-OPTIONAL2 activity, the external web application stopped accepting HTTP and HTTPS connections from the Kali Linux environment.

#### Troubleshooting Performed

The following areas were checked:

- Internet connectivity.
- DNS resolution.
- HTTP port 80 connectivity.
- HTTPS port 443 connectivity.
- HTTPS requests using cURL.
- Kali Linux restart.
- Host-computer restart.

#### Observations

Internet connectivity remained functional and the target hostname continued to resolve successfully.

However, connections to ports 80 and 443 were refused during the tests.

Restarting Kali Linux and subsequently restarting the host computer did not change the observed condition.

#### Current Resolution

The troubleshooting process established that the issue was not caused by a complete loss of Internet connectivity or DNS resolution inside Kali Linux.

The underlying reason for the external service's unavailability has not been established from the available evidence.

The condition is therefore documented as:

```text
Troubleshooting Observation — Not a Confirmed Vulnerability
```

W3-OPTIONAL2 remains in progress.

---

## 10. Skills Practiced

The Week 3 practical activities provided hands-on experience with:

- Cybersecurity.
- Ethical Hacking.
- Password Security.
- Password Auditing.
- Password Cracking.
- John the Ripper.
- Kali Linux.
- Linux command-line operations.
- PDF password-verification extraction.
- Password hash analysis.
- Dictionary attacks.
- Wordlist preparation.
- THC Hydra.
- HTTP authentication.
- HTTP POST forms.
- Web authentication testing.
- Manual security-result validation.
- Automated tool-result analysis.
- Apache.
- PHP.
- cURL.
- Netcat.
- DNS troubleshooting.
- TCP connectivity testing.
- Network troubleshooting.
- Cybersecurity reporting.
- Risk analysis.
- Security recommendations.
- Authorization and scope management.

---

## Recommended Repository Structure

Use the following GitHub repository structure:

```text
networkwalks-B082-week3-Phase1-2/
├── README.md
│
├── files/
│   ├── My Locked PDF1.pdf
│   ├── My Locked PDF2.pdf
│   └── My Locked PDF3.pdf
│
├── outputs/
│   └── password-hashes/
│       ├── hash1.txt
│       ├── hash2.txt
│       └── hash3.txt
│
└── screenshots/
    ├── W3-PM1/
    ├── W3-PM2/
    ├── W3-OPTIONAL1/
    └── W3-OPTIONAL2/
```

The same three PDF/hash pairs are referenced by W3-PM1, W3-PM2, and W3-OPTIONAL1. The screenshots remain separated by module because each module demonstrates a different password-recovery method.

---

## 👤 Report Prepared By

**Georges Khoury**  
Cybersecurity & Ethical Hacking Intern  
**Batch:** B082 – NetworkWalks

## 📌 Project Information

- **Program Name:** Cybersecurity Program at NetworkWalks
- **Week:** 03
- **W3-PM1:** Password Cracking with John the Ripper (JTR) — Completed
- **W3-PM2:** Password Cracking with NetworkWalks Tools — Completed
- **W3-OPTIONAL1:** z. Optional Module Lab - JTR Password Cracking Lab v1 (AI-version) — Completed
- **W3-OPTIONAL2:** Mediroza Hospital Web Authentication Security Assessment — In Progress
- **Primary Environment:** Kali Linux
- **Topics:** Password Security, Password Recovery, Authentication Testing & Web Security
- **Repository:** GitHub

---

**-End-**

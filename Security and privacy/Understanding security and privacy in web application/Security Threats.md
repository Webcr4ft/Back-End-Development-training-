# Common Security Threats and How to Mitigate Them

## Overview

Attackers constantly look for weaknesses to **steal data, disrupt systems, and extort money** from users and platforms. Below are five common threats and the main ways to defend against each.

| # | Threat | What It Targets | Main Mitigation |
|---|---|---|---|
| 1 | Phishing | Users' trust | Awareness training, email authentication |
| 2 | Malware | Devices and files | Updates, patching, antimalware software |
| 3 | Credential stuffing | Authentication systems | Multi-factor authentication (MFA) |
| 4 | DDoS | System availability | Cloud-based traffic filtering |
| 5 | Insider threats | Internal data | Least privilege, log monitoring |

---

## 1. Phishing

Criminals send **fraudulent emails that mimic trusted corporations**. The goal is to trick users into:

- Clicking malicious links
- Sharing account passwords
- Giving up other sensitive information

### How to mitigate

- **Security awareness training:** Employees learn to spot suspicious sender addresses and urgent-sounding formatting.
- **Email authentication protocols:** Software teams deploy these to block malicious messages **before they reach the user's inbox**.

---

## 2. Malware

Malware is malicious software. It includes:

- **Viruses**
- **Spyware**
- **Ransomware:** encrypts a victim's files, then demands a large payment to unlock them

### How to mitigate

- **Software teams:** run automated updates and patch known vulnerabilities.
- **Users:** install updates immediately and use antimalware software.

> **Note:** Security is **multi-layered**. Both teams and users must do their part.

---

## 3. Credential Stuffing

Attackers use **automated tools** to test millions of stolen username and password combinations across many websites.

> **Why it works:** Many people **reuse the same password** on multiple platforms.

### How to mitigate

Enforce **multi-factor authentication (MFA)**, which requires a second verification step, such as:

- A code from a mobile authenticator app
- A one-time password (OTP)
- Email verification

Even if a hacker steals the password, they **cannot access the account without the second token**.

---

## 4. Distributed Denial of Service (DDoS)

DDoS attacks target **availability**. Attackers flood a website with massive amounts of fake traffic. This overloads the server, crashes it, and blocks legitimate customers.

### How to mitigate

Use **cloud-based traffic filtering services**, such as:

- Cloudflare
- Akamai
- AWS Shield

These platforms analyze traffic spikes, **filter out malicious packets**, and let normal user traffic through.

---

## 5. Insider Threats

These come from people **inside the company**:

- **Disgruntled employees** who intentionally steal data
- **Careless workers** who accidentally leak information

### How to mitigate

- **Principle of least privilege:** workers can access only the files they need for their daily tasks.
- **Log monitoring:** security teams watch system logs to flag unusual data downloads or unauthorized file access.

---

## Key Takeaways

- **Phishing** exploits people, so train users and filter email.
- **Malware** (including ransomware) is countered by patching, updating, and antimalware tools.
- **Credential stuffing** succeeds because of password reuse, so enforce MFA.
- **DDoS** attacks overload servers, so use traffic-filtering services.
- **Insider threats** are limited by least privilege and log monitoring.
- No single defense is enough. Security works best in **layers**.

---

## Questions

*(Add your questions here.)*

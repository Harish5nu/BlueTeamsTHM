# Detecting Web Attacks

> **Platform:** TryHackMe
> **Difficulty:** Beginner–Intermediate
> **Category:** Web Security / SOC Analysis / Blue Team

---

## 📌 Introduction

Web attacks are one of the most common initial access vectors used by attackers. Public-facing web applications often sit in front of databases and critical infrastructure, making them attractive targets.

In this room, you learn how to **detect web-based attacks** using:

* Log analysis
* Network traffic inspection
* Web Application Firewalls (WAFs)

---

## 🎯 Objectives

* Learn common **client-side** and **server-side** attack types
* Understand the **benefits and limitations** of log-based detection
* Explore **network traffic–based detection** methods

---

## 🧑‍💻 Client-Side Attacks

Client-side attacks exploit weaknesses in **user behavior** or **browser-side execution**. These attacks occur entirely on the victim’s device, often leaving little to no trace in server logs or network traffic.

### Why They’re Dangerous

* Execute malicious scripts in the browser
* Steal cookies and session tokens
* Manipulate user actions invisibly
* Expanded attack surface due to third‑party plugins

### SOC Visibility Limitations

From a SOC perspective:

* No visibility into browser execution
* Minimal suspicious network traffic
* Requires endpoint or browser-side controls

### Common Client-Side Attacks

* **Cross-Site Scripting (XSS)** – Injecting malicious scripts into trusted websites
* **Cross-Site Request Forgery (CSRF)** – Forcing authenticated users to send unwanted requests
* **Clickjacking** – Overlaying invisible elements to trick users into clicking

### Key Answers

* **Attack class relying on user behavior/device:** Client-Side
* **Most common client-side attack:** XSS

---

## 🖥️ Server-Side Attacks

Server-side attacks exploit vulnerabilities in:

* Application logic
* Backend services
* Databases
* Server misconfigurations

Unlike client-side attacks, these usually leave **logs and network evidence**.

### Common Server-Side Attacks

* **Brute Force** – Repeated login attempts using automated tools
* **SQL Injection (SQLi)** – Manipulating backend SQL queries
* **Command Injection** – Executing system commands via user input

### Real-World Impact Examples

* T-Mobile (2021): Brute-force breach exposing 50M+ records
* MOVEit (2023): SQLi affecting 2,700+ organizations

### Key Answers

* **Attack class exploiting server vulnerabilities:** Server-Side
* **Attack that dumps database contents:** SQLi

---

## 📜 Log-Based Detection

Web servers log every request, making logs a powerful detection source.

### Common Access Log Fields

| Field         | Indicator                             |
| ------------- | ------------------------------------- |
| Client IP     | Malicious or unexpected geolocation   |
| Timestamp     | Abnormal frequency or timing          |
| Status Code   | Repeated 404s or odd responses        |
| Response Size | Too large or too small                |
| Referrer      | Doesn’t match site flow               |
| User-Agent    | Tools like `sqlmap`, `wpscan`, `ffuf` |

### Attack Chain Seen in Logs

1. Directory fuzzing (200 responses)
2. Brute-force login attempts (repeated POSTs)
3. Successful login (302 redirect)
4. SQL Injection attempts on search forms

### Log Limitations

* POST bodies are **not logged** by default
* Credentials and payloads may be invisible
* Logging depends on server configuration

---

## 🕵️ Investigation: TryBankMe Breach

You analyzed `access.log` to reconstruct the attack path.

### Findings

* **Directory fuzz User-Agent:** `FFUF v2.1.0`
* **Brute-force target page:** `/login.php`
* **Decoded SQLi payload:**

```
%' OR '1'='1
```

---

## 🌐 Network-Based Detection

Network traffic analysis provides **full visibility** into requests and responses.

### What You Can See

* Full HTTP headers
* POST bodies
* Cookies and credentials
* Uploaded/downloaded data

> ⚠️ Encrypted protocols (HTTPS/SSH) limit payload visibility without decryption keys.

### Attack Sequence in Wireshark

1. Directory fuzzing
2. Brute-force login (successful packet identified)
3. SQL injection attempts

### Key Discoveries

* **Valid password found:** `astrongpassword123`
* **Database flag extracted:**

```
THM{dumped_the_db}
```

### Useful Wireshark Tips

* Use `http` filter
* Right-click → **Follow HTTP Stream**

---

## 🔥 Web Application Firewalls (WAF)

WAFs act as gatekeepers, inspecting and filtering web requests **before** they reach the application.

### What WAFs Inspect

* Full web requests (Layer 7)
* Encrypted TLS traffic (after decryption)

### Rule Categories

| Rule Type               | Purpose                     |
| ----------------------- | --------------------------- |
| Attack pattern blocking | Detect SQLi, XSS, etc.      |
| IP reputation           | Block known malicious IPs   |
| Custom rules            | App-specific protections    |
| Rate limiting           | Prevent brute force & abuse |

### Example Custom Rule

```
IF User-Agent CONTAINS "BotTHM"
THEN BLOCK
```

### Challenge-Response

* CAPTCHA challenges instead of outright blocks
* Useful for reducing false positives

### Threat Intelligence Integration

* OWASP Top 10 protections
* CVE-based updates
* Global IP reputation feeds (e.g., Cloudflare)

---

## ✅ Conclusion

In this room, you learned how to:

* Identify **client-side vs server-side** web attacks
* Detect attacks using **logs** and **network traffic**
* Understand detection limitations
* Apply **WAF rules** to mitigate threats

By correlating multiple data sources, analysts can move beyond isolated alerts and develop stronger detection and response capabilities.

---

## 📚 Prerequisites & Resources

* OWASP Top 10
* Intro to Log Analysis
* Wireshark: The Basics

---

## 🚀 Status

Target Machine: **Off**
Room Completion: **Ready to proceed**

Happy hunting & keep sharpening those blue-team skills 🔵🛡️

# Defensive Security Intro

> **Platform:** TryHackMe
> **Difficulty:** Beginner
> **Category:** Defensive Security / Blue Team

---

## 🛡️ Think Like a Defender

Defensive security is the practice of **protecting, monitoring, and securing systems and devices** against attacks.

Unlike offensive security (where systems are attacked to find weaknesses), defensive security focuses on:

* Detecting suspicious activity
* Investigating potential attacks
* Responding quickly **before damage occurs**

Defenders continuously monitor systems using dashboards, alerts, and security tools to keep organizations safe.

---

## 🎯 Main Goal of Defensive Security

The primary objective of defensive security is:

✅ **Detect and respond to attacks**

Defenders do **not** attack systems — they observe, analyze, contain, and prevent threats.

---

## 🚨 Detect Suspicious Activity

The first step in defensive security is identifying behavior that **does not look normal**. This information appears as **alerts** in monitoring systems.

### What Was Done

* Opened the monitoring dashboard (View Site)
* Reviewed recent alerts
* Identified the source generating abnormal traffic

### Why This Matters

Monitoring tools help defenders decide:

* What activity is benign
* What requires investigation
* What must be stopped immediately

### ✅ Answer

* **Suspicious Source IP:**

```
32.122.195.63
```

---

## 🔍 Identify the Attack

Once suspicious activity is detected, defenders must identify **what type of attack is occurring**.

### Attack Identified

* **Attack Type:** Web Discovery

The attacker is attempting to locate sensitive or hidden pages on the website.

### What Was Observed

* Reviewed **URL Discovery Attempts**
* Attacker tried to access administrative pages

### Why This Matters

Understanding what an attacker is searching for helps defenders:

* Secure exposed endpoints
* Block malicious behavior
* Prevent similar attacks in the future

### ✅ Answer

* **Latest URL Targeted:**

```
https://fakebank.com/admin
```

---

## ⛔ Stop the Attack (Containment)

After identifying the attack, defenders take immediate action to **stop further damage**. This phase is known as **containment**.

### Actions Taken

* Blocked the attacker’s IP address
* Applied rate limiting to prevent abuse
* Updated security rules
* Implemented additional protective measures

### Why This Matters

Containment:

* Stops the attacker immediately
* Gives defenders time to fix vulnerabilities
* Prevents attack escalation

### ✅ Flag

```
THM{FAKEBANK-SECURED}
```

---

## 🧠 Key Takeaways

* Defensive security is about **monitoring, detection, and response**
* Alerts are the starting point of every investigation
* Identifying the attack type guides the response
* Containment prevents further damage
* Thinking like a defender means **protecting systems, not attacking them**

---

## 🚀 Room Status

✔ Suspicious activity detected
✔ Attack identified
✔ Attacker contained
✔ System secured

---

**Next Step:** Continue building blue-team skills and move toward advanced detection and response 🔵🛡️

#  Ethio Telecom Advanced Threat Detection System
**A Hybrid Machine Learning Architecture for Critical Infrastructure Protection**

##  Project Overview
This project was developed as a research initiative to protect Ethiopian national infrastructure—specifically **Ethio Telecom** and the **Telebirr** mobile money platform—from sophisticated network intrusions. Traditional firewalls rely on static signatures, which fail against invisible "Zero-Day" attacks. 

To solve this, I engineered a **Two-Stage Hybrid Anomaly Detection Pipeline** using the NSL-KDD dataset. The resulting model operates not just as a classifier, but as a live Security Operations Center (SOC) dashboard that traces attacker fingerprints (Bytes sent, Failed Logins, Root access attempts) in real-time.

---

##  The Hybrid Architecture (Two-Stage Pipeline)
Instead of relying on a single algorithm, this project utilizes a sequential gating mechanism:

* **STAGE 1: The Supervised Firewall (Random Forest):** 
  All incoming traffic is instantly scanned by a 100-tree Random Forest Multi-Class model. Evaluated using Gini Impurity, it identifies and instantly destroys 99% of historical, known threats (DoS, Probing, U2R, R2L).
* **STAGE 2: The Zero-Day Trap (Isolation Forest):**
  If a hacker disguises an attack to bypass Stage 1, the packet is passed to a Semi-Supervised Isolation Forest. Trained *exclusively* on pure, normal traffic, this algorithm calculates mathematical path lengths to isolate hidden, never-before-seen anomalies.

---

##  Key Results & Innovations
* **Precision Targeting:** Successfully mapped 39 distinct raw attack strings into 4 standard categories (DoS, Probe, U2R, R2L) for streamlined classification.
* **Class Imbalance Resolution:** Handled severe dataset imbalance by injecting **SMOTE** (Synthetic Minority Over-sampling Technique) to teach the model how to catch extremely rare (but highly destructive) root-level server breaches.
* **Minimized False Alarms:** By switching the Isolation Forest to a "Normal-Only" training paradigm, the True Negative rate reached **99%**, guaranteeing that legitimate Ethio Telecom customers would never be falsely blocked from their mobile banking apps.
* **Automated Threat Intel Dashboard:** Built a live Python simulation that tracks the exact protocol (`TCP/UDP`), service (`HTTP/Telnet`), and payload size of the attacker, generating actionable Incident Reports for system administrators.

---

## 🛠️ Technology Stack
* **Language:** Python 3
* **Libraries:** `pandas`, `NumPy`, `Scikit-Learn`, `Imbalanced-Learn (SMOTE)`
* **Visualization:** `Matplotlib`, `Seaborn`
* **Deployment Packaging:** `joblib` (.pkl serialization packaging)

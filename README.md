# Harlow & Voss Partners - Enterprise AD Security Assessment

**46-day comprehensive security assessment demonstrating the complete BUILD → ATTACK → DEFEND lifecycle.**

## 🎯 Executive Summary

This project showcases enterprise-grade security assessment combining:
- ✅ **Built** production-grade Active Directory environment (3 VMs, isolated network)
- ✅ **Attacked** with 9 realistic scenarios (MITRE ATT&CK mapped)
- ✅ **Defended** with controls & detection testing

**Key Results:**
- 1 successful compromise (pnair account via password spray)
- 33% detection coverage measured (67% blind spots identified)
- 3 compliance gaps identified (SEC/GLBA regulations)
- USD 2-5M annual breach risk quantified
- 380% ROI calculated for recommended investments

---

## 📊 What's Included

### 📄 Main Assessment Report
**File:** `HARLOW_VOSS_COMPREHENSIVE_SECURITY_ASSESSMENT_UNIFIED.pdf`

Complete professional assessment with:
- Problem statement & business context
- Executive summary (decision-maker focused)
- Assessment scope & regulatory requirements
- 9 attack scenarios with MITRE ATT&CK mapping
- 5 defensive controls implemented
- 3-priority remediation roadmap (30-90 days)
- Risk analysis & ROI calculations (380% over 5 years)
- 4 comprehensive appendices

**Audience:** C-suite, Board of Directors, Regulatory bodies

---

### 🔧 Technical Project Overview
**File:** `TECHNICAL_PROJECT_OVERVIEW.md`

Detailed technical breakdown showing:

#### **PHASE 1: BUILD THE INFRASTRUCTURE (20 days)**
- VirtualBox setup (3 VMs: DC, Workstation, Kali)
- Domain creation (harlowvoss.local)
- User accounts created (3 human + 1 service account)
- **3 critical problems solved:**
  1. Hyper-V/VirtualBox hypervisor conflict → RESOLVED
  2. Windows Server 2022 ISO boot loop (4 failed rebuilds) → RESOLVED
  3. DNS resolution failures after domain promotion → RESOLVED

#### **PHASE 2: ATTACK THE INFRASTRUCTURE (15 days)**
- 9 realistic attack scenarios executed
- 1 successful compromise (pnair account)
- Attack methodology documented with:
  - Objective
  - Technique
  - Command executed
  - Results
  - Detection capability
  - MITRE ATT&CK classification
  - Business impact

**Attacks Executed:**
1. Network Reconnaissance (Nmap)
2. LLMNR Poisoning (Responder) → Hash captured
3. Offline Dictionary Attack (Hashcat) → Failed (password protected)
4. SPN Discovery → svc-backup identified
5. **Password Spray (netexec) → pnair COMPROMISED** ✓
6. **Kerberoasting (impacket) → TGS extracted** ✓
7. **Lateral Movement → DC accessed** ✓
8. Kerberos Dictionary Attack → Failed (strong password)
9. Privilege Escalation (Theoretical)

#### **PHASE 3: DEFEND THE INFRASTRUCTURE (11 days)**
- 5 defensive controls implemented
- 5 audit policies enabled
- Phase 2 attacks re-executed with logging
- Detection measured: **33% (3 of 9 attacks detected)**

**Gaps Identified:**
- 67% detection blind spots (network-layer, offline attacks)
- No SIEM (real-time alerting missing)
- No MFA (password-spray vulnerable)
- No EDR (process-level visibility missing)

---

## 🏗️ Infrastructure Built

```
┌─────────────────────────────────────────────┐
│        HARLOW & VOSS PARTNERS LAB            │
│              HVP-LAN Network                 │
│         (192.168.60.0/24 Isolated)           │
├─────────────────────────────────────────────┤
│                                             │
│  HV-DC01                  HV-WK01           │
│  192.168.60.10            192.168.60.20     │
│  Windows Server 2022      Windows 11 Pro    │
│  ✓ Domain Controller      ✓ Domain Member   │
│  ✓ DNS, Kerberos          ✓ Workstation     │
│  ✓ LDAP, NetBIOS          ✓ User endpoint   │
│                                             │
│              ┌──────────────┐               │
│              │   Kali-66    │               │
│              │ 192.168.60.66│               │
│              │ Kali Linux   │               │
│              │ ✓ Attack Tool│               │
│              └──────────────┘               │
│                                             │
│  Domain: harlowvoss.local                   │
│  Users: rvoss, dwhitfield, pnair, svc-bkp  │
│                                             │
└─────────────────────────────────────────────┘
```

**Active Directory Configuration:**
- Domain: harlowvoss.local
- Forest/Domain Level: Windows Server 2016 Functional
- Services: DNS, Kerberos, LDAP, NetBIOS
- Users: 4 accounts (3 human, 1 service with SPN)
- Audit Policies: 5 enabled for detection testing

---

## 🎯 Key Findings

### Finding 1: CRITICAL - 56% Detection Gap
**CVSS Score: 9.0**

Windows Event Logs only detect 3 of 9 attacks (33%). Missing detections:
- Network reconnaissance (Nmap) - invisible
- LLMNR poisoning - network layer
- Offline password cracking - occurs on attacker's machine
- Service account discovery - buried in noise
- Kerberos cracking - offline

**Impact:** Compromise could persist 200+ days undetected

---

### Finding 2: CRITICAL - No MFA
**CVSS Score: 8.8**

All authentication password-only. Attack 5 (password spray) successfully compromised pnair account.

**Regulatory Violation:** GLBA Safeguards Rule Section 314.4(d) mandates MFA

---

### Finding 3: HIGH - No Centralized Monitoring (SIEM)
**CVSS Score: 7.5**

Event Viewer manual review means:
- Detection delayed (5-7 days typical)
- Cannot meet SEC 4-business-day disclosure requirement
- No real-time alerting
- No correlation between events

---

### Finding 4: CRITICAL - Regulatory Non-Compliance
- ❌ SEC Cybersecurity Disclosure Rules (no incident detection procedures)
- ❌ GLBA Safeguards Rule (no MFA, no continuous monitoring)

---

## 💰 Financial Impact

### Breach Cost Scenarios

| Scenario | Probability | Cost | Reputational |
|----------|-------------|------|-------------|
| **Data Exfiltration** | 20% | $350K-1.1M | Minimal |
| **Account Compromise** | 50% | $1.9M-4.7M | Moderate |
| **Wire Fraud** | 30% | $17.5M-87M+ | Severe |

**Annual Expected Loss:** $437,500 (17.5% breach probability × $2.5M avg)

---

## 🚀 Recommended Solution (Priority 1: 30 Days)

**Investment: $150K Year 1**

### 1. Deploy SIEM (Splunk)
- Cost: $5-6K/year
- Timeline: 2-3 weeks
- Impact: Enables real-time detection, meets SEC requirement
- Detection improvement: 33% → 85-90%

### 2. Implement MFA (Azure AD)
- Cost: $2,160/year (45 users × $4/month)
- Timeline: 2 weeks
- Impact: Prevents password spray (Attack 5)
- Compliance: Satisfies GLBA MFA requirement

### 3. Enable Kerberos Armor
- Cost: Free (native Windows feature)
- Timeline: 1 day
- Impact: Mitigates Kerberoasting attacks

### Financial Results:
- Breach probability: 15-20% → 4%
- Expected annual loss: $437K → $100K
- 5-year avoided losses: **$1,687,500**
- Net benefit: **$1,337,500**
- **ROI: 380% over 5 years**
- **Payback period: 7-17 months**

---

## 📚 Repository Structure

```
/harlow-voss-security-assessment/
│
├── README.md (this file)
│
├── TECHNICAL_PROJECT_OVERVIEW.md
│   └─ Complete BUILD→ATTACK→DEFEND breakdown
│   └─ All 9 attacks documented with commands
│   └─ Phase 1, 2, 3 detailed progress
│
├── HARLOW_VOSS_COMPREHENSIVE_SECURITY_ASSESSMENT_UNIFIED.pdf
│   └─ 110-130 page professional assessment
│   └─ Business-focused for stakeholders
│   └─ C-suite ready
│
├── APPENDICES/
│   ├── Lab_Configuration.md
│   │   └─ VM specs, network config, AD setup
│   │
│   ├── Attack_Commands.md
│   │   └─ All 9 attack commands with parameters
│   │
│   ├── Defensive_Controls.md
│   │   └─ 5 controls implemented with config
│   │
│   └── Standards_Alignment.md
│       └─ NIST, MITRE ATT&CK, OWASP, CIS, SEC, GLBA
│
└── EVIDENCE/
    └─ [Screenshot placeholders - ready for insertion]
        ├─ Figure 1: Windows Features (Hyper-V disabled)
        ├─ Figure 2: VirtualBox Storage Settings
        ├─ Figure 3: DNS Manager
        ├─ Figure 4: netexec Password Spray Output
        ├─ Figure 5: System Clock Synchronization
        ├─ Figure 6: SIEM Dashboard (future-state)
        ├─ Figure 7: MFA Setup (future-state)
        ├─ Figure 8: Risk Matrix
        ├─ Figure 9: Breach Cost Pie Chart
        └─ Figure 10: ROI Comparison
```

---

## 🛠️ Tools & Technologies

**Attack Tools:**
- Nmap 7.94 (network reconnaissance)
- Responder 3.1.4 (LLMNR poisoning)
- netexec 1.1.1 (password spray, SMB)
- impacket 0.11.0 (Kerberoasting)
- Hashcat 6.2.6 (hash cracking)

**Infrastructure:**
- VirtualBox 7.0.10 (hypervisor)
- Windows Server 2022 (domain controller)
- Windows 11 Pro (workstation)
- Kali Linux 2024.1 (attack platform)

**Frameworks:**
- NIST Cybersecurity Framework
- MITRE ATT&CK (9 techniques mapped)
- OWASP Risk Rating
- CIS Critical Controls
- SEC Cybersecurity Disclosure Rules
- GLBA Safeguards Rule

---

## 📊 Attack Results Summary

| # | Attack | Technique | Compromise | Detection | Status |
|---|--------|-----------|-----------|-----------|--------|
| 1 | Recon | Nmap scan | Systems mapped | ❌ None | ✓ |
| 2 | LLMNR Poison | Responder | Hash captured | ❌ None | ✓ |
| 3 | Dict Attack | Hashcat | Failed (good) | ❌ None | ✓ |
| 4 | SPN Discovery | impacket | Target found | ⚠️ Partial | ✓ |
| 5 | Password Spray | netexec | **pnair ✓** | ✅ Yes | ✓ |
| 6 | Kerberoasting | impacket | TGS extracted | ✅ Yes | ✓ |
| 7 | Lateral Move | netexec | DC accessed | ✅ Yes | ✓ |
| 8 | Kerberos Crack | Hashcat | Failed (good) | ❌ None | ✓ |
| 9 | Priv Escalation | Theoretical | N/A | ⚠️ Conditional | ✗ |

**Detection Coverage: 33% (3 of 9)**

---

## 🎓 Skills Demonstrated

✅ **Infrastructure Design & Deployment**
- Designed production-grade Active Directory environment
- Resolved 3 critical infrastructure problems
- Created realistic user accounts and service principals

✅ **Attack Execution & Analysis**
- Demonstrated 9 attack techniques (MITRE ATT&CK mapped)
- Executed network and endpoint attacks
- Analyzed detection capabilities and blind spots

✅ **Defense Implementation & Testing**
- Implemented 5 defensive controls
- Configured 5 audit policies
- Measured detection coverage empirically

✅ **Compliance & Risk Analysis**
- Identified SEC/GLBA regulatory gaps
- Quantified financial risk (USD 2-5M)
- Calculated ROI for investments (380%)

✅ **Technical Communication**
- Documented complete 46-day assessment
- Explained findings to business audience
- Provided actionable recommendations with timelines

---

## 📋 Assessment Phases

| Phase | Duration | Milestones | Status |
|-------|----------|-----------|--------|
| **Phase 1: BUILD** | 20 days | 3 VMs, domain, users, infrastructure problems solved | ✅ COMPLETE |
| **Phase 2: ATTACK** | 15 days | 9 scenarios, 1 compromise, attacks documented | ✅ COMPLETE |
| **Phase 3: DEFEND** | 11 days | 5 controls, audit policies, detection measured | ✅ COMPLETE |
| **TOTAL** | **46 days** | **Enterprise assessment** | ✅ COMPLETE |

---

## 🔗 Related Files

- **Full Assessment Report:** `HARLOW_VOSS_COMPREHENSIVE_SECURITY_ASSESSMENT_UNIFIED.pdf`
- **Technical Deep Dive:** `TECHNICAL_PROJECT_OVERVIEW.md` (this document)
- **Lab Configuration:** See APPENDICES/Lab_Configuration.md
- **Attack Commands:** See APPENDICES/Attack_Commands.md
- **Defensive Controls:** See APPENDICES/Defensive_Controls.md
- **Standards Alignment:** See APPENDICES/Standards_Alignment.md

---

## ⚠️ Disclaimer

This assessment was conducted in isolated laboratory environment. All findings are evidence-based and reproducible. This lab is NOT connected to any production systems. No real customers or financial data were involved.

---

## 📞 Questions?

This project demonstrates:
- Enterprise security assessment methodology
- Real-world attack simulation
- Defense implementation & testing
- Business risk quantification

Suitable for:
- Security analyst interviews
- Enterprise security roles
- Consulting engagements
- SOC analyst positions
- Security architecture discussions

---

**Assessment Complete:** July 30, 2026  
**Document Classification:** CONFIDENTIAL - Portfolio Use

*This assessment showcases the complete security lifecycle: infrastructure design, realistic attack simulation, and defensive control implementation. All findings based on empirical testing in isolated environment.*

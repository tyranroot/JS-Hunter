# 🔒 JS Key & Secret Leak Scanner

**An Enterprise-Grade Cybersecurity Scanner & Audit Utility to Detect Exposed Credentials, API Keys, Private Tokens, and Security Vulnerabilities in Public Web JavaScript Files.**

[![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

---

## 📖 Overview

In modern web development, shipping configurations or credentials inside client-side builds (JavaScript bundles, static assets, etc.) is one of the most critical avenues for credential leakages. Every single key compiled into client-side JS is readable by script crawlers, automated attackers, and security auditors.

The **JS Key & Secret Leak Scanner** is a comprehensive, full-stack cybersecurity instrument designed to audit public URLs or pasted script blocks, fetch external static scripts, run intensive heuristic regex patterns, and determine entropy ratings. Integrating the power of **TyranRoot**, this tool provides real-time security summaries and customized, step-by-step rotation/mitigation guidelines for each exposed signature.

---

## ⚡ Core Features

-   **🌐 Resource Web Crawler**: Enter any target website link. The backend engine bypasses CORS limitations, crawls the main HTML document, extracts up to 8 referenced script URLs (relative or absolute), and resolves them in parallel.
-   **🛡️ Multi-Heuristic Pattern Matcher**: Scan files against 11+ professional, high-fidelity regular expression rules configured for industry-standard keys (AWS, Google, Stripe, GitHub, Slack, JWT, Generic variable layouts).
-   **📊 Shannon Entropy Metric Calculation**: Calculates the Shannon Entropy level of detected matches to identify true randomized security tokens and eliminate basic code placeholder false positives.
-   **👁️ Interactive Secrets Inspection**: Review detected keys in a secure visual terminal context. Masked by default, keys can be toggled visibly for validation and copied instantly.
-   **📋 Preloaded Demonstration Templates**: Equipped with simulated insecure code blocks (Firebase, AWS, GitHub PATs, Stripe) to test the scanner immediately in one click.

---

## 🛠️ Security Signatures Covered

The scanner possesses built-in regular expression heuristics engineered for the following credentials:

| Signature Type | Threat Level | Heuristic Indicator Pattern | Primary Security Action |
| :--- | :---: | :---: | :--- |
| **AWS Secret Access Key** | `Critical` | `(?i)aws(.{0,20})?['"][A-Za-z0-9/+=]{40}['"]` | Immediately revoke in IAM; delete key. |
| **Stripe Secret Key** | `Critical` | `sk_live_[a-zA-Z0-9]{24,99}` | Retract from Stripe Portal; migrate server-side. |
| **Slack Incoming Webhook** | `Critical` | `hooks.slack.com/services/T.../B.../...` | Disable integration; regenerate webhook URL. |
| **Slack Bot OAuth Token** | `Critical` | `xoxb-[0-9]{11}-[0-9]{12}-[a-zA-Z0-9]{24}` | Revoke bot permissions in Slack Workspace. |
| **GitHub Access Token** | `Critical` | `ghp_[a-zA-Z0-9]{36}` / `github_pat_[0-9a-zA-Z]{82}` | Invalidate in Developer Settings; replace. |
| **Google Cloud/Maps API Key**| `High` | `AIzaSy[A-Za-z0-9-_]{35}` | Restrict using HTTP Referrers in Google Cloud. |
| **JSON Web Token (JWT)** | `High` | `eyJhbGciOi[A-Za-z0-9-_]+\.[A-Za-z0-9-_]+\....` | Re-verify signing secrets; set short exp times. |
| **Stripe Restricted Key** | `High` | `rk_live_[0-9a-zA-Z]{24,99}` | Minimise write scopes; secure permissions. |
| **Generic Secret Assignments** | `High` | `(api_key\|secret_key)\s*:=\s*['"...` | Resolve variable states on the server config. |
| **Stripe Public Key** | `Low` | `pk_live_[0-9a-zA-Z]{24,99}` | Safe client-side, but keep scopes locked. |

---


## 🚀 Setting Up Locally


### 1. Install in  Termux 
Navigate into your folder and run:
```bash
pkg update -y
pkg install git python python3 -y
git clone https://github.com/tyranroot/JS-Hunter.git
cd JS-Hunter
pip3 install -r requirements.txt
python3 JS-Hunter.py
```

### 2. Configure Environment Variables
```env
pip3 install -r requirements.txt
```
*(install all module and all dependents by pip3 .)*

### 3. Run One Line Command For Linux
```bash
sudo apt uodate -y && git clone https://github.com/tyranroot/Js-Hunter.git && cd JS-Hunter && python3 JS-Hunter.py
```

## 🥷 Project Output
```bash

┌──(TyraxZero)(tyranroot㉿TyranRoot)-[~/REPO/JS-HUNTER]
└─$ python3 JS-Hunter.py

                   ██╗███████╗    ███████╗███████╗ ██████╗██████╗ ███████╗████████╗
                   ██║██╔════╝    ██╔════╝██╔════╝██╔════╝██╔══██╗██╔════╝╚══██╔══╝
                   ██║███████╗    ███████╗█████╗  ██║     ██████╔╝█████╗     ██║
              ██   ██║╚════██║    ╚════██║██╔══╝  ██║     ██╔══██╗██╔══╝     ██║
              ╚█████╔╝███████║    ███████║███████╗╚██████╗██║  ██║███████╗   ██║
               ╚════╝ ╚══════╝    ╚══════╝╚══════╝ ╚═════╝╚═╝  ╚═╝╚══════╝   ╚═╝

      ██╗  ██╗██╗   ██╗███╗   ██╗████████╗███████╗██████╗
      ██║  ██║██║   ██║████╗  ██║╚══██╔══╝██╔════╝██╔══██╗
      ███████║██║   ██║██╔██╗ ██║   ██║   █████╗  ██████╔╝
      ██╔══██║██║   ██║██║╚██╗██║   ██║   ██╔══╝  ██╔══██╗
      ██║  ██║╚██████╔╝██║ ╚████║   ██║   ███████╗██║  ██║
      ╚═╝  ╚═╝ ╚═════╝ ╚═╝  ╚═══╝   ╚═╝   ╚══════╝╚═╝  ╚═╝

  Enter target URL: https://example.com


```

## 🤝 Contributing & Feedback

Contributions, issues, and feature requests are welcome! If you have suggestions to enhance the heuristic patterns or integrate additional third-party scanners, feel free to open a pull request or submit an issue ticket. Let's make the web a safer place together.

---

## 💖 Appreciation & Thanks

Thank you for choosing **SentinelScope**! We are deeply committed to elevating your security posture and protecting your applications from accidental credential leakages. Your trust inspires us to continuously refine our diagnostic models and engineer sophisticated defensive utilities.

If this scanner has helped you audit, identify, or secure an exposed token in your build pipeline, please consider giving it a ⭐ on GitHub and sharing it with your cybersec & development team!

---

## 📧 Connect & Support

Have questions, collaboration proposals, or custom penetration testing requests? Feel free to reach out to our primary channels:

*   **💻 GitHub Profile**: [TyranRoot](https://github.com/tyranroot)
*   **📧 Email**: [TyranRoot ](mailto:tyranroot@gmail.com) 
*   **🔵 Facebook**: [TyranRoot](https://www.facebook.com/profile.php?id=61585652805918) 
*   **📸 Instagram Hub**: [TyranRoot](https://instagram.com/tyranroot) 
*   **🎵 TikTok**: [TyranRoot](https://www.tiktok.com/@tyranroot?is_from_webapp=1&sender_device=pc)


---







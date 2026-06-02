# 🔒 JS Key & Secret Leak Scanner

**An Enterprise-Grade Cybersecurity Scanner & Audit Utility to Detect Exposed Credentials, API Keys, Private Tokens, and Security Vulnerabilities in Public Web JavaScript Files.**

[![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

---

## 📖 Overview

In modern web development, shipping configurations or credentials inside client-side builds (JavaScript bundles, static assets, etc.) is one of the most critical avenues for credential leakages. Every single key compiled into client-side JS is readable by script crawlers, automated attackers, and security auditors.

The **JS Key & Secret Leak Scanner** is a comprehensive, full-stack cybersecurity instrument designed to audit public URLs or pasted script blocks, fetch external static scripts, run intensive heuristic regex patterns, and determine entropy ratings. Integrating the power of **Google Gemini 3.5-Flash**, this tool provides real-time security summaries and customized, step-by-step rotation/mitigation guidelines for each exposed signature.

---

## ⚡ Core Features

-   **🌐 Resource Web Crawler**: Enter any target website link. The backend engine bypasses CORS limitations, crawls the main HTML document, extracts up to 8 referenced script URLs (relative or absolute), and resolves them in parallel.
-   **🛡️ Multi-Heuristic Pattern Matcher**: Scan files against 11+ professional, high-fidelity regular expression rules configured for industry-standard keys (AWS, Google, Stripe, GitHub, Slack, JWT, Generic variable layouts).
-   **📊 Shannon Entropy Metric Calculation**: Calculates the Shannon Entropy level of detected matches to identify true randomized security tokens and eliminate basic code placeholder false positives.
-   **👁️ Interactive Secrets Inspection**: Review detected keys in a secure visual terminal context. Masked by default, keys can be toggled visibly for validation and copied instantly.
-   **🔮 Deep Gemini AI Security Auditing**: Clicking "Audit with Gemini" sends the context snippet to Gemini. It automatically generates a specialized detailed threat assessment, exploit vectors, and a step-by-step mitigation handbook.
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

## 🏗️ Technical Architecture

### Backend Stack (`/server.ts`)
-   **Express Framework**: Coordinates clean API endpoints and handles streaming static assets.
-   **Fetch Parser**: Grabs target code elements and reads script URLs safely.
-   **Shannon Entropy Engine**: Custom TypeScript implementation tracking data patterns.
-   **Google GenAI SDK**: Integrates `@google/genai` to lazily instantiate Gemini calls.

### Frontend Stack (`/src/`)
-   **Vite**: The fast web server powering rapid rendering.
-   **React 19**: Modern component lifecycle, custom states, and modular layouts.
-   **Tailwind CSS**: Modern utility classes establishing a high-contrast slate aesthetic.
-   **Lucide Icons**: Beautiful, clean vector security icons.
-   **React-Markdown**: Safely rendering structural markdown code generated by the security model.

---

## 🚀 Setting Up Locally


### 1. Install in  Termux 
Navigate into your folder and run:
```bash
pkg update -y
https://github.com/tyranroot/JS-Hunter.git
cd JS-Hunter
pip3 install -r requirements.txt
python3 JS-Hunter.py
```

### 2. Configure Environment Variables
```env
pip3 install -r requirements.txt
```
*(No client-side configs are needed. The API key is fully restricted on server processes.)*

### 3. Run One Line Command in Linux
```bash
sudo apt uodate -y && git clone https://github.com/tyranroot/Js-Hunter.git && cd JS-Hunter && python3 JS-Hunter.py
```


---

## 🔐 Remediation Recommendations (Global Advice)

If a leak is identified inside your production environment, follow these universal security steps:
1.  **Immediate Revocation (Revoke Key/Token)**: Place high priority on deleting or revoking the exposed token in the corresponding provider portal (e.g. AWS Console, Google Cloud Portal, Stripe Dashboard) to prevent external exploitation.
2.  **Environment Variable Integration**: Relocate any sensitive credentials to secure environment variables, accessing them dynamically inside server-side scripts (e.g. `process.env.API_KEY`).
3.  **Implement Reference Restrictions**: For keys that must reside client-side (such as Google Maps/Maps API), apply strict domain, HTTP referrer, or IP restrictions in the developer console to prevent execution from external URL sources.

---

## 📄 License & Terms

Authorized for security auditing, penetration testing, and software development quality checks. 

**License**: Distributed under the standard **MIT License**. Check individual file headers for specific copyright properties.

---
*Created as a verified cybersecurity utility to promote web vulnerability reduction.*

# Browser Security Posture Assessment

A single-file, self-contained web tool that **safely simulates modern web attacks against your existing security stack** (Secure Web Gateway, firewall, endpoint agent, or enterprise browser) and grades how well your controls hold up.

It combines — and expands on — the capabilities of public browser-security assessment platforms such as **browser.security** (Last Mile Reassembly testing) and **BrowserTotal** (browser posture, fingerprint, hardening and extension analysis), all in one page with **no installation and no data collection**.

> **Everything runs locally in the browser** and uses only universally-recognized, **benign test artifacts** (the EICAR standard, the Palo Alto Networks Wildfire test PE, AMTSO test pages, and synthetic non-real canary data). The host machine is never exposed to actual malware, real credentials are never transmitted, and no real PII is used.

## Why this matters

Legacy network security inspects traffic *as it flies by over the wire*. Modern attacks defeat this by reassembling the malicious file, script, or phishing page **inside the browser's memory**, after the traffic has already cleared inspection. This suite checks whether your controls see what actually happens at the last mile — in the browser itself.

## How to use it

1. Open `index.html` (or the hosted page) in the browser/environment you want to test.
2. Click **Run Full Assessment** to execute the analytical modules automatically, or work through each tab manually.
3. For attack simulations, click each **dashboard tile** to record whether your stack **Blocked 🛡️** or **Bypassed ❌** the test. The **Posture Score** gauge updates live (Grade A–F).
4. Use **Export Scorecard 📥** to save a PNG of the dashboard for audits and reports.

Run it first in a baseline environment (network controls only), then again inside your protected environment, and compare the scores.

---

## Assessment categories

The tool is organized into six tabbed categories covering **15 tests**.

### 📁 Malicious Files — Last Mile Reassembly (Tests 1–8)
Benign EICAR / Wildfire test payloads delivered via client-side reassembly techniques that bypass network file scanning:

1. **Web-Worker Malware Chunking** — file pulled in micro-chunks and reassembled off the main thread.
2. **Web-Worker File Smuggling** — Base64 string decoded into a binary inside a background worker.
3. **Polymorphic JavaScript** — a unique, randomized script signature is generated on every run.
4. **Quishing (Airgap Jump)** — QR code shifts execution to an unmanaged mobile device.
5. **Advanced SVG Smuggling** — payload hidden in the metadata of an invisible SVG element.
6. **Browser-Based Crypto-Jacking** — hidden workers hijack the CPU and beacon to a mining pool.
7. **WebSocket + Malware** — payload streamed over an encrypted `wss://` tunnel.
8. **Malicious Obfuscation** — payload fragmented into hex/unicode-escaped variables.

### 🎣 Phishing (Test 9)
- **Locally-rendered phishing page** — a benign, inert mock corporate login page reassembled in the browser (no data is sent) to test DOM-level detection.
- **Phishing-URL reachability** — checks whether your filter blocks known phishing test URLs.

### 🌐 Malicious Sites & URL Scanner (Tests 10–11)
- **URL & Domain Risk Scanner** — a client-side heuristic engine flagging homograph/punycode look-alikes, IP-literal hosts, embedded credentials, risky TLDs, deep subdomains and brand impersonation, with a risk score.
- **Malicious-Site Category Blocking** — attempts to reach industry-standard AMTSO / Palo Alto test URLs to confirm your SWG category filtering works.

### 🔓 Web DLP / Data Exfiltration (Test 12)
Attempts to exfiltrate **synthetic canary data** (a documented Visa test card number, a fake SSN pattern, a unique canary token, or a sample secret key) over three channels — `fetch()` JSON, form-style POST, and a query-string beacon — to find gaps where your Data Loss Prevention controls fail to redact or block.

### 🧬 Browser Posture & Fingerprint (Test 13)
A read-only enumeration of everything a website can silently learn about your device: user agent, OS, CPU/memory, screen, timezone, GPU renderer (WebGL), a canvas fingerprint hash, and a **WebRTC local-IP leak** check.

### 🔒 Hardening & Extensions (Tests 14–15)
- **Security-Hardening Checklist** — verifies secure context, Web Crypto, Trusted Types, cross-origin isolation, Permissions Policy and more, with pass/warn/fail and a score.
- **Extension Exposure Probe** — privacy-respecting heuristic detection of active extensions (wallets, password managers, Grammarly, dev tools, content blockers) that hold page-level access.

---

**Disclaimer:** This tool is strictly for **authorized, educational, and defensive security testing** of environments you own or are permitted to assess. It uses only benign, industry-standard test strings and synthetic data so that security heuristics can be triggered without exposing the host to real risk, malware, credential theft, or live data loss.

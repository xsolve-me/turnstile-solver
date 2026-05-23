# Cloudflare Challenge Solver (Turnstile & IUAM)

[![Website](https://img.shields.io/badge/Website-xsolve.me-blue?style=for-the-badge&logo=google-chrome)](https://xsolve.me)
[![Documentation](https://img.shields.io/badge/Docs-docs.xsolve.me-green?style=for-the-badge&logo=gitbook)](https://docs.xsolve.me/)

A high-performance, ultra-fast API solver for **Cloudflare Turnstile** and **Cloudflare IUAM (Under Attack Mode)** challenges. Designed for seamless, automated web scraping, data extraction, and bot automation.

---

## 📊 Screenshot

![Xsolve API Solver Screenshot](image.png)

---

## 🔗 Links
* **Website:** [https://xsolve.me](https://xsolve.me)
* **Documentation:** [https://docs.xsolve.me/](https://docs.xsolve.me/)

---

## ✨ Features
* 🚀 **High Speed:** Solves under **1-4s**
* 🛡️ **Advanced Bypass:** Bypasses Turnstile (`task.turnstile`) and IUAM (`task.iuam`) defense layers.
* 💳 **Pay-Per-Solve:** 100% success-only billing policy.
* 🔌 **Simple Integration:** Integrate easily using HTTP requests in Python, JavaScript, Curl, Go, PHP, etc.

---

## 💰 Pricing & Available Tasks

We offer high-performance solvers at competitive prices:

| Available Task | Task Identifier | Price (per 1k requests) |
| :--- | :--- | :--- |
| **Cloudflare Turnstile** | `task.turnstile` | **$0.08** |
| **Cloudflare IUAM** | `task.iuam` | **$0.08** |

* ⚡ **Cost:** **$0.00008** per one solve
* ✔️ **Only pay for successful solves**
* 🪙 **Payment Method:** **Cryptocurrency**

### 💳 Deposit Bonuses

Get extra balance when you deposit more! Maximum deposit: **$500**.

| Deposit Range | Bonus | Example |
| :--- | :--- | :--- |
| Under $25 | 0% | $10 → $10 balance |
| $25 – $49 | **20%** | $30 → $36 balance |
| $50 – $99 | **30%** | $75 → $97.50 balance |
| $100 – $500 | **40%** | $200 → $280 balance |

### 💰 Deposit Value Examples

That's over **12,500** CAPTCHAs solved for just a single dollar!

| Deposit Amount | Bonus | Total Balance | Solves / Tokens |
| :--- | :--- | :--- | :--- |
| **$1** | — | $1 | 12,500 (12.5k) |
| **$5** | — | $5 | 62,500 (62.5k) |
| **$25** | +$5 | $30 | 375,000 (375k) |
| **$50** | +$15 | $65 | 812,500 (812.5k) |
| **$100** | +$40 | $140 | 1,750,000 (1.75m) |
| **$500** | +$200 | $700 | 8,750,000 (8.75m) |

## 🚀 Quick Integration (Python)

To integrate our solver into your application, use the following simple Python example:

```python
import requests

url = "https://api.xsolve.me/task"

headers = {
    "X-Api-Key": "YOUR_API_KEY",
    "Content-Type": "application/json"
}

payload = {
    "mode": "turnstile",
    "url": "https://example.com",  # Replace with the target site URL
    "sitekey": "0x4AAAAAA..."      # Replace with the target Turnstile sitekey
}

response = requests.post(url, headers=headers, json=payload)
print(response.json())
```

For full API documentation, other languages (Curl, JavaScript), and custom integrations, check our [Documentation](https://docs.xsolve.me/) or log in to your dashboard at [xsolve.me](https://xsolve.me).

---

## 💬 Community & Support
* **Telegram Channel:** [https://t.me/rex_update](https://t.me/rex_update)
* **Discord Server:** [https://discord.gg/eM6wqY7z53](https://discord.gg/eM6wqY7z53)

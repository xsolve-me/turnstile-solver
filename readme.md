# Xsolve - Cloudflare Turnstile & IUAM Solver API

[![Website](https://img.shields.io/badge/Website-xsolve.me-0ea5e9?style=for-the-badge)](https://xsolve.me)
[![Docs](https://img.shields.io/badge/Docs-docs.xsolve.me-22c55e?style=for-the-badge)](https://docs.xsolve.me/)
[![Telegram](https://img.shields.io/badge/Telegram-@xsolveupdates-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/xsolveupdates)
[![Discord](https://img.shields.io/badge/Discord-Join-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/eM6wqY7z53)

HTTP API for **Cloudflare Turnstile** and **Cloudflare IUAM (Under Attack Mode)**.

Send a JSON request. Get a Turnstile token or a `cf_clearance` cookie back, typically in **1–4 seconds**. One endpoint, one API key, one price.

| Requests processed | Target uptime | Average solve time | Price |
| :----------------: | :-----------: | :----------------: | :---: |
| 500m+ | 99.9% | < 3s | **$0.08 / 1k** |

Failed solves are not billed.

---

## Dashboard

![Xsolve request history: Turnstile solves completing in 1.1–1.7s at $0.00008 each](image.png)

Create an account, copy your API key, and watch live request history at [xsolve.me](https://xsolve.me).

---

## Features

- **Fast:** typical solve time is 1–4 seconds
- **Two task types:** Turnstile (`task.turnstile`) and IUAM (`task.iuam`)
- **Pay for success only:** unsuccessful solves are free
- **One JSON endpoint:** `POST https://api.xsolve.me/task`
- **Proxy support:** HTTP, HTTPS, and SOCKS5
- **Drop-in migration:** swap the base URL and API key if you already use Solverify, NSLSolver, CapSolver, 2Captcha, Anti-Captcha, and similar solvers

---

## How it works

1. Create an account at [xsolve.me](https://xsolve.me) and copy your API key.
2. `POST` the challenge `url` (and `sitekey` for Turnstile) to `/task`.
3. Use the returned token, or replay the `cf_clearance` cookie and `User-Agent` through the same proxy.

---

## Pricing

One flat rate for both task types. No tiers.

| Task | Identifier | Price |
| ---- | ---------- | ----- |
| Cloudflare Turnstile | `task.turnstile` | **$0.08 / 1k** |
| Cloudflare IUAM | `task.iuam` | **$0.08 / 1k** |

- **$0.00008** per successful solve
- Unsuccessful solves are free
- Payment: **cryptocurrency**

### Deposit bonuses

| Deposit | Bonus | Example |
| ------- | ----- | ------- |
| Under $25 | - | $10 → $10 |
| $25 – $49 | **20%** | $30 → $36 |
| $50 – $99 | **30%** | $75 → $97.50 |
| $100 – $500 | **40%** | $200 → $280 |

### What $1 actually buys

About **12,500** successful solves per dollar at the base rate.

| Deposit | Bonus | Balance | Solves |
| ------- | ----- | ------- | ------ |
| $1 | - | $1 | 12,500 |
| $5 | - | $5 | 62,500 |
| $25 | +$5 | $30 | 375,000 |
| $50 | +$15 | $65 | 812,500 |
| $100 | +$40 | $140 | 1,750,000 |
| $500 | +$200 | $700 | 8,750,000 |

---

## Migration

Coming from Solverify, NSLSolver, CapSolver, 2Captcha, Anti-Captcha, CapMonster, NextCaptcha, EzCaptcha, NopeCHA, or DeathByCaptcha? Most integrations only need two changes:

1. Base URL → `https://api.xsolve.me`
2. API key → your Xsolve key

See the [migration guide](https://docs.xsolve.me/migration).

---

## Quick start

All requests use the same endpoint and header:

```http
POST https://api.xsolve.me/task
X-Api-Key: YOUR_API_KEY
Content-Type: application/json
```

### Turnstile

```python
import requests

response = requests.post(
    "https://api.xsolve.me/task",
    headers={"X-Api-Key": "YOUR_API_KEY"},
    json={
        "mode": "turnstile",
        "url": "https://example.com",
        "sitekey": "0x4AAAAAA...",
    },
)

print(response.json())
```

**Success**

```json
{
  "token": "0.3g00PIzENb3goEq4-D.....",
  "elapsed": "1.55s",
  "status": "completed"
}
```

| Field | Required | Description |
| ----- | -------- | ----------- |
| `mode` | yes | Must be `turnstile` |
| `url` | yes | Page that hosts the widget |
| `sitekey` | yes | Turnstile sitekey |
| `action` | no | Widget `action`, e.g. `login` |
| `cdata` | no | Widget `cData` |
| `proxy` | no | `http://`, `https://`, or `socks5://` |

Send `action` and `cdata` only when the target widget provides them.

### IUAM (Under Attack Mode)

A proxy is **required** for IUAM tasks.

```python
import requests

response = requests.post(
    "https://api.xsolve.me/task",
    headers={"X-Api-Key": "YOUR_API_KEY"},
    json={
        "mode": "iuam",
        "url": "https://example.com",
        "proxy": "socks5://user:pass@host:port",
    },
)

print(response.json())
```

**Success**

```json
{
  "headers": {
    "Cookie": "cf_clearance=cZ3ow5J194Lyer0BTI64.....;",
    "User-Agent": "Mozilla/5.0 ..."
  },
  "ip": "127.0.0.1",
  "elapsed": "1.55s",
  "status": "completed"
}
```

Replay the returned `Cookie` and `User-Agent` on later requests through the **same proxy**. The clearance is tied to that IP and user agent.

| Field | Required | Description |
| ----- | -------- | ----------- |
| `mode` | yes | Must be `iuam` |
| `url` | yes | IUAM challenge page URL |
| `proxy` | yes | `http://`, `https://`, or `socks5://` |

### cURL

```bash
curl -X POST https://api.xsolve.me/task \
  -H "X-Api-Key: YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "mode": "turnstile",
    "url": "https://example.com",
    "sitekey": "0x4AAAAAA..."
  }'
```

### Errors

Failed solves return a JSON body and are **not billed**.

```json
{
  "message": "An error occurred",
  "status": "failed"
}
```

JavaScript, Go, Java, Rust examples and the full field reference: [docs.xsolve.me](https://docs.xsolve.me/).

---

## Support

| | |
| --- | --- |
| Website | [xsolve.me](https://xsolve.me) |
| Documentation | [docs.xsolve.me](https://docs.xsolve.me/) |
| Telegram | [t.me/xsolveupdates](https://t.me/xsolveupdates) |
| Discord | [discord.gg/eM6wqY7z53](https://discord.gg/eM6wqY7z53) |

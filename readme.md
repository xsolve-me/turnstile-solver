# Xsolve - Cloudflare Turnstile & IUAM Solver API

[![Website](https://img.shields.io/badge/Website-xsolve.me-0ea5e9?style=for-the-badge)](https://xsolve.me)
[![Docs](https://img.shields.io/badge/Docs-docs.xsolve.me-22c55e?style=for-the-badge)](https://docs.xsolve.me/)
[![Telegram](https://img.shields.io/badge/Telegram-@xsolveupdates-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/xsolveupdates)
[![Discord](https://img.shields.io/badge/Discord-Join-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/eM6wqY7z53)

Low-latency HTTP API for **Cloudflare Turnstile** and **Cloudflare IUAM (Under Attack Mode)**. Send a JSON request, get a token or clearance cookie back, typically in **1-4 seconds**.

| Requests processed | Target uptime | Average solve time | Price |
| :----------------: | :-----------: | :----------------: | :---: |
| 500m+ | 99.9% | &lt; 3s | **$0.08 / 1k** |

You only pay for successful solves.

---

## Request Example

![Xsolve request history showing Turnstile solves around 1.1-1.7s at $0.00008 each](image.png)

Balance, API keys, and live request history live in one place: [xsolve.me](https://xsolve.me).

---

## Features

- **Fast:** Typical solve time is 1-4 seconds
- **Two task types:** Turnstile (`task.turnstile`) and IUAM (`task.iuam`)
- **Pay for success only:** Failed solves are not billed
- **Simple JSON API:** One `POST` to `https://api.xsolve.me/task`
- **Proxy support:** HTTP, HTTPS, and SOCKS5
- **Drop-in migration:** Coming from Solverify, NSLSolver, or CapSolver? Change the base URL and API key

---

## How it works

1. Create an account at [xsolve.me](https://xsolve.me) and copy your API key
2. `POST` the challenge `url` (and `sitekey` for Turnstile) to `/task`
3. Use the returned token or `cf_clearance` cookie in your request

---

## Pricing

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
| Under $25 | - | $10 -> $10 |
| $25 - $49 | **20%** | $30 -> $36 |
| $50 - $99 | **30%** | $75 -> $97.50 |
| $100 - $500 | **40%** | $200 -> $280 |

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

If you already use Solverify, NSLSolver, or CapSolver, most integrations only need two changes:

1. Base URL → `https://api.xsolve.me`
2. API key → your Xsolve key

See the [migration guide](https://docs.xsolve.me/migration).

---

## Quick start

All requests use the same endpoint and header:

```
POST https://api.xsolve.me/task
X-Api-Key: YOUR_API_KEY
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

Optional Turnstile fields when the widget provides them:

| Field | Required | Description |
| ----- | -------- | ----------- |
| `mode` | yes | Must be `turnstile` |
| `url` | yes | Page that hosts the widget |
| `sitekey` | yes | Turnstile sitekey |
| `action` | no | Widget `action`, e.g. `login` |
| `cdata` | no | Widget `cData` |
| `proxy` | no | `http://`, `https://`, or `socks5://` |

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

Replay the returned `Cookie` and `User-Agent` on subsequent requests through the **same proxy**.

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

More languages (JavaScript, Go, Java, Rust) and the full field reference: [docs.xsolve.me](https://docs.xsolve.me/).

---

## Support

| | |
| --- | --- |
| Website | [xsolve.me](https://xsolve.me) |
| Documentation | [docs.xsolve.me](https://docs.xsolve.me/) |
| Telegram | [t.me/xsolveupdates](https://t.me/xsolveupdates) |
| Discord | [discord.gg/eM6wqY7z53](https://discord.gg/eM6wqY7z53) |

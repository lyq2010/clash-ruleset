# clash-ruleset

[简体中文](README.md) | **English**

[![Stars](https://img.shields.io/github/stars/lyq2010/clash-ruleset?style=flat-square&logo=github)](https://github.com/lyq2010/clash-ruleset/stargazers)
[![Forks](https://img.shields.io/github/forks/lyq2010/clash-ruleset?style=flat-square&logo=github)](https://github.com/lyq2010/clash-ruleset/network/members)
[![Last Commit](https://img.shields.io/github/last-commit/lyq2010/clash-ruleset?style=flat-square)](https://github.com/lyq2010/clash-ruleset/commits/main)
[![Repo Size](https://img.shields.io/github/repo-size/lyq2010/clash-ruleset?style=flat-square)](https://github.com/lyq2010/clash-ruleset)
[![License](https://img.shields.io/github/license/lyq2010/clash-ruleset?style=flat-square)](LICENSE)

A personal [Mihomo](https://github.com/MetaCubeX/mihomo) (Clash.Meta) configuration and custom rule set.

It ships a main config `clash.yaml` for use with [Sub-Store](https://github.com/sub-store-org/Sub-Store), plus several self-hosted custom rule lists (`.list`) loaded remotely via `rule-providers` — so rules can be tweaked without touching the main config.

## ✨ Features

- **TUN mode** — `mixed` stack with `auto-route` / `auto-redirect` for transparent system-wide proxying.
- **Fake-IP DNS** — `enhanced-mode: fake-ip`; domestic DoH (AliDNS, DNSPod) for resolution, Cloudflare / Google as fallback, with GEOIP-CN fallback filtering.
- **Traffic sniffing** — sniffs HTTP / TLS / QUIC, skipping common domestic domains (Baidu, QQ, etc.).
- **Fine-grained routing** — dedicated groups per service (YouTube, Google, AI, GitHub, Microsoft, Telegram, Netflix, TikTok, PayPal, Apple, Steam, …), each with regional preference.
- **Per-region auto latency test** — Hong Kong / Japan / Singapore / United States / Taiwan, each with a `url-test` auto group and a manual selection group.
- **Ad blocking** — anti-AD rules; matched traffic is `REJECT`ed.

## 📁 Files

| File | Purpose |
| --- | --- |
| `clash.yaml` | Mihomo main config, consumed by **Sub-Store** to generate subscriptions for **mobile devices** |
| `direct.list` | Force-direct domains (UGREEN Cloud, PT-site trackers, airport updates, Samsung, Nvidia, Razer, Kaspersky, …) |
| `default-proxy.list` | Force-proxy domains (PT sites, selected frequently-used sites) |
| `Binance.list` | Binance-related domains |
| `mail.list` | Mail service domains (Proton, mail.com) |
| `docker.list` | Docker-related domains, used **standalone by OpenClash on the router** (not referenced by `clash.yaml`) |

## 🚀 Usage

### Mobile (clash.yaml + Sub-Store)

> ⚠️ `clash.yaml` contains **no nodes** by itself — every proxy group selects nodes from your subscription via `include-all: true`, so an airport subscription is required.

1. Add your airport subscription in Sub-Store.
2. Apply this repo's `clash.yaml` as the mihomo config template.
3. Import the Sub-Store-generated subscription link into a Mihomo-core client (Mihomo Party / Clash Verge Rev / ClashX Meta, …).
4. Custom rule lists are pulled automatically from this repo's `main` branch via `rule-providers`, refreshed every 24 hours.

### Router (docker.list + OpenClash)

`docker.list` is an independently maintained list of Docker-related domains, referenced by OpenClash on the router — separate from and unaffected by `clash.yaml`.

## 🔗 Custom Rule Subscription URLs

```
https://raw.githubusercontent.com/lyq2010/clash-ruleset/refs/heads/main/direct.list
https://raw.githubusercontent.com/lyq2010/clash-ruleset/refs/heads/main/default-proxy.list
https://raw.githubusercontent.com/lyq2010/clash-ruleset/refs/heads/main/Binance.list
https://raw.githubusercontent.com/lyq2010/clash-ruleset/refs/heads/main/mail.list
https://raw.githubusercontent.com/lyq2010/clash-ruleset/refs/heads/main/docker.list
```

## 📌 Routing Priority (top to bottom)

Private/direct domains → custom group → Apple → AI / GitHub / per-service groups → China domains (direct) → service IP ranges → China IPs (direct) → ad blocking (REJECT) → Steam → fallback (default proxy).

## ⚠️ Notes

- The config contains personal-specific IPs (e.g. `43.167.173.84`), domains and grouping habits — adjust before reuse.
- Public rule sources: [MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat), [anti-AD](https://github.com/privacy-protection-tools/anti-AD), [blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script).

## 📄 License

[MIT](LICENSE) © lyq2010

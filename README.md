# clash-ruleset

**简体中文** | [English](README.en.md)

[![Stars](https://img.shields.io/github/stars/lyq2010/clash-ruleset?style=flat-square&logo=github)](https://github.com/lyq2010/clash-ruleset/stargazers)
[![Forks](https://img.shields.io/github/forks/lyq2010/clash-ruleset?style=flat-square&logo=github)](https://github.com/lyq2010/clash-ruleset/network/members)
[![Last Commit](https://img.shields.io/github/last-commit/lyq2010/clash-ruleset?style=flat-square)](https://github.com/lyq2010/clash-ruleset/commits/main)
[![Repo Size](https://img.shields.io/github/repo-size/lyq2010/clash-ruleset?style=flat-square)](https://github.com/lyq2010/clash-ruleset)
[![License](https://img.shields.io/github/license/lyq2010/clash-ruleset?style=flat-square)](LICENSE)

个人自用的 [Mihomo](https://github.com/MetaCubeX/mihomo)(Clash.Meta)配置与自定义分流规则集。

包含一份用于 [Sub-Store](https://github.com/sub-store-org/Sub-Store) 的 mihomo 主配置 `clash.yaml`,以及若干自托管的自定义规则列表(`.list`),通过 `rule-providers` 远程加载,方便随时增删而无需改动主配置。

## ✨ 特性

- **TUN 模式**:`mixed` 协议栈 + `auto-route` / `auto-redirect`,全局透明代理。
- **Fake-IP DNS**:`enhanced-mode: fake-ip`,国内 DoH(阿里、腾讯)解析,国外走 Cloudflare / Google 兜底,并按 GEOIP-CN 回退。
- **流量嗅探(Sniffer)**:对 HTTP / TLS / QUIC 嗅探,跳过百度、QQ 等常见国内域名。
- **精细化分流**:按服务(YouTube、Google、AI、GitHub、Microsoft、Telegram、Netflix、TikTok、PayPal、Apple、Steam 等)独立分组,各组按地区优选。
- **地区节点自动测速**:香港 / 日本 / 新加坡 / 美国 / 台湾,各有 `url-test` 自动组与手动选择组。
- **去广告**:接入 anti-AD 规则,命中即 `REJECT`。

## 📁 文件说明

| 文件 | 用途 |
| --- | --- |
| `clash.yaml` | Mihomo 主配置,用于 **Sub-Store** 生成订阅,专供**移动端设备**使用 |
| `direct.list` | 强制直连域名(绿联云、PT 站 Tracker、机场更新、三星、Nvidia、雷蛇、卡巴斯基等) |
| `default-proxy.list` | 强制走代理域名(PT 站、部分常用网站) |
| `Binance.list` | 币安相关域名 |
| `mail.list` | 邮箱服务域名(Proton、mail.com) |
| `docker.list` | Docker 相关域名,供**路由器端 OpenClash 单独使用**(不接入 `clash.yaml`) |

## 🚀 使用方法

### 移动端(clash.yaml + Sub-Store)

> ⚠️ `clash.yaml` 本身**不含任何节点**,所有代理组通过 `include-all: true` 从订阅中筛选节点,需配合机场订阅使用。

1. 在 Sub-Store 中添加你的机场订阅。
2. 将本仓库的 `clash.yaml` 作为 mihomo 配置模板套用。
3. 在 Mihomo 内核客户端(Mihomo Party / Clash Verge Rev / ClashX Meta 等)中导入 Sub-Store 生成的订阅链接。
4. 自定义规则列表已通过 `rule-providers` 自动从本仓库 `main` 分支拉取,每 24 小时更新一次。

### 路由器端(docker.list + OpenClash)

`docker.list` 为独立维护的 Docker 相关域名列表,供路由器上的 OpenClash 引用,与 `clash.yaml` 互不影响。

## 🔗 自定义规则订阅地址

```
https://raw.githubusercontent.com/lyq2010/clash-ruleset/refs/heads/main/direct.list
https://raw.githubusercontent.com/lyq2010/clash-ruleset/refs/heads/main/default-proxy.list
https://raw.githubusercontent.com/lyq2010/clash-ruleset/refs/heads/main/Binance.list
https://raw.githubusercontent.com/lyq2010/clash-ruleset/refs/heads/main/mail.list
https://raw.githubusercontent.com/lyq2010/clash-ruleset/refs/heads/main/docker.list
```

## 📌 分流优先级(自上而下)

直连私有域名 → 自用分组 → Apple → AI / GitHub / 各大服务 → 国内域名直连 → 服务 IP 段 → 国内 IP 直连 → 去广告拦截 → Steam → 漏网之鱼(默认代理)。

## ⚠️ 注意事项

- 配置中包含个人专属的 IP(如 `43.167.173.84`)、域名与分组习惯,直接套用前请按需调整。
- 公开规则集主要来源:[MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat)、[anti-AD](https://github.com/privacy-protection-tools/anti-AD)、[blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script)。

## 📄 License

[MIT](LICENSE) © lyq2010

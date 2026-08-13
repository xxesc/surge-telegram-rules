# Surge Telegram 分流规则


把 Telegram 的域名和服务器 IP 段分流到代理节点，解决国内无法直连 Telegram 的问题。

## 使用方法

### 方式一：内联规则（推荐，不依赖外部规则集）

把 [surge-telegram-rules.conf](surge-telegram-rules.conf) 中 `[Rule]` 段的内容粘贴到 Surge 配置的 `[Rule]` 区域（放在 `FINAL` 规则之前）。

> 规则里的目标策略默认是 `Proxy`，如果你的配置里策略组叫别的名字（如 `节点选择`、`🚀 代理` 等），替换成你自己的策略组名即可。

### 方式二：RULE-SET 精简版

用 [telegram.list](telegram.list)（规则集格式，不含策略名），策略写在 RULE-SET 行上：

```ini
[Rule]
# 本地文件（下载 telegram.list 到 Surge 的 App Group 目录后引用）
RULE-SET,/private/var/mobile/Containers/Shared/AppGroup/<你的SurgeAppGroupID>/telegram.list,Proxy

# 或者用 URL（jsDelivr CDN，国内可访问，自动更新）
RULE-SET,https://cdn.jsdelivr.net/gh/xxesc/surge-telegram-rules@main/telegram.list,Proxy
```

> ⚠️ RULE-SET 引用的文件必须是**规则集格式**（每行 `类型,值`，不带策略名、没有 `[Rule]` 段头）。
> 不要用 surge-telegram-rules.conf 当规则集文件，否则会报「外部规则集解析失败」。

## 规则内容

- **域名**：t.me、telegram.org、telegram.me、telegram.dog、telesco.pe、telegra.ph、cdn-telegram.org、tdesktop.com
- **IP 段**：Telegram 官方服务器 CIDR（91.108.0.0/16 系列、149.154.160.0/20、185.76.151.0/24 及 IPv6 段）
- 所有 IP 规则带 `no-resolve`，避免对域名触发多余 DNS 解析

## 许可

MIT License

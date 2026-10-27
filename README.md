# openwrt-ipk-24.10-x86_64

ImmortalWrt **24.10.x / x86_64** 固件用的第三方 IPK 集合，供 ImageBuilder 构建时预装。

所有包取自 `https://down.dllkids.xyz/openwrt-feed/24.10/x86_64/`，
下载后已逐一核对索引中的 SHA256，并验证包内二进制的真实架构为 **ELF 64-bit x86-64**。

## 目录结构

```
.
├── x86_64/          # 全部 ipk
├── packages.txt     # 要装进固件的包名（每行一个）
├── SHA256SUMS       # 校验和
└── README.md
```

## 包含的包

| 功能 | 包 | 版本 | 说明 |
|---|---|---|---|
| 远程控制 | `ddnsto` | 4.2.2~8664-r1 | 含 `ddnstod`（x86-64 ELF），需在 ddnsto.com 取 token |
| 远程控制 | `luci-app-ddnsto` | 27.177.41028~3d34244 | LuCI 前端 |
| DNS 去广告 | `adguardhome` | 0.107.79-r1 | 含 `AdGuardHome`（x86-64 ELF） |
| DNS 去广告 | `luci-app-adguardhome` | 27.202.38035~0934b9c | LuCI 前端 |
| DNS | `luci-app-smartdns` | 27.189.38192~eead6d6 | 前端；`smartdns` 核心取自官方源 |
| 流量监控 | `bandix` | 0.12.10-r1 | 含 `bandix`（x86-64 ELF） |
| 流量监控 | `luci-app-bandix` | 27.299.55398~ced9e3e | LuCI 前端 |
| 应用过滤 | `appfilter` | 7.0.1-r1 | 含 `oafd`（x86-64 ELF），OpenAppFilter 后端 |
| 应用过滤 | `luci-app-oaf` | 27.238.32154~dcc3364 | LuCI 前端 |

## 依赖来源（均可在官方 24.10.6 源中解析）

- `libc` / `ca-bundle`（Provides `ca-certs`）/ `curl` / `wget-ssl` / `zoneinfo-all` / `conntrack` / `iw`
- `luci-base` / `luci-compat` / `luci-lua-runtime` / `luci-lib-jsonc`
- `libubox20240329` / `libubus20250102` / `libuci20250120` / `libjson-c5` / `libblobmsg-json20240329` / `libuci-lua` / `libsqlite3-0` / `libcurl4`
- `kmod-oaf` `6.6.133.2025.04.17~f845584c-r1`（官方 kmods 源，与 24.10.6 内核 6.6.133 匹配）
- `smartdns` `48-r1`（官方 packages 源）

## 注意事项

1. **`appfilter` + `luci-app-oaf` 与官方源的 `luci-app-appfilter` 互斥**，两者都装会争抢同一后端，请只保留一套。
2. **EasyTier 不在本仓库**：该 feed 只提供 `luci-app-easytier`（前端），缺少 `easytier` 核心包。
   如需 EasyTier，仍从 `dl.openwrt.ai` 取核心与前端成套的版本。
3. 部分 LuCI 前端版本号（`27.xxx`）高于官方 24.10.6 的 LuCI（`26.208`），依赖项已确认可满足，
   但若刷机后菜单异常，请优先怀疑这里的版本错配。
4. 包未经签名，来源为第三方镜像；已固定版本并附 `SHA256SUMS` 便于校验。

## 校验

```bash
cd x86_64 && sha256sum -c ../SHA256SUMS
```

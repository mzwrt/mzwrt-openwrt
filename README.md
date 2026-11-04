# mzwrt OpenWrt 固件

## 简介

本固件是基于 OpenWrt 系统定制化开发，专为 **CMCC RAX3000M** 路由器优化，旨在提供一个低延迟、高吞吐量、稳定高速的网络体验。固件启用了多种先进的网络优化技术和加密算法，同时深度定制化内核，针对 **MediaTek Filogic** 系列芯片做了专门的优化。

**25.12 已经发布：https://github.com/mzwrt/mzwrt-25-12  建议使用24.10感觉稳定性更好**

**如果usb挂载硬盘或EMMC版本，建议使用 fstrim 来增加硬盘寿命，固件支持 fstrim**


**默认使用清华云源**

**重点：WIFI 国家首选 CN 和 US 备选 CA**
## 固件特性

### 1. 硬件支持

- **目标平台**：专为 **MediaTek Filogic** 系列芯片和 **CMCC RAX3000M** 路由器进行深度优化，确保硬件性能最大化。
- **文件系统支持**：支持 **ext4**, **NTFS3**, **exFAT**, **SquashFS**, **F2FS** 等多种文件系统，适应各种存储需求。

### 2. 网络优化

- **BBR TCP 拥塞控制**：启用了 **BBR** 算法，优化网络带宽利用，提升高延迟网络下的表现。支持多路复用。
- **最新的网络调度器**：有效降低高负载下的网络延迟，提升整体用户体验。
- **多种加密算法支持**：支持 **AES**, **SHA256**, **DES**, **ChaCha20** 等硬件加速加密算法，提供更高的数据传输安全性。
- **Wi-Fi 6 特性**：全面支持 **Wi-Fi 6**（802.11ax）特性，如 MU-MIMO、OFDMA 等，在高密度设备环境下依然能提供稳定的无线连接。

### 3. 安全性增强

- **SSL/TLS 支持**：固件启用 **OpenSSL**，支持最新的 **TLS 1.3** 协议和 SSL压缩特性，增强数据传输的安全性。
- **防火墙与网络安全**： **nftables** 官方推荐的 **firewall4** 提供强大的包过滤和防火墙功能，防止恶意攻击和网络入侵。
- **DNS 安全**：启用了 **AdGuardHome**，提供更安全的 DNS 查询服务，增强网络隐私保护并有效防止广告、恶意网站的侵害。

### 4. 内核与性能优化

- **内核优化**：根据 **CMCC RAX3000M** 进行深度定制化内核优化，降低系统延迟，提高网络吞吐量。
- **高效压缩与解压**：固件支持 **LZ4**, **ZSTD**, **XZ** 等高效压缩算法，优化文件存储和操作性能。
- **ZRAM 支持**：启用 **ZRAM**，提升内存管理效率，适应高负载环境，保证系统稳定性。

### 5. 用户界面与功能增强

- **LuCI 界面**：固件内置 **LuCI** Web 界面，支持中文语言包，简化路由器的管理和配置。
- **广告拦截功能**：集成 **luci-app-adguardhome**，提供本地 DNS 层级广告拦截，提升用户体验。
- **OpenClash 支持**：集成 **luci-app-openclash**，提供多种加密代理功能，保障网络隐私和安全。

### 6. 存储与文件管理

- **磁盘管理**：支持 **NTFS**, **ext4**, **exFAT** 等文件系统，兼容各类存储设备，支持 **fstrim** 对 SSD 的性能优化。
- **USB 存储支持**：支持 **USB 2.0/3.0** 存储设备，具备硬件加速存储功能。
- **文件压缩与解压**：支持多种压缩格式，包括 **TAR**, **XZ**, **ZSTD** 等，方便文件传输和备份。

### 7. 稳定性与兼容性

- **低延迟**：经过多次不同时间，不同负载测试，在高负载情况下延迟依然不会很高
- **高速率**：经过30天的持续跟进测试，没有出现掉速，波动，断流等情况，高负载情况下依然稳定
- **兼容性强**：固件经过精心优化，确保在不同硬件配置和环境下的稳定运行。

## 刷机教程

### 1. NAND 版本刷机教程

请参考 [NAND 版本刷机教程](https://github.com/mzwrt/mzwrt-openwrt/tree/main/Flash-NAND) 进行刷机操作。

### 2. EMMC 版本刷机教程

请参考 [EMMC 版本刷机教程](https://github.com/mzwrt/mzwrt-openwrt/tree/main/Flash-EMMC) 进行刷机操作。

## 固件下载

- [固件发布页面](https://github.com/mzwrt/mzwrt-openwrt/releases)

## 第三方插件

| 插件名称         | 功能描述                                                         |
|------------------|------------------------------------------------------------------|
| **OpenClash**    | 提供代理功能，支持多种加密协议，保障网络隐私和安全。              |
| **AdGuardHome**  | 提供广告拦截功能，支持 **DNSSEC** 和 **DHCPv6**，增强 DNS 查询的安全性，防止广告和恶意网站的侵害。 |

## 调优指南（RAX3000M / MT7981）

目标：**国内直连低延迟、高速率**；**跨境走 OpenClash 尽量高吞吐**。两者不能靠「全局代理」同时拉满。

固件内也可查看：`/etc/mzwrt/openclash-tuning.txt`

### 1. 网络设置调优

#### 固件已默认开启（一般不用改）

| 项目 | 说明 |
|------|------|
| 软/硬 Flow Offloading | 国内 DIRECT 走 MT7981 硬件转发，降延迟、提吞吐 |
| Packet Steering | 双核分散软中断，减轻单核打满毛刺 |
| BBR + `fq_pie` | 拥塞控制与队列；本机出站 TCP 受益 |
| TCP 窗口 / `slow_start_after_idle=0` | 利于跨境长肥管道 |
| ZRAM | 512MB 内存更稳 |

自检：

```sh
uci show firewall.@defaults[0] | grep flow
uci get network.globals.packet_steering
sysctl net.ipv4.tcp_congestion_control net.core.default_qdisc
```

期望大致为：`flow_offloading='1'`、`flow_offloading_hw='1'`、`packet_steering='1'`、`bbr`、`fq_pie`。

#### 建议保持

- **不要为了 OpenClash 长期关闭硬件卸载**，否则国内游戏/下载会明显变慢。
- 有线测国内带宽与延迟；Wi‑Fi 再单独看信道干扰（国家码首选 **CN**）。
- USB / EMMC 存储建议定期执行 `fstrim`，延长寿命。

#### 可选微调（按需）

```sh
# 确认卸载已开（若被改掉）
uci set firewall.@defaults[0].flow_offloading='1'
uci set firewall.@defaults[0].flow_offloading_hw='1'
uci commit firewall
/etc/init.d/firewall restart

uci set network.globals.packet_steering='1'
uci commit network
/etc/init.d/network restart
```

---

### 2. OpenClash 调优（跨境）

#### 推荐组合

| 项 | 推荐 | 原因 |
|----|------|------|
| 运行模式 | **Rule** | 只有需要的流量走代理 |
| 大陆分流 | 开启「绕过中国大陆 IP / 域名直连」 | 国内走 DIRECT，才能吃硬件卸载 |
| 入站 | **Fake-IP + TUN** | 劫持完整、跨境解析快 |
| 协议栈 | **System**（不要用 gvisor 追速度） | 出站 TCP 走内核，才能用上 BBR + 大窗口 |
| 日常 | **不要 Global** | Global 会拖慢所有国内访问 |

#### 节点与协议

- 延迟低 ≠ 下载快；用 URL-Test / 自动选择看**实际下载**，不要只看延迟。
- 优先质量稳定的落地：VLESS Reality、Trojan、Hysteria2、TUIC 等（按你的机场能力选）。
- 少叠中转；MTU 异常时在节点或 TUN 里试 **1280～1400**。
- 核心若支持，可开 **TCP 并发（tcp-concurrent）**。

#### 与硬件卸载的关系

- **DIRECT（国内）**：可被软/硬卸载 → 低延迟、高速率。
- **PROXY（跨境）**：不走硬件卸载（正常）→ 速度主要看节点与 System 栈。
- 若「开了 Clash 后国内也变慢」：先查是否误开 Global、大陆规则是否 DIRECT、卸载是否被关。

---

### 3. AdGuardHome（ADG）调优

固件已集成 **LuCI + AdGuardHome 二进制**。重点是和 OpenClash **不要抢乱 DNS**。

#### 推荐拓扑（二选一，不要叠两套 Fake-IP）

**方案 A（稳妥，适合多数家庭）**

1. 局域网设备 DNS → 路由器（或 AGH）。
2. **AdGuardHome** 负责广告拦截 / 过滤。
3. 需要代理的解析：AGH 上游指到 OpenClash 的 DNS（或混合端口）；国内可直连上游。
4. OpenClash 开 DNS；Fake-IP 可开，异常域名再加白名单。

**方案 B**

- 局域网 DNS 直接指 AGH；AGH 上游走 Clash。
- 同样：**AGH 与 Clash 不要无序双双占用 :53**。

#### AGH 实用建议

- 过滤列表：先少后多；列表过多会涨内存、拖慢解析（512MB 机器尤其注意）。
- 开启合理缓存；不要同时开一堆重型 DNSSEC/并行上游导致超时。
- 银行 / 游戏 / 公司 VPN 域名解析异常时：在 AGH 或 OpenClash 对域名**放行/白名单**，而不是关卸载。
- 首次使用：在 LuCI → AdGuardHome 完成初始化，确认服务在跑、端口不与 dnsmasq/Clash 冲突。

#### 自检

```sh
# AGH / DNS 相关进程与端口（按你实际安装路径可能略有不同）
netstat -lntp 2>/dev/null | grep -E ':53|:3000|:8080' || ss -lntp | grep -E ':53|:3000'
```

客户端 `nslookup` 一个广告域名与一个国内域名，确认拦截与解析都正常；再开 OpenClash 测跨境站点。

---

### 4. 调优后建议验证

1. **国内有线**：关代理或走 DIRECT，测延迟与带宽（应接近宽带口径）。
2. **国内 Wi‑Fi / 游戏**：看延迟毛刺；必要时换信道，国家码 CN。
3. **跨境**：只测代理节点下载；对比协议栈 System vs gvisor（应用 System）。
4. 稳定观察：是否掉流、国内是否被 Global 拖慢、内存是否因 AGH 列表过多吃紧。

## 鸣谢

感谢以下项目和开发者为本固件提供的支持和贡献：

- **OpenWrt**：感谢 OpenWrt 项目提供的开源固件平台，作为我们固件的基础。
- **AdGuardHome**：感谢 AdGuardHome 项目为我们提供强大的广告拦截和 DNS 安全功能。
- **OpenClash**：感谢 OpenClash 提供的代理功能，帮助增强网络隐私保护。
- **MediaTek**：感谢 MediaTek 提供的 Filogic 系列芯片，为我们的路由器硬件提供了稳定的支持。

此外，还要感谢所有贡献者和社区成员，他们的努力和建议使得这一切成为可能。

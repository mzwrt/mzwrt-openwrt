# MzWrt CMCC RAX3000M 更新说明

- 2026-02-27 修复 EMMC 不能保存配置问题
- 2026-03-01 修复 NAT，修复加密
- 2026-03-28 添加主题显示 CPU 温度和 WIFI 芯片温度
- 2026-03-29 修复 CPU 温度显示名称和 WIFI 温度不显示
- 2026-03-29 更新到 24.10.6
- 2026-03-30 修复固件漏洞，根据 OpenWrt 安全规则，关闭 CONFIG_KERNEL_MAGIC_SYSRQ 和 CONFIG_KERNEL_DEBUG_FS 增强安全性
- 2026-04-01 修复 WIFI 信道和功率配置遗漏（CN 5G WIFI6 / CA 全信道）
- 2026-04-14 针对网友 wanjq1991 反馈不能跑满千兆问题，修复内核参数和网络抖动，提升稳定性
- 2026-06-24 从 24.10.6 升级到稳定版 24.10.7
- 2026-07-10 修改 OpenClash 版本为 v0.47.055（后续版本删除一键配置，安装后请手动更新核心）
- 2026-11-05 编译迁回本仓库；统一 version.conf；长期稳定画像 + 国内直连 HW offload / 跨境 OpenClash 双路径调优

编译配置仓库：https://github.com/mzwrt/config（`mzwrt-openwrt/`）

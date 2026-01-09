# CMCC RAX3000M EMMC OpenWrt 刷机指南

本指南面向 **EMMC CMCC RAX3000M 路由器**，假设已经刷入了 H 大 U-Boot 或其他 U-BOOT。通过四个步骤，即可成功刷入固件。

本指南同样适配 openwrt 官方系统，如果你想用官方系统就将除 U-BOOT 以外的所有文件替换为 openwrt 官方文件即可


> ⚠️ **注意**：刷机有风险，请确保电源稳定。按照步骤操作可降低风险。

> ⚠️ **注意**：假设你是新机请直接跳过第一步从第二步开始操作先刷入U-boot在进行第一步操作，防止变砖

> ⚠️ **注意**：请严格按照步骤走，我测试过十几次都没问题，变砖概不负责！！！

---

## 准备工作 （仔细阅读！）

1. 路由器为 **EMMC 版本**。
2. 已刷入 **H 大 U-Boot** 或 刷入其他 U-boot 
3. 请到<a target="_blank" href="https://github.com/mzwrt/mzwrt-openwrt/releases" target="_blank">发布页</a>下载以下三个文件
4. 下载提供的以下固件：
   - `MzWrt-mediatek-filogic-cmcc_rax3000m-emmc-gpt.bin`
   - `MzWrt-mediatek-filogic-cmcc_rax3000m-emmc-preloader.bin`
   - `MzWrt-mediatek-filogic-cmcc_rax3000m-initramfs-recovery.itb`
   - `MzWrt-mediatek-filogic-cmcc_rax3000m-squashfs-sysupgrade.itb`

5. 准备好 U-Boot 固件：
   - `U-boot.bin` <a target="_blank" href="https://drive.wrt.moe/uboot/mediatek" target="_blank">下载链接</a>
- **`下文称呼都以结尾单词进行称呼不再称呼全称`**  
### 固件文件解释
- **`gpt.bin`**  
  这个文件对应 **gpt 分区**，是 **EMMC 的 gpt 分区表**，你如果备份官方固件那么就是 **gpt.bin**，是启动过程中的第一阶段读取分区信息，让启动程序知道我应该从哪里可以正确的启动系统。这个文件可以使用你以前备份的 `gpt.bin`，它通常由你自己或他人备份。刷入此文件后，路由器能够完成第一阶段的引导操作，并为后续的 U-Boot 加载做准备。

- **`preloader.bin`**  
  这个文件对应 **BL2 分区**，也叫 **引导分分区**，你如果备份官方固件那么就是 **mtd1_BL2.bin**，是启动过程中的第二阶段引导加载系统。这个文件可以使用你以前备份的 `preloader.bin`，它通常由你自己或他人备份。刷入此文件后，路由器能够完成第一阶段的引导操作，并为后续的 U-Boot 加载做准备。

- **`recovery.itb`**  
  这是包含 **OpenWrt 恢复镜像**的文件，属于 **第二阶段**的启动文件。通过此文件，路由器可以进入 **OpenWrt 恢复模式**，该模式允许你进一步执行系统升级或其他操作。它通常用于刷入新系统或修复系统。

- **`sysupgrade.itb`**  
  这是用于 **系统升级的固件文件**。在完成前面的恢复步骤后，你可以使用此文件将路由器升级到最新的 OpenWrt 系统版本。这个文件一般是最新的系统固件，能够为你提供最新的特性和修复的 bug。

---

## 刷机步骤 1 ：刷 EMMC 分区表

1. 路由器按 **复位键** 进入 U-Boot。
2. 在浏览器中访问：
<a href="http://192.168.1.1/gpt.html" target="_blank">http://192.168.1.1/gpt.html</a>

3. 刷入 ** gpt.bin ** 文件。
4. 完成后，路由器重启进入 U-Boot。

## 刷机步骤 2 ： 刷分区引导文件

1. 路由器按 **复位键** 进入 U-Boot。
2. 在浏览器中访问：
<a href="http://192.168.1.1/bl2.html" target="_blank">http://192.168.1.1/bl2.html</a>

3. 刷入 ** preloader.bin** 文件。
4. 完成后，路由器重启进入 U-Boot。

---

### **步骤 3：刷 U-Boot**

1. 浏览器访问：
<a href="http://192.168.1.1/uboot.html" target="_blank">http://192.168.1.1/uboot.html</a>

2. 刷入带有 **U-Boot.bin** 的固件。
3. 完成后，进入新的 U-Boot。

---

### **步骤 4：刷 Recovery**
> ⚠️ **注意**：下面还有一步，能进后台不代表就可以食用了！！
1. 再次进入 U-boot <a href="http://192.168.1.1" target="_blank">http://192.168.1.1</a>
2. 在新的 U-Boot 中，刷入 ** recovery.itb** 文件。
3. 完成后，路由器启动进入 ** 恢复模式**。
   

---

### **步骤 5：刷系统固件**

1. 进入系统 Web 界面或命令行。
2. 升级刷入 ** sysupgrade.itb** 文件。
3. 刷机完成，系统运行正常。

---

## 总结

- 这是 **一次搞定的刷机流程**，不再需要寻找多个 MTD 文件或尝试各种固件。
- 按照上述四步操作，几乎可以保证刷机成功。
- 希望本指南能为其他用户提供启发和帮助。

---

## 警告

- 刷机有风险，请自行承担风险。
- 不要中途断电，否则可能造成路由器无法启动。
- 建议在刷机前备份原始 U-Boot 和配置。

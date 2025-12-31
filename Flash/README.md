# CMCC RAX3000M NAND 和 EMMC 版 OpenWrt 刷机指南

本指南面向 **NAND EMMC 版 CMCC RAX3000M 路由器**，假设已经刷入了 H 大 U-Boot。通过四个步骤，即可成功刷入 OpenWrt 官方固件。



> ⚠️ **注意**：刷机有风险，请确保电源稳定。按照步骤操作可降低风险。

> ⚠️ **注意**：假设你是新机请直接跳过第一步从第二步开始操作直接刷入U-boot即可！！

> ⚠️ **注意**：请严格按照步骤走，我测试过十几次都没问题，变砖概不负责！！！

---

## 准备工作 （仔细阅读！）

1. 路由器为 **NAND 版本**。如果是 **EMMC 版本** 请仔细阅读刷机步骤下面的注意内容
2. 已刷入 **H 大 U-Boot**。假设你是新机请直接跳过第一步从第二步开始操作直接刷入U-boot即可！！
3. 浏览器和电脑在同一网络，浏览器可访问 `192.168.1.1`。
4. 下载 OpenWrt 官方提供的以下固件：
   - `preloader.bin`
   - `recovery.itb`
   - `sysupgrade.itb`
5. 准备好 U-Boot 固件：
   - `U-boot.bin` <a target="_blank" href="https://drive.wrt.moe/uboot/mediatek" target="_blank">下载链接</a>

本页面也提供了所有文件，是基于openwrt官方的文件用于救砖，**mtd1_BL2.bin**是官方备份出来的，**preloader**是openwrt官方文件

### 固件文件解释

- **`preloader.bin`**  
  这个文件对应 **BL2 分区**，也叫 **preloader**，你如果备份官方固件那么就是 **mtd1_BL2.bin**，是启动过程中的第一阶段引导程序。这个文件可以使用你以前备份的 `preloader.bin`，它通常由你自己或他人备份。刷入此文件后，路由器能够完成第一阶段的引导操作，并为后续的 U-Boot 加载做准备。

- **`recovery.itb`**  
  这是包含 **OpenWrt 恢复镜像**的文件，属于 **第二阶段**的启动文件。通过此文件，路由器可以进入 **OpenWrt 恢复模式**，该模式允许你进一步执行系统升级或其他操作。它通常用于刷入新系统或修复系统。

- **`sysupgrade.itb`**  
  这是用于 **系统升级的固件文件**。在完成前面的恢复步骤后，你可以使用此文件将路由器升级到最新的 OpenWrt 系统版本。这个文件一般是最新的系统固件，能够为你提供最新的特性和修复的 bug。

---

## 刷机步骤
> ⚠️ **注意**：这个是 NAND 版 如果是EMMC版本多一个步骤，在步骤一之前进U-boot后访问 <a href="http://192.168.1.1/gpt.html" target="_blank">http://192.168.1.1/gpt.html</a> 然后刷入EMMC-GPT.bin后再继续按照步骤一继续操作即可
### **步骤 1：刷 Preloader**

1. 路由器按 **复位键** 进入 U-Boot。
2. 在浏览器中访问：
<a href="http://192.168.1.1/bl2.html" target="_blank">http://192.168.1.1/bl2.html</a>

3. 刷入 **OpenWrt 官方 preloader.bin** 文件。
4. 完成后，路由器重启进入 U-Boot。

---

### **步骤 2：刷 U-Boot**

1. 浏览器访问：
<a href="http://192.168.1.1/uboot.html" target="_blank">http://192.168.1.1/uboot.html</a>

2. 刷入带有 **U-Boot.bin** 的固件。
3. 完成后，进入新的 U-Boot。

---

### **步骤 3：刷 Recovery**

1. 在新的 U-Boot 中，刷入 **OpenWrt 官方 recovery.itb** 文件。
2. 完成后，路由器启动进入 **OpenWrt 恢复模式**。

---

### **步骤 4：刷系统固件**

1. 进入系统 Web 界面或命令行。
2. 升级刷入 **OpenWrt 官方 sysupgrade.itb** 文件。
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

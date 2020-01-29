# 微星 B360M 迫击炮 黑苹果 OpenCore EFI

## 鸣谢

[GeQ1an](https://github.com/GeQ1an/MSI-B360M-MORTAR-HACKINTOSH-OPENCORE-EFI)<br>[xjn](https://blog.xjn819.com/)<br>
[andot](https://github.com/andot/MSI-B360M-MORTAR-IMACPRO-EFI/)<br>
[daliansky](https://github.com/daliansky) ([黑果小兵](https://blog.daliansky.net/))<br>
[tonymoses](http://bbs.pcbeta.com/viewthread-1835637-1-1.html)<br>
[cattyhouse](https://github.com/cattyhouse/oc-guide/)<br>
[osx86zh](https://t.me/osx86zh/) ([Telegram](https://telegram.org/) 讨论组)

## EFI 介绍

此 EFI 使用 iMacPro1.1 机型，微星 B360M 迫击炮 的**无核显**用户可直接修改使用，默认启用全部 USB 端口，[OpenCore](https://github.com/acidanthera/OpenCorePkg) 版本：0.5.4

### 可正常工作
- [x] 网卡（板载）
- [x] 显卡（独显）/ 硬解 4K（HEVC + H.264）
- [x] WiFi（PCI-E 设备） / 蓝牙（PCI-E 设备）
- [x] 隔空投送 / 接力 / 随航
- [x] FaceTime / iMessage / Apple Music / Apple TV Plus
- [x] 原生电源管理
- [x] 自动睡眠 
- [x] 其他白果功能（99%）

### 我的配置

|         硬件       |                   型号                     |
|-------------------:|:------------------------------------------|
|               主板 | 微星 B360M 迫击炮                               |
|             处理器 | 英特尔酷睿 i5-9400F                          |
|               显卡 | 公版 Radeon™ RX 5700 XT（由技嘉代工 |
|        无线 + 蓝牙 | BCM94360CD（双频 1750M + 蓝牙 4.0）PCI-E 无线网卡  |
|             耳机 | Razer Kraken 7.1 V2雷蛇北海巨妖  |

### 兼容的配置

|         硬件       |                              型号                           |
|-------------------:|:------------------------------------------------------------|
|               主板 | 微星 B360M 迫击炮                                    |
|             处理器 | 英特尔第 8 代、第 9 代酷睿处理器               |
|               显卡 | RX 560 / RX 570 / RX 580 / RX 590 / RX VEGA⁵⁶ / RX VEGA⁶⁴ / Radeon VII / RX 5500 XT / RX 5700 / RX 5700 XT |
|               硬盘 | 除了几个特例（如三星 PM981），基本都可以                               |
|               内存 | 除了非常差的，基本都可以                                        |
|        无线 + 蓝牙 | 黑苹果免驱版无线 + 蓝牙 PCI-E 网卡都可以                          |
|     摄像头 + 麦克风 | macOS 免驱版都可以                                             |
|  机箱 + 电源 + 风扇 | 根据个人喜好和 CPU、显卡的功率来决定                               |
|             显示器 | 根据个人喜好选择（推荐 4K 分辨率）                                |
|  键盘 + 鼠标 + 音箱 | 根据个人喜好选择                                                |
|           其它外设 | 根据个人喜好选配                                              |

*显卡优先选择蓝宝石，其次选择迪兰恒进、华硕和微星，尽量不选择盈通和讯景，一定避开 RX 580 2048SP 版本！*<br>
*如果选择购买新显卡，推荐 RX 5500 XT、 RX 5700 和 RX 5700 XT 这三个型号。*<br>


## 更新记录
#### 2020.01.22
添加300系主板原生支持NVRAM

#### 2020.01.04
使用 OpenCore 官方补丁间接修复「不开启小憩无法进入睡眠」的问题，移除 SSDT-SBUS.aml 文件。<br>
*不开启小憩的目的是睡眠后不被自动唤醒，开启 OC 的「禁用 RTC 唤醒计划」补丁后，打开小憩功能可以正常进入睡眠，且不会被自动唤醒，间接达到「不开启小憩进入睡眠」的状态，如不需要可以手动关闭该补丁（感谢 [ArchFeh](https://github.com/GeQ1an/MSI-B360M-MORTAR-HACKINTOSH-OPENCORE-EFI/issues/5) 的提醒）。*<br>
![](https://raw.githubusercontent.com/GeQ1an/MSI-B360M-MORTAR-HACKINTOSH-OPENCORE-EFI/master/Images/Explain/ProperTree_Kernel_Patch.png)

## 使用 EFI
准备 [ProperTree](https://blog.xjn819.com/wp-content/uploads/2019/10/ProperTree.zip) 用来编辑配置文件，请勿使用其他编辑器编辑（切记）。<br>
OpenCore 拥有高度的可定制化，建议先参考下面的说明使用配置好的基础版本，之后再通过 [xjn 博客](https://blog.xjn819.com/?p=543) 和 [黑果小兵博客](https://blog.daliansky.net/OpenCore-BootLoader.html) 学习更多内容进行修改。

### BIOS 设置
*请先确定正在使用的 BIOS 版本，[迫击炮](https://cn.msi.com/Motherboard/support/B360M-MORTAR) 7B23v16 以上，[迫击炮钛金版](https://cn.msi.com/Motherboard/support/B360M-MORTAR-TITANIUM) 7B23vA6 以上，否则请参考官方文档升级 BIOS 至最新版本。*<br>
<br>
STTINGS\高级\PCI子系统设置\Above 4G memory/Crypto Currency mining [允许]<br>
<br>
STTINGS\高级\内建显示配置\设置第一显卡 [PEG]<br>
STTINGS\高级\内建显示配置\集成显卡多显示器 [允许] （如果使用拥有核显的处理器）<br>
<br>
STTINGS\高级\ACPI设置\电源 LED 灯 [双色]（如果选择 [闪烁]，睡眠时电源灯将不断闪烁）<br>
<br>
STTINGS\高级\USB设置\XHCI Hand-off [允许]<br>
STTINGS\高级\USB设置\传统USB支持 [允许]<br>
<br>
STTINGS\高级\电源管理设置\ErP Ready [允许]<br>
<br>
STTINGS\高级\Windows操作系统的配置\Windows 10 WHQL支持 [允许]<br>
STTINGS\高级\Windows操作系统的配置\MSI 快速开机 [禁止]<br>
STTINGS\高级\Windows操作系统的配置\快速开机 [禁止]<br>
<br>
STTINGS\高级\唤醒事件设置\唤醒事件管理 [BIOS]<br>
STTINGS\高级\唤醒事件设置\USB设备从S3/S4/S5唤醒 [允许]<br>
<br>
STTINGS\启动\启动NumLock状态 [关]（macOS 默认可使用数字键盘）<br>
STTINGS\启动\启动模式选择 [UEFI]<br>
<br>
OC(Overclocking)\CPU 特征\Intel 虚拟化技术 [允许]（必须）<br>
OC(Overclocking)\CPU 特征\Intel VT-D 技术 [禁止]（必须）<br>
OC(Overclocking)\CPU 特征\CFG锁定 [禁止]（必须！）<br>

### 直接使用
仅适合使用 9400F 处理器的用户！<br>
下载整包后，如果之前在 Clover 时就使用`iMacPro1,1`机型，可直接使用之前的三码，或使用 [Clover Configurator](https://mackie100projects.altervista.org/download-clover-configurator/) （其他工具亦可）选择`iMacPro1.1`机型生成新的三码 + ROM，用 ProperTree 打开`/EFI/OC/config.plist`文件，填入到 PlatformInfo > Generic 位置中（如下图）。<br>
![](https://raw.githubusercontent.com/GeQ1an/MSI-B360M-MORTAR-HACKINTOSH-OPENCORE-EFI/master/Images/Explain/ProperTree_PlatformInfo.png)<br>
保存后，先通过 USB 测试引导，无问题后将 EFI 文件夹放置到启动磁盘 EFI 分区，重启电脑。

### 核显使用
适合使用核显处理器的用户。<br>
1. 填入`iMac19,1`机型的三码 + ROM 信息到`/EFI/OC/config.plist`文件 PlatformInfo > Generic 处，并将机型修改为`iMac19,1`。
3. 添加`/EFI/OC/config.plist`文件 DeviceProperties > Add > PciRoot(0x0)/Pci(0x2,0x0) 下 AAPL,ig-platform-id 这一行参数（如下图）。<br> 
![](https://raw.githubusercontent.com/GeQ1an/MSI-B360M-MORTAR-HACKINTOSH-OPENCORE-EFI/master/Images/Explain/ProperTree_DeviceProperties.png)
5. 参考 [xjn 博客](https://blog.xjn819.com/?p=543) 的完善部分「3.4 加载原生电源管理」替换自己处理器对应的 SSDT-PLUG.aml 到`/EFI/OC/ACPI/`目录。
<br>
保存后，将 EFI 文件夹放置到启动磁盘 EFI 分区，重启电脑。

### 进阶使用
1. 参考 [xjn 博客](https://blog.xjn819.com/?p=543) 的进阶部分「4.1 CPU 的变频优化」生成`CPUFriendDataProvider.kext`HWP 变频文件，放入`/EFI/OC/Kexts/`，添加`/EFI/OC/config.plist`文件 Kernel > Add项
2. 参考 [黑果小兵博客](https://blog.daliansky.net/Intel-FB-Patcher-USB-Custom-Video.html) 生成`USBPorts.kext`USB 定制文件，放入`/EFI/OC/Kexts/`替换同名文件，打开`/EFI/OC/config.plist`，关闭 Kernel > Add > 7，打开 8。<br>
![](https://raw.githubusercontent.com/GeQ1an/MSI-B360M-MORTAR-HACKINTOSH-OPENCORE-EFI/master/Images/Explain/ProperTree_Kernel_USB.png)

## Q&A
1. **开机时苹果 logo 显示不正常怎么办？**<br>
   有两个方法可以解决这个问题。<br>
   方法一：在`/EFI/OC/config.plist`配置文件 Misc—–Boot——Resolution 处填写正确的显示器分辨率；<br>
   方法二：将 BIOS「STTINGS\启动\全荧幕商标」设置为 [允许]。<br>
   两种方法选择其一即可，经反复测试，在微星 B360M 迫击炮（钛金版）上我更推荐方法二。<br>
   *如果同时使用方法一和方法二，开机 logo 的显示依旧会不正常。*

## 写在最后
作为一个黑果小白，欢迎指正错误及提出建议，我会及时更新此 EFI。

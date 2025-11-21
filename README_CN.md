# Lenovo-M720Q-OpenCore-EFI

[English](./README.md) | 简体中文

:loudspeaker: 在使用此 EFI 前，请完整阅读并理解本文档，以避免对系统甚至硬件造成不可预知的损害。

![about_this_mac](./README.assets/about_this_mac.png)

本仓库为 **[联想 ThinkCentre M720Q Tiny](https://www.lenovo.com/us/en/p/desktops/thinkcentre/m-series-tiny/thinkcentre-m720q/11tc1mtm72q)** 提供基于 **[OpenCore](https://github.com/acidanthera/OpenCorePkg)** 引导加载程序 ([v1.0.6](https://github.com/acidanthera/OpenCorePkg/releases/tag/1.0.6)) 的 EFI 配置。

MacOS 的大部分功能运行良好，包括：

- [x] DP/HDMI 视频输出 (VGA 未测试)
- [x] 音频输出 (内置扬声器和耳机插孔均可用)
- [x] USB 端口
- [x] 睡眠、唤醒、休眠
- [x] 有线网络、Wi-Fi、蓝牙 (在 Sonoma 或 Sequoia 上同样正常工作)
- [x] 隔空投送、接力、iMessage、FaceTime 等

![control_center](./README.assets/control_center.png)

## 硬件配置

|   组件    |                                                                                   型号                                                                                   |
| :-------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|   主板    |                                                                                   B360                                                                                   |
| BIOS 版本 | [M1UKT77A/1.0.0.119](https://support.lenovo.com/us/en/downloads/ds503907-flash-bios-update-thinkcentre-m720t-m720s-m720q-m920t-m920s-m920q-m920x-thinkstation-p330-tiny) |
|    CPU    |                                                                              Intel i5-9500T                                                                              |
|   核显    |                                                                          Intel UHD Graphics 630                                                                          |
|   声卡    |                                                                              Realtek ALC235                                                                              |
| 有线网卡  |                                                                               Intel I219-V                                                                               |
| 无线网卡  |                                                                                BCM94360Z4                                                                                |

## 目录结构

```plaintext
Lenovo-M720Q-OpenCore-EFI
├── EFI_No_Broadcom_Fix
│   ├── BOOT
│   └── OC
│       ├── ...
│       ├── config_DEBUG.plist
│       ├── config_DEBUG_CFG_Unlocked.plist
│       └── config_RELEASE.plist
└── EFI_With_Broadcom_Fix
    └── ...
```

由于苹果已停止对 Broadcom Wi-Fi 芯片组的支持（在 2017 年之前 Mac 中使用），需要在 Sonoma 及后续的系统上使用额外的 kext 和配置才能使它们正常工作。

因此，本仓库提供了两个版本的 EFI：

- [`EFI_No_Broadcom_Fix`](./EFI_No_Broadcom_Fix) 适用于 Ventura 及更早的系统，或不使用 Broadcom 网卡的情况
- [`EFI_With_Broadcom_Fix`](./EFI_With_Broadcom_Fix) 适用于 **Sonoma 及更新系统中使用 Broadcom 网卡的情况**

并且由于官方 BIOS 未提供 CFG Lock 的切换选项，需要手动去解锁。因此，我在每个 EFI 文件夹中提供了多个版本的 config.plist 文件：

- `config_DEBUG.plist`：在未解锁 CFG 时使用。
- `config_DEBUG_CFG_Unlocked.plist`：在解锁 CFG 后使用。
- `config_RELEASE.plist`：禁用启动过程中的调试信息。

请选择合适的配置文件并**重命名为 `config.plist`**。

*:warning: 请注意：请务必在 `config.plist` 文件中将 `PlatformInfo` 部分替换为您自己的值。*

## MacOS 26 Tahoe

本 EFI 配置已在 **MacOS 26 Tahoe** 上测试通过。

为了获得更好的兼容性，建议将 `DeviceProperties` 修改为苹果明确支持的设备，例如 *iMac (Retina 5K, 27 inch, 2020)*（详情见[此页面](https://support.apple.com/en-us/122867)）。

:warning: 请注意：截至本文档撰写时（2025 年 9 月 27 日），最新版本的 [OCLP (2.4.1)](https://github.com/dortania/OpenCore-Legacy-Patcher) 尚不支持 Tahoe。这意味着 Broadcom 无线网卡无法驱动，影响 **Wi-Fi、蓝牙、隔空投送和接力** 等功能。

有线以太网连接不受影响。

<img src="./README.assets/about_this_mac_tahoe.png" alt="about_this_mac_tahoe" width="300">

<img src="./README.assets/control_center_tahoe.png" alt="control_center_tahoe" width="300">

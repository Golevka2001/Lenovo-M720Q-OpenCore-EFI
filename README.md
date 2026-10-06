# Lenovo-M720Q-OpenCore-EFI

English | [简体中文](./README_CN.md)

> [!NOTE]
> Before using this EFI, please read and understand the README completely to avoid unpredictable damage to the system or even hardware.

![about_this_mac](./README.assets/about_this_mac.png)

This repository provides the EFI configuration for **[Lenovo ThinkCentre M720Q Tiny](https://www.lenovo.com/us/en/p/desktops/thinkcentre/m-series-tiny/thinkcentre-m720q/11tc1mtm72q)** with **[OpenCore](https://github.com/acidanthera/OpenCorePkg)** bootloader ([v1.0.8](https://github.com/acidanthera/OpenCorePkg/releases/tag/1.0.8)).

Most of the features of macOS are working fine and stable, including:

- [x] DP/HDMI video output (VGA not tested)
- [x] Audio output (both internal speaker and headphone jack)
- [x] USB ports
- [x] Sleep, Wake, Hibernate
- [x] Ethernet, Wi-Fi, Bluetooth
- [x] AirDrop, Handoff, iMessage, FaceTime ...

![control_center](./README.assets/control_center.png)
![airdrop](./README.assets/airdrop.png)

## Hardware Configuration

|  Component   |                                                                                  Model                                                                                   |
| :----------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| Motherboard  |                                                                                   B360                                                                                   |
| BIOS Version | [M1UKT79A/1.0.0.121](https://support.lenovo.com/us/en/downloads/ds503907-flash-bios-update-thinkcentre-m720t-m720s-m720q-m920t-m920s-m920q-m920x-thinkstation-p330-tiny) |
|     CPU      |                                                                              Intel i5-9500T                                                                              |
|     iGPU     |                                                                          Intel UHD Graphics 630                                                                          |
|    Audio     |                                                                              Realtek ALC235                                                                              |
|   Ethernet   |                                                                               Intel I219-V                                                                               |
|   Wireless   |                                                                                BCM94360Z4                                                                                |

## Folder Structure

```plaintext
Lenovo-M720Q-OpenCore-EFI
├── Sequoia
│   ├── EFI_No_Broadcom_Fix
│   │   ├── BOOT
│   │   └── OC
│   │       ├── ...
│   │       ├── config_DEBUG.plist
│   │       ├── config_DEBUG_CFG_Unlocked.plist
│   │       └── config_RELEASE.plist
│   └── EFI_With_Broadcom_Fix
│       └── ...
└── Tahoe
    ├── EFI_No_Broadcom_Fix
    │   └── ...
    └── EFI_With_Broadcom_Fix
        └── ...
```

### EFI Version Information

This repository provides two sets of EFI configurations organized by macOS version:

- [`Sequoia`](./Sequoia) for macOS Sequoia and earlier
- [`Tahoe`](./Tahoe) for macOS Tahoe

Since Apple has dropped support for the Broadcom Wi-Fi chipsets used in pre-2017 Macs, additional kexts and configurations are required to make them work properly on Sonoma and newer systems.

Therefore, each set of EFI configurations includes two versions:

- `EFI_No_Broadcom_Fix` for systems not using Broadcom cards
- `EFI_With_Broadcom_Fix` for **systems using Broadcom cards**

### config.plist Version Information

Since the official BIOS does not provide an option to switch **CFG Lock**, it must be unlocked manually ([reference](https://github.com/psvajaz/Lenovo-ThinkCentre-M720Q-i3-9100-Hackintosh/blob/main/Tools/README.md)). Therefore, I have provided multiple versions of the `config.plist` file in each EFI folder:

- `config_DEBUG.plist`: To be used when CFG is not unlocked.
- `config_DEBUG_CFG_Unlocked.plist`: To be used after CFG has been unlocked.
- `config_RELEASE.plist`: Debug information during the boot process is disabled.

Choose the appropriate configuration file and **rename it to `config.plist`**.

> [!WARNING]
> Remember to replace `[REPLACE]` in the `PlatformInfo` section with your own values in the `config.plist` file.

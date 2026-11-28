# ThinkPad T470 (Tahoe) — OpenCore EFI

macOS Hackintosh EFI untuk **Lenovo ThinkPad T470 (Tahoe)** menggunakan **OpenCore**.  
SMBIOS: `MacBookPro15,2`

---

## 💻 Spesifikasi Laptop

| Komponen | Detail |
|---|---|
| **Model** | Lenovo ThinkPad T470 (Tahoe) |
| **CPU** | Intel Core i-series (Kaby Lake / Gen 7) |
| **GPU** | Intel HD Graphics (iGPU) — via WhateverGreen |
| **Display** | Built-in LVDS / eDP panel (Display-30e4-521 kext) |
| **RAM** | Upgradable (DDR4 SO-DIMM) |
| **Storage** | NVMe SSD — via NVMeFix |
| **WiFi** | Intel Wireless — AirportItlwm / itlwm |
| **Bluetooth** | Intel Bluetooth — IntelBluetoothFirmware + IntelBTPatcher + BlueToolFixup |
| **Ethernet** | Intel I219-LM — IntelMausi |
| **Audio** | AppleALC + SimpleHDA |
| **Trackpad** | VoodooI2C + VoodooI2CHID + VoodooRMI + VoodooSMBus |
| **Keyboard** | VoodooPS2Controller + BrightnessKeys |
| **Battery** | SMCBatteryManager |
| **USB** | USBMap (custom mapped) |
| **Light Sensor** | SMCLightSensor + YogaSMC |
| **USB Tethering** | HoRNDIS |

---

## 🗂️ Struktur EFI

```
EFI/
├── BOOT/
│   └── BOOTx64.efi          # Fallback bootloader
└── OC/
    ├── config.plist          # Konfigurasi utama OpenCore
    ├── config.plist.backup   # Backup konfigurasi
    ├── ACPI/                 # SSDT custom
    ├── Drivers/              # OpenCore drivers
    ├── Kexts/                # Kernel extensions
    ├── Resources/            # OpenCanopy icons & labels
    └── Tools/                # Utilities (OpenShell, CleanNvram, dll)
```

---

## 🔧 Kexts yang Digunakan

| Kategori | Kext |
|---|---|
| **Core** | Lilu, VirtualSMC |
| **GPU** | WhateverGreen |
| **Audio** | AppleALC, SimpleHDA |
| **WiFi** | AirportItlwm, itlwm, IO80211FamilyLegacy, IOSkywalkFamily |
| **Bluetooth** | IntelBluetoothFirmware, IntelBTPatcher, BlueToolFixup |
| **Ethernet** | IntelMausi |
| **Trackpad** | VoodooI2C, VoodooI2CHID, VoodooRMI, VoodooSMBus |
| **Keyboard** | VoodooPS2Controller, BrightnessKeys |
| **Battery** | SMCBatteryManager, SMCLightSensor, SMCProcessor, SMCSuperIO |
| **NVMe** | NVMeFix |
| **USB** | USBMap |
| **CPU Power** | CPUFriend, CPUFriendDataProvider |
| **Sensor** | YogaSMC |
| **USB Tether** | HoRNDIS |
| **Fix** | RTCMemoryFixup, HibernationFixup, RestrictEvents, NoTouchID, AMFIPass |
| **Display** | Display-30e4-521 |

---

## 📋 ACPI / SSDT

| File | Fungsi |
|---|---|
| SSDT-AC | AC adapter |
| SSDT-BATX | Battery extended |
| SSDT-DEVICE | Device injection |
| SSDT-EC | Embedded controller |
| SSDT-GPI0 | GPIO pinning (trackpad) |
| SSDT-GPRW | Fix immediate wake dari sleep |
| SSDT-HWAC | Hardware access control |
| SSDT-INIT | Inisialisasi |
| SSDT-KBRD / SSDT-KBTA | Keyboard |
| SSDT-PNLF | Brightness control |
| SSDT-SLEEP | Sleep/wake fix |
| SSDT-UTILS | Utilities |
| SSDT-XHC | USB controller |
| SSDT-YOGASMC | YogaSMC support |

---

## 🚀 Perubahan Terbaru (2026-11-28)

- ✅ Update semua **kexts** ke versi terbaru
- ✅ Refresh **SSDT ACPI** tables
- ✅ Update **OpenCore drivers** (OpenRuntime, OpenCanopy, HfsPlus, AudioDxe, dll)
- ✅ Update `config.plist` + backup copies tersimpan
- ✅ Fix mode file (permissions) di Resources & Tools
- ✅ Tambah README lengkap

---

## ⚙️ SMBIOS

| Field | Value |
|---|---|
| **SystemProductName** | MacBookPro15,2 |
| **SystemMemoryStatus** | Upgradable |

> [!WARNING]
> Jangan gunakan Serial Number / UUID dari repo ini secara langsung. Generate SMBIOS baru menggunakan [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS).

---

## 📥 Cara Pakai

1. Clone repo ini
2. Copy folder `EFI/` ke EFI System Partition (ESP) laptop kamu
3. Sesuaikan `config.plist` dengan hardware spesifik kamu (jika diperlukan)
4. Reboot dan pilih entry OpenCore

---

*Dibuat dengan ❤️ untuk komunitas Hackintosh Indonesia.*

# EFI Hackintosh Lenovo T470 (Kaby Lake) - macOS Tahoe

Jadi gini ceritanya, gue udah berhasil pasang macOS Tahoe di ThinkPad T470 gue. Ini EFI yang gue pake sehari-hari buat kerja dan kuliah. 

Awalnya gue fork dari EFI-nya suhu `userminer2` yang aslinya buat T470s. Tapi karena T470 gue ini pake prosesor Kaby Lake (i5-7300U) dan susah banget nemu yang bener-bener *plug and play*, akhirnya gue oprek sendiri sampe jalan mulus kayak sekarang. Daripada ilmunya cuma numpang lewat, mending gue share aja di sini. Siapa tau ada yang lagi pusing nyari EFI buat T470.

> **Tips:** Pas nyalain laptop, tahan tombol `Esc` atau `Alt` buat munculin *boot picker* OpenCore-nya.

---

## 🚀 Gimana Performanya?

Udah gue tes buat ngoding, ngetik dokumen, sama *browsing* harian. Jujur, ini udah enak banget buat *daily driver*:
*   **Grafis:** Akselerasi Metal (Intel HD 620) jalan penuh. Animasi *smooth*, gak ada yang *glitch*. Palingan *lag* dikit pas pertama kali buka app berat.
*   **Baterai:** Buat *browsing* santai 4-5 jam. Buat *coding* sambil ngetik dokumen tembus 6-7 jam. Tapi kalau dipake *gaming* atau *rendering*, ya wasalam, 2 jam doang.
*   **Konektivitas:** Bluetooth aman, Wi-Fi jalan pakai `itlwm.kext`. HDMI (audio + display) normal, USB-C juga jalan.
*   **Periferal:** Keyboard (termasuk *fn keys*) normal, *trackpad* mulus semua *gesture*, *trackpoint* ijo legendaris juga hidup.
*   **Audio:** Speaker sama *jack* headphone aman.
*   **Dual Battery:** Persentase baterai akurat, gak ngaco (ini pakai *patch* `SSDT-BATX`).
*   **Update:** Bisa OTA langsung dari *Settings*, dan Apple ID + App Store jalan normal.

## ❌ Yang Belum Bisa (Jujur Aja)

*   **AirDrop:** Belum jalan karena kita pakai `itlwm.kext`. Butuh `AirportItlwm` yang katanya masih *Work In Progress*.
*   **Continuity/Handoff:** Kadang bisa, kadang enggak. Masih *finicky* banget.

---

## 💻 Spek Test (Laptop Gue)

Ini spek T470 yang gue pake buat ngetes EFI ini:

| Komponen | Detail |
| :--- | :--- |
| **Model** | Lenovo ThinkPad T470 |
| **CPU** | Intel Core i5-7300U (Kaby Lake) |
| **GPU** | Intel HD Graphics 620 |
| **RAM** | 12 GB DDR4 |
| **Storage** | SSD 2.5" (via Enclosure) |
| **Layar** | Full HD (1920x1080) |
| **SMBIOS** | `MacBookPro14,1` |
| **macOS** | Tahoe (26.x) |

*(Catatan: Kalau RAM lu cuma 8GB, saran gue jangan maksa pakai Tahoe. Mending turun ke macOS Ventura aja. Efek "Liquid Glass" di Tahoe lumayan ngabisin RAM kalau lu sering buka banyak aplikasi. Tapi karena RAM gue 12GB, Tahoe jalan lumayan lancar.)*

---

## ⚙️ Wajib Dilakuin (Setup)

1.  **Generate Serial Number Sendiri!** 
    Gak usah pakai `config.plist` gue mentah-mentah. Ganti `MLB`, `SystemSerialNumber`, dan `SystemUUID` pakai **GenSMBIOS** (bikinan corpnewt). Jangan sampai serial number lu bocor atau malah ketuker sama punya orang.
2.  **Gak Perlu Root Patching!** 
    Ini kabar baiknya. EFI ini udah *plug and play*, gak perlu oprek-oprek system file aneh-aneh.
3.  **Buat Audio:**
    *   Kalau lu pakai macOS Tahoe versi baru, install aja file `HDAUniversal.pkg` yang udah gue sediain di repo ini.
    *   Kalau lu pakai macOS versi lama, bisa pakai `VoodooHDA.kext`.
4.  **Buat Wi-Fi:**
    *   Karena kita pakai `itlwm.kext`, lu wajib *download* aplikasi **HeliPort** (file `.zip` udah gue siapin di repo) dan pindahin ke folder `/Applications`. Jangan lupa masukin ke *Login Items* biar otomatis *connect* pas nyala.

---

## 🔥 Post-Install (Biar Gak Panas & Awet)

Ini yang paling sering orang lupain. Di macOS Tahoe, efek visualnya lumayan berat buat hardware jadul. Biar laptop gak *overheat* dan kipas gak muter kenceng kayak *jet* pas dicas, **wajib** jalanin command ini di Terminal:

```bash
sudo pmset -a lowpowermode 1
Atau gampangnya masuk ke Settings > Battery > Battery Saver > Always.

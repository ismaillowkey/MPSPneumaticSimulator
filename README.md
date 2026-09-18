# 🏭 MPS Pneumatic Simulator — Distribution & PLC Examples

[![GitHub Release](https://img.shields.io/github/v/release/ismaillowkey/MPSPneumaticSimulator?color=0091DC&logo=github)](https://github.com/ismaillowkey/MPSPneumaticSimulator/releases)
[![Platform](https://img.shields.io/badge/Platform-Windows%2010%20%7C%2011-0078D6?logo=windows)](https://github.com/ismaillowkey/MPSPneumaticSimulator/releases)
[![Framework](https://img.shields.io/badge/.NET%20Framework-4.7.2-512BD4)](https://dotnet.microsoft.com/)
[![License](https://img.shields.io/badge/License-Freeware-10B981)](#)
[![Saweria](https://img.shields.io/badge/Dukung-Saweria-E11D48?logo=heart)](https://saweria.co/ismaillowkey)

Selamat datang di repositori resmi distribusi **MPS Pneumatic Simulator** dan kumpulan **Example Program PLC**. Repositori ini menyediakan berkas instalasi resmi (*setup installer*) aplikasi simulator serta kode contoh ladder diagram PLC (Omron, Mitsubishi, Haiwell, dll.) yang dapat langsung digunakan untuk pembelajaran mekatronika dan otomasi industri.

---

## 📥 Download Installer Terbaru

Unduh installer setup versi terbaru pada halaman **[GitHub Releases](https://github.com/ismaillowkey/MPSPneumaticSimulator/releases)**:

| Berkas | Versi | Platform | Tautan Unduhan |
| :--- | :--- | :--- | :--- |
| **MPS_Pneumatic_Simulator_v0.4.0_Setup.exe** | **v0.4.0** *(Latest)* | Windows 10 / 11 (x86 & x64) | [Download Setup (.exe)](https://github.com/ismaillowkey/MPSPneumaticSimulator/releases/latest) |

### Persyaratan Sistem
* **Sistem Operasi:** Windows 10 atau Windows 11 (32-bit / 64-bit)
* **Runtime:** .NET Framework 4.7.2 (sudah terpasang secara bawaan di Windows 10/11)
* **Grafis:** Direct3D / DirectX 9 ke atas (Hardware Accelerated)
* **Ruang Penyimpanan:** ~30 MB

---

## ✨ Fitur Unggulan Simulator

MPS Pneumatic Simulator dirancang untuk mensimulasikan sistem otomasi mekatronika nyata (*Modular Production System*) secara 3D interaktif dan dapat dikendalikan langsung oleh PLC fisik maupun simulator software PLC.

### 1. 🏭 Stasiun MPS Distributing (Festo CIROS Standard 3D)
* **Silinder Dorong (1A1):** Mendorong benda kerja keluar dari tabung magasin ke titik pengambilan (*pick-up point*).
* **Lengan Putar Swivel (2A1):** Silinder ayun semi-rotary 0° hingga 90° memindahkan benda kerja ke stasiun berikutnya.
* **Gripper Vakum Suction Cup (3A1):** Pengisap benda kerja menggunakan generator venturi dengan sensor tekanan vakum (3B1) dan semprotan pelepas benda (3M2).
* **Sensor Deteksi Benda Optik (1B4):** Mendeteksi keberadaan benda kerja di titik ambil.
* **Emulasi Mekanis Tutup Benda:** Tutup solid (*solid lid*) akan membentur cup fitting sehingga sudut swivel tertahan di 5.5° dan sensor 2B1 tidak aktif (sama persis dengan perilaku hardware fisik Festo).

### 2. ⚡ Plat Trainer Electro-Pneumatic (3 Silinder Kerja Ganda)
* **3 Silinder Horisontal Anti-Tabrakan:** Silinder A (1A1), B (2A1), dan C (3A1) berjajar di atas meja profil aluminium.
* **Katup Bi-stable 5/2-Way:** Katup solenoid ganda (Y1 maju, Y2 mundur) dengan selang pneumatik realistis.
* **Katup Cekik Satu Arah Seri GRLA (Flow Control):** Dilengkapi slider interaktif 0% s.d. 100% dan animasi baut kuningan naik-turun real-time untuk mengatur kecepatan gerak piston.
* **Mode Urutan Sekuens Otomatis:** Sekuens default A+ B+ B- C+ C- A- dengan siklus loop terus-menerus.

### 3. 🔌 Multi-Protocol PLC Driver Support
* **Omron CX-Simulator:** Koneksi bridge otomatis tanpa kabel fisik langsung ke instance simulasi CX-Programmer via FINS Protocol.
* **Mitsubishi FX3U:** Komunikasi serial programming port / ethernet (Device bit X/Y).
* **Haiwell PLC:** Protokol Modbus RTU / TCP (Discrete Input / Coil).
* **TCP/IP Raw Server:** Socket server untuk integrasi software custom atau script Python / Node.js.

### 4. 🔄 Auto Check for Update
Aplikasi dilengkapi fitur pengecekan pembaruan otomatis di latar belakang saat startup serta tombol menu *Check for Update* yang terhubung langsung ke rilis repositori GitHub ini.

---

## 📂 Katalog Contoh Program PLC (Example program PLC/)

Repositori ini menyertakan folder **Example program PLC/** yang berisi template dan proyek program PLC siap pakai:

`
📁 Example program PLC/
└── 📁 MPS Distributing plc omron/
    ├── 📄 mps_distributing.cxp   # Proyek ladder diagram Omron CX-Programmer
    └── 📄 mps_distributing.opt   # Konfigurasi workspace CX-Programmer
`

### 🚀 Cara Menghubungkan ke Omron CX-Programmer:
1. Pasang dan buka **Omron CX-Programmer**.
2. Buka berkas proyek:  
   Example program PLC/MPS Distributing plc omron/mps_distributing.cxp
3. Nyalakan simulator internal CX-Programmer dengan memilih menu:  
   **Simulation ➔ Work Online Simulator** (atau tekan Ctrl + Shift + W).
4. Jalankan **MPS Pneumatic Simulator**.
5. Buka stasiun **MPS Distributing**, lalu pada panel koneksi PLC:
   * Pilih Device: Omron CP1 CX Simulator
   * Klik tombol **Connect**.
6. Simulator akan langsung terhubung dan tersinkronisasi secara real-time dengan logika ladder CX-Simulator!

---

## 📋 Tabel Pemetaan I/O (I/O Mapping Reference)

Gunakan tabel pemetaan alamat I/O berikut sebagai acuan penulisan program ladder PLC:

### 1. Stasiun MPS Distributing

#### 📥 Digital Inputs (Sensor ke PLC)
| Simbol | Alamat Default (Omron) | Keterangan |
| :--- | :--- | :--- |
| **1B1** | CIO 0.00 | Silinder Dorong (Pusher) Posisi Mundur / Home |
| **1B2** | CIO 0.01 | Silinder Dorong (Pusher) Posisi Maju / Extended |
| **1B3** | CIO 0.02 | Sensor Tabung Magasin Benda Kerja Ada |
| **1B4** | CIO 0.03 | Sensor Optik Titik Ambil Depan (*Pick-up Nest*) |
| **2B1** | CIO 0.04 | Lengan Putar Posisi Magasin (0°) |
| **2B2** | CIO 0.05 | Lengan Putar Posisi Stasiun Berikutnya (90°) |
| **3B1** | CIO 0.06 | Sensor Tekanan Vakum Hisap Benda Terdeteksi (*VPEV*) |
| **S_AUTO**| CIO 0.07 | Sakelar Pemilih Mode (0 = Manual, 1 = Auto) |
| **PB_A** | CIO 0.08 | Tombol Hijau Start / Run (NO, Momentary) |
| **PB_B** | CIO 0.09 | Tombol Merah Stop / Reset (NC, Normal 1, Tekan 0) |

#### 📤 Digital Outputs (Aktuator dari PLC)
| Simbol | Alamat Default (Omron) | Keterangan |
| :--- | :--- | :--- |
| **1M1** | CIO 100.00 | Solenoid Silinder Dorong Ejector Maju |
| **2M1** | CIO 100.01 | Solenoid Lengan Putar ke Depan (Transfer 90°) |
| **2M2** | CIO 100.02 | Solenoid Lengan Putar ke Tabung (Magasin 0°) |
| **3M1** | CIO 100.03 | Katup Solenoid Generator Vakum Suction ON |
| **3M2** | CIO 100.04 | Katup Solenoid Semburan Pulsa Pelepas Benda (*Eject Pulse*) |
| **LIGHT_G**| CIO 100.05 | Lampu Menara Hijau (*Running / Normal*) |
| **LIGHT_Y**| CIO 100.06 | Lampu Menara Kuning (*Standby / Waiting*) |
| **LIGHT_R**| CIO 100.07 | Lampu Menara Merah (*Alarm / Emergency Stop*) |

---

### 2. Plat Trainer Electro-Pneumatic (3 Silinder)

#### 📥 Digital Inputs (Magnetic Reed Sensor)
| Simbol | Alamat Default | Fungsi |
| :--- | :--- | :--- |
| **1B1** | CIO 0.00 | Silinder A Posisi Mundur (Home) |
| **1B2** | CIO 0.01 | Silinder A Posisi Maju (Extended) |
| **2B1** | CIO 0.02 | Silinder B Posisi Mundur (Home) |
| **2B2** | CIO 0.03 | Silinder B Posisi Maju (Extended) |
| **3B1** | CIO 0.04 | Silinder C Posisi Mundur (Home) |
| **3B2** | CIO 0.05 | Silinder C Posisi Maju (Extended) |

#### 📤 Digital Outputs (5/2-Way Solenoid Valves)
| Simbol | Alamat Default | Fungsi |
| :--- | :--- | :--- |
| **1Y1** | CIO 100.00 | Aktuasi Maju Silinder A (A+) |
| **1Y2** | CIO 100.01 | Aktuasi Mundur Silinder A (A-) |
| **2Y1** | CIO 100.02 | Aktuasi Maju Silinder B (B+) |
| **2Y2** | CIO 100.03 | Aktuasi Mundur Silinder B (B-) |
| **3Y1** | CIO 100.04 | Aktuasi Maju Silinder C (C+) |
| **3Y2** | CIO 100.05 | Aktuasi Mundur Silinder C (C-) |

---

## 🎮 Navigasi & Kontrol Kamera 3D

| Aksi Mouse / Keyboard | Fungsi |
| :--- | :--- |
| **Klik Kanan + Drag** | Rotasi / Orbit kamera 3D bebas |
| **Klik Tengah (Scroll Wheel) + Drag** | Menggeser sudut pandang kamera (*Pan*) |
| **Putar Roda Mouse (Scroll)** | Zoom in / Zoom out |
| **Klik Benda Kerja di Palet** | Memasukkan benda kerja (Merah / Hitam / Silver) ke tabung magasin |
| **Klik Tombol Kosongkan Magasin** | Mengosongkan tabung magasin |

---

## 🤝 Kontribusi & Request Contoh Program PLC

Apakah Anda memiliki program PLC untuk stasiun MPS ini menggunakan merk lain seperti:
* **Siemens (TIA Portal / S7-1200 / S7-300)**
* **Mitsubishi (GX Works 2 / GX Works 3)**
* **Schneider (EcoStruxure Machine Expert)**
* **Beckhoff (TwinCAT)**

Silakan kirimkan berkas program Anda melalui **Pull Request** ke folder Example program PLC/ agar dapat dimanfaatkan oleh para pelajar dan praktisi otomasi industri lainnya!

---

## 💖 Dukung Pengembang

Aplikasi ini dikembangkan secara independen untuk mendukung pendidikan otomasi dan mekatronika di Indonesia. Jika aplikasi dan contoh program ini bermanfaat untuk Anda, pertimbangkan untuk memberikan donasi secangkir kopi:

👉 **[Dukung melalui Saweria (https://saweria.co/ismaillowkey)](https://saweria.co/ismaillowkey)**

---

**Dikembangkan oleh:** [Ismail Lowkey](https://github.com/ismaillowkey)  
**Tautan Repositori:** [https://github.com/ismaillowkey/MPSPneumaticSimulator](https://github.com/ismaillowkey/MPSPneumaticSimulator)
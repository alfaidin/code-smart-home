
🏠 Advanced Smart Home Hub - ESP32 Dual-Core RTOS
Proyek ini adalah sistem kontrol dan monitoring rumah pintar komprehensif yang dirancang menggunakan ESP32. Sistem ini tidak hanya berfungsi sebagai saklar jarak jauh, tetapi juga sebagai pusat manajemen energi dan sistem keamanan baterai (BMS) yang terintegrasi dengan ekosistem Telegram.
🧠 Arsitektur Sistem: Dual-Core RTOS
Salah satu keunggulan utama proyek ini adalah penggunaan FreeRTOS untuk membagi beban kerja secara efisien pada dua core ESP32:
 * Core 0 (Background Task): Menangani konektivitas WiFi, Web Server, protokol Telegram Bot, dan polling sensor berat (PZEM & BMS). Ini memastikan data tetap up-to-date tanpa mengganggu visual.
 * Core 1 (UI & Interaction): Menangani render grafis pada TFT ILI9341 dan responsivitas touchscreen. Hasilnya adalah antarmuka pengguna yang mulus tanpa lag saat memproses data internet.
🚀 Fitur Unggulan
1. ⚡ Monitoring Energi Presisi (PZEM-004T)
Menggunakan sensor industri PZEM-004T untuk memantau parameter listrik AC secara real-time:
 * Tegangan (V), Arus (A), Daya (W), dan Akumulasi Energi (kWh).
 * Frekuensi (Hz) dan Power Factor (PF) untuk memantau kualitas daya listrik rumah.
2. 🔋 Smart BMS (Battery Management System) 3S
Sistem pemantauan baterai LiPo/Li-ion 3 sel (11.1V - 12.6V):
 * Individual Cell Monitoring: Memantau tegangan tiap sel untuk mendeteksi ketidakseimbangan (imbalance).
 * Auto-Notification: Mengirim peringatan ke Telegram jika tegangan sel di bawah 3.5V (Kritis).
 * Calibration Mode: Fitur kalibrasi ADC via Serial Monitor untuk akurasi pembacaan tegangan yang tinggi.
3. 🛡️ Keamanan Berlapis (Secured Relay)
Kontrol beban listrik (lampu/perangkat) dengan sistem keamanan:
 * PIN Protection: Akses saklar di layar TFT memerlukan kode keamanan.
 * Safety Warning: Peringatan visual sebelum aktivasi relay.
 * Remote Override: Kontrol penuh via Telegram Bot jika Anda berada di luar rumah.
4. 🌙 TFT Night Mode & Ambient Lamp
Fitur estetika yang mengubah fungsi layar menjadi lampu tidur:
 * Dapat diaktifkan via perintah Telegram (/tft_white, /tft_red, dll).
 * Mengubah seluruh layar menjadi emisi cahaya warna tertentu.
 * One-Touch Wakeup: Sentuh layar sekali untuk mematikan mode lampu dan kembali ke dashboard utama.
5. 🌐 Konektivitas Dual-Mode
 * Station Mode (STA): Terhubung ke router WiFi rumah untuk akses internet (Telegram & NTP Time).
 * Access Point Mode (AP): Menyediakan jaringan lokal mandiri untuk konfigurasi darurat dan Web Dashboard lokal di 192.168.4.1.
🛠️ Spesifikasi Teknis
| Komponen | Deskripsi |
|---|---|
| Microcontroller | ESP32 (Dual Core 240MHz) |
| Display | TFT ILI9341 2.8" (320x240 Resolution) |
| Touch Sensor | XPT2046 Resistive Touch |
| Power Sensor | PZEM-004T V3.0 (Isolasi Optocoupler) |
| Data Protocol | MQTT/HTTP, WebSockets, Telegram API |
| Time Sync | NTP Server (pool.ntp.org) |
📥 Cara Penggunaan
 * Persiapan: Instal semua library yang tertera di kode program.
 * Konfigurasi: Masukkan SSID WiFi dan Token Bot Telegram Anda.
 * Kalibrasi: Jika pembacaan baterai tidak akurat, gunakan perintah GUIDE pada Serial Monitor (115200 baud) untuk masuk ke mode kalibrasi ADC.
 * Akses Web: Buka browser dan ketik http://smarthome.local (mDNS) atau IP address yang muncul di layar saat startup.
📝 Catatan Keamanan
> Peringatan: Proyek ini melibatkan arus AC tegangan tinggi (PZEM). Pastikan semua sambungan terisolasi dengan baik. Penggunaan relay untuk beban induktif besar disarankan menggunakan tambahanced

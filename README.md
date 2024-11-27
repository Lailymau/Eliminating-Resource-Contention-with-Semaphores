# Exercise 8 - Using Semaphores to Protect Critical Sections

## 📄 Deskripsi Singkat
Proyek ini adalah implementasi sistem multitasking menggunakan **RTOS (Real-Time Operating System)** pada STM32 untuk mengontrol empat LED dengan pola berkedip tertentu. Dengan bantuan semaphore, sumber daya bersama dapat diakses dengan aman tanpa menimbulkan konflik.

---

## 🎯 Tujuan
1. 🔦 Memahami konsep multitasking dengan RTOS.
2. 🔗 Mengimplementasikan semaphore untuk mengelola akses ke sumber daya bersama.
3. 💡 Mengontrol beberapa LED secara bersamaan dengan pola berkedip teratur dan aman.

---

## 🛠️ Peralatan
- **Hardware**:
  - Microcontroller: STM32 (diuji pada STM32CubeMX dan STM32CubeIDE).
  - 4 LED: Hijau, Merah, Oranye, dan Biru.
  - Breadboard dan resistor.
- **Software**:
  - STM32CubeIDE untuk pengembangan kode.
  - STM32CubeMX untuk konfigurasi perangkat keras (file `.ioc`).

---

## ⚙️ Langkah Implementasi
1. 🔧 **Konfigurasi Perangkat Keras**:
   - Semua LED dihubungkan ke pin GPIO yang diatur sebagai output.
   - Clock sistem diatur untuk memastikan RTOS bekerja dengan frekuensi stabil.

2. 🖥️ **Penulisan Kode Utama**:
   - Setiap LED memiliki tugasnya sendiri di dalam RTOS.
   - Semaphore digunakan untuk memastikan hanya satu tugas yang dapat mengakses sumber daya kritis dalam satu waktu.

3. 🚦 **Tugas RTOS**:
   - **GreenTask**: Mengontrol LED Hijau (kritikal).
   - **RedTask**: Mengontrol LED Merah (kritikal).
   - **OrangeTask**: Mengontrol LED Oranye (non-kritikal).
   - **Blue LED**: Indikator konflik jika semaphore gagal diambil.

4. 🔗 **Semaphore**:
   - Digunakan untuk memastikan akses eksklusif ke sumber daya bersama (fungsi `AccessSharedData`).

5. 🛠️ **Simulasi Konflik**:
   - Konflik dihasilkan dengan mempercepat interval akses sumber daya kritis.
   - Jika konflik terjadi, **LED Biru** menyala untuk memberikan peringatan.

---

## 📜 Struktur Kode
### Fungsi Utama
- **AccessSharedData**: Mensimulasikan akses ke sumber daya kritis dengan penundaan (500 ms) dan memastikan status flag diatur dengan benar untuk mencegah konflik.
- **GreenTask dan RedTask**: Mengambil semaphore sebelum mengakses `AccessSharedData` untuk mencegah konflik.
- **OrangeTask**: Berkedip secara independen tanpa pengaruh semaphore.
- **SimulateReadWriteOperation**: Loop dummy untuk mensimulasikan waktu proses.

---

## 📊 Hasil yang Diharapkan
- Semua LED berkedip sesuai tugas masing-masing:
  - **LED Hijau**: Berkedip dengan interval teratur (500 ms), menunjukkan akses ke sumber daya kritis.
  - **LED Merah**: Berkedip dengan pola serupa, dengan kontrol akses ke sumber daya kritis.
  - **LED Oranye**: Berkedip cepat (50 ms) secara independen tanpa pengaruh semaphore.
- Tidak ada **konflik akses** pada sumber daya bersama.
- **LED Biru** menyala **hanya jika terjadi konflik** (indikasi semaphore gagal diambil).

---

## 🧪 Hasil Percobaan



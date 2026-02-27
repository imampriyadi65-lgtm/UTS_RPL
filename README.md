# Sistem Absensi Tamu Berbasis Registrasi Online dan QR Code

**Dibuat oleh:**

- imam priyadi (220220006)

Sistem ini dirancang untuk mempermudah pencatatan tamu dalam sebuah instansi dengan memanfaatkan registrasi online dan QR Code. Sistem ini meningkatkan efisiensi operasional, memperkuat keamanan data, dan memudahkan pelacakan kunjungan tamu.

## Latar Belakang

Metode manual menggunakan buku tamu sering menimbulkan masalah seperti:

- Kesalahan pencatatan
- Antrian panjang
- Sulit melakukan pelacakan data

Sistem absensi berbasis registrasi online dengan QR Code memungkinkan tamu mendaftar sebelum kedatangan dan memperoleh identitas digital yang dapat diverifikasi cepat oleh resepsionis.

## Use Case Diagram

**Actor:**

- Tamu
- Resepsionis

![Use Case Diagram](https://github.com/hawasih/UTS-Rekayasa-Perangkat-Lunak/blob/main/Use%20Case%20Diagram%20.png)

## Class Diagram

![Class Diagram](https://github.com/hawasih/UTS-Rekayasa-Perangkat-Lunak/blob/main/Class%20Diagram.jpeg)

### Penjelasan Kelas Utama

1. **Tamu**
   - Menyimpan data tamu dan QR Code.
   - Interaksi: Registrasi → QRCodeGenerator → Check-in → AbsensiService.

2. **Resepsionis**
   - Melakukan pemindaian QR Code dan validasi tamu.
   - Interaksi: QRCodeScanner → AbsensiService → AbsensiRepository.

3. **QRCodeGenerator & QRCodeScanner**
   - Generator: Membuat QR Code dari ID tamu.
   - Scanner: Membaca QR Code untuk validasi.

4. **AbsensiLog**
   - Catatan kedatangan tamu.
   - Hubungan 1-to-many dengan Tamu.

5. **TamuRepository & AbsensiRepository**
   - Mengelola penyimpanan data ke database.
   - Digunakan oleh service terkait.

6. **TamuService & AbsensiService**
   - Service yang mengatur registrasi dan check-in tamu.

## Prinsip SOLID yang Digunakan

- **Single Responsibility Principle (SRP)**: Setiap kelas memiliki satu tanggung jawab, memudahkan maintainability dan testing.
- **Contoh:** QRCodeGenerator hanya membuat QR Code, TamuService hanya mengelola registrasi.

## Design Pattern

- **Singleton**: DatabaseConnection
- **Factory Method**: GuestFactory
- **Builder**: GuestRegistrationBuilder

## Activity Diagram

![Activity Diagram](https://github.com/hawasih/UTS-Rekayasa-Perangkat-Lunak/blob/main/activity%20diagram.png)

### Ringkasan Aktivitas

1. Tamu membuka form registrasi → mengisi data → sistem validasi → simpan ke database → generate QR → kirim ke tamu.
2. Tamu datang → resepsionis scan QR → sistem verifikasi → update absensi → tamu dipersilahkan masuk.

## Sequence Diagram

![Sequence Diagram](https://github.com/hawasih/UTS-Rekayasa-Perangkat-Lunak/blob/main/sequence%20diagram.png)

### Ringkasan Sequence

1. Registrasi tamu → validasi data → simpan → generate QR → kirim ke tamu.
2. Tamu hadir → QR discan → sistem validasi → update kehadiran → notifikasi berhasil masuk.

## Siklus Hidup Data Tamu

1. **Registered:** Data tamu tersimpan.
2. **QRGenerated:** QR Code dihasilkan.
3. **Arrived:** Tamu hadir di lokasi.
4. **Verified:** QR Code tervalidasi.
5. **CheckedIn:** Tamu resmi masuk.
6. **Completed:** Kunjungan selesai.

## Evaluasi Desain

**Maintainability**

- Setiap kelas memiliki tanggung jawab tunggal (SRP).
- Mudah diperbaiki karena modul-modul terpisah.
- Menggunakan design pattern yang stabil.

  **Reusability**

- `GuestFactory` dapat digunakan untuk berbagai jenis tamu.
- `QRCodeGenerator` dapat digunakan untuk tiket, reservasi, dll.
- `DatabaseConnection` Singleton digunakan di seluruh modul.

  **Scalability**

- Penerapan Open/Closed Principle memudahkan penambahan fitur baru.
- Repository memudahkan migrasi database.
- Builder memudahkan penambahan field registrasi.

## Usulan Pengembangan Sistem

- Fitur check-out otomatis menggunakan GPS/beacon.
- Dashboard monitoring kunjungan secara realtime.
- Notifikasi otomatis ke divisi terkait.
- Integrasi door-access untuk pintu otomatis.

---


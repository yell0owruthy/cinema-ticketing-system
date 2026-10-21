Markdown
<div align="center">
  <img src="public/image/logo.png" alt="Logo Bioskop" width="120">

  # 🎬 Sistem Informasi Tiket Bioskop (Cinema Ticketing System)

  Aplikasi pemesanan tiket bioskop berbasis web yang dirancang secara profesional dengan fitur manajemen jadwal, pemesanan tiket, dan pelaporan rekapitulasi data dinamis. Proyek ini dibangun untuk memenuhi persyaratan Uji Kompetensi / Sertifikasi Keahlian Rekayasa Perangkat Lunak (RPL).

  ![Laravel](https://img.shields.io/badge/Laravel-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)
  ![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)
  ![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)
  ![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
</div>

---

## ✨ Fitur Utama

Sistem ini menggunakan multi-autentikasi (Breeze) yang membagi hak akses menjadi dua peran utama:

### 🛡️ Administrator (Admin)
- **Dashboard Statistik:** Ringkasan aktivitas dan menu pintasan utama.
- **Kelola Jadwal & Film:** CRUD data jadwal tayang, deskripsi film, dan harga tiket.
- **Kelola Penonton:** Manajemen data akun pengguna yang terdaftar di sistem.
- **Laporan Penjualan:** Rekapitulasi transaksi pemesanan tiket dengan fitur **Filter Rentang Tanggal (Periode)** serta kalkulasi otomatis total tiket terjual dan total pendapatan.

### 👤 Penonton (User)
- **Katalog Film:** Menampilkan daftar film yang sedang tayang beserta jadwal dan harga tiket.
- **Pemesanan Tiket:** Form pemesanan tiket bioskop secara real-time.
- **Riwayat Transaksi:** Tabel riwayat pembelian tiket bioskop beserta status pembayaran dan total harga.

---

## 🛠️ Teknologi yang Digunakan

- **Framework:** Laravel 10 / 11
- **Frontend:** Blade Templating, Tailwind CSS, Alpine.js
- **Database:** MySQL
- **Autentikasi:** Laravel Breeze
- **Ikon & Tipografi:** SVG Icons, Google Fonts

---

## 🚀 Panduan Instalasi (Local Development)

Ikuti langkah-langkah berikut untuk menjalankan project ini di komputer lokal Anda:

**1. Clone Repository**
```bash
git clone [https://github.com/username-kamu/nama-repo-kamu.git](https://github.com/username-kamu/nama-repo-kamu.git)
cd nama-repo-kamu
2. Install Dependencies

Bash
composer install
npm install
3. Konfigurasi Environment
Duplikat file .env.example menjadi .env, lalu atur koneksi database Anda:

Bash
cp .env.example .env
php artisan key:generate
(Pastikan Anda sudah membuat database kosong di MySQL/phpMyAdmin, misalnya bernama db_bioskop, lalu sesuaikan DB_DATABASE di dalam file .env)

4. Migrasi Database & Seeder Data Dummy
Jalankan perintah ini untuk membangun struktur tabel dan mengisi 15 data dummy penonton beserta riwayat transaksi otomatis:

Bash
php artisan migrate
php artisan db:seed --class=PemesananSeeder
5. Kompilasi Aset Frontend & Jalankan Server
Buka dua terminal berbeda dan jalankan perintah berikut secara bersamaan:

Bash
# Terminal 1 (Untuk memproses Tailwind CSS)
npm run dev

# Terminal 2 (Untuk menjalankan server Laravel)
php artisan serve
Aplikasi kini dapat diakses melalui browser di: http://127.0.0.1:8000

🔐 Akses Akun Dummy (Seeder)
Gunakan kredensial berikut untuk masuk ke dalam sistem:

Akses Admin:

Email: admin@bioskop.com

Password: password

Akses Penonton (Pilih salah satu dari 15 dummy):

Email: dummy1@bioskop.com (bisa diganti angka 1-15)

Password: password

📸 Dokumentasi Antarmuka (Screenshots)
(Tambahkan screenshot aplikasi Anda di sini nanti untuk mempercantik repositori)

Screenshot Dashboard Admin

Screenshot Halaman Laporan

Screenshot Halaman Pemesanan User

🎬 Sistem Informasi Tiket Bioskop (Cinema Ticketing System)

  Aplikasi pemesanan tiket bioskop berbasis web yang dirancang secara profesional dengan fitur manajemen jadwal, pemesanan tiket, dan pelaporan rekapitulasi data dinamis. Proyek ini dibangun untuk memenuhi persyaratan Uji Kompetensi / Sertifikasi Keahlian Rekayasa Perangkat Lunak (RPL).

  ![Laravel](https://img.shields.io/badge/Laravel-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)
  ![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)
  ![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)
  ![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
</div>



# Sistem Pemesanan Tiket Bioskop

Aplikasi web untuk mengelola jadwal tayang film dan pemesanan tiket bioskop. Admin dapat mengelola jadwal, harga tiket, data penonton, dan laporan transaksi. Penonton dapat melihat jadwal, memesan tiket, serta memeriksa riwayat pemesanan.

## Fitur

### Admin

- Dashboard admin.
- Menambah, melihat, mengubah, dan menghapus jadwal tayang beserta harga tiket.
- Mengelola data akun penonton.
- Melihat laporan transaksi berdasarkan rentang tanggal, termasuk jumlah tiket terjual dan total pendapatan.

### Penonton

- Membuat akun, masuk, dan mengelola profil.
- Melihat katalog jadwal film dan harga tiket.
- Memesan satu atau lebih tiket.
- Melihat riwayat pemesanan dan total pembayaran.

### Sistem

- Hak akses dibedakan berdasarkan peran `admin` dan `user`.
- Data aplikasi disimpan di SQLite secara default.
- Antarmuka dirender menggunakan Blade, dengan aset frontend yang dibangun melalui Vite dan Tailwind CSS.

## Teknologi

- PHP 8.2+
- Laravel 12
- SQLite
- Blade
- Tailwind CSS 3
- Vite 7
- Alpine.js

## Persyaratan

Pastikan perangkat sudah memiliki:

- PHP 8.2 atau lebih baru, dengan ekstensi PHP yang dibutuhkan Laravel (termasuk `pdo_sqlite` untuk database bawaan).
- [Composer](https://getcomposer.org/).
- [Node.js dan npm](https://nodejs.org/).

## Instalasi

Jalankan perintah berikut dari direktori proyek. Contoh ini menggunakan PowerShell di Windows.

1. Pasang dependensi PHP:

   ```powershell
   composer install
   ```

2. Siapkan konfigurasi lingkungan dan database SQLite:

   ```powershell
   if (-not (Test-Path .env)) { Copy-Item .env.example .env }
   if (-not (Test-Path database\database.sqlite)) {
       New-Item -ItemType File -Path database\database.sqlite | Out-Null
   }
   ```

   Perintah ini mempertahankan file `.env` dan database SQLite yang sudah ada. Pastikan konfigurasi database di `.env` menunjuk ke SQLite atau database lain yang ingin digunakan.

3. Buat application key dan jalankan migrasi:

   ```powershell
   php artisan key:generate
   php artisan migrate
   ```

4. Pasang dependensi frontend dan bangun aset:

   ```powershell
   npm install
   npm run build
   ```

## Menjalankan aplikasi

Untuk menjalankan server Laravel, worker antrean, log, dan Vite secara bersamaan dalam mode pengembangan:

```powershell
composer run dev
```

Atau jalankan server Laravel dan Vite secara terpisah di dua terminal:

```powershell
php artisan serve
```

```powershell
npm run dev
```

Kemudian buka [http://localhost:8000](http://localhost:8000).

## Data awal dan akun demo

Untuk membuat akun demo yang didefinisikan di `DatabaseSeeder`, jalankan:

```powershell
php artisan db:seed
```

Seeder menyediakan akun berikut:

| Peran yang dimaksud | Email | Kata sandi |
| --- | --- | --- |
| Admin | `admin@bioskop.com` | `password` |
| Penonton | `penonton@bioskop.com` | `password` |

**Catatan:** model `User` saat ini tidak memasukkan kolom `role` ke daftar mass-assignment. Akibatnya, peran yang diberikan oleh seeder dapat tersimpan sebagai `user` (peran default database). Jika akun demo admin belum dapat membuka area admin, ubah perannya melalui Tinker:

```powershell
php artisan tinker
```

```php
\App\Models\User::where('email', 'admin@bioskop.com')->update(['role' => 'admin']);
```

Keluar dari Tinker dengan `exit`. Akun demo menggunakan kata sandi sederhana dan hanya untuk pengembangan lokal—ganti atau hapus akun tersebut sebelum aplikasi digunakan di lingkungan lain.

Seeder opsional `PemesananSeeder` membuat data film, jadwal, harga, serta data pemesanan contoh:

```powershell
php artisan db:seed --class=PemesananSeeder
```

## Pengujian dan build

Jalankan pengujian aplikasi:

```powershell
composer test
```

Build aset frontend untuk penggunaan non-development:

```powershell
npm run build
```

## Struktur proyek

```text
app/
  Http/Controllers/    Controller autentikasi, admin, dan pemesanan
  Http/Middleware/     Middleware pemeriksaan peran
  Models/              Model User, Film, Jadwal, HargaTiket, Pemesanan
database/
  migrations/          Struktur tabel dan relasi database
  seeders/             Akun serta data contoh
resources/
  views/               Halaman Blade untuk admin, penonton, dan autentikasi
  js/                  Entry point JavaScript
  css/                 Entry point stylesheet
routes/
  web.php              Route web aplikasi
tests/
  Feature/             Pengujian fitur dan autentikasi
  Unit/                Pengujian unit
```

## Alur data utama

- Satu film dapat memiliki beberapa jadwal tayang.
- Setiap jadwal memiliki harga tiket.
- Pemesanan menghubungkan akun penonton dengan jadwal, jumlah tiket, total harga, dan status.
- Laporan admin menghitung pendapatan dan jumlah tiket dari data pemesanan pada periode yang dipilih.

## Catatan implementasi

- Pemesanan saat ini langsung diberi status **Lunas**. Integrasi payment gateway belum tersedia.
- Data film dibuat saat admin menambahkan jadwal; judul yang belum ada akan dibuat otomatis.
- Tidak ada pengelolaan jumlah kursi atau kapasitas studio pada implementasi saat ini.
- Konfigurasi bawaan proyek menggunakan SQLite. Sesuaikan variabel `DB_*` di `.env` jika ingin menggunakan database lain.
- Jangan gunakan `.env` lokal atau akun demo dengan kata sandi bawaan untuk deployment produksi.

## Lisensi

Proyek ini menggunakan kerangka kerja Laravel. Lisensi kode aplikasi mengikuti ketentuan yang ditetapkan oleh pemilik proyek.
#

<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

<p align="center">
<a href="https://github.com/laravel/framework/actions"><img src="https://github.com/laravel/framework/workflows/tests/badge.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

# LaraPress - Aplikasi Blog Sederhana

LaraPress adalah aplikasi blog sederhana yang dibangun menggunakan Laravel 12 untuk tujuan pembelajaran dan pengembangan keterampilan web development.

## 📋 Tentang Proyek

Proyek ini dibuat sebagai bagian dari pembelajaran Laravel framework. LaraPress mendemonstrasikan konsep-konsep dasar Laravel seperti routing, views, dan struktur MVC.

## 🚀 Fitur yang Sudah Diimplementasikan

### 1. **Halaman Utama (Welcome Page)**
   - Mengubah tampilan default Laravel menjadi halaman sederhana
   - Menampilkan judul "Selamat Datang di LaraPress"
   - Struktur HTML yang bersih dan minimal

### 2. **Halaman Tentang Kami**
   - Route: `/about`
   - Menampilkan informasi tentang LaraPress
   - Menjelaskan tujuan proyek sebagai pembelajaran Laravel 12

### 3. **Halaman Kontak**
   - Route: `/kontak`
   - Menampilkan informasi kontak pengembang

## 📁 Struktur File yang Dimodifikasi

### File yang Dibuat/Dimodifikasi:

1. **`resources/views/welcome.blade.php`**
   - Mengubah tampilan default Laravel yang kompleks menjadi struktur HTML sederhana
   - Menampilkan pesan sambutan untuk pengunjung blog

2. **`resources/views/about.blade.php`** (BARU)
   - File view baru untuk halaman "Tentang Kami"
   - Berisi informasi tentang LaraPress sebagai proyek pembelajaran

3. **`resources/views/kontak.blade.php`** (BARU)
   - File view baru untuk halaman "kontak"
   - Berisi informasi tentang kontak pengembang

4. **`routes/web.php`**
   - Menambahkan route baru `/about` yang mengarah ke view `about.blade.php`
   - Menambahkan route baru `/kontak` yang mengarah ke view `kontak.blade.php`

## 🛠️ Langkah-langkah Implementasi

### Step 1: Modifikasi Halaman Welcome
Mengubah file `resources/views/welcome.blade.php` dari tampilan default Laravel (266 baris) menjadi HTML sederhana:

```html
<!DOCTYPE html>
<html>
<head>
 <title>Selamat Datang di LaraPress</title>
</head>
<body>
 <h1>Selamat Datang di Blog LaraPress</h1>
 <p>Ini adalah halaman utama dari aplikasi blog kita.</p>
 <a href="/tentang-kami">Lihat Halaman Tentang Kami</a>
 <a href="/kontak">Kembali ke Halaman Utama</a>
</body>
</html>
```

### Step 2: Membuat Route Baru
Menambahkan route baru di `routes/web.php`:

```php
Route::get('/about', function () {
    return view('about');
});
Route::get('/kontak', function () {
    return view('kontak');
});

### Step 3: Membuat View About
Membuat file baru `resources/views/about.blade.php`:

```html
<html>
<head>
 <title>Tentang Kami - LaraPress</title>
</head>
<body>
 <h1>Tentang LaraPress</h1>
 <p>LaraPress adalah sebuah proyek blog sederhana yang dibuat untuk
mempelajari dasar-dasar framework Laravel 12.</p>

<a href="/">Kembali ke Halaman Utama</a>
<a href="/kontak">Kembali ke Halaman Utama</a>

</body>
</html>
```

### Step 4: Membuat View Contact
Membuat file baru `resources/views/contact.blade.php`:

```html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Selamat Datang di LaraPress</title>
</head>
<body>

    <nav>
        <div class="logo">LaraPress</div>
    </nav>

    <div class="container">
        <h1>Kontak Tim Kami</h1>
        <div class="col">
            <div id="form">
                <form action="#" method="post">
                    <label for="nama1">Nama</label>
                    <input type="text" id="nama1" name="nama" placeholder="Masukkan nama kamu" required>

                    <label for="email1">Email</label>
                    <input type="email" id="email1" name="email" placeholder="Masukkan email kamu" required>

                    <label for="pesan1">Pesan</label>
                    <textarea id="pesan1" name="pesan" placeholder="Tulis pesan kamu..." required></textarea>

                    <button type="submit">Kirim Pesan</button>
                </form>
            </div>

            <div class="info">
                <h3>Hubungi Kami</h3>
                <p>Email: support@larapress.com</p>
                <p>Telepon: (021) 123-4567</p>
                  <iframe
                    src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3952.965197674812!2d110.3671!3d-7.801389!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x2e7a578c0e1234ab%3A0xabcdef1234567890!2sDummy%20Location!5e0!3m2!1sid!2sid!4v1234567890123"
                    width="500" height="240" style="border:0;" allowfullscreen="" loading="lazy">
                </iframe>
                <a href="/">Kembali ke Halaman Utama</a>
                <a href="/tentang-kami">Lihat Halaman Tentang Kami</a>
            </div>
        </div>
    </div>

</body>
</html>
```

## 🌐 Endpoint yang Tersedia

| Route | Method | Deskripsi |
|-------|--------|-----------|
| `/` | GET | Halaman utama LaraPress |
| `/about` | GET | Halaman tentang LaraPress |
| `/kontak` | GET | Halaman tentang kontak pengembang |

## 💻 Teknologi yang Digunakan

- **Framework**: Laravel 12
- **PHP Version**: 8.x
- **Database**: MySQL
- **Frontend**: Blade Template Engine, HTML, CSS
- **Build Tool**: None

## 📦 Instalasi

1. Clone repository ini:
```bash
git clone https://github.com/xnoname2003/prak-pbw-a/tree/main/Prak3/LaraPress
```

2. Install dependencies:
```bash
composer install
npm install
```

3. Buat file `.env`:
```bash
cp .env.example .env
```

4. Generate application key:
```bash
php artisan key:generate
```

5. Jalankan development server:
```bash
php artisan serve
```

6. Akses aplikasi di browser:
```
http://localhost:8000
```
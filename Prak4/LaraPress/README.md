<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

<p align="center">
<a href="https://github.com/laravel/framework/actions"><img src="https://github.com/laravel/framework/workflows/tests/badge.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

# Praktikum 4: Sistem Autentikasi dengan Laravel Breeze

**Nama:** Zidan wali Arubusman  
**NPM:** 4523210001  
**Tanggal:** 17 Oktober 2025  
**Materi:** Implementasi Autentikasi Pengguna   
**Dosen Pengampu:** Bambang Riono Arsad, S.Kom., MMSI

---

## 📋 Deskripsi

Pada praktikum ini, kita akan menambahkan fitur autentikasi lengkap menggunakan Laravel Breeze, termasuk:
- Registrasi pengguna baru
- Login & Logout
- Dashboard pengguna
- Profile management
- Password reset
- Email verification
- Session management

---

## 🔐 Konsep Autentikasi

### Apa itu Autentikasi?

**Autentikasi** adalah proses verifikasi identitas pengguna. Menjawab pertanyaan: **"Siapa Anda?"**

**Analogi:** Seperti menunjukkan KTP di gerbang kampus - satpam memverifikasi bahwa Anda adalah orang yang sah.

### Autentikasi vs Otorisasi

| Autentikasi | Otorisasi |
|-------------|-----------|
| "Siapa Anda?" | "Apa yang boleh Anda lakukan?" |
| Login dengan password | User role & permissions |
| Memverifikasi identitas | Mengontrol akses |

### Alur Kerja Login

```
1. User input email & password
   ↓
2. Aplikasi cari user berdasarkan email
   ↓
3. Hash password yang diinput
   ↓
4. Bandingkan hash dengan database
   ↓
5. Jika cocok → Buat session
   ↓
6. User berhasil login
```

### Password Hashing

**Kenapa password di-hash?**
- Password TIDAK disimpan dalam bentuk asli (plain text)
- Di-hash menggunakan algoritma satu arah (Bcrypt/Argon2)
- Meskipun database bocor, password tetap aman

**Analogi:** Seperti menggiling daging jadi sosis - mudah mengubah daging jadi sosis, tapi tidak bisa balik lagi.

### Session & Cookies

**Analogi Stempel Konser:**
- Login = Tunjukkan tiket di pintu masuk
- Cookie = Stempel di tangan Anda
- Selanjutnya = Cukup tunjukkan stempel, tidak perlu tiket lagi

---

## 🛠️ Langkah-langkah Implementasi

### Langkah 1: Install Laravel Breeze

```bash
composer require laravel/breeze --dev
```

**Penjelasan:** Install package Breeze sebagai development dependency.

---

### Langkah 2: Install Scaffolding Breeze

```bash
php artisan breeze:install blade --pest
```

**Pilihan:**
- Template: Blade with Alpine
- Testing: Pest

**Yang diinstall:**
- Controllers autentikasi
- Views (login, register, dll)
- Routes autentikasi
- Tailwind CSS
- Testing setup

---

### Langkah 3: Install Dependencies Frontend

```bash
npm install
```

**Penjelasan:** Install dependencies JavaScript yang dibutuhkan (Tailwind CSS, Alpine.js, dll).

---

### Langkah 4: Compile Assets

```bash
npm run dev
```

**Penjelasan:** Compile CSS dan JavaScript menggunakan Vite.

---

### Langkah 5: Jalankan Migrasi

```bash
php artisan migrate
```

**Yang ditambahkan ke database:**
- Tabel `users` (jika belum ada)
- Tabel `password_reset_tokens`
- Tabel `sessions`
- Kolom `remember_token` di tabel users

---

## 📂 File yang Ditambahkan oleh Breeze

### Controllers (9 files)
Lokasi: `app/Http/Controllers/Auth/`

| File | Fungsi |
|------|--------|
| `AuthenticatedSessionController.php` | Login & Logout |
| `RegisteredUserController.php` | Registrasi user baru |
| `PasswordResetLinkController.php` | Request reset password |
| `NewPasswordController.php` | Set password baru |
| `EmailVerificationNotificationController.php` | Kirim email verifikasi |
| `EmailVerificationPromptController.php` | Tampil notif verifikasi |
| `VerifyEmailController.php` | Verifikasi email |
| `PasswordController.php` | Update password |
| `ConfirmablePasswordController.php` | Konfirmasi password |

### Views (6 files)
Lokasi: `resources/views/auth/`

| File | Fungsi |
|------|--------|
| `login.blade.php` | Form login |
| `register.blade.php` | Form registrasi |
| `forgot-password.blade.php` | Form lupa password |
| `reset-password.blade.php` | Form reset password |
| `verify-email.blade.php` | Halaman verifikasi email |
| `confirm-password.blade.php` | Form konfirmasi password |

### Layouts & Components
- `resources/views/layouts/app.blade.php` - Layout utama
- `resources/views/layouts/guest.blade.php` - Layout untuk guest
- `resources/views/layouts/navigation.blade.php` - Navigation bar
- `resources/views/dashboard.blade.php` - Dashboard
- `resources/views/profile/edit.blade.php` - Edit profile

### Routes
- `routes/auth.php` - Semua route autentikasi

---

## 🌐 Routes Autentikasi

### Public Routes
| Route | Method | Deskripsi |
|-------|--------|-----------|
| `/` | GET | Halaman Utama|
| `/about` | GET | Halaman About Us|
| `/contact` | GET | Halaman Contact|
| `/login` | GET, POST | Halaman & proses login |
| `/register` | GET, POST | Halaman & proses registrasi |
| `/forgot-password` | GET, POST | Request link reset password |
| `/reset-password/{token}` | GET, POST | Reset password dengan token |

### Protected Routes (Perlu Login)
| Route | Method | Deskripsi |
|-------|--------|-----------|
| `/dashboard` | GET | Dashboard user |
| `/profile` | GET | Halaman edit profile |
| `/profile` | PATCH | Update profile |
| `/profile` | DELETE | Hapus akun |
| `/logout` | POST | Logout |
| `/verify-email` | GET | Notifikasi verifikasi email |
| `/confirm-password` | GET, POST | Konfirmasi password |

---

## 🔒 Middleware Protection

### Apa itu Middleware?

Middleware adalah "penjaga" yang memeriksa request sebelum mencapai controller.

**Analogi:** Satpam yang cek kartu akses sebelum Anda masuk gedung.

### Cara Menggunakan Middleware

**Single Route:**
```php
Route::get('/dashboard', function () {
    return view('dashboard');
})->middleware('auth');
```

**Route Group:**
```php
Route::middleware('auth')->group(function () {
    Route::get('/dashboard', [DashboardController::class, 'index']);
    Route::get('/profile', [ProfileController::class, 'edit']);
});
```

**Multiple Middleware:**
```php
Route::get('/dashboard', function () {
    return view('dashboard');
})->middleware(['auth', 'verified']);
```

---

## 🎨 Fitur Breeze yang Tersedia

### 1. Autentikasi Dasar
- ✅ Registrasi pengguna baru
- ✅ Login dengan email & password
- ✅ Logout
- ✅ Remember Me functionality

### 2. Password Management
- ✅ Lupa password (kirim link via email)
- ✅ Reset password dengan token
- ✅ Update password di profile
- ✅ Konfirmasi password untuk aksi sensitif

### 3. Email Verification
- ✅ Kirim email verifikasi saat registrasi
- ✅ Verifikasi email dengan link
- ✅ Kirim ulang email verifikasi
- ✅ Middleware `verified` untuk route

### 4. Profile Management
- ✅ Edit profile (name, email)
- ✅ Update password
- ✅ Delete account

### 5. Session Management
- ✅ Session handling otomatis
- ✅ Cookie management
- ✅ CSRF protection

---

## 🔐 Fitur Keamanan

### 1. Password Hashing
```php
// Password di-hash sebelum disimpan
'password' => Hash::make($request->password)

// Verifikasi password
Hash::check($request->password, $user->password)
```

**Algoritma:** Bcrypt (default Laravel)

### 2. CSRF Protection
```blade
<form method="POST" action="{{ route('login') }}">
    @csrf  <!-- Token CSRF wajib -->
    <!-- form fields -->
</form>
```

### 3. Session Security
- Session ID di-regenerate setelah login
- HttpOnly cookies (tidak bisa diakses JavaScript)
- Secure cookies di production (HTTPS)

### 4. Rate Limiting
- Throttle di route login (anti brute force)
- Throttle di email verification
- Throttle di password reset

---

## 📊 Database Schema

### Tabel: users
| Column | Type | Description |
|--------|------|-------------|
| id | bigint | Primary key |
| name | string | Nama user |
| email | string | Email (unique) |
| email_verified_at | timestamp | Waktu verifikasi email |
| password | string | Password (hashed) |
| remember_token | string | Token untuk "Remember Me" |
| created_at | timestamp | Waktu dibuat |
| updated_at | timestamp | Waktu diupdate |

### Tabel: password_reset_tokens
| Column | Type | Description |
|--------|------|-------------|
| email | string | Email user |
| token | string | Token reset password |
| created_at | timestamp | Waktu dibuat |

### Tabel: sessions
| Column | Type | Description |
|--------|------|-------------|
| id | string | Session ID |
| user_id | bigint | ID user (nullable) |
| ip_address | string | IP address |
| user_agent | text | Browser info |
| payload | longtext | Session data |
| last_activity | integer | Waktu aktivitas terakhir |

---
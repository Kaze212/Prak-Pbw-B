<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

<p align="center">
<a href="https://github.com/laravel/framework/actions"><img src="https://github.com/laravel/framework/workflows/tests/badge.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

# Laporan Laravel Filament

## Zidan Wali Arubusman

## 4523210001

## Installation

### 1. Buat Proyek Laravel Baru

1. Buat Proyek Kosong

    ```
    laravel new smpmentari_filament
    ```

2. Masuk ke Direktori Laravel smpmentari_filament

    ```
    cd smpmentari_filament
    ```

3. Coba Jalankan Server Untuk Uji Coba

    ```
    php artisan serve
    ```

### 2. Konfigurasi Database

1. Buka Aplikasi Service Kesayangan Kalian & Siapkan DB
    - Bisa pake MAMP, XAMPP
2. Konfigurasi .env
    - Buka file .env di root proyek, sesuaikan dengan berikut :
      ```
      DB_CONNECTION=mysql
      DB_HOST=127.0.0.1
      DB_PORT=8889
      DB_DATABASE=smpmentari_filament
      DB_USERNAME=root
      DB_PASSWORD=root
      ```
3. Migrasi Awal
    - Jika belum ada database smpmentari_filament, ketik yes untuk membuat database
        ```
        php aritisan migrate
        ```

### 3. Install Filament

1. Pasang Paket Filament

    ```
    composer require "filament/filament"
    ```

2. Generate Panel Admin

    ```
    php artisan filament:install --panels
    ```
    `- Panel ID = admin`

3. Buat Akun Filament

    ```
    php artisan make:filament-user
    ```
    ```
    - nama : root
    - email : root@email.com
    - password : root
    ```

4. Link Storage Untuk Upload
    - Jalankan server php artisan serve buka di browser 127.0.0.1:8000/admin
    ```
    php artisan storage:link
    ```

### 4. Desain Data Minimal (Tema SMP Mentari)

-   Kita pakai dua entitas untuk CRUD latihan:
    1.  kegiatan : judul, tanggal, ringkasan, isi, foto
    2.  siswa : nisn, nama, jenis_kelamin, kelas, tanggal_lahir, alamat

- Buat Model + Migrasi

    ```
    php artisan make:model Kegiatan -m
    ```
    ```
    php artisan make:model Siswa -m
    ```

- Edit Migrasi :

    1. di file proyek `database/migrations/xxxx_xx_xx_xxxxxx_create_kegiatans_table.php`

        ```
        public function up(): void
        {
            Schema::create('kegiatans', function (Blueprint $table) {
                $table->id();
                $table->string('judul');
                $table->date('tanggal');
                $table->string('ringkasan')->nullable();
                $table->text('isi')->nullable();
                $table->string('foto')->nullable(); // path gambar
                $table->timestamps();
            });
        }
        ```

    2. di file proyek `database/migrations/xxxx_xx_xx_xxxxxx_create_siswas_table.php`

        ```
        public function up(): void
        {
            Schema::create('siswas', function (Blueprint $table) {
                $table->id();
                $table->string('nisn')->unique();
                $table->string('nama');
                $table->enum('jenis_kelamin', ['L', 'P']);
                $table->string('kelas'); // contoh: 7A, 8B, 9C
                $table->date('tanggal_lahir')->nullable();
                $table->text('alamat')->nullable();
                $table->timestamps();

            });
        }
        ```

- Jalakan migrasi

    ```
    php artisan migrate
    ```

### 5. Generate Filament Resource (CRUD Otomatis)

1. Filament akan membuat halaman List / Create / Edit lengkap.

    ```
    php artisan make:filament-resource Kegiatan --generate
    ```
    ```
    php artisan make:filament-resource Siswa --generate
    ```

    Perintah di atas membuat:

    -   `app/Filament/Resources/KegiatanResource.php`
    -   `app/Filament/Resources/KegiatanResource/Pages/{Create,Edit,List}Kegiatans.php`
    -   `app/Filament/Resources/SiswaResource.php`
    -   `app/Filament/Resources/SiswaResource/Pages/{Create,Edit,List}Siswas.php`

2.  Form & Tabel KegiatanResource

    Edit `app/Filament/Resources/KegiatanResource.php` bagian `form()` dan `table()` contoh minimal:
    1. `KegiatanResource.php`
    2. `KegiatanForm.php`
    3. `KegiatanTable.php`

3. Form & Tabel SiswaResource

    1. `SiswaResource.php`
    2. `SiswaTable.php`
    3. `SiswaForm.php`
    4. `App\Models\Kegiatan.php`
    5. `App\Models\Siswa.php`

### 6. Branding Panel : Identitas SMP Mentari

-   Buka `app/Providers/Filament/AdminPanelProvider.php` dan sesuaikan:
    ```
    ->brandName('SMP Mentari')
    ->navigationGroups([
        'Akademik', 'Publikasi'
    ])
    ->sidebarCollapsibleOnDesktop(true);
    ```

### 7. Halaman Depan (Public) yang Simple

-   Walau fokus praktikum adalah Filament (admin), tambahkan landing page publik agar konteks sekolah terasa.

    1. Route

        ```
        Route::get('/', function () {
            return view('welcome');
        });

        Route::get('/kegiatan', function () {
            return view('kegiatan-public', [
                'items' => \App\Models\Kegiatan::latest()->paginate(9),
            ]);
        });
        ```

-   View `resources/views/kegiatan-public.blade.php`
-   View `resources/views/layouts/app.blade.php`
-   Pastikan sudah menjalankan `php artisan storage:link` agar gambar dari `FileUpload` tampil di halaman publik.

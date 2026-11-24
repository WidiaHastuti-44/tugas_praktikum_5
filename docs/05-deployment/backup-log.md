# Deployment Guide - SIKA

        1. Kebutuhan Sistem
- XAMPP (Apache + MySQL / MariaDB) versi terbaru
- VS Code
- Browser (Chrome / Edge)
- OS: Windows 10 / 11

        2. Cara Menjalankan di Komputer Lokal (Localhost)
1. Buka XAMPP Control Panel.
2. Klik **Start** pada Apache dan MySQL, pastikan statusnya hijau / Running.
3. Buka browser, ketik `http://localhost/phpmyadmin`.
4. Buat database baru dengan nama `sika_db` (Collation: utf8mb4_general_ci).
5. Klik tab **Import**, pilih file `database/sika.sql`, lalu klik **Go**.
6. Pastikan 4 tabel berhasil dibuat: `mahasiswa`, `dosen`, `matakuliah`, `krs`.
7. Letakkan folder project `SIKA` di dalam `C:/xampp/htdocs/`.
8. Buka browser, ketik `http://localhost/SIKA`.
9. Aplikasi SIKA siap digunakan.

         3. Cara Import Database Manual
Jika file `sika.sql` belum ada, jalankan perintah ini di phpMyAdmin > SQL:
```sql
CREATE DATABASE sika_db;
USE sika_db;
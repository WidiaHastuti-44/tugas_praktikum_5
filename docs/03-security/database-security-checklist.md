# Security Policy - SIKA

         1. Tujuan
Melindungi data mahasiswa, dosen, dan nilai KRS dari akses tidak sah, perubahan ilegal, dan kehilangan data.

         2. Akses Database
- Database `sika_db` hanya bisa diakses lewat user yang berwenang.
- User `root` di XAMPP hanya untuk keperluan lokal / pengembangan.
- Dilarang membagikan password database ke pihak luar.
- Untuk aplikasi production, buat user khusus dengan hak akses terbatas (hanya SELECT, INSERT, UPDATE, DELETE), bukan user `root`.

         3. Kontrol Akses Aplikasi
- Admin: bisa menambah, mengubah, menghapus data mahasiswa, dosen, mata kuliah.
- Mahasiswa: hanya bisa melihat dan mengisi KRS miliknya sendiri.
- Dosen: hanya bisa melihat KRS mata kuliah yang diampunya dan menginput nilai.
- Setiap aksi login harus dicatat (username dan waktu login).

         4. Perlindungan Data
- Password tidak boleh disimpan dalam bentuk teks biasa (plaintext). Harus di-hash menggunakan `password_hash()` / bcrypt.
- Input dari user harus divalidasi untuk mencegah SQL Injection.
- Gunakan Prepared Statement / Parameterized Query, dilarang menggabungkan input user langsung ke dalam query SQL.
- NIM dan NIDN adalah data sensitif, tidak boleh ditampilkan ke publik.

         5. Backup dan Recovery
- Backup database dilakukan setiap minggu dalam format `.sql`.
- File backup disimpan di folder `database/backup/` dan diberi nama tanggal, contoh: `sika_backup_2026-11-24.sql`.
- Uji restore backup secara berkala agar backup dipastikan bisa dipakai.

         6. Audit dan Logging
- Setiap perubahan data penting (tambah / hapus mahasiswa, ubah nilai) dicatat di tabel log atau file log.
- Log minimal berisi: siapa yang mengubah, kapan, dan data apa yang diubah.

         7. Keamanan Lingkungan
- XAMPP hanya dijalankan di komputer lokal, jangan dibuka aksesnya ke internet publik tanpa firewall.
- Matikan service MySQL / Apache jika tidak digunakan.
- Selalu update XAMPP dan VS Code ke versi terbaru.
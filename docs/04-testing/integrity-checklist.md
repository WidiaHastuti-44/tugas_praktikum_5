# Test Cases - SIKA

## Cara Pengujian
Pengujian dilakukan di phpMyAdmin (localhost) dengan menjalankan query SQL dan memeriksa hasilnya sesuai dengan hasil yang diharapkan.

Database yang diuji: `sika_db`

     TC-01: Menambah Data Mahasiswa Valid
- **Query:** `INSERT INTO mahasiswa VALUES ('240101001', 'Andi', 'Informatika', 2024, 'Mataram');`
- **Harus Berhasil:** Ya, data muncul di tabel mahasiswa.
- **Status:** PASS jika data muncul.

    TC-02: Menambah Mahasiswa dengan NIM Duplikat
- **Query:** Masukkan NIM yang sama 2x.
- **Harus Berhasil:** Tidak, harus ditolak karena NIM adalah Primary Key.
- **Status:** PASS jika muncul error Duplicate Entry.

    TC-03: Menambah KRS dengan NIM yang Tidak Ada
- **Query:** `INSERT INTO krs (nim, kode_mk, semester, tahun_akademik) VALUES ('999999', 'IF101', 1, '2024/2025');`
- **Harus Berhasil:** Tidak, harus ditolak karena NIM tidak ada di tabel mahasiswa (Foreign Key).
- **Status:** PASS jika muncul error Foreign Key Constraint.

     TC-04: Menambah KRS dengan Kode MK yang Tidak Ada
- **Query:** `INSERT INTO krs (nim, kode_mk, semester, tahun_akademik) VALUES ('240101001', 'XX999', 1, '2024/2025');`
- **Harus Berhasil:** Tidak, harus ditolak karena Kode MK tidak ada.
- **Status:** PASS jika muncul error Foreign Key Constraint.

     TC-05: Menambah KRS Valid
- **Query:** `INSERT INTO krs (nim, kode_mk, semester, tahun_akademik) VALUES ('240101001', 'IF101', 1, '2024/2025');`
- **Harus Berhasil:** Ya.
- **Status:** PASS jika data KRS muncul.

     TC-06: Menghitung Total SKS Mahasiswa
- **Query:** `SELECT SUM(m.sks) AS total_sks FROM krs k JOIN matakuliah m ON k.kode_mk = m.kode_mk WHERE k.nim = '240101001';`
- **Harus Berhasil:** Ya, total SKS muncul dan benar.
- **Status:** PASS jika total SKS sesuai jumlah SKS mata kuliah yang diambil.

    TC-07: Menghapus Mahasiswa
- **Query:** `DELETE FROM mahasiswa WHERE nim = '240101001';`
- **Harus Berhasil:** Ya, dan data KRS milik mahasiswa tersebut ikut terhapus (ON DELETE CASCADE).
- **Status:** PASS jika mahasiswa dan KRS-nya hilang.

     TC-08: Menghapus Dosen yang Masih Mengampu Mata Kuliah
- **Query:** Hapus dosen yang NIDN-nya masih dipakai di tabel matakuliah.
- **Harus Berhasil:** Tidak, harus ditolak / atau dipastikan dulu tidak ada mata kuliah yang memakai NIDN tersebut.
- **Status:** PASS jika ditolak atau tidak merusak data matakuliah.

     Hasil Pengujian
| ID | Hasil | Keterangan |
| --- | --- | --- |
| TC-01 | PASS | |
| TC-02 | PASS | |
| TC-03 | PASS | |
| TC-04 | PASS | |
| TC-05 | PASS | |
| TC-06 | PASS | |
| TC-07 | PASS | |
| TC-08 | PASS | |
# Data Dictionary - SIKA (sika_db)

     1. Tabel `mahasiswa`
Menyimpan data mahasiswa.

| Kolom | Tipe Data | Keterangan |
| --- | --- | --- |
| nim | VARCHAR(20) | Primary Key, NIM mahasiswa, unik, tidak boleh NULL |
| nama | VARCHAR(100) | Nama lengkap mahasiswa |
| prodi | VARCHAR(50) | Program studi, contoh: Informatika |
| angkatan | INT | Tahun angkatan, contoh: 2024 |
| alamat | TEXT | Alamat mahasiswa |

     2. Tabel `dosen`
Menyimpan data dosen pengampu.

| Kolom | Tipe Data | Keterangan |
| --- | --- | --- |
| nidn | VARCHAR(20) | Primary Key, NIDN dosen, unik |
| nama | VARCHAR(100) | Nama lengkap dosen |
| prodi | VARCHAR(50) | Program studi dosen |
| email | VARCHAR(100) | Email dosen, unik |

    3. Tabel `matakuliah`
Menyimpan data mata kuliah.

| Kolom | Tipe Data | Keterangan |
| --- | --- | --- |
| kode_mk | VARCHAR(10) | Primary Key, kode mata kuliah |
| nama_mk | VARCHAR(100) | Nama mata kuliah |
| sks | INT | Jumlah SKS, contoh: 3 |
| semester | INT | Semester mata kuliah ditawarkan |
| nidn | VARCHAR(20) | Foreign Key ke `dosen.nidn`, dosen pengampu |

      4. Tabel `krs`
Menyimpan data Kartu Rencana Studi mahasiswa.

| Kolom | Tipe Data | Keterangan |
| --- | --- | --- |
| id_krs | INT | Primary Key, Auto Increment |
| nim | VARCHAR(20) | Foreign Key ke `mahasiswa.nim` |
| kode_mk | VARCHAR(10) | Foreign Key ke `matakuliah.kode_mk` |
| semester | INT | Semester pengambilan KRS |
| tahun_akademik | VARCHAR(10) | Contoh: 2024/2025 |
| nilai | CHAR(2) | Nilai akhir, contoh: A, B, C, NULL jika belum ada nilai |

     5. Relasi Antar Tabel
- `mahasiswa (1)` ke `krs (N)` : Satu mahasiswa bisa punya banyak KRS
- `matakuliah (1)` ke `krs (N)` : Satu mata kuliah bisa diambil banyak mahasiswa
- `dosen (1)` ke `matakuliah (N)` : Satu dosen bisa mengampu banyak mata kuliah

         6. Aturan Integritas
- `krs.nim` harus ada di `mahasiswa.nim` (ON DELETE CASCADE)
- `krs.kode_mk` harus ada di `matakuliah.kode_mk`
- `matakuliah.nidn` harus ada di `dosen.nidn`
- `nim`, `nidn`, `kode_mk` tidak boleh duplikat dan tidak boleh NULL
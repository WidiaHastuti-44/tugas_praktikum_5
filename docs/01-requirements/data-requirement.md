 Data Requirement - SIKA

 1. Gambaran Sistem
SIKA (Sistem Informasi KRS Akademik) adalah sistem untuk mengelola data mahasiswa, dosen, mata kuliah, dan Kartu Rencana Studi (KRS). Sistem ini memastikan setiap mahasiswa hanya mengambil mata kuliah yang valid dan setiap data tersimpan secara terintegrasi.

Database: `sika_db`
DBMS: MariaDB / MySQL (via XAMPP)

 2. Entitas dan Kebutuhan Data

    3 Mahasiswa
- NIM sebagai Primary Key, unik, tidak boleh kosong
- Nama, prodi, angkatan, alamat
- Satu mahasiswa bisa mengambil banyak KRS

    4 Dosen
- NIDN / ID Dosen sebagai Primary Key
- Nama, prodi, email
- Satu dosen bisa mengampu banyak mata kuliah

    5  Mata Kuliah
- Kode MK sebagai Primary Key
- Nama MK, SKS, semester, dosen pengampu
- SKS digunakan untuk menghitung total beban SKS mahasiswa

    6 tabel  KRS
- ID KRS sebagai Primary Key
- NIM (Foreign Key ke mahasiswa)
- Kode MK (Foreign Key ke mata kuliah)
- Semester, tahun akademik, nilai
- Satu KRS hanya milik satu mahasiswa dan satu mata kuliah

   A. Kebutuhan Fungsional
1. Admin dapat menambah, mengubah, menghapus data mahasiswa, dosen, dan mata kuliah.
2. Mahasiswa dapat mengisi KRS dan melihat total SKS.
3. Sistem menolak KRS jika NIM tidak ada di tabel mahasiswa.
4. Sistem menolak KRS jika Kode MK tidak ada di tabel mata kuliah.
5. Sistem menampilkan KRS per mahasiswa dan per semester.

   B. Kebutuhan Non-Fungsional
- Data harus konsisten (tidak ada data yatim / orphan).
- NIM dan Kode MK harus unik.
- Backup database dilakukan dalam format `.sql`.
- Akses database hanya oleh user yang berwenang.

   C Aturan Integritas
- Primary Key: NIM, Kode MK, ID KRS tidak boleh NULL dan harus unik.
- Foreign Key: `krs.nim` harus ada di `mahasiswa.nim`, `krs.kode_mk` harus ada di `matakuliah.kode_mk`.
- Total SKS maksimal 24 SKS per semester.
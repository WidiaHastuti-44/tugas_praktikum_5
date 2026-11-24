Tanggal: 25 Nov 2026
Backup: mysqldump -u root sika_db > backup-sika.sql (BERHASIL)
Restore: mysql -u root sika_restore < backup-sika.sql (BERHASIL)
Verifikasi di sika_restore:
- Tabel: krs, mahasiswa, mata_kuliah, prodi
- COUNT mahasiswa = 8 (sama dengan database asli)
Kesimpulan: Backup/Restore BERHASIL, data tidak hilang.
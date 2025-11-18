# 🌟 Website Donasi Yayasan — Spesifikasi Fitur & Arsitektur

Dokumen ini berisi rangkuman lengkap fitur, alur sistem, desain database, teknologi, dan rekomendasi enterprise untuk pengembangan website donasi yayasan berbasis Laravel.

---

## 1. Fitur Utama Website Donasi Yayasan

### A. Frontend Website (Publik)

Fitur yang dapat dilihat oleh semua pengunjung:

- Profil Yayasan  
- Visi & Misi  
- Program Donasi:
  - Pendidikan
  - Sosial
  - Panti Asuhan
  - Kesehatan
- Daftar Anak Asuh (foto, usia, sekolah, kebutuhan)
- Update perkembangan tiap anak
- Total donasi terkumpul
- Daftar donatur (opsional anonim)
- Cara donasi
- Halaman konfirmasi donasi

---

### B. Modul Donatur

Login menggunakan **Email + OTP**.

Fitur:

- Dashboard donatur  
- Riwayat donasi  
- Melihat progress anak yang didanai  
- Notifikasi update terbaru dari admin  

---

### C. Modul Admin Yayasan

Admin dapat mengelola:

- Data anak yayasan  
- Upload perkembangan (foto, pdf, teks)  
- Donasi masuk ke rekening yayasan  
- Verifikasi donasi:
  - Manual
  - Otomatis berbasis OCR mutasi bank  
- Laporan donasi per program  
- Broadcast notifikasi ke semua donatur  

---

## 2. Alur Donasi

### (1) Donasi Umum — ke Yayasan

- Donasi masuk ke rekening yayasan
- Digunakan sesuai program
- Update perkembangan tampil di halaman *Laporan Yayasan*

### (2) Donasi Anak Asuh

- Donasi tetap masuk ke rekening yayasan
- Ditandai sebagai donasi untuk anak tertentu
- Admin mengunggah perkembangan:
  - Nilai raport
  - Laporan kegiatan
  - Foto perkembangan
  - Kebutuhan bulanan

Donatur hanya dapat melihat progress anak yang mereka bantu.

---

## 3. Desain Database (Laravel Migration Ready)

Tabel utama sistem:

- `users`
- `children`
- `donations`
- `donation_updates`
- `foundation_updates`
- `bank_mutations`
- `donation_programs`

Masing-masing tabel menggunakan **UUID** sebagai primary key dan relasi antar tabel sesuai ER Diagram.

---

## 4. Alur Verifikasi Donasi

### Manual

1. Donatur upload bukti transfer  
2. Admin memeriksa bukti  
3. Admin memilih jenis donasi:
   - Donasi umum
   - Donasi anak tertentu  
4. Status berubah menjadi **verified**

### Otomatis (OCR Mutasi Bank)

1. Sistem mengambil mutasi rekening yayasan  
2. Sistem mencocokkan:
   - Nominal
   - Berita transfer  
3. Jika cocok, donasi **auto-verified**

---

## 5. Flow Donasi Anak Asuh

1. Donatur memilih anak → klik **"Donasi untuk Anak ini"**  
2. Mengisi nominal donasi  
3. Upload bukti transfer  
4. Admin memverifikasi  
5. Donatur dapat melihat:
   - Laporan perkembangan terbaru
   - Perkembangan pendidikan
   - Total donasi anak

---

## 6. Struktur Halaman Website

### Public Pages
- Home  
- Tentang Yayasan  
- Galeri / Update  
- Daftar Anak Asuh  
- Detail Anak Asuh  
- Program Donasi  
- Cara Donasi  
- Hubungi Kami  

### Donatur Pages
- Dashboard Donatur  
- Riwayat Donasi  
- Anak yang Didanai  
- Update Terbaru  

### Admin Pages
- Kelola Anak  
- Kelola Donasi  
- Update Perkembangan Anak  
- Update Yayasan  
- Mutasi Bank  
- Laporan Donasi  
- Pengaturan Website  

---

## 7. Teknologi yang Direkomendasikan

### Frontend
- Laravel Blade / Inertia + Vue.js  
- TailwindCSS  

### Backend
- Laravel 11+  
- UUID sebagai Primary Key  
- Laravel Sanctum (auth donatur & admin)  
- Laravel Scheduler (fetch mutasi bank otomatis)  

### Storage
- Amazon S3 atau DigitalOcean Spaces  

---

## 8. Fitur Premium (Enterprise Level)

- Integrasi pembayaran otomatis (Midtrans, Xendit, Duitku)
- QRIS Dynamic
- Auto-match mutasi bank
- Bot WhatsApp (notifikasi konfirmasi donasi)
- Dashboard real-time monitoring
- Notifikasi email & WhatsApp
- Multi-cabang yayasan (multi-tenant)
- Grafik laporan donasi per anak / per program  

---
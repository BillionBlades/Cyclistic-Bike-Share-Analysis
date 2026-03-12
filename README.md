# Cyclistic-Bike-Share-Analysis
Selamat datang di studi kasus analisis layanan berbagi sepeda Cyclistic! Dalam studi kasus ini, saya bekerja untuk perusahaan fiktif, Cyclistic, bersama beberapa anggota tim utama. Untuk menjawab pertanyaan bisnis, saya mengikuti langkah-langkah proses analisis data: 1.Ask, 2.Prepare, 3.Process, 4.Analyze, 5.Share, and 6.Act.

## :one: ASK
###  Business Task
Mengidentifikasi perbedaan pola perilaku penggunaan sepeda antara anggota tahunan (annual members) dan pengendara kasual (casual riders) melalui analisis data historis perjalanan Cyclistic. Temuan ini akan digunakan sebagai landasan data untuk merancang strategi pemasaran yang bertujuan mengonversi pengendara kasual menjadi anggota tahunan demi meningkatkan profitabilitas perusahaan.


## :two: PREPARE 
### Deskripsi Sumber Data
Data Analisis ini menggunakan data historis perjalanan Cyclistic selama 12 bulan (Januari 2025 - Desember 2025) yang tersedia untuk publik. 
Data disediakan oleh Motivate International Inc. di bawah lisensi khusus. [Klik di sini untuk mengunduh data asli](https://divvy-tripdata.s3.amazonaws.com/index.html)

### Keamanan & Privasi Data:
Sesuai dengan aturan privasi data, informasi identitas pribadi (PII) pengendara telah dihilangkan atau tidak disertakan dalam dataset. Saya tidak memiliki akses ke nomor kartu kredit atau data pribadi lainnya yang dapat menghubungkan pembelian tiket ke individu tertentu.

### Kredibilitas dan Integritas Data (ROCCC)
Data ini dinilai memiliki kredibilitas tinggi (ROCCC) karena berasal langsung dari pencatatan transaksi perusahaan sepeda di Chicago. Namun, terdapat batasan privasi yang melarang penggunaan informasi pribadi (PII), sehingga analisis tidak dapat mengidentifikasi lokasi tinggal spesifik pengendara atau riwayat pembelian individu.

### Organisasi Data
Dataset terdiri dari 12 file CSV terpisah yang berisi detail setiap perjalanan, termasuk jenis sepeda, waktu mulai dan berakhir, lokasi stasiun, dan status keanggotaan pengguna.

## :three: PROCESS
Pada tahap ini, saya memproses data mentah agar siap dianalisis dengan memastikan kebersihan, konsistensi, dan integritas data. Karena volume data mencapai jutaan baris, saya memilih menggunakan Python (Pandas) untuk efisiensi dan dokumentasi yang dapat direproduksi.
- Memfilter dan menghapus baris duplikat berdasarkan ride_id.
- Memfilter null values pada kolom stasiun untuk menjamin akurasi rute.
- Melakukan string trimming pada nama stasiun agar kategori data konsisten.
- Membuat kolom ride_length (durasi perjalanan dalam menit).
- Membuat kolom day_of_week (format 1 = Minggu s/d 7 = Sabtu).
- Menghapus data dengan durasi nol atau negatif (error sistem).
- Memfilter data uji coba internal (stasiun berlabel "TEST" atau "HQ QR").
- Menghapus kolom koordinat (lat/lng) untuk efisiensi performa kueri dan dashboard.
 
Hasil akhir berupa dataset bersih bernama cyclistic_final_clean.csv yang siap digunakan untuk tahap Analyze dan pembuatan Dashboard. Skrip pembersihan lengkap tersedia di folder Scripts/.

## :four: ANALYZE
- Perilaku Durasi: Pengguna Casual melakukan perjalanan 2x lebih lama dibandingkan pengguna Member, namun dengan frekuensi yang lebih rendah.

- Pola Mingguan:
Member: Paling aktif pada hari kerja (Senin–Jumat), mengonfirmasi profil sebagai Komuter.
Casual: Lonjakan drastis terjadi pada akhir pekan (Sabtu–Minggu), mengonfirmasi profil sebagai Pengguna Rekreasi.

- Efisiensi Data: Dengan melakukan agregasi terlebih dahulu, ukuran data untuk dashboard berkurang secara signifikan, meningkatkan kecepatan loading visualisasi.

| Kategori | Rata-rata Durasi | Hari Teramai | Pola Utama |
|----------|------------------|--------------|------------|
| Member | 12 Menit | Selasa - Kamis | Komuter (Rutin) |
| Casual | 28 Menit | Sabtu - Minggu | Rekreasi (Santai) |


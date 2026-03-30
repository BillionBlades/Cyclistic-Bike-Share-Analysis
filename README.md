# 🚴 Cyclistic-Bike-Share-Analysis
Selamat datang di studi kasus analisis layanan berbagi sepeda Cyclistic! Dalam studi kasus ini, saya bekerja untuk perusahaan fiktif, Cyclistic, bersama beberapa anggota tim utama. Untuk menjawab pertanyaan bisnis, saya mengikuti langkah-langkah proses analisis data: 1.Ask, 2.Prepare, 3.Process, 4.Analyze, 5.Share, and 6.Act.

## ❓ ASK
###  Business Task
Mengidentifikasi perbedaan pola perilaku penggunaan sepeda antara anggota tahunan (annual members) dan pengendara kasual (casual riders) melalui analisis data historis perjalanan Cyclistic. Temuan ini akan digunakan sebagai landasan data untuk merancang strategi pemasaran yang bertujuan mengonversi pengendara kasual menjadi anggota tahunan demi meningkatkan profitabilitas perusahaan.


## 📝 PREPARE 
### Deskripsi Sumber Data
Data Analisis ini menggunakan data historis perjalanan Cyclistic selama 12 bulan (Januari 2025 - Desember 2025) yang tersedia untuk publik. 
Data disediakan oleh Motivate International Inc. di bawah lisensi khusus. [Klik di sini untuk mengunduh data asli](https://divvy-tripdata.s3.amazonaws.com/index.html)

### Keamanan & Privasi Data:
Sesuai dengan aturan privasi data, informasi identitas pribadi (PII) pengendara telah dihilangkan atau tidak disertakan dalam dataset. Saya tidak memiliki akses ke nomor kartu kredit atau data pribadi lainnya yang dapat menghubungkan pembelian tiket ke individu tertentu.

### Kredibilitas dan Integritas Data (ROCCC)
Data ini dinilai memiliki kredibilitas tinggi (ROCCC) karena berasal langsung dari pencatatan transaksi perusahaan sepeda di Chicago. Namun, terdapat batasan privasi yang melarang penggunaan informasi pribadi (PII), sehingga analisis tidak dapat mengidentifikasi lokasi tinggal spesifik pengendara atau riwayat pembelian individu.

### Organisasi Data
Dataset terdiri dari 12 file CSV terpisah yang berisi detail setiap perjalanan, termasuk jenis sepeda, waktu mulai dan berakhir, lokasi stasiun, dan status keanggotaan pengguna.

## ⚙️ PROCESS
Pada tahap ini, saya memproses data mentah agar siap dianalisis dengan memastikan kebersihan, konsistensi, dan integritas data. Karena volume data mencapai jutaan baris, saya memilih menggunakan Python (Pandas) untuk efisiensi dan dokumentasi yang dapat direproduksi.
- Memfilter dan menghapus baris duplikat berdasarkan ride_id.
- Memfilter null values pada kolom stasiun untuk menjamin akurasi rute.
- Melakukan string trimming pada nama stasiun agar kategori data konsisten.
- Membuat kolom ride_length (durasi perjalanan dalam menit).
- Membuat kolom day_of_week (format 1 = Minggu s/d 7 = Sabtu).
- Menghapus data dengan durasi nol atau negatif (error sistem).
- Memfilter data uji coba internal (stasiun berlabel "TEST" atau "HQ QR").
- Menghapus kolom koordinat (lat/lng) untuk efisiensi performa kueri dan dashboard.
 
Catatan Teknis: Hasil akhir berupa dataset bersih bernama cyclistic_final_clean.csv yang siap digunakan untuk tahap Analyze dan pembuatan Dashboard. Skrip pembersihan lengkap tersedia di folder [Scripts/](scripts) dengan nama process.ipynb.

## 💡 ANALYZE
### Langkah Analisis
- Agregasi Data: Mengelompokkan jutaan baris data berdasarkan tipe pengguna (member_casual) dan hari dalam seminggu (day_of_week).
- Kalkulasi Statistik: Menghitung rata-rata (mean), median, dan frekuensi perjalanan untuk mengidentifikasi perbedaan perilaku yang signifikan.
- Identifikasi Tren: Menghitung total perjalanan per hari untuk menentukan waktu puncak penggunaan bagi masing-masing kategori.
- Optimalisasi: Mengekspor hasil ringkasan ke file CSV terpisah guna mempercepat performa visualisasi di tahap Share.

### Key Insights
- Member = Komuter: Konsisten di hari kerja dengan durasi singkat.
- Casual = Weekend Warriors: Melonjak tajam di akhir pekan dengan durasi perjalanan jauh lebih lama dari pada member.
- Peluang Bisnis: Kampanye pemasaran harus fokus pada konversi pengguna "akhir pekan" (Casual) menjadi member dengan paket khusus rekreasi.

Catatan Teknis: Skrip Python yang digunakan untuk menghasilkan agregasi ini dapat ditemukan di folder  [Scripts/](scripts) dengan nama analyze.ipynb

| Kategori | Rata-rata Durasi | Hari Teramai | Pola Utama |
|----------|------------------|--------------|------------|
| Member | 12 Menit | Selasa - Kamis | Komuter (Rutin) |
| Casual | 28 Menit | Sabtu - Minggu | Rekreasi (Santai) |

## 📊 Share
Analisis divisualisasikan menggunakan Tableau untuk membandingkan perilaku Member vs Casual.
**[Lihat Dashboard Interaktif Di Sini](https://public.tableau.com/views/CyclisticBikeShare_17745963908950/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)**

## 🚀 ACT
**Temuan Kunci:**
* **Casual Riders** bersepeda 2x lebih lama dibandingkan Member.
* **Members** mendominasi hari kerja (komuter), **Casual** melonjak di akhir pekan (rekreasi).

**Rekomendasi Strategis:**
1. Kampanye Konversi "Weekend Warrior"
   Target: Pengguna Casual yang rutin bersepeda di hari Sabtu dan Minggu.
   Aksi: Kirimkan notifikasi aplikasi atau email di hari Jumat sore yang menawarkan potongan harga khusus untuk upgrade ke Annual Membership.
   Alasan: Data menunjukkan lonjakan pengguna Casual di akhir pekan. Menawarkan konversi tepat saat mereka ingin bersepeda akan meningkatkan peluang "closing".

2. Paket Keanggotaan Berbasis Durasi (Seasonal Membership)
   Target: Pengguna Casual dengan rata-rata durasi perjalanan di atas 20 menit.
   Aksi: Buat paket keanggotaan musiman (misal: paket 3 bulan musim panas) dengan harga lebih terjangkau daripada keanggotaan tahunan penuh.
   Alasan: Karena durasi Casual 2x lebih lama dari Member, mereka mungkin merasa keanggotaan tahunan terlalu "serius", namun paket musiman akan terasa lebih cocok dengan pola rekreasi mereka.

3. Insentif "Long-Ride" untuk Anggota Tahunan
   Target: Pengguna Casual yang sering melakukan perjalanan panjang.
   Aksi: Berikan poin atau rewards khusus bagi Annual Members yang melakukan perjalanan lebih dari 30 menit (fitur yang saat ini sering digunakan oleh Casual).
   Alasan: Menunjukkan kepada pengguna Casual bahwa menjadi Member bukan hanya untuk komuter (perjalanan singkat), tapi juga memberikan keuntungan ekonomis untuk perjalanan santai yang lama.


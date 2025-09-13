


# Rancangan Aplikasi LaundryKu Management yang Komprehensif

## 1. Fitur Utama (Core Features)
### 1.1 Manajemen Bisnis Laundry
- **Master Data Laundry**
  - Registrasi multi-cabang (manajemen grup laundry)
  - Detail informasi laundry: nama, alamat lengkap, koordinat GPS, jam operasional
  - Fasilitas laundry: 50+ opsi (layanan antar-jemput, express, dry cleaning, setrika saja, dll)
  - Dokumen legal: SIUP, NPWP, izin operasional
  - Kontak manajemen: pemilik, manajer operasional, supervisor, keuangan
- **Manajemen Layanan**
  - Kategori layanan: Cuci Basah, Cuci Kering, Setrika Saja, Dry Cleaning, Express, Premium
  - Detail per layanan: harga per kg, harga per item, estimasi waktu pengerjaan, kapasitas maksimum
  - Harga dinamis: tarif dasar, tarif express, tarif membership, tarif promo
  - Kontrol inventori: total mesin cuci, mesin pengering, setrika uap, kapasitas produksi harian
  - Galeri layanan: integrasi tampilan proses laundry
- **Manajemen Harga**
  - Rencana tarif: tarif reguler, tarif membership, tarif korporat, tarif paket
  - Aturan tarif: minimum berat, minimum order, harga berdasarkan jenis pakaian
  - Penegakan paritas tarif di semua saluran
  - Alat manajemen hasil: rekomendasi harga berdasarkan permintaan
  - Pelacakan dan analisis tarif kompetitor

### 1.2 Sistem Pemesanan & Penjadwalan
- **Mesin Pemesanan**
  - Pemesanan multi-saluran: walk-in, telepon, online, aplikasi mobile, korporat
  - Pemeriksaan kapasitas real-time dengan pemetaan jadwal produksi
  - Mesin perhitungan tarif dengan aplikasi diskon otomatis
  - Modifikasi pemesanan: perubahan tanggal, penambahan layanan, pengurangan item
  - Manajemen pemesanan grup dengan alokasi blok kapasitas
  - Manajemen daftar tunggu untuk kapasitas penuh
- **Manajemen Reservasi**
  - Pelacakan status pemesanan: Menunggu Penjemputan, Diterima, Proses, Selesai, Diantar, Dibatalkan
  - Manajemen deposit: berbasis persentase, jumlah tetap, tanpa deposit
  - Metode jaminan: pembayaran di muka, COD, e-wallet, transfer bank
  - Kebijakan pembatalan: fleksibel, moderat, tidak dapat dikembalikan dengan perhitungan penatalaksanaan
  - Catatan pemesanan dan pelacakan permintaan khusus (instruksi pencucian khusus)
  - Reservasi grup dengan pemesanan utama dan sub-pemesanan
- **Manajemen Distribusi**
  - Konektivitas saluran: situs web langsung, aplikasi mobile, marketplace, metasearch
  - Manajemen alokasi: alokasi per saluran, kontrol stop order
  - Pemuatan tarif: pembaruan tarif massal, tarif promosi
  - Manajemen pembatasan: minimum berat, tertutup untuk penjemputan
  - Pemantauan paritas: alert perbedaan tarif di seluruh saluran

### 1.3 Proses Digital Order
- **Registrasi Digital**
  - Pre-order online: pengiriman data pelanggan sebelum penjemputan
  - Pemindaian identitas dengan ekstraksi data OCR
  - Tanda tangan digital untuk tanda terima order
  - Pengambilan foto pakaian untuk dokumentasi kondisi awal
  - Pengumpulan informasi kontak darurat dan preferensi pencucian
  - Sistem barcode/QR code untuk tracking item
- **Manajemen Label & Tracking**
  - Generasi label mobile untuk tracking smartphone
  - Cetak label RFID untuk item pakaian
  - Penetapan dan pelacakan item per order
  - Manajemen label master untuk staf
  - Deaktivasi dan penerbitan ulang label yang hilang
  - Audit trail item dengan timestamp dan pelacakan pengguna
- **Proses Delivery**
  - Opsi delivery ekspres: aplikasi mobile, SMS notifikasi
  - Posting otomatis biaya tambahan
  - Pratinjau tagihan dan resolusi sengketa
  - Generasi tanda terima digital dengan pengiriman email/SMS
  - Pengumpulan umpan balik pelanggan setelah delivery
  - Perhitungan dan pemberian poin loyalitas

### 1.4 Keuangan & Laporan
- **Manajemen Pendapatan**
  - Pelacakan pendapatan harian berdasarkan layanan dan saluran
  - Perhitungan dan analisis ARPU (Pendapatan Rata-rata Per Pelanggan)
  - Pemantauan LTV (Nilai Seumur Hidup Pelanggan)
  - Analisis profitabilitas per layanan
  - Peramalan pendapatan dengan integrasi machine learning
  - Analisis segmentasi pasar (retail, korporat, subscription)
- **Operasi Keuangan**
  - Manajemen piutang: penagihan korporat, penagihan agen
  - Hutang: pembayaran vendor, pelacakan komisi
  - Manajemen kas: rekonsiliasi kas harian, pemantauan float
  - Pemrosesan pembayaran digital: penyelesaian batch, penanganan chargeback
  - Manajemen pajak: perhitungan PPN, pelaporan pajak, kepatuhan pajak
  - Penanganan multi-mata uang dengan manajemen nilai tukar
- **Pelaporan Keuangan**
  - Pernyataan P&L per departemen dan cabang
  - Neraca dan laporan arus kas
  - Analisis varians anggaran vs aktual
  - Pelacakan dan pengendalian biaya departemen
  - Manajemen aset tetap dan depresiasi
  - Audit trail untuk semua transaksi keuangan

### 1.5 Integrasi Channel Manager
- **Konektivitas Marketplace**
  - Integrasi XML/API dua arah dengan marketplace utama
  - Sinkronisasi kapasitas dan tarif real-time
  - Pengambilan dan pemrosesan konfirmasi pemesanan
  - Manajemen konten: foto, deskripsi, fasilitas
  - Agregasi ulasan dan manajemen respons
  - Analitik kinerja per saluran
- **Integrasi Aplikasi Mobile**
  - Konektivitas dengan aplikasi mobile laundry
  - Distribusi untuk pelanggan individual
  - Pemuatan tarif dan kontrol kapasitas
  - Penanganan modifikasi dan pembatalan pemesanan
  - Pelacakan dan rekonsiliasi komisi
- **Saluran Pemesanan Langsung**
  - Integrasi mesin pemesanan dengan situs web laundry
  - Konektivitas meta-search (Google, Tripadvisor)
  - Konektivitas wholesaler untuk operator tur
  - Integrasi alat pemesanan korporat
  - Konektivitas API untuk mitra afiliasi

## 2. Fitur Pendukung (Supporting Features)
### 2.1 Manajemen Pelanggan (Customer Management)
- **Database Pelanggan**
  - Profil pelanggan komprehensif: data pribadi, preferensi, perilaku
  - Riwayat pelanggan: semua transaksi, pola pengeluaran, preferensi layanan
  - Segmentasi pelanggan: VIP, reguler, korporat, subscription, retail
  - Pemetaan hubungan: koneksi keluarga, afiliasi korporat
  - Riwayat komunikasi: semua interaksi di seluruh saluran
  - Manajemen privasi: pelacakan persetujuan, kebijakan retensi data
- **Program Loyalitas & Subscription**
  - Keanggotaan berbasis tier: Basic, Pro, Premium
  - Sistem penghargaan: poin basic, poin bonus, event pengali
  - Penebusan poin: diskon, gratis layanan, upgrade fasilitas, mitra
  - Manfaat keanggotaan: prioritas layanan, gratis antar-jemput, fasilitas khusus
  - Manajemen kedaluwarsa: rollover poin, kualifikasi tier
  - Integrasi kemitraan: e-commerce, penyedia layanan, mitra ritel
- **Komunikasi Pelanggan**
  - Komunikasi multi-saluran: email, SMS, WhatsApp, notifikasi push
  - Pesan otomatis: pra-penjemputan, pasca-layanan, penawaran khusus
  - Pesan personal berdasarkan preferensi pelanggan
  - Manajemen kampanye: penawaran promosi, undangan acara
  - Pengumpulan umpan balik: survei pasca-layanan, manajemen ulasan
  - Manajemen keluhan: pelacakan, eskalasi, resolusi

### 2.2 Manajemen Pengguna & Peran
- **Administrasi Pengguna**
  - Manajemen pengguna multi-cabang dengan struktur hierarkis
  - Kontrol akses berbasis peran dengan izin granular
  - Manajemen profil pengguna: data pribadi, kredensial, preferensi
  - Manajemen sesi: kontrol login bersamaan, timeout sesi
  - Kebijakan kata sandi: kompleksitas, kedaluwarsa, prosedur reset
  - Audit trail: semua tindakan pengguna dicatat dengan timestamp
- **Definisi Peran**
  - Super Admin: akses seluruh sistem, manajemen konfigurasi
  - Pemilik Laundry: akses multi-cabang, pelaporan keuangan
  - Manajer Operasional: akses penuh cabang tunggal
  - Kepala Departemen: akses khusus departemen
  - Customer Service: manajemen pemesanan dan pelanggan
  - Staff Produksi: manajemen status order dan tugas
  - Keuangan: operasi keuangan dan pelaporan
- **Matriks Izin**
  - Izin tingkat objek: lihat, buat, edit, hapus
  - Izin tingkat bidang: hanya-baca, dapat diedit, tersembunyi
  - Izin bersyarat: alur kerja persetujuan, batas pengeluaran
  - Izin berbasis waktu: akses sementara, izin terjadwal
  - Izin berbasis lokasi: khusus cabang, khusus departemen

### 2.3 Manajemen Inventori
- **Inventori Mesin & Peralatan**
  - Pelacakan status mesin real-time: tersedia, digunakan, perawatan, rusak
  - Manajemen tipe mesin dengan kemampuan pewarisan dan penggantian
  - Integrasi status perawatan dengan jadwal pemeliharaan
  - Pelacakan dan resolusi permintaan perbaikan
  - Manajemen fitur mesin: kapasitas, konsumsi daya, efisiensi
  - Peramalan kebutuhan mesin berdasarkan data historis dan pemesanan
- **Inventori Bahan & Suplai**
  - Manajemen inventori deterjen, pelembut, dan bahan kimia
  - Pelacakan inventori plastik, kemasan, dan pengisian otomatis
  - Inventori perlengkapan kantor untuk operasional
  - Manajemen formula pencampuran dengan biaya bahan
  - Manajemen pemasok dan pemrosesan pesanan pembelian
  - Pelacakan limbah dan analisis pengendalian biaya
- **Manajemen Aset**
  - Daftar aset tetap dengan pelacakan depresiasi
  - Penjadwalan pemeliharaan dan manajemen pesanan kerja
  - Manajemen siklus hidup aset: akuisisi, pemeliharaan, pembuangan
  - Penandaan aset dan pelacakan lokasi
  - Manajemen garansi dan pelacakan kontrak layanan
  - Analisis kinerja dan utilisasi aset

### 2.4 Manajemen Produksi
- **Manajemen Status Order**
  - Dashboard status order real-time dengan pewarnaan
  - Pembaruan status otomatis berdasarkan input staff produksi
  - Penetapan order prioritas untuk pelanggan VIP dan express
  - Proses inspeksi kualitas dengan titik kontrol kualitas
  - Pelacakan dan manajemen item yang ditemukan/dilaporkan
  - Pelacakan preferensi pelanggan untuk penetapan instruksi khusus
- **Manajemen Tugas**
  - Penetapan tugas harian berdasarkan status order dan prioritas
  - Penyeimbangan beban kerja di antara staf produksi
  - Pelacakan waktu dan durasi tugas
  - Inspeksi kontrol kualitas dan penilaian
  - Manajemen persediaan: deterjen, plastik, kemasan, perlengkapan
  - Pelacakan kinerja staf dan analisis produktivitas
- **Pemeliharaan Pencegahan**
  - Pemeliharaan terjadwal untuk semua mesin dan peralatan
  - Generasi dan pelacakan pesanan kerja
  - Manajemen vendor untuk pemeliharaan khusus
  - Pelacakan dan penganggaran biaya pemeliharaan
  - Manajemen siklus hidup peralatan
  - Pelacakan kepatuhan untuk persyaratan keselamatan dan peraturan

### 2.5 Pelaporan & Analitik
- **Pelaporan Operasional**
  - Laporan operasional harian: order masuk, order selesai, order antar
  - Laporan pendapatan: berdasarkan layanan, saluran, segmen pasar
  - Laporan perkiraan: kapasitas, pendapatan, kebutuhan staf
  - Laporan laju: laju pemesanan vs periode sebelumnya
  - Laporan penjemputan: pemesanan baru, pembatalan, modifikasi
  - Laporan kinerja saluran: produksi, biaya, pendapatan bersih
- **Pelaporan Keuangan**
  - Ringkasan pendapatan harian dengan perincian departemen
  - Pernyataan P&L bulanan dengan analisis varians
  - Pernyataan arus kas dan proyeksi
  - Laporan usia piutang
  - Laporan kinerja anggaran vs aktual
  - Pelaporan pajak dan dokumentasi kepatuhan
- **Analitik Lanjutan**
  - Peramalan permintaan dengan machine learning
  - Rekomendasi optimasi harga
  - Analisis nilai seumur hidup pelanggan
  - Analisis segmentasi pasar
  - Benchmarking kompetitif
  - Analitik prediktif untuk no-show dan pembatalan

## 3. User Flow (Alur Pengguna)
### 3.1 Flow Pemesanan Kompleks
1. **Tahap Pertanyaan**
   - Pelanggan → Memeriksa ketersediaan melalui situs web/telepon/aplikasi
   - Sistem → Menampilkan ketersediaan dan tarif real-time
   - Pelanggan → Memilih layanan dan jadwal penjemputan
   - Sistem → Menghitung total harga dengan pajak dan biaya
2. **Tahap Pemesanan**
   - Pelanggan → Memberikan detail pribadi dan metode pembayaran
   - Sistem → Memvalidasi data dan memproses otorisasi pembayaran
   - Sistem → Menghasilkan konfirmasi pemesanan dan ID unik
   - Sistem → Mengirim konfirmasi melalui email/SMS
   - Sistem → Memperbarui kapasitas di semua saluran
3. **Tahap Pra-Penjemputan**
   - Sistem → Mengirim email pra-penjemputan dengan informasi detail
   - Pelanggan → Menyelesaikan registrasi online dan memberikan preferensi
   - Sistem → Memperbarui profil pelanggan dan permintaan khusus
   - Sistem → Memberi tahu departemen terkait tentang penjemputan
4. **Tahap Penjemputan**
   - Pelanggan → Menunjukkan konfirmasi pemesanan/ID ke kurir
   - Kurir → Memverifikasi pemesanan dan memproses penerimaan item
   - Sistem → Menetapkan nomor tracking dan menghasilkan label
   - Sistem → Memperbarui status order menjadi Diterima
   - Sistem → Memberi tahu produksi tentang order baru

### 3.2 Flow Proses Order Lengkap
1. **Flow Pre-Order**
   - Pelanggan → Menerima notifikasi penjemputan 1 jam sebelum kedatangan
   - Pelanggan → Menyiapkan item dan menyelesaikan pre-order melalui aplikasi
   - Sistem → Memverifikasi identitas dan metode pembayaran
   - Sistem → Menetapkan jadwal dan menghasilkan tracking ID
   - Sistem → Mengirim notifikasi kurir siap menjemput
2. **Flow Penjemputan**
   - Kurir → Tiba di lokasi pelanggan dan memindai tracking ID
   - Sistem → Memverifikasi validitas tracking dan memberikan akses data
   - Kurir → Melakukan dokumentasi foto dan menyerahkan tanda terima
   - Sistem → Mencatat waktu penjemputan dan memberi tahu pusat
   - Opsional: Interaksi pelanggan dengan kurir untuk bantuan
3. **Flow Delivery**
   - Pelanggan → Meminta delivery melalui aplikasi mobile/SMS
   - Sistem → Meninjau folio dan menghitung saldo akhir
   - Pelanggan → Meninjau dan menyetujui biaya
   - Sistem → Memproses pembayaran dan menghasilkan tanda terima
   - Sistem → Menonaktifkan tracking ID dan memperbarui status order
   - Sistem → Mengirim pesan terima kasih dan permintaan umpan balik

### 3.3 Flow Manajemen Keuangan
1. **Pengakuan Pendapatan Harian**
   - Sistem → Memposting pendapatan layanan otomatis pada tengah malam
   - Sistem → Menghitung pajak dan biaya layanan
   - Sistem → Mengalokasikan pendapatan ke akun yang sesuai
   - Sistem → Menghasilkan laporan pendapatan harian
   - Manajer Keuangan → Meninjau dan menyetujui pendapatan harian
2. **Penutupan Akhir Bulan**
   - Sistem → Menghasilkan laporan keuangan awal
   - Tim Keuangan → Merekonsiliasi akun dan menyesuaikan entri
   - Sistem → Menghitung akrual dan prabayar
   - Sistem → Menghasilkan laporan keuangan akhir
   - Manajemen → Meninjau dan menyetujui laporan keuangan
3. **Flow Audit Trail**
   - Pengguna → Melakukan transaksi keuangan
   - Sistem → Mencatat transaksi dengan ID pengguna dan timestamp
   - Sistem → Memvalidasi transaksi terhadap aturan bisnis
   - Sistem → Memperbarui catatan keuangan
   - Auditor → Meninjau log transaksi dan laporan

### 3.4 Flow Channel Manager
1. **Flow Penyiapan Awal**
   - Admin → Mengonfigurasi koneksi saluran
   - Sistem → Menguji konektivitas API dan otentikasi
   - Admin → Memetakan layanan dan rencana tarif
   - Sistem → Memvalidasi pemetaan dan mengaktifkan saluran
   - Sistem → Memulai proses sinkronisasi
2. **Flow Sinkronisasi Harian**
   - Sistem → Memeriksa pemesanan baru dari saluran
   - Sistem → Memproses pemesanan dan memperbarui sistem internal
   - Sistem → Mendorong pembaruan kapasitas ke saluran
   - Sistem → Mendorong pembaruan tarif ke saluran
   - Sistem → Menghasilkan laporan status sinkronisasi
3. **Flow Resolusi Masalah**
   - Sistem → Mendeteksi kesalahan atau perbedaan sinkronisasi
   - Sistem → Memberi tahu admin dengan detail kesalahan
   - Admin → Menyelidiki dan menyelesaikan masalah
   - Sistem → Menyinkronkan kembali data yang terpengaruh
   - Sistem → Mencatat resolusi dan memperbarui status

## 4. Endpoint API yang Diperlukan
### 4.1 Autentikasi & Otorisasi
| Endpoint | Method | Deskripsi | Request Data | Response Data |
|----------|--------|-----------|--------------|---------------|
| `/api/v1/auth/login` | POST | Autentikasi pengguna | ```json { "email": "string", "password": "string", "rememberMe": "boolean" } ``` | ```json { "accessToken": "string", "refreshToken": "string", "user": { "id": "string", "name": "string", "email": "string", "role": "string" } } ``` |
| `/api/v1/auth/refresh` | POST | Refresh token akses | ```json { "refreshToken": "string" } ``` | ```json { "accessToken": "string", "refreshToken": "string" } ``` |
| `/api/v1/auth/logout` | POST | Logout pengguna | ```json { "refreshToken": "string" } ``` | ```json { "success": true } ``` |
| `/api/v1/auth/forgot-password` | POST | Memulai reset kata sandi | ```json { "email": "string" } ``` | ```json { "success": true, "message": "Reset link sent" } ``` |
| `/api/v1/auth/reset-password` | POST | Menyelesaikan reset kata sandi | ```json { "token": "string", "password": "string", "confirmPassword": "string" } ``` | ```json { "success": true } ``` |
| `/api/v1/auth/change-password` | POST | Mengubah kata sandi | ```json { "currentPassword": "string", "newPassword": "string" } ``` | ```json { "success": true } ``` |
| `/api/v1/auth/validate` | GET | Memvalidasi token saat ini | Header: `Authorization: Bearer <token>` | ```json { "valid": true, "userId": "string" } ``` |
| `/api/v1/users/me` | GET | Mendapatkan profil pengguna saat ini | Header: `Authorization: Bearer <token>` | ```json { "id": "string", "name": "string", "email": "string", "role": "string", "permissions": ["string"], "laundries": ["string"] } ``` |
| `/api/v1/users/me` | PUT | Memperbarui profil pengguna saat ini | ```json { "name": "string", "email": "string", "phone": "string", "avatar": "string" } ``` | ```json { "id": "string", "name": "string", "email": "string", "phone": "string", "avatar": "string" } ``` |
| `/api/v1/users/permissions` | GET | Mendapatkan izin pengguna | Header: `Authorization: Bearer <token>` | ```json { "permissions": { "resource": ["read", "create", "update", "delete"] } } ``` |

### 4.2 Manajemen Laundry
| Endpoint | Method | Deskripsi | Request Data | Response Data |
|----------|--------|-----------|--------------|---------------|
| `/api/v1/laundries` | GET | Mendapatkan semua laundry | Query: `page`, `limit`, `search`, `status` | ```json { "data": [{ "id": "string", "name": "string", "address": "string", "status": "string" }], "pagination": { "page": "number", "limit": "number", "total": "number" } } ``` |
| `/api/v1/laundries` | POST | Membuat laundry baru | ```json { "name": "string", "address": "string", "city": "string", "country": "string", "postalCode": "string", "phone": "string", "email": "string", "description": "string", "facilities": ["string"] } ``` | ```json { "id": "string", "name": "string", "address": "string", "status": "active" } ``` |
| `/api/v1/laundries/{id}` | GET | Mendapatkan detail laundry | Path: `id` | ```json { "id": "string", "name": "string", "address": "string", "coordinates": { "lat": "number", "lng": "number" }, "facilities": ["string"], "images": ["string"], "documents": ["string"], "contacts": { "owner": { "name": "string", "phone": "string", "email": "string" } } } ``` |
| `/api/v1/laundries/{id}` | PUT | Memperbarui laundry | Path: `id`<br>Body: Sama seperti POST | ```json { "id": "string", "name": "string", "address": "string", "status": "active" } ``` |
| `/api/v1/laundries/{id}` | DELETE | Menghapus laundry | Path: `id` | ```json { "success": true } ``` |
| `/api/v1/laundries/{id}/facilities` | GET | Mendapatkan fasilitas laundry | Path: `id` | ```json { "facilities": [{ "id": "string", "name": "string", "category": "string", "icon": "string" }] } ``` |
| `/api/v1/laundries/{id}/facilities` | POST | Memperbarui fasilitas laundry | Path: `id`<br>Body: ```json { "facilities": ["string"] } ``` | ```json { "success": true } ``` |
| `/api/v1/laundries/{id}/images` | GET | Mendapatkan gambar laundry | Path: `id` | ```json { "images": [{ "id": "string", "url": "string", "caption": "string", "isPrimary": "boolean" }] } ``` |
| `/api/v1/laundries/{id}/images` | POST | Mengunggah gambar laundry | Path: `id`<br>Form Data: `images[]` (file), `captions[]` (string) | ```json { "images": [{ "id": "string", "url": "string", "caption": "string" }] } ``` |
| `/api/v1/laundries/{id}/images/{imageId}` | DELETE | Menghapus gambar laundry | Path: `id`, `imageId` | ```json { "success": true } ``` |

### 4.3 Manajemen Layanan
| Endpoint | Method | Deskripsi | Request Data | Response Data |
|----------|--------|-----------|--------------|---------------|
| `/api/v1/laundries/{id}/services` | GET | Mendapatkan layanan berdasarkan laundry | Path: `id`<br>Query: `category`, `status` | ```json { "services": [{ "id": "string", "name": "string", "category": "string", "status": "string", "pricePerKg": "number", "estimatedTime": "number" }] } ``` |
| `/api/v1/services` | POST | Membuat layanan baru | ```json { "laundryId": "string", "name": "string", "category": "string", "description": "string", "pricePerKg": "number", "pricePerItem": "number", "estimatedTime": "number", "isActive": "boolean" } ``` | ```json { "id": "string", "name": "string", "category": "string", "status": "active" } ``` |
| `/api/v1/services/{id}` | GET | Mendapatkan detail layanan | Path: `id` | ```json { "id": "string", "name": "string", "category": "string", "description": "string", "pricePerKg": "number", "pricePerItem": "number", "estimatedTime": "number", "isActive": "boolean", "rates": { "baseRate": "number", "expressRate": "number" } } ``` |
| `/api/v1/services/{id}` | PUT | Memperbarui layanan | Path: `id`<br>Body: Sama seperti POST | ```json { "id": "string", "name": "string", "category": "string", "status": "active" } ``` |
| `/api/v1/services/{id}` | DELETE | Menghapus layanan | Path: `id` | ```json { "success": true } ``` |
| `/api/v1/services/{id}/availability` | GET | Mendapatkan ketersediaan layanan | Path: `id`<br>Query: `date`, `timeSlot` | ```json { "availability": [{ "date": "string", "timeSlot": "string", "availableCapacity": "number", "price": "number" }] } ``` |
| `/api/v1/services/{id}/status` | POST | Memperbarui status layanan | Path: `id`<br>Body: ```json { "isActive": "boolean", "reason": "string" } ``` | ```json { "success": true } ``` |
| `/api/v1/service-categories` | GET | Mendapatkan semua kategori layanan | Query: `laundryId` | ```json { "categories": [{ "id": "string", "name": "string", "description": "string" }] } ``` |
| `/api/v1/service-categories` | POST | Membuat kategori layanan | ```json { "laundryId": "string", "name": "string", "description": "string" } ``` | ```json { "id": "string", "name": "string", "description": "string" } ``` |
| `/api/v1/service-categories/{id}` | PUT | Memperbarui kategori layanan | Path: `id`<br>Body: Sama seperti POST | ```json { "id": "string", "name": "string", "description": "string" } ``` |
| `/api/v1/service-categories/{id}/rates` | GET | Mendapatkan tarif kategori layanan | Path: `id`<br>Query: `dateFrom`, `dateTo` | ```json { "rates": [{ "date": "string", "rate": "number", "ratePlan": "string" }] } ``` |

### 4.4 Manajemen Order
| Endpoint | Method | Deskripsi | Request Data | Response Data |
|----------|--------|-----------|--------------|---------------|
| `/api/v1/orders` | GET | Mendapatkan semua order | Query: `laundryId`, `status`, `customerId`, `dateFrom`, `dateTo`, `page`, `limit` | ```json { "data": [{ "id": "string", "orderNumber": "string", "customer": { "id": "string", "name": "string" }, "service": { "id": "string", "name": "string" }, "status": "string", "pickupDate": "string", "deliveryDate": "string" }], "pagination": { "page": "number", "limit": "number", "total": "number" } } ``` |
| `/api/v1/orders` | POST | Membuat order | ```json { "laundryId": "string", "customerId": "string", "serviceId": "string", "pickupDate": "string", "deliveryDate": "string", "weight": "number", "items": [{"name": "string", "quantity": "number", "price": "number"}], "paymentMethod": "string", "specialInstructions": "string" } ``` | ```json { "id": "string", "orderNumber": "string", "status": "confirmed", "totalAmount": "number" } ``` |
| `/api/v1/orders/{id}` | GET | Mendapatkan detail order | Path: `id` | ```json { "id": "string", "orderNumber": "string", "customer": { "id": "string", "name": "string", "email": "string", "phone": "string" }, "service": { "id": "string", "name": "string", "category": "string" }, "status": "string", "pickupDate": "string", "deliveryDate": "string", "weight": "number", "items": [{"name": "string", "quantity": "number", "price": "number"}], "ratePlan": "string", "totalAmount": "number", "payments": [{ "id": "string", "amount": "number", "method": "string", "status": "string" }], "specialInstructions": "string" } ``` |
| `/api/v1/orders/{id}` | PUT | Memperbarui order | Path: `id`<br>Body: ```json { "pickupDate": "string", "deliveryDate": "string", "weight": "number", "items": [{"name": "string", "quantity": "number", "price": "number"}], "serviceId": "string", "specialInstructions": "string" } ``` | ```json { "id": "string", "orderNumber": "string", "status": "confirmed" } ``` |
| `/api/v1/orders/{id}` | DELETE | Membatalkan order | Path: `id`<br>Body: ```json { "reason": "string", "penaltyApplied": "boolean" } ``` | ```json { "id": "string", "status": "cancelled", "cancellationDate": "string" } ``` |
| `/api/v1/orders/{id}/confirm` | POST | Mengonfirmasi order | Path: `id` | ```json { "id": "string", "status": "confirmed", "confirmationDate": "string" } ``` |
| `/api/v1/orders/{id}/modify` | POST | Memodifikasi order | Path: `id`<br>Body: ```json { "modifications": { "dates": { "pickupDate": "string", "deliveryDate": "string" }, "service": { "serviceId": "string" }, "items": [{"name": "string", "quantity": "number", "price": "number"}] } } ``` | ```json { "id": "string", "status": "modified", "modificationDate": "string" } ``` |
| `/api/v1/orders/availability` | GET | Memeriksa ketersediaan | Query: `laundryId`, `serviceId`, `pickupDate`, `deliveryDate`, "weight" | ```json { "available": true, "services": [{ "id": "string", "name": "string", "availableCapacity": "number", "totalRate": "number" }] } ``` |
| `/api/v1/orders/{id}/pickup` | POST | Memproses penjemputan | Path: `id`<br>Body: ```json { "items": [{"name": "string", "quantity": "number", "price": "number"}], "weight": "number", "photos": ["string"], "paymentCollected": "boolean" } ``` | ```json { "id": "string", "status": "picked_up", "pickupTime": "string", "items": [{"name": "string", "quantity": "number", "price": "number"}] } ``` |
| `/api/v1/orders/{id}/deliver` | POST | Memproses pengiriman | Path: `id`<br>Body: ```json { "paymentMethod": "string", "finalAmount": "number" } ``` | ```json { "id": "string", "status": "delivered", "deliveryTime": "string", "finalAmount": "number" } ``` |
| `/api/v1/orders/{id}/invoice` | GET | Mendapatkan invoice order | Path: `id` | ```json { "id": "string", "orderId": "string", "transactions": [{ "id": "string", "description": "string", "amount": "number", "date": "string", "type": "charge/payment" }], "total": "number", "balance": "number" } ``` |

### 4.5 Manajemen Pelanggan
| Endpoint | Method | Deskripsi | Request Data | Response Data |
|----------|--------|-----------|--------------|---------------|
| `/api/v1/customers` | GET | Mendapatkan semua pelanggan | Query: `search`, `laundryId`, "subscriptionTier", `page`, `limit` | ```json { "data": [{ "id": "string", "name": "string", "email": "string", "phone": "string", "subscriptionTier": "string", "totalOrders": "number" }], "pagination": { "page": "number", "limit": "number", "total": "number" } } ``` |
| `/api/v1/customers` | POST | Membuat pelanggan baru | ```json { "name": "string", "email": "string", "phone": "string", "address": "string", "city": "string", "country": "string", "idType": "string", "idNumber": "string", "preferences": ["string"] } ``` | ```json { "id": "string", "name": "string", "email": "string", "phone": "string" } ``` |
| `/api/v1/customers/{id}` | GET | Mendapatkan detail pelanggan | Path: `id` | ```json { "id": "string", "name": "string", "email": "string", "phone": "string", "address": { "street": "string", "city": "string", "country": "string", "postalCode": "string" }, "identification": { "type": "string", "number": "string", "expiry": "string" }, "preferences": ["string"], "subscription": { "tier": "string", "points": "number", "memberSince": "string" } } ``` |
| `/api/v1/customers/{id}` | PUT | Memperbarui pelanggan | Path: `id`<br>Body: Sama seperti POST | ```json { "id": "string", "name": "string", "email": "string", "phone": "string" } ``` |
| `/api/v1/customers/{id}/history` | GET | Mendapatkan riwayat pelanggan | Path: `id`<br>Query: `limit`, `offset` | ```json { "orders": [{ "id": "string", "laundry": { "id": "string", "name": "string" }, "service": { "name": "string", "category": "string" }, "pickupDate": "string", "deliveryDate": "string", "totalAmount": "number", "status": "string" }] } ``` |
| `/api/v1/customers/{id}/preferences` | GET | Mendapatkan preferensi pelanggan | Path: `id` | ```json { "preferences": { "service": { "category": "string", "detergent": "string", "fragrance": "string" }, "specialInstructions": ["string"] } } ``` |
| `/api/v1/customers/{id}/preferences` | POST | Memperbarui preferensi pelanggan | Path: `id`<br>Body: ```json { "service": { "category": "string", "detergent": "string", "fragrance": "string" }, "specialInstructions": ["string"] } ``` | ```json { "success": true } ``` |
| `/api/v1/customers/{id}/subscription` | GET | Mendapatkan info subscription pelanggan | Path: `id` | ```json { "subscription": { "tier": "string", "points": "number", "memberSince": "string", "nextTier": { "name": "string", "pointsNeeded": "number" }, "transactions": [{ "id": "string", "type": "earned/redeemed", "points": "number", "date": "string", "description": "string" }] } } ``` |
| `/api/v1/customers/{id}/communication` | POST | Mengirim komunikasi ke pelanggan | Path: `id`<br>Body: ```json { "channel": "email/sms/whatsapp", "template": "string", "data": { "key": "value" } } ``` | ```json { "success": true, "messageId": "string" } ``` |

### 4.6 Manajemen Keuangan
| Endpoint | Method | Deskripsi | Request Data | Response Data |
|----------|--------|-----------|--------------|---------------|
| `/api/v1/transactions` | GET | Mendapatkan semua transaksi | Query: `laundryId`, `type`, `dateFrom`, `dateTo`, `page`, `limit` | ```json { "data": [{ "id": "string", "type": "charge/payment", "description": "string", "amount": "number", "date": "string", "method": "string", "status": "string" }], "pagination": { "page": "number", "limit": "number", "total": "number" } } ``` |
| `/api/v1/transactions` | POST | Membuat transaksi | ```json { "laundryId": "string", "orderId": "string", "type": "charge/payment", "description": "string", "amount": "number", "method": "string", "reference": "string" } ``` | ```json { "id": "string", "type": "charge", "amount": "number", "status": "completed" } ``` |
| `/api/v1/transactions/{id}` | GET | Mendapatkan detail transaksi | Path: `id` | ```json { "id": "string", "type": "charge/payment", "description": "string", "amount": "number", "date": "string", "method": "string", "status": "string", "order": { "id": "string", "orderNumber": "string" }, "user": { "id": "string", "name": "string" } } ``` |
| `/api/v1/transactions/{id}` | PUT | Memperbarui transaksi | Path: `id`<br>Body: ```json { "description": "string", "amount": "number", "method": "string" } ``` | ```json { "id": "string", "type": "charge", "amount": "number", "status": "updated" } ``` |
| `/api/v1/transactions/{id}` | DELETE | Membatalkan transaksi | Path: `id`<br>Body: ```json { "reason": "string" } ``` | ```json { "id": "string", "status": "voided", "voidDate": "string" } ``` |
| `/api/v1/reports/revenue` | GET | Mendapatkan laporan pendapatan | Query: `laundryId`, `dateFrom`, `dateTo`, `groupBy` (day/week/month) | ```json { "report": { "totalRevenue": "number", "serviceRevenue": "number", "deliveryRevenue": "number", "otherRevenue": "number", "breakdown": [{ "date": "string", "serviceRevenue": "number", "deliveryRevenue": "number", "otherRevenue": "number", "total": "number" }] } } ``` |
| `/api/v1/reports/occupancy` | GET | Mendapatkan laporan kapasitas | Query: `laundryId`, `dateFrom`, `dateTo`, `groupBy` (day/week/month) | ```json { "report": { "capacityRate": "number", "arpu": "number", "totalCapacity": "number", "usedCapacity": "number", "breakdown": [{ "date": "string", "capacityRate": "number", "arpu": "number" }] } } ``` |
| `/api/v1/reports/financial` | GET | Mendapatkan laporan keuangan | Query: `laundryId`, `dateFrom`, `dateTo`, `type` (p&l/balance/cashflow) | ```json { "report": { "type": "p&l", "period": { "start": "string", "end": "string" }, "revenue": { "total": "number", "breakdown": [{ "category": "string", "amount": "number" }] }, "expenses": { "total": "number", "breakdown": [{ "category": "string", "amount": "number" }] }, "netProfit": "number" } } ``` |
| `/api/v1/reports/generate` | POST | Menghasilkan laporan kustom | ```json { "laundryId": "string", "reportType": "string", "filters": { "dateFrom": "string", "dateTo": "string", "departments": ["string"] }, "columns": ["string"], "format": "pdf/excel/csv" } ``` | ```json { "reportId": "string", "status": "processing", "downloadUrl": "string" } ``` |
| `/api/v1/invoices` | GET | Mendapatkan semua faktur | Query: `laundryId`, `status`, `dateFrom`, `dateTo`, `page`, `limit` | ```json { "data": [{ "id": "string", "invoiceNumber": "string", "customer": { "name": "string", "type": "corporate/individual" }, "amount": "number", "status": "string", "dueDate": "string" }], "pagination": { "page": "number", "limit": "number", "total": "number" } } ``` |
| `/api/v1/invoices` | POST | Membuat faktur | ```json { "laundryId": "string", "customerId": "string", "customerType": "corporate/individual", "items": [{ "description": "string", "amount": "number", "quantity": "number" }], "dueDate": "string" } ``` | ```json { "id": "string", "invoiceNumber": "string", "totalAmount": "number", "status": "draft" } ``` |
| `/api/v1/invoices/{id}` | GET | Mendapatkan detail faktur | Path: `id` | ```json { "id": "string", "invoiceNumber": "string", "customer": { "id": "string", "name": "string", "type": "corporate/individual" }, "items": [{ "description": "string", "amount": "number", "quantity": "number", "total": "number" }], "totalAmount": "number", "status": "string", "issueDate": "string", "dueDate": "string", "payments": [{ "id": "string", "amount": "number", "date": "string", "method": "string" }] } ``` |

### 4.7 Manajemen Saluran
| Endpoint | Method | Deskripsi | Request Data | Response Data |
|----------|--------|-----------|--------------|---------------|
| `/api/v1/channels` | GET | Mendapatkan semua saluran | Query: `laundryId`, `type`, `status` | ```json { "channels": [{ "id": "string", "name": "string", "type": "marketplace/app/website", "status": "connected/disconnected", "lastSync": "string" }] } ``` |
| `/api/v1/channels` | POST | Menghubungkan saluran baru | ```json { "laundryId": "string", "type": "marketplace/app", "provider": "string", "credentials": { "apiKey": "string", "apiSecret": "string", "laundryId": "string" } } ``` | ```json { "id": "string", "name": "string", "status": "connecting" } ``` |
| `/api/v1/channels/{id}` | GET | Mendapatkan detail saluran | Path: `id` | ```json { "id": "string", "name": "string", "type": "marketplace/app", "provider": "string", "status": "connected", "lastSync": "string", "mappings": { "services": [{ "channelId": "string", "localId": "string" }], "ratePlans": [{ "channelId": "string", "localId": "string" }] } } ``` |
| `/api/v1/channels/{id}` | PUT | Memperbarui saluran | Path: `id`<br>Body: ```json { "credentials": { "apiKey": "string", "apiSecret": "string" }, "mappings": { "services": [{ "channelId": "string", "localId": "string" }] } } ``` | ```json { "id": "string", "status": "updated" } ``` |
| `/api/v1/channels/{id}` | DELETE | Memutuskan saluran | Path: `id` | ```json { "success": true } ``` |
| `/api/v1/channels/{id}/sync` | POST | Sinkronisasi manual | Path: `id`<br>Body: ```json { "syncType": "full/incremental", "dataTypes": ["rates", "capacity", "content"] } ``` | ```json { "syncId": "string", "status": "started" } ``` |
| `/api/v1/channels/{id}/orders` | GET | Mendapatkan order saluran | Path: `id`<br>Query: `dateFrom`, `dateTo`, `status` | ```json { "orders": [{ "id": "string", "channelOrderId": "string", "status": "string", "pickupDate": "string", "deliveryDate": "string", "service": { "channelId": "string", "localId": "string" }, "totalAmount": "number" }] } ``` |
| `/api/v1/channels/{id}/rates` | POST | Memperbarui tarif | Path: `id`<br>Body: ```json { "ratePlanId": "string", "rates": [{ "date": "string", "rate": "number" }] } ``` | ```json { "success": true, "updatedRates": "number" } ``` |
| `/api/v1/channels/{id}/capacity` | GET | Mendapatkan kapasitas | Path: `id`<br>Query: `dateFrom`, `dateTo`, `serviceId` | ```json { "capacity": [{ "date": "string", "service": { "channelId": "string", "localId": "string" }, "available": "number", "total": "number" }] } ``` |
| `/api/v1/channels/{id}/status` | GET | Mendapatkan status sinkronisasi | Path: `id` | ```json { "status": "connected", "lastSync": "string", "nextSync": "string", "errors": [{ "type": "string", "message": "string", "date": "string" }] } ``` |

### 4.8 Manajemen Pengguna
| Endpoint | Method | Deskripsi | Request Data | Response Data |
|----------|--------|-----------|--------------|---------------|
| `/api/v1/users` | GET | Mendapatkan semua pengguna | Query: `laundryId`, `role`, `status`, `search`, `page`, `limit` | ```json { "data": [{ "id": "string", "name": "string", "email": "string", "role": "string", "status": "active/inactive", "lastLogin": "string" }], "pagination": { "page": "number", "limit": "number", "total": "number" } } ``` |
| `/api/v1/users` | POST | Membuat pengguna | ```json { "name": "string", "email": "string", "password": "string", "role": "string", "laundryIds": ["string"], "permissions": ["string"] } ``` | ```json { "id": "string", "name": "string", "email": "string", "role": "string", "status": "active" } ``` |
| `/api/v1/users/{id}` | GET | Mendapatkan detail pengguna | Path: `id` | ```json { "id": "string", "name": "string", "email": "string", "role": "string", "status": "active/inactive", "laundries": [{ "id": "string", "name": "string" }], "permissions": ["string"], "lastLogin": "string", "createdAt": "string" } ``` |
| `/api/v1/users/{id}` | PUT | Memperbarui pengguna | Path: `id`<br>Body: ```json { "name": "string", "email": "string", "role": "string", "laundryIds": ["string"], "permissions": ["string"] } ``` | ```json { "id": "string", "name": "string", "email": "string", "role": "string", "status": "active" } ``` |
| `/api/v1/users/{id}` | DELETE | Menghapus pengguna | Path: `id` | ```json { "success": true } ``` |
| `/api/v1/users/{id}/activate` | POST | Mengaktifkan pengguna | Path: `id` | ```json { "id": "string", "status": "active" } ``` |
| `/api/v1/users/{id}/deactivate` | POST | Menonaktifkan pengguna | Path: `id` | ```json { "id": "string", "status": "inactive" } ``` |
| `/api/v1/roles` | GET | Mendapatkan semua peran | Query: `laundryId` | ```json { "roles": [{ "id": "string", "name": "string", "description": "string", "permissions": ["string"] }] } ``` |
| `/api/v1/roles` | POST | Membuat peran | ```json { "name": "string", "description": "string", "permissions": ["string"], "laundryId": "string" } ``` | ```json { "id": "string", "name": "string", "description": "string" } ``` |
| `/api/v1/roles/{id}` | PUT | Memperbarui peran | Path: `id`<br>Body: ```json { "name": "string", "description": "string", "permissions": ["string"] } ``` | ```json { "id": "string", "name": "string", "description": "string" } ``` |
| `/api/v1/permissions` | GET | Mendapatkan semua izin | Query: `resource` | ```json { "permissions": [{ "id": "string", "name": "string", "resource": "string", "action": "string", "description": "string" }] } ``` |

### 4.9 Manajemen Sistem
| Endpoint | Method | Deskripsi | Request Data | Response Data |
|----------|--------|-----------|--------------|---------------|
| `/api/v1/system/config` | GET | Mendapatkan konfigurasi sistem | Query: `laundryId` (opsional) | ```json { "config": { "currency": "string", "timezone": "string", "dateFormat": "string", "language": "string", "features": { "featureName": "boolean" }, "integrations": { "integrationName": { "enabled": "boolean", "settings": {} } } } } ``` |
| `/api/v1/system/config` | PUT | Memperbarui konfigurasi sistem | ```json { "laundryId": "string", "settings": { "currency": "string", "timezone": "string", "features": { "featureName": "boolean" } } } ``` | ```json { "success": true } ``` |
| `/api/v1/system/logs` | GET | Mendapatkan log sistem | Query: `level`, `dateFrom`, `dateTo`, `service`, `page`, `limit` | ```json { "logs": [{ "id": "string", "timestamp": "string", "level": "info/warn/error", "service": "string", "message": "string", "details": {} }], "pagination": { "page": "number", "limit": "number", "total": "number" } } ``` |
| `/api/v1/system/backups` | POST | Membuat backup | ```json { "type": "full/incremental", "include": ["database", "files"] } ``` | ```json { "backupId": "string", "status": "started", "estimatedSize": "number" } ``` |
| `/api/v1/system/backups` | GET | Mendapatkan daftar backup | Query: `type`, `dateFrom`, `dateTo`, `page`, `limit` | ```json { "backups": [{ "id": "string", "type": "full/incremental", "size": "number", "status": "completed/failed", "createdAt": "string", "expiresAt": "string" }], "pagination": { "page": "number", "limit": "number", "total": "number" } } ``` |
| `/api/v1/system/backups/{id}/restore` | POST | Memulihkan backup | Path: `id`<br>Body: ```json { "restorePoint": "string", "options": { "database": true, "files": true } } ``` | ```json { "restoreId": "string", "status": "started" } ``` |
| `/api/v1/system/health` | GET | Pemeriksaan kesehatan sistem | - | ```json { "status": "healthy", "version": "string", "database": "healthy", "cache": "healthy", "services": { "serviceName": "healthy/degraded" } } ``` |
| `/api/v1/system/metrics` | GET | Metrik sistem | Query: `period` (hourly/daily/weekly) | ```json { "metrics": { "cpu": { "usage": "number", "cores": "number" }, "memory": { "used": "number", "total": "number", "percentage": "number" }, "disk": { "used": "number", "total": "number", "percentage": "number" }, "network": { "in": "number", "out": "number" }, "responseTime": { "avg": "number", "p95": "number", "p99": "number" } } } ``` |
| `/api/v1/system/notifications` | POST | Mengirim notifikasi sistem | ```json { "type": "info/warn/error", "channel": "email/sms/push", "recipients": ["string"], "title": "string", "message": "string", "data": {} } ``` | ```json { "success": true, "notificationId": "string" } ``` |

## 5. Halaman (View) yang Dibutuhkan
### 5.1 Halaman Autentikasi
- **Halaman Login**
    - Bidang email/nama pengguna dan kata sandi
    - Checkbox ingat saya
    - Tautan lupa kata sandi
    - Pemilih bahasa
    - Pemilih laundry/cabang untuk pengguna multi-cabang
    - Opsi login sosial (Google, Microsoft)
- **Halaman Lupa Kata Sandi**
    - Bidang email untuk reset kata sandi
    - Verifikasi CAPTCHA
    - Pertanyaan keamanan (opsional)
    - Pesan sukses dengan instruksi
- **Halaman Reset Kata Sandi**
    - Bidang kata sandi baru dengan indikator kekuatan
    - Bidang konfirmasi kata sandi
    - Tampilan persyaratan kata sandi
    - Tombol kirim dengan validasi
- **Halaman Registrasi**
    - Formulir informasi laundry
    - Formulir pembuatan pengguna admin
    - Penerimaan syarat dan ketentuan
    - Pilihan paket langganan (Basic, Pro, Premium)
    - Pengumpulan informasi pembayaran

### 5.2 Halaman Dashboard
- **Dashboard Utama**
    - Kartu metrik kunci: kapasitas terpakai, ARPU, LTV, total pendapatan
    - Ringkasan order masuk dan selesai hari ini
    - Grafik pendapatan (harian/mingguan/bulanan)
    - Ikhtisar status order dengan pewarnaan
    - Feed aktivitas terbaru
    - Tombol aksi cepat (order baru, penjemputan, pengiriman)
- **Dashboard Keuangan**
    - Perincian pendapatan berdasarkan kategori
    - Pelacakan biaya dan anggaran vs aktual
    - Ringkasan arus kas
    - Usia piutang
    - Indikator kinerja keuangan
    - Tombol ekspor laporan keuangan
- **Dashboard Operasional**
    - Status tugas produksi
    - Ikhtisar permintaan perawatan
    - Metrik kinerja staf
    - Skor kepuasan pelanggan
    - Tingkat inventori
    - Alert dan notifikasi operasional

### 5.3 Halaman Manajemen Laundry
- **Halaman Daftar Laundry**
    - Opsi pencarian dan filter
    - Tabel data dengan informasi laundry
    - Tombol aksi (edit, lihat, hapus)
    - Aksi massal (aktifkan, nonaktifkan)
    - Kontrol paginasi
    - Ekspor ke CSV/Excel
- **Halaman Detail Laundry**
    - Tampilan dan edit informasi laundry
    - Galeri foto dengan unggah/hapus
    - Manajemen fasilitas
    - Manajemen informasi kontak
    - Bagian unggah dokumen
    - Integrasi peta lokasi
- **Halaman Manajemen Layanan**
    - Daftar layanan dengan detail yang dapat diperluas
    - Manajemen kategori layanan
    - Konfigurasi harga
    - Ikhtisar status layanan
    - Kemampuan pembaruan massal
    - Manajemen foto layanan

### 5.4 Halaman Order
- **Kalender Order**
    - Toggle tampilan bulanan/mingguan/harian
    - Status order berkode warna
    - Modifikasi pemesanan drag-and-drop
    - Filter berdasarkan layanan atau status
    - Legenda untuk indikator status
    - Pembuatan pemesanan cepat dari kalender
- **Daftar Order**
    - Pencarian dan filter tingkat lanjut
    - Tabel data dengan detail order
    - Tombol aksi untuk setiap order
    - Operasi massal (konfirmasi, batalkan)
    - Kustomisasi kolom
    - Fungsi ekspor
- **Halaman Order Baru**
    - Wizard pemesanan multi-langkah
    - Fungsionalitas pencarian/pembuatan pelanggan
    - Tampilan ketersediaan layanan
    - Perhitungan tarif dan aplikasi diskon
    - Pengumpulan metode pembayaran
    - Permintaan dan catatan khusus
- **Halaman Detail Order**
    - Tampilan informasi order lengkap
    - Detail dan riwayat pelanggan
    - Manajemen invoice
    - Pemrosesan penjemputan/pengiriman
    - Opsi modifikasi dan pembatalan
    - Riwayat komunikasi

### 5.5 Halaman Manajemen Pelanggan
- **Halaman Daftar Pelanggan**
    - Pencarian berdasarkan nama, email, telepon
    - Filter segmentasi pelanggan
    - Tabel data dengan informasi pelanggan
    - Indikator tier subscription
    - Tombol aksi (lihat, edit, komunikasi)
    - Ekspor database pelanggan
- **Halaman Profil Pelanggan**
    - Tampilan dan edit informasi pribadi
    - Timeline riwayat transaksi
    - Preferensi dan permintaan khusus
    - Informasi program subscription
    - Riwayat komunikasi
    - Profil terkait (keluarga, korporat)
- **Halaman Program Subscription**
    - Tampilan struktur tier anggota (Basic, Pro, Premium)
    - Riwayat penghasilan dan penebusan poin
    - Ikhtisar manfaat keanggotaan
    - Pelacakan kualifikasi tier
    - Integrasi program mitra
    - Manajemen penawaran promosi

### 5.6 Halaman Manajemen Keuangan
- **Halaman Transaksi**
    - Daftar transaksi dengan filter dan pencarian
    - Detail transaksi dengan informasi lengkap
    - Opsi tambah, edit, dan hapus transaksi
    - Rekonkiasi transaksi
    - Ekspor data transaksi
    - Kategorisasi transaksi otomatis
- **Halaman Laporan**
    - Pilihan jenis laporan (pendapatan, kapasitas, keuangan)
    - Filter tanggal dan kustomisasi parameter
    - Preview laporan dengan opsi unduh
    - Penjadwalan laporan otomatis
    - Manajemen template laporan
    - Distribusi laporan ke email
- **Halaman Invoice**
    - Daftar invoice dengan status pembayaran
    - Detail invoice dengan item dan perhitungan
    - Pembuatan invoice baru
    - Pengiriman invoice ke pelanggan
    - Pelacakan pembayaran invoice
    - Pengingat pembayaran otomatis

### 5.7 Halaman Manajemen Pengguna
- **Halaman Daftar Pengguna**
    - Tabel pengguna dengan informasi dasar
    - Filter berdasarkan peran, status, dan laundry
    - Opsi tambah, edit, dan hapus pengguna
    - Aktivasi dan deaktivasi pengguna
    - Reset kata sandi pengguna
    - Ekspor data pengguna
- **Halaman Profil Pengguna**
    - Informasi pribadi dan kontak
    - Riwayat login dan aktivitas
    - Peran dan izin pengguna
    - Akses ke laundry/cabang
    - Preferensi pengguna
    - Riwayat perubahan profil
- **Halaman Manajemen Peran**
    - Daftar peran dengan deskripsi
    - Detail peran dengan daftar izin
    - Pembuatan dan kustomisasi peran
    - Penugasan peran ke pengguna
    - Template peran standar
    - Hierarki peran dan pewarisan izin

### 5.8 Halaman Manajemen Sistem
- **Halaman Konfigurasi**
    - Pengaturan umum sistem
    - Konfigurasi integrasi dengan pihak ketiga
    - Pengaturan notifikasi dan email
    - Konfigurasi keamanan
    - Pengaturan regional (bahasa, mata uang, zona waktu)
    - Preferensi tampilan dan UI
- **Halaman Log Sistem**
    - Riwayat aktivitas sistem
    - Filter log berdasarkan level, layanan, dan tanggal
    - Detail log dengan informasi lengkap
    - Ekspor log untuk analisis
    - Pencarian teks dalam log
    - Monitoring error dan exception
- **Halaman Backup & Pemulihan**
    - Daftar backup dengan informasi detail
    - Pembuatan backup manual dan terjadwal
    - Pemulihan sistem dari backup
    - Konfigurasi jadwal backup otomatis
    - Monitoring status backup
    - Manajemen penyimpanan backup

## 6. Fitur Berdasarkan Tier Subscription

### 6.1 Tier Basic (Rp 500.000/bulan atau Rp 5.000.000/tahun)
- **Fitur Utama:**
  - Maksimal 1 cabang laundry
  - Maksimal 50 pelanggan aktif
  - Maksimal 2 staf
  - 1 device admin web
  - 2 device staff (Android/Web)
  - 100 transaksi/bulan
  - Basic reporting

- **Fitur Aplikasi:**
  - Dashboard sederhana
  - Manajemen order dasar
  - Manajemen pelanggan dasar
  - Laporan keuangan dasar
  - Notifikasi email dasar
  - Manajemen layanan terbatas (maksimal 5 layanan)

- **Batasan:**
  - Tidak ada integrasi marketplace
  - Tidak ada mobile app untuk pelanggan
  - Tidak ada program loyalitas
  - Tidak ada analitik lanjutan
  - Tidak ada multi-cabang

### 6.2 Tier Pro (Rp 1.000.000/bulan atau Rp 10.000.000/tahun)
- **Fitur Utama:**
  - Maksimal 3 cabang laundry
  - Maksimal 200 pelanggan aktif
  - Maksimal 10 staf
  - Unlimited device admin web
  - 10 device staff (Android/Web/Desktop)
  - 500 transaksi/bulan
  - Advanced reporting & analytics
  - Integration with payment gateways

- **Fitur Aplikasi:**
  - Dashboard lengkap dengan analitik
  - Manajemen order lengkap dengan tracking
  - Manajemen pelanggan lengkap dengan segmentasi
  - Laporan keuangan lengkap dengan forecasting
  - Notifikasi multi-channel (email, SMS, WhatsApp)
  - Manajemen layanan lengkap (maksimal 15 layanan)
  - Program loyalitas dasar
  - Integrasi dengan marketplace (1 channel)
  - Mobile app untuk pelanggan (basic)

- **Batasan:**
  - Tidak ada AI-powered recommendations
  - Tidak ada custom integrations
  - Tidak ada white-label solution
  - Tidak ada multi-language support

### 6.3 Tier Premium (Rp 2.000.000/bulan atau Rp 20.000.000/tahun)
- **Fitur Utama:**
  - Unlimited cabang laundry
  - Unlimited pelanggan aktif
  - Unlimited staf
  - Unlimited semua device
  - Unlimited transaksi
  - Full features & custom integrations
  - Priority support
  - White-label solution
  - Multi-branch support

- **Fitur Aplikasi:**
  - Semua fitur Tier Pro
  - Dashboard enterprise dengan real-time analytics
  - Manajemen order enterprise dengan workflow automation
  - Manajemen pelanggan enterprise dengan AI-powered insights
  - Laporan keuangan enterprise dengan predictive analytics
  - Notifikasi omnichannel dengan personalization
  - Manajemen layanan tak terbatas
  - Program loyalitas lengkap dengan tier multi-level
  - Integrasi dengan unlimited marketplace
  - Mobile app enterprise untuk pelanggan (full features)
  - AI-powered recommendations
  - Custom integrations
  - White-label solution
  - Multi-language support
  - Priority customer support
  - Custom development options
  - Franchise management tools

---

Rancangan ini menyediakan kerangka kerja lengkap untuk aplikasi laundry berbasis subscription dengan tiga tier yang berbeda (Basic, Pro, Premium). Sistem ini dirancang untuk skalabilitas, dengan mempertimbangkan kebutuhan bisnis laundry dari skala kecil hingga enterprise. Rancangan ini mencakup semua aspek yang diperlukan untuk pengembangan aplikasi yang komprehensif, termasuk fitur utama, fitur pendukung, alur pengguna, endpoint API, dan halaman yang dibutuhkan.
# QA Automation Guidelines — TokoKampus

## Role & Scope
- Bertindak sebagai Senior QA Engineer yang melakukan **Black-Box Testing** secara eksternal pada target website: `https://bug.xilkxill.my.id`.
- Tester Name: **Dio Lutvi Andre**
- Pengujian dilakukan murni melalui interaksi browser (Playwright Chromium), pemantauan Console Log, dan Network Request tanpa akses source code.

## Mandatory Execution Phases

### Phase 0: Website Specification Extraction (WAJIB DILAKUKAN PERTAMA)
Sebelum menyusun test case atau menjalankan pengujian fungsional:
1. Buka `https://bug.xilkxill.my.id` menggunakan Playwright Chromium dan tunggu hingga state `networkidle` atau elemen layar loading (`Memuat TokoKampus...`) hilang sepenuhnya.
2. Cari dan buka halaman, menu navigasi, tombol, atau modal yang memuat **Spesifikasi Website / Panduan / Ketentuan Sistem** (misalnya menu "Spesifikasi", "Tentang", "Info", "Docs", atau tautan di header/footer).
3. Ekstrak seluruh teks spesifikasi, aturan bisnis (business rules), batasan input, dan ketentuan fitur yang tertulis di halaman tersebut, lalu simpan ke file `qa-results/extracted_specifications.md`.
4. Gunakan dokumen `extracted_specifications.md` tersebut sebagai sumber kebenaran utama (**Expected Result**) untuk mendeteksi penyimpangan atau bug pada sistem.

### Phase 1: Test Planning & Execution
1. Petakan seluruh fitur yang tercantum dalam spesifikasi (seperti registrasi akun, login, katalog, keranjang, checkout & voucher, pengisian alamat, top-up saldo, dll.) ke dalam skenario **Positive Testing**, **Negative Testing**, **Boundary Value Analysis**, dan **UI/Responsiveness Testing**.
2. Jalankan pengujian menggunakan Playwright, pantau Console Error serta kegagalan Network/HTTP Request, dan verifikasi apakah perilaku sistem sesuai dengan spesifikasi yang diekstrak pada Phase 0.
3. Jangan mengklaim bug tanpa bukti screenshot dan langkah reproduksi yang terverifikasi.

## Important Rules
1. Dilarang melakukan transaksi atau pembayaran sungguhan. Gunakan data dummy untuk pengujian form, registrasi, dan checkout.
2. Simpan seluruh file output hanya di dalam folder `qa-results/`.

## Output & Format Laporan
1. Salin file `qa-template/template_bug_report.xlsx` ke `qa-results/TokoKampus_QA_Bug_Report.xlsx` tanpa menghapus formatting, aturan warna, catatan panduan merah, baris contoh abu-abu, maupun Data Validation (dropdown) bawaan.
2. Inspeksi aturan Data Validation di dalam file Excel terlebih dahulu menggunakan `openpyxl` agar nilai pada kolom bertanda dropdown (`Fitur`, `Severity`, `Priority`, `Status Terakhir`, `Status Lama`, `Status Baru`) selalu sesuai dengan pilihan valid yang tersedia di template.
3. Mulai isi data temuan baru tepat pada baris kosong di bawah baris contoh sesuai instruksi pada header template.

### Worksheet 1: Bug Report
Isi 14 kolom secara berurutan:
- **Bug ID**: Format `BUG-01`, `BUG-02`, dst. (beri fill warna kuning pada sel ini).
- **Tanggal**: Format `DD/MM/YYYY` (tanggal pengujian dilakukan).
- **Ditemukan Oleh**: `Dio Lutvi Andre`
- **Fitur**: Pilih nilai yang sesuai dari dropdown kolom Fitur (contoh: `Checkout & Voucher`, dll.).
- **Judul Bug**: Ringkasan singkat dan jelas mengenai masalah yang ditemukan.
- **Teknik yang Digunakan**: Contoh: `Negative Testing`, `Positive Testing`, `Boundary Value Analysis`, `UI Testing`.
- **Penjelasan Teknik (cara menerapkan dan data uji)**: Jelaskan secara runtut data uji yang digunakan, skenario aksi yang dilakukan, perilaku yang seharusnya terjadi, dan analisis penyebab teknis (misalnya error dari tab Console/Network).
- **Langkah Reproduksi**: Tulis dalam bentuk daftar bernomor (`1.`, `2.`, `3.`, dst.) secara detail.
- **Hasil yang Diharapkan**: Perilaku sistem yang semestinya berdasarkan spesifikasi website.
- **Hasil Aktual**: Perilaku nyata yang terjadi saat pengujian, sertakan pesan error Console/HTTP jika ada.
- **Severity**: Pilih dari dropdown (`Critical`, `High`, `Medium`, `Low`).
- **Priority**: Pilih dari dropdown (`High`, `Medium`, `Low`).
- **Status Terakhir**: Pilih dari dropdown (`Confirmed` jika bug sudah terbukti dapat direproduksi dengan bukti screenshot).
- **Bukti (Link)**: Path relatif menuju file screenshot di folder `qa-evidence/` (contoh: `qa-evidence/BUG-01.png`).

### Worksheet 2: Bug Log
Untuk setiap bug yang ditemukan dan berhasil direproduksi, catat 2 baris riwayat status berurutan (mengikuti contoh pada template):
- Baris 1: `Status Lama` = `New`, `Status Baru` = `New` (saat bug pertama kali terdeteksi).
- Baris 2: `Status Lama` = `New`, `Status Baru` = `Confirmed` (setelah bug diverifikasi dan direproduksi ulang).
- Isi kolom `Bug ID`, `Tanggal` (`D/M/YYYY` atau `DD/MM/YYYY`), `Diubah Oleh` (`Dio Lutvi Andre`), dan `Keterangan` secara lengkap.

## Bug Evidence
- Ambil screenshot setiap kali bug berhasil direproduksi menggunakan browser Chromium.
- Simpan di `qa-results/qa-evidence/` dengan format nama sesuai Bug ID (contoh: `BUG-01.png`).
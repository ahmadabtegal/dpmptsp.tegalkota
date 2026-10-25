# Website DPMPTSP Kota Tegal — paket awal

## Isi paket
- `index.html`: frontend statis untuk GitHub Pages.
- `assets/logo-kota-tegal.png`: lambang Kota Tegal.
- `assets/logo-dpmptsp.png`: logo DPMPTSP.
- `assets/favicon.ico` dan `assets/favicon.png`: favicon.
- `Database_DPMPTSP_Kota_Tegal.xlsx`: template database untuk diimpor ke Google Sheets.
- `Code.gs`: API Google Apps Script untuk membaca data dari Google Sheets.

## 1. Siapkan database Google Sheets
1. Buka Google Drive → New → Google Sheets.
2. Impor `Database_DPMPTSP_Kota_Tegal.xlsx` ke Google Sheets.
3. Pastikan nama tab tetap: `Pengaturan`, `Berita`, `Layanan`, `Dokumen`, `FAQ`, `Kontak`.
4. Salin ID spreadsheet dari URL: `https://docs.google.com/spreadsheets/d/SPREADSHEET_ID/edit`.

## 2. Pasang API Apps Script
1. Dari spreadsheet, pilih Extensions → Apps Script.
2. Ganti kode awal dengan isi `Code.gs`.
3. Ganti `ISI_ID_GOOGLE_SHEET_DI_SINI` dengan ID spreadsheet.
4. Simpan, lalu Deploy → New deployment → type Web app.
5. Execute as: Me; Who has access: Anyone (sesuaikan kebijakan keamanan instansi).
6. Deploy dan salin URL Web App yang berakhiran `/exec`.
7. Uji URL dengan menambahkan `?action=health`, lalu `?action=all`.

## 3. Hosting frontend di GitHub Pages
1. Buat repository GitHub, misalnya `website-dpmptsp-tegal`.
2. Upload `index.html` dan folder `assets/` ke root repository.
3. Commit perubahan.
4. Settings → Pages → Build and deployment → Deploy from a branch → `main` / `/ (root)`.
5. Tunggu URL GitHub Pages tampil. Domain resmi dapat diarahkan oleh admin domain/hosting setelah koordinasi DNS dan HTTPS.

## 4. Pengaturan yang masih diperlukan
- URL dashboard Peluang/Potensi Investasi yang berdiri terpisah belum diberikan. Tautan dashboard perlu diisi pada konfigurasi frontend sebelum publikasi.
- Verifikasi nomor telepon, email, alamat, dokumen, berita, serta tautan layanan sebelum tayang.
- Data contoh berstatus DRAFT/VERIFIKASI tidak dipublikasikan oleh API.
- API ini hanya menyediakan pembacaan data (GET); pengelolaan data dilakukan langsung pada Google Sheets. Jangan menambahkan endpoint tulis publik tanpa autentikasi.
- Untuk produksi, sebaiknya gunakan akun Google institusi dan repository milik instansi, bukan akun pribadi.

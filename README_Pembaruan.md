# Pembaruan Website DPMPTSP Kota Tegal

Paket ini disusun berdasarkan baseline yang diberikan pada 25 Oktober 2026. File `index.html` merupakan frontend publik, `Code.gs` backend Google Apps Script, dan `Admin.html` merupakan dashboard admin yang dijalankan di dalam Apps Script agar proses administrasi tidak bergantung pada request lintas-domain dari GitHub Pages.

## Isi paket
- `index.html` — portal publik dengan tambahan pengaduan/SP4N-LAPOR!, SKM/IKM, integritas-antigratifikasi, akses kelompok rentan, panduan OSS/KBLI, statistik, FAQ, dan pencarian.
- `Code.gs` — API publik, validasi status publikasi, perluasan skema sheet, pembatasan percobaan login, token sesi, validasi Standar Pelayanan, timestamp pembaruan otomatis, dan audit trail.
- `Admin.html` — halaman admin untuk mengelola konten menggunakan `google.script.run`.
- Folder `assets/` tidak disertakan karena file aset asli tidak diunggah bersama baseline. Pertahankan folder aset yang sudah ada di hosting (logo Kota Tegal, logo DPMPTSP, favicon).

## Instalasi / pembaruan
1. **Cadangkan** spreadsheet dan versi Apps Script yang sedang berjalan.
2. Buka proyek Google Apps Script yang digunakan website.
3. Ganti isi file `Code.gs` dengan file pada paket ini.
4. Tambahkan file HTML baru bernama persis `Admin` (Apps Script akan menyimpan sebagai `Admin.html`) dan tempel isi `Admin.html`.
5. Pastikan Script Properties berikut sudah tersedia:
   - `SPREADSHEET_ID`
   - `ADMIN_USERNAME`
   - `ADMIN_PASSWORD` (gunakan kata sandi kuat dan unik; jangan ditulis di kode)
6. Simpan proyek dan jalankan/otorisasi sesuai permintaan Google jika diperlukan.
7. Buka **Deploy → Manage deployments**, edit deployment Web App yang saat ini dipakai, pilih **New version**, lalu deploy. Gunakan konfigurasi yang sama seperti sebelumnya (umumnya Execute as: Me; akses sesuai kebijakan instansi).
8. Jika URL `/exec` berubah, perbarui konstanta `API_URL` di `index.html` dengan URL deployment terbaru.
9. Ganti `index.html` pada hosting statis (misalnya GitHub Pages) dengan versi dari paket ini. Jangan menghapus folder `assets/`.
10. Buka website, lalu uji menu publik, dokumen, pengumuman, peta, dan tautan. Klik **Admin**; login seharusnya membuka dashboard admin di Apps Script.
11. Saat website publik memanggil `action=all`, tab baru dan kolom yang belum tersedia akan dibuat/ditambahkan otomatis. Periksa Google Sheets setelah pertama kali membuka website.

## Catatan struktur database
Tab tambahan yang akan dibuat otomatis: `Pengaduan`, `SKM`, `Integritas`, `Statistik`, `PanduanOSS`. Kolom yang belum tersedia pada tab lama akan ditambahkan di sebelah kanan tanpa memindahkan kolom lama. Tab `AuditTrail` dibuat saat aktivitas admin pertama kali dicatat. Data lama tidak dihapus.

## Status publikasi
- Gunakan `AKTIF` untuk konten siap tampil ke publik.
- Gunakan `DRAFT` untuk konten yang belum diverifikasi.
- Konten tanpa status aktif tidak ditampilkan pada API publik.
- Konten Standar Pelayanan berstatus aktif harus mengisi 14 komponen: persyaratan; sistem/mekanisme/prosedur; jangka waktu; biaya/tarif; produk pelayanan; penanganan pengaduan; dasar hukum; sarana/prasarana; kompetensi pelaksana; pengawasan internal; jumlah pelaksana; jaminan pelayanan; jaminan keamanan/keselamatan; evaluasi kinerja. Nama layanan juga wajib diisi sebagai identitas record.

## Penting sebelum dipublikasikan
- Periksa dan verifikasi isi standar, biaya, jam pelayanan, nomor kontak, URL PPID, URL dashboard investasi, dan kanal pelaporan sebelum mengaktifkan publikasi.
- Isi sheet `Pengaturan` hanya dengan data yang memang layak publik. API publik menggunakan daftar kunci pengaturan yang diizinkan; kunci lain tidak ikut dikirim ke publik.
- Jangan menyimpan password, token, atau kredensial pada spreadsheet atau kolom `Pengaturan`.
- Audit trail merekam login/logout dan perubahan data admin. Batasi akses editor proyek Apps Script dan spreadsheet hanya kepada petugas berwenang.
- Fitur yang bergantung pada data instansi (nilai IKM, statistik, fasilitas kelompok rentan, WBS/kanal lokal) harus diisi berdasarkan informasi resmi terverifikasi. Paket ini tidak mengarang nilai IKM, statistik, atau URL WBS.
- Pengujian di sini mencakup pemeriksaan sintaks JavaScript dan struktur file. Login, izin deployment, koneksi ke spreadsheet nyata, dan alur publikasi tetap harus diuji setelah deployment karena memerlukan akses ke akun/proyek Google milik instansi.

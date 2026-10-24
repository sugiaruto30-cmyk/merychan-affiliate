# Merychan Endorse Tracker

Aplikasi web responsif dan PWA (Progressive Web App) untuk pendataan kerja sama endorse. Bisa digunakan di laptop/desktop dan dipasang di HP Android/iPhone dari browser yang mendukung instalasi web app.

## Fitur
- Dashboard nilai kontrak, jumlah endorse, status aktif, uang diterima, dan sisa pembayaran.
- Tambah, edit, hapus, cari, dan filter data endorse.
- Deadline konten dan daftar pembayaran tertunda.
- Ekspor CSV, ekspor/impor JSON, dan gabung data dari backup.
- PWA manifest + service worker untuk aset aplikasi yang dapat di-cache.
- Integrasi Google Drive opsional untuk menyimpan/memulihkan backup JSON.

## Jalankan lokal
Karena service worker dan Google OAuth memerlukan origin web, jalankan melalui server lokal (bukan membuka `index.html` langsung). Contoh:

```bash
python -m http.server 8000
```

Lalu buka `http://localhost:8000` di folder proyek ini.

## Pasang di HP
1. Hosting folder ini ke layanan HTTPS statis seperti GitHub Pages, Netlify, atau Cloudflare Pages.
2. Buka URL situs di Chrome Android atau Safari iPhone.
3. Android: menu browser → **Install app / Tambahkan ke layar utama**. iPhone: tombol Share → **Add to Home Screen**.

## Google Drive
Integrasi Drive tidak dapat aktif tanpa kredensial OAuth milik pemilik aplikasi. Untuk mengaktifkannya:
1. Buat proyek di Google Cloud Console.
2. Aktifkan **Google Drive API**.
3. Konfigurasikan OAuth consent screen dan buat OAuth Client ID tipe **Web application**.
4. Tambahkan origin HTTPS tempat aplikasi di-host (serta `http://localhost:8000` untuk pengujian) di **Authorized JavaScript origins**.
5. Masukkan Client ID ke `config.js` pada `GOOGLE_CLIENT_ID`.
6. Host ulang, buka aplikasi, lalu pilih **Backup Data → Hubungkan Google Drive**.

Aplikasi menggunakan scope `drive.file` dan membuat/memperbarui file bernama `Merychan-Endorse-Tracker-backup.json`. Token Google hanya disimpan dalam memori sesi, bukan localStorage. Google Drive backup adalah tindakan manual melalui tombol simpan/pulihkan, bukan sinkronisasi otomatis setiap perubahan.

## Catatan data
Data operasional tersimpan di localStorage browser/perangkat. Data tidak otomatis berpindah antarperangkat. Gunakan Google Drive backup atau ekspor JSON secara rutin. Hindari memasukkan informasi sensitif yang tidak diperlukan.

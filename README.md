# Sekolah Absenku - Paket Aplikasi PWA

Isi paket ini sudah diubah dari 1 file HTML menjadi aplikasi web yang bisa dipasang di HP seperti aplikasi.

## Isi file
- `index.html` — aplikasi utama Absenku.
- `manifest.json` — pengaturan nama aplikasi, ikon, warna, dan mode layar penuh.
- `sw.js` — service worker agar aplikasi bisa dibuka lebih cepat dan sebagian tetap bisa dipakai setelah pernah dibuka.
- `icons/` — ikon aplikasi ukuran 192 dan 512.

## Cara pakai paling mudah di HP Android
1. Upload folder ini ke hosting HTTPS, misalnya Cloudflare Pages, Netlify, Vercel, atau GitHub Pages.
2. Buka link aplikasinya di Chrome Android.
3. Tekan menu titik tiga Chrome.
4. Pilih **Tambahkan ke layar utama** atau **Install app**.
5. Aplikasi Absenku akan muncul seperti aplikasi biasa di layar HP.

## Catatan penting
- Data tetap tersimpan di browser/localStorage dan fitur Cloudflare Sync di HTML tetap bisa dipakai jika URL Worker sudah diisi.
- Untuk menjadi APK Android asli, gunakan paket ini sebagai sumber WebView/TWA atau layanan builder APK. PWA ini adalah versi paling ringan dan cepat untuk dipasang.
- Fitur ekspor gambar memakai library html2canvas dari CDN. Pastikan HP terkoneksi internet minimal saat pertama kali fitur itu digunakan.

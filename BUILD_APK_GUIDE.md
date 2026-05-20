# Panduan Lengkap: Membuat APK Android dari Absenku PWA

Aplikasi Absenku adalah Progressive Web App (PWA) yang dapat dikonversi menjadi APK Android. Berikut panduan lengkap untuk berbagai metode.

## Metode 1: Menggunakan GitHub Pages + PWA Builder (TERMUDAH)

### Langkah 1: Deploy ke GitHub Pages
1. Pastikan repository sudah public
2. Buka **Settings** → **Pages**
3. Pilih branch: `main`
4. Folder: `/ (root)`
5. Klik **Save**
6. Tunggu hingga mendapat URL seperti: `https://adendhaedi001-eng.github.io/Absenku/`

### Langkah 2: Gunakan PWA Builder (Microsoft)
1. Buka https://www.pwabuilder.com/
2. Masukkan URL: `https://adendhaedi001-eng.github.io/Absenku/`
3. Klik **Start**
4. Di bagian **Your PWAs**, klik **Package for stores**
5. Pilih **Android** dan klik **Generate Download**
6. Download file `.apk` yang sudah jadi

**Keuntungan:** Gratis, cepat, tidak perlu setup kompleks
**Hasil:** APK siap install di HP Android

---

## Metode 2: Menggunakan Cloudflare Pages + PWA Builder

Jika ingin hosting lebih cepat atau domain custom:

1. Push code ke GitHub
2. Login ke https://pages.cloudflare.com/
3. Hubungkan repository Absenku
4. Build settings:
   - Build command: (kosongkan, PWA tidak butuh build)
   - Build output directory: `/`
5. Deploy
6. Dapatkan URL seperti: `https://absenku.pages.dev/`
7. Ikuti **Metode 1** langkah 2 dengan URL baru ini

---

## Metode 3: Menggunakan Bubblewrap (Untuk Kontrol Penuh)

Jika ingin kontrol lebih dan signing certificate sendiri:

### Instalasi Prerequisites
```bash
# Install Node.js dari https://nodejs.org/ (versi LTS)
# Pastikan sudah install

# Install Bubblewrap
npm install -g @bubblewrap/cli

# Install Android SDK (opsional, jika ingin build sendiri)
# Download dari https://developer.android.com/studio
```

### Generate APK
```bash
# Buat folder project
mkdir absenku-apk
cd absenku-apk

# Inisialisasi Bubblewrap dengan URL PWA
bubblewrap init --manifest https://adendhaedi001-eng.github.io/Absenku/manifest.json

# Build APK
bubblewrap build
```

Hasil APK ada di folder `dist/`

---

## Metode 4: Menggunakan Android Studio (Kontrol Maksimal)

Untuk developer yang ingin modifikasi native code:

1. Download Android Studio dari https://developer.android.com/studio
2. Buat project baru: **File** → **New** → **New Project**
3. Pilih template: **No Activity** atau **Empty Activity**
4. Di `AndroidManifest.xml`, tambahkan:
```xml
<activity android:name=".MainActivity">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>

<application>
    <activity android:name="android.webkit.WebViewActivity" />
</application>
```

5. Buat custom WebView untuk load URL PWA
6. Build APK melalui **Build** → **Build Bundle(s) / APK(s)** → **Build APKs**

---

## Metode Rekomendasi untuk Anda

**Gunakan Metode 1 (PWA Builder)** karena:
- ✅ Paling cepat (5 menit selesai)
- ✅ Gratis
- ✅ Tidak perlu setup tools rumit
- ✅ Hasil APK langsung siap install
- ✅ Automatic update jika PWA berubah
- ✅ Signed dengan sertifikat aman

---

## Apa yang Terjadi Setelah APK Jadi?

### Ukuran File
- APK Absenku: ~8-15 MB (kecil, ringan)
- Saat install: ~25-35 MB (dengan Android runtime)

### Fitur yang Tetap Jalan
- ✅ Absensi, Nilai, Iuran, Prestasi
- ✅ Share WhatsApp, Export CSV, Download JPG
- ✅ Storage lokal 30 hari automatic backup
- ✅ Cloudflare sync (jika Worker URL diisi)
- ✅ Service Worker (buka cepat, offline mode)

### Distribusi APK

#### Opsi A: Google Play Store
1. Buat Google Play Developer Account ($25 sekali)
2. Upload APK ke Play Console
3. Tunggu review (1-3 jam)
4. APK live di Play Store
5. Setiap update, upload versi baru

#### Opsi B: Share Direct (Paling Cepat)
1. Upload APK ke server/cloud storage
2. Buat link download publik
3. Share link ke guru/siswa
4. Mereka download langsung ke HP
5. Install: **Settings** → **Security** → **Allow Unknown Sources**

#### Opsi C: GitHub Release
1. Di repository ini, buat **Release** baru
2. Upload file APK
3. Share link release ke siswa
4. Mereka download dari GitHub

---

## Checklist Sebelum Build APK

- [x] `manifest.json` sudah ada dengan icon 192x192 dan 512x512
- [x] `sw.js` (service worker) sudah ada
- [x] `index.html` responsive dan buka di mobile Chrome
- [x] App bisa offline (setelah pertama kali dibuka)
- [x] HTTPS / hosting dengan SSL (required PWA)

---

## Troubleshooting

### APK Tidak Install di HP Lama (Android 5-6)
- PWA Builder default targetkan Android 7+
- Untuk dukungan lama, gunakan Bubblewrap dengan custom minSdkVersion

### APK Ukuran Besar
- PWA Builder menambah ~2-3 MB untuk runtime Chrome
- Normal dan minimal untuk WebView app

### APK Tidak Bisa Offline
- Pastikan `sw.js` ada dan valid
- Manifest.json harus accessible dari HTTPS
- Cache mungkin belum ter-update, buka app 2x

### Update Aplikasi
Setiap kali ubah code HTML/JS:
1. Push ke GitHub/Cloudflare
2. Buat release APK baru
3. User update dari app atau download APK baru

---

## Rekomendasi Update Berkelanjutan

Untuk kemudahan update tanpa rebuild APK:

1. **Deploy PWA ke Cloudflare Pages**
   - APK tetap sama
   - Update web app otomatis
   - Service worker cache refresh setiap hari

2. **Atau gunakan GitHub Pages**
   - Link PWA bisa dibagikan
   - APK diupdate sebulan sekali kalau ada feature besar

3. **Jangan sering rebuild APK**
   - PWA Builder sudah handle auto-update dari source
   - Cukup update web app, APK tetap sama

---

## Link Helpful

- PWA Builder: https://www.pwabuilder.com/
- GitHub Pages Setup: https://docs.github.com/en/pages
- Manifest Validator: https://manifest-validator.appspot.com/
- Android Test Device: Gunakan emulator Android Studio atau HP Android 7+
- WebView Best Practice: https://developer.android.com/reference/android/webkit/WebView

---

**Total Waktu Produksi:** 5-15 menit (tergantung metode)

Pilih Metode 1 untuk hasil tercepat! 🚀

# 🚀 Panduan Deploy ke Railway

Panduan lengkap untuk mendeploy portfolio website ini ke Railway tanpa mengubah kode.

## ✅ Prasyarat

- Akun GitHub (sudah punya)
- Akun Railway (gratis di https://railway.app)
- Node.js v18+ (untuk testing lokal, opsional)

---

## 📋 Langkah-Langkah Deploy

### 1️⃣ Siapkan Environment Variables

Repo ini sudah memiliki `.env.example`. Anda perlu membuat file `.env` lokal:

**Di komputer Anda (jangan push ke GitHub!):**
```bash
cp .env.example .env
```

**Edit `.env` dengan password yang aman:**
```env
ADMIN_PASSWORD=password_admin_anda_yang_aman
SESSION_SECRET=secret_yang_panjang_dan_random_minimal_32_karakter
```

💡 Tips membuat `SESSION_SECRET` yang bagus:
```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

### 2️⃣ Push ke GitHub

File `.env` sudah di `.gitignore`, jadi aman tidak akan terupload:

```bash
git add .
git commit -m "Setup for Railway deployment"
git push origin main
```

### 3️⃣ Buat Akun & Login Railway

1. Buka https://railway.app
2. Klik "Login" → "Login with GitHub"
3. Authorize Railway untuk akses repo GitHub Anda

### 4️⃣ Deploy ke Railway

**Langkah di Railway Dashboard:**

1. Klik **"New Project"** (tombol biru di kanan atas)
2. Pilih **"Deploy from GitHub repo"**
3. Cari dan pilih repo: `XiaomiBOT/hanzweb`
4. Railway akan otomatis mulai build

**Saat build berlangsung:**
- Railway mendeteksi Astro + Node.js
- Instal dependencies
- Build aplikasi

### 5️⃣ Set Environment Variables

Setelah build selesai:

1. Di Railway Dashboard, klik project Anda
2. Buka tab **"Variables"**
3. Tambahkan 2 variabel:
   - **Key:** `ADMIN_PASSWORD` → **Value:** `password_anda`
   - **Key:** `SESSION_SECRET` → **Value:** `secret_anda`

4. Klik **"Save"** → Railway akan redeploy otomatis

### 6️⃣ Tunggu Deploy Selesai

- Status berubah menjadi **"Success"**
- Klik link domain yang muncul (misal: `hanzweb-production.up.railway.app`)

---

## ✨ Website Live!

Sekarang website Anda bisa diakses di:
- **Domain public:** `https://hanzweb-production.up.railway.app`
- **Admin login:** `https://hanzweb-production.up.railway.app/admin/login`

### Login Admin
- URL: `/admin/login`
- Password: `ADMIN_PASSWORD` yang Anda set di Railway Variables

---

## 🔄 Update Kode (Push Baru)

Setiap kali Anda push ke `main` branch:

```bash
git push origin main
```

Railway **otomatis rebuild dan deploy** dalam 1-2 menit. Tidak perlu manual apa-apa.

---

## 🌐 Setup Custom Domain (Opsional)

Kalau mau domain custom (misal: `portfolio.com`):

1. Di Railway Dashboard → **Settings** → **Domains**
2. Klik **"Add Custom Domain"**
3. Masukkan domain Anda
4. Update DNS setting di registrar domain Anda (misal: Namecheap, GoDaddy)
5. Railway akan kasih instruksi DNS yang detail

---

## 📊 Monitoring & Logs

Di Railway Dashboard:
- **Logs:** Lihat real-time console output
- **Metrics:** CPU, memory usage
- **Deployments:** History semua deployment

Kalau ada error, lihat tab **"Logs"** untuk debugging.

---

## 🆘 Troubleshooting

### ❌ Deployment Failed
- Cek **Logs** di Railway Dashboard
- Pastikan `package.json` valid
- Cek apakah ada error di build process

### ❌ Admin Login Tidak Bekerja
- Pastikan `ADMIN_PASSWORD` sudah diset di Railway Variables
- Tunggu 30 detik setelah update Variables (auto redeploy)
- Clear browser cache atau coba incognito mode

### ❌ File Upload Tidak Menyimpan
- Railway menggunakan ephemeral filesystem (file bisa hilang saat redeploy)
- Untuk production, gunakan external storage (Cloudinary, Supabase, dll)
- Untuk sekarang, upload bersifat temporary saja

### ❌ Database Error
- Database SQLite disimpan di Railway filesystem
- Data aman selama Railway container masih running
- Untuk backup, download dari Railway Dashboard

---

## 💰 Railway Pricing

**Gratis:** $5/bulan credit (biasanya cukup untuk 1-2 portofolio)
- Jika exceed, Anda bisa tambah payment method untuk lanjut

---

## 📝 Catatan Penting

✅ **Aman:**
- `.env` tidak ter-push ke GitHub (sudah di `.gitignore`)
- Password dan secret hanya ada di Railway, tidak di public repo

⚠️ **Keterbatasan:**
- SQLite database disimpan lokal (bisa hilang kalau Railway restart)
- Upload folder bersifat temporary (file bisa hilang saat redeploy)
- Jika ingin production-ready, upgrade ke database eksternal (PostgreSQL) dan storage eksternal

---

## 🚀 Selesai!

Website Anda sekarang live di Railway dengan Astro + Node.js, tanpa mengubah satu baris kode pun.

Setiap update code → push ke GitHub → Railway auto-deploy. Mudah!

Pertanyaan? Lihat dokumentasi lengkap:
- Railway: https://docs.railway.app
- Astro: https://docs.astro.build
- Project ini: lihat `GUIDE.md`

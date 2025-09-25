# 🚀 Panduan Deployment GitHub Pages

## Workflow Deployment Otomatis

Website Hall of Fame Mahasiswa Kelompok 4 menggunakan GitHub Actions untuk deployment otomatis ke GitHub Pages.

### 📋 Langkah Setup

1. **Enable GitHub Pages**:
   - Buka repository di GitHub
   - Pergi ke **Settings** → **Pages**  
   - Di bagian **Source**, pilih **GitHub Actions**

2. **Workflow akan otomatis berjalan** ketika:
   - Push ke branch `main` atau `programmer`
   - Pull request ke branch `main`

3. **Akses website** di: 
   ```
   https://aprilianza.github.io/CAK3BAB3-IMPLEMENTASI_DAN-PENGUJIAN_PERANGKAT_LUNAK-IF-47-08-Kelompok4/
   ```

### 🔧 Fitur Workflow

- ✅ **Otomatis build** website dari `main.html`
- ✅ **Copy semua aset** (gambar, CSS, JS)
- ✅ **Rename main.html** menjadi `index.html`
- ✅ **Generate 404 page** otomatis
- ✅ **Deploy ke GitHub Pages**

### 📊 Status Badge

Tambahkan badge ini ke README.md:
```markdown
![Deploy Status](https://github.com/aprilianza/CAK3BAB3-IMPLEMENTASI_DAN-PENGUJIAN_PERANGKAT_LUNAK-IF-47-08-Kelompok4/workflows/Deploy%20Hall%20of%20Fame%20Website/badge.svg)
```

### 🛠️ File yang Di-Deploy

- `main.html` → `index.html` (homepage)
- `purple_.png` (logo kelompok)
- `404.html` (halaman error otomatis)
- Semua aset lainnya (CSS, JS, gambar)

### 📝 Troubleshooting

**Jika deployment gagal dengan "Not Found" atau "Get Pages site failed":**

1. **Manual Setup GitHub Pages**:
   - Pergi ke **Settings** → **Pages**
   - **Source**: Pilih **"GitHub Actions"** (bukan Deploy from branch)
   - Klik **Save**

2. **Cek Repository Permissions**:
   - **Settings** → **Actions** → **General**
   - **Workflow permissions**: Pilih **"Read and write permissions"**
   - Centang **"Allow GitHub Actions to create and approve pull requests"**

3. **Alternatif Workflow**:
   - Gunakan file `deploy-alternative.yml` yang lebih robust
   - Atau disable `deploy.yml` dan gunakan yang alternatif

4. **Manual Troubleshooting**:
   ```bash
   # Cek apakah Pages sudah enabled via GitHub CLI
   gh api repos/:owner/:repo/pages
   ```

**Jika masih error "HttpError: Not Found":**
1. Pastikan repository **public** atau upgrade ke GitHub Pro
2. Tunggu 24 jam setelah enable GitHub Pages pertama kali
3. Coba **disable** dan **enable** kembali GitHub Pages
4. Gunakan workflow alternative: `deploy-alternative.yml`

**Jika website tidak muncul:**
1. Tunggu 5-10 menit setelah deployment
2. Cek URL GitHub Pages di **Settings** → **Pages**
3. Pastikan branch yang benar dipilih
4. Clear browser cache atau coba incognito mode

---
**Created by Kelompok 4 - Implementasi dan Pengujian Perangkat Lunak**
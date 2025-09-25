# Laporan Audit — Hall of Fame Mahasiswa (main.html)

**File yang diaudit:** `main.html`

**Tanggal audit:** 2025-09-25

**Auditor:** Ahmad Refi

**Scope:** pemeriksaan front-end (HTML / CSS / JS), security (klien), aksesibilitas, maintainability, serta pemetaan ke issue repository.

---

## 1 — Ringkasan singkat

`main.html` sudah memiliki desain modern dengan struktur grid, animasi sederhana, dan layout responsif. Namun masih ada beberapa hal yang perlu diperbaiki terutama dari sisi **keamanan link eksternal**, **aksesibilitas**, serta **maintainability** (struktur kode dan fallback aset).

---

## 2 — Tabel Hasil Audit (disesuaikan dengan Issue di repo)

| No | Issue | Programmer | Configuration Manager | Status | Catatan |
| --- | --- | --- | --- | --- | --- |
| 1 | **#8 Style and feature** | Aprilianza Muhammad Yusup, Muhammad Ihsan Naufal | Ananda Marchel | Open | Style sudah modern, tapi perlu ditambahkan `:focus` untuk aksesibilitas & minifikasi CSS. |
| 2 | **#5 Card Anggota Kelompok** | Aprilianza Muhammad Yusup | Ananda Marchel | Open | Sudah sesuai, tapi `innerHTML` sebaiknya diganti `textContent`/DOM builder agar lebih aman. Tambahkan fallback avatar. |
| 3 | **#4 Footer – About Us** | Muhammad Ihsan Naufal | Ananda Marchel | Open | Link eksternal di footer perlu `rel="noopener noreferrer"` bila menggunakan `target="_blank"`. |
| 4 | **#3 Quotes Section** | Aprilianza Muhammad Yusup | Ananda Marchel | Open | Struktur HTML sebaiknya menggunakan `<section>` semantik. Tambahkan kontras warna sesuai WCAG. |
| 5 | **#1 Hero Section Landing Page Kelompok** | Muhammad Ihsan Naufal | Ananda Marchel | Open | Hero section sudah menarik, tapi sebaiknya pakai landmark `<main>` agar lebih semantik. |

---

## 3 — Temuan detail & rekomendasi

### Keamanan

- **Rel="noopener noreferrer"** harus ditambahkan di semua link dengan `target="_blank"`.
- Hindari penggunaan `innerHTML` untuk data dinamis. Ganti dengan `textContent` atau builder DOM.

### Aksesibilitas

- Tambahkan landmark semantik `<main>`, `<section>`, `<article>`.
- Berikan style `:focus` agar navigasi keyboard terlihat.
- Periksa kontras warna terutama di teks sekunder (Quotes, Footer).

### Maintainability

- Pisahkan CSS/JS ke file terdedikasi (`styles.css`, `app.js`).
- Tambahkan fallback avatar (gambar default jika URL error).
- Minifikasi CSS/JS saat deployment.
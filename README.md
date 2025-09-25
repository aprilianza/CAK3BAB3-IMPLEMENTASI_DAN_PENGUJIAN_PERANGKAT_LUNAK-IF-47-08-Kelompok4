# Laporan Audit — Hall of Fame Mahasiswa (main.html)

**File yang diaudit:** `main.html`  
**Tanggal audit:** 2025-09-25  
**Auditor:** Ahmad Refi  
**Scope:** pemeriksaan front-end (HTML / CSS / JS), security (klien), aksesibilitas, maintainability, dan rekomendasi proses kolaborasi.

---

## 1 — Ringkasan singkat
`main.html` adalah halaman statis yang memiliki desain modern, animasi halus, dan layout responsif. Banyak praktik baik (label form, penggunaan `alt` pada gambar, responsive grid). Namun ditemukan beberapa perbaikan penting untuk keamanan klien, aksesibilitas, dan maintainability.

**Prioritas perbaikan:**
1. Tambah `rel="noopener noreferrer"` pada semua link yang memakai `target="_blank"`. *(Medium)*  
2. Hindari `innerHTML` untuk data yang bisa berasal dari sumber eksternal — gunakan `textContent` atau DOM-safe builder. *(Low–Medium)*  
3. Tambah fallback untuk avatar (gambar default) jika URL avatar bermasalah. *(Low)*  
4. Perbaiki semantik HTML (pakai `<main>`, `<section>`, `<article>`), dan tambahkan style :focus untuk keyboard users. *(Low)*

---

## 2 — Tabel Hasil Audit (tampilan seperti diminta)
> Catatan: Issue/PR/Status = `N/A` karena tidak tersedia dari file statis. Untuk data real, sertakan `git log` / akses repo / daftar PR & Issue.

| No | Issue ID | PR ID | Programmer | Configuration Manager | Status | Catatan |
|---:|:--------:|:-----:|:-----------|:---------------------:|:------:|:--------|
| 1 | N/A | N/A | aprilianza muhammad yusup | ananda marchel | N/A | Nama muncul di `main.html`. Audit teknis dilakukan pada file. |
| 2 | N/A | N/A | — | — | N/A | Untuk isi tabel Issue/PR: sediakan daftar Issue/PR atau akses repo. |

---

## 3 — Temuan detail & rekomendasi

### Keamanan (Medium)
- **target="_blank" tanpa rel** → Tambahkan `rel="noopener noreferrer"` ke link GitHub.
- **innerHTML** digunakan untuk memasukkan teks dari `data` → ganti dengan pembuatan elemen dan `textContent` jika data bisa berasal dari luar.

### Aksesibilitas (Low–Medium)
- Gunakan landmark semantik: ubah wrapper utama jadi `<main>`; tiap kartu bisa jadi `<article>`.
- Tambahkan visible `:focus` style (mis. outline atau box-shadow) agar pengguna keyboard tahu fokus saat navigasi.
- Periksa kontras warna untuk teks sekunder (WCAG AA).

### Maintainability & Perf (Low)
- Pisahkan CSS & JS ke `styles.css` dan `app.js` untuk kemudahan pengelolaan.
- Tambahkan fallback avatar (`onerror` handler) agar gambar rusak tidak tampil broken.
- Pertimbangkan minifikasi saat deploy.

---

## 4 — Patch kode (perbaikan cepat, contoh)
Ganti fungsi `renderCards()` (yang menggunakan `innerHTML`) dengan metode DOM-safe seperti contoh berikut (potong untuk README; masukkan ke `app.js`):

```js
function renderCards(role = 'all') {
  const cardsContainer = document.getElementById('cards');
  cardsContainer.innerHTML = '';
  const filtered = role === 'all' ? data : data.filter(d => d.role === role);

  filtered.forEach((person, i) => {
    const card = document.createElement('article');
    card.className = 'card';
    card.style.animationDelay = `${i * 0.1}s`;

    const img = document.createElement('img');
    img.className = 'avatar';
    img.src = person.avatar;
    img.alt = person.name;
    img.onerror = () => { img.src = 'assets/default-avatar.png'; };

    const roleDiv = document.createElement('div');
    roleDiv.className = 'role';
    roleDiv.textContent = person.role;

    const nameDiv = document.createElement('div');
    nameDiv.className = 'name';
    nameDiv.textContent = person.name;

    const hobbyDiv = document.createElement('div');
    hobbyDiv.className = 'hobby';
    hobbyDiv.textContent = `Hobi: ${person.hobby}`;

    const link = document.createElement('a');
    link.className = 'github-link';
    link.href = person.github;
    link.target = '_blank';
    link.rel = 'noopener noreferrer';
    link.setAttribute('aria-label', `GitHub ${person.name}`);
    link.innerHTML = `<svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 0C5.37..." /></svg> GitHub`;

    card.append(img, roleDiv, nameDiv, hobbyDiv, link);
    cardsContainer.appendChild(card);
  });
}

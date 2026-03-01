# Portfolio — Reswara Ganendra Rashi Dewa

> Mini Project 1 — Pemrograman Berbasis Web  
> 2409116100 — Kelas C 2024

### Link Website Portofolio: https://reswara26.github.io/pbw-minpro1/
---

## 🛠️ Teknologi yang Digunakan

| Teknologi | Kegunaan |
|---|---|
| **HTML5** | Struktur dasar halaman web |
| **CSS3** | Styling, animasi, dan layout kustom |
| **Bootstrap 5** | Grid system, navbar responsif, progress bar, utilities |
| **Vue JS 3** | Interpolasi data, rendering dinamis dengan `v-for`, `data()`, dan `.mount()` |
| **Google Fonts** | Font Bebas Neue, DM Sans, Space Mono |

---

## 📁 Struktur File

```
portfolio/
├── index.html       # File utama halaman web
├── style.css        # File styling kustom
├── README.md        # Dokumentasi proyek
└── images/
    ├── dewa.jpeg    # Foto profil
    ├── sertif_1.png # Sertifikat 1
    ├── sertif_2.png # Sertifikat 2
    └── Sertif_3.png # Sertifikat 3
```

---

## 📸 Tampilan Setiap Section / Fitur

### 1. Navbar
Navbar fixed di bagian atas halaman. Berisi logo inisial **RG.**, tautan navigasi ke tiap section (Home, About Me, Certificates), dan tombol **View Work**. Di layar kecil (mobile), navbar akan berubah menjadi burger menu yang bisa di-toggle.

---

### 2. Section Home (Hero Section)
Halaman pertama yang muncul saat website dibuka. Berisi:
- Teks sapaan **"Hello, my name is"**
- Nama lengkap **Reswara Ganendra Rashi Dewa** dalam huruf besar
- Keterangan sebagai mahasiswa Sistem Informasi Universitas Mulawarman Angkatan 2024
- Badge **Web Dev**, **Database**, **UI/UX**
- Foto profil dengan bingkai kuning dan elemen dekoratif geometris
- Teks background besar bertuliskan **"PORTFOLIO"** sebagai efek visual
- Indikator scroll animasi di bagian bawah

---

### 3. Section About Me
Berisi informasi tentang diri, terbagi menjadi dua kolom:

**Kolom Kiri:**
- Judul "Who Am I?"
- Dua paragraf deskripsi diri
- Dua kartu pengalaman organisasi (ROHIS dan INFORSA)

**Kolom Kanan:**
- Judul "Skills"
- 5 progress bar skill: MySQL & Database, HTML & CSS, Computer, Teamwork, Leadership

---

### 4. Section Certificates
Menampilkan 3 kartu sertifikat dalam layout grid. Setiap kartu berisi:
- Foto sertifikat
- Label "Certificate"
- Judul sertifikat
- Deskripsi singkat keterangan sertifikat

---

### 5. Footer
Bagian paling bawah halaman. Berisi logo inisial, nama lengkap, dan teks hak cipta.

---

## 💻 Penjelasan Code Setiap Section / Fitur

### 🔷 Struktur Dasar HTML

```html
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Reswara Ganendra — Portfolio</title>
  <!-- Link Bootstrap 5, Google Fonts, dan style.css -->
</head>
<body>
  <div id="app">
    <!-- Seluruh konten Vue JS berada di dalam div#app -->
  </div>
</body>
</html>
```

Tag `<!DOCTYPE html>` mendeklarasikan dokumen sebagai HTML5. Tag `<meta viewport>` memastikan halaman responsif di perangkat mobile. Seluruh konten dibungkus dalam `<div id="app">` sebagai titik mount Vue JS.

---

### 🔷 Navbar (Bootstrap 5 + Vue JS)

```html
<nav class="navbar navbar-expand-lg custom-navbar fixed-top">
  <div class="container-fluid px-4 px-lg-5">

    <div class="nav-logo">{{ logo }}<span class="accent">.</span></div>

    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navMenu">
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navMenu">
      <ul class="navbar-nav mx-auto gap-lg-4">
        <li class="nav-item" v-for="link in navLinks" :key="link.href">
          <a class="nav-link custom-nav-link" :href="link.href">{{ link.label }}</a>
        </li>
      </ul>
    </div>

  </div>
</nav>
```

**Bootstrap 5:** Class `navbar navbar-expand-lg` membuat navbar yang otomatis collapse menjadi burger menu di layar kecil. Class `fixed-top` membuat navbar selalu terlihat saat scroll. `px-4 px-lg-5` adalah Bootstrap spacing utilities.

**Vue JS:** `{{ logo }}` menampilkan data logo dari `data()`. `v-for="link in navLinks"` melakukan perulangan untuk merender setiap item menu secara dinamis dari array `navLinks` di `data()`. `:href="link.href"` adalah binding atribut dinamis.

---

### 🔷 Section Home / Hero (Bootstrap 5 + Vue JS)

```html
<section id="home" class="hero">
  <div class="container-fluid px-4 px-lg-5">
    <div class="row align-items-center hero-row g-5">

      <!-- Kolom Teks -->
      <div class="col-12 col-lg-7">
        <p class="hero-greeting">Hello, my name is</p>
        <h1 class="hero-name">
          <span v-for="(line, i) in nameParts" :key="i">
            <span :class="{ accent: i === nameParts.length - 1 }">{{ line }}</span><br />
          </span>
        </h1>
        <p class="hero-sub" style="white-space: pre-line;">{{ subtitle }}</p>
        <div class="d-flex flex-wrap gap-2 mt-3">
          <span class="custom-badge" v-for="badge in badges" :key="badge">{{ badge }}</span>
        </div>
      </div>

      <!-- Kolom Foto -->
      <div class="col-12 col-lg-5 d-flex justify-content-center justify-content-lg-end">
        <div class="hero-photo-wrap">
          <div class="photo-frame">
            <img :src="profilePhoto" alt="Foto Reswara Ganendra" class="profile-img" />
          </div>
        </div>
      </div>

    </div>
  </div>
</section>
```

**Bootstrap 5:** `row` dan `col-12 col-lg-7` / `col-12 col-lg-5` membagi layout menjadi dua kolom pada layar besar (≥992px) dan satu kolom penuh di layar kecil. `d-flex`, `flex-wrap`, `gap-2`, `mt-3` adalah utility classes Bootstrap untuk flexbox dan spacing.

**Vue JS:** `v-for="(line, i) in nameParts"` melakukan loop untuk menampilkan nama baris per baris. `:class="{ accent: i === nameParts.length - 1 }"` menambahkan class `accent` (warna kuning) secara kondisional hanya pada baris terakhir nama. `v-for="badge in badges"` merender setiap badge dari array. `:src="profilePhoto"` binding sumber gambar secara dinamis.

---

### 🔷 Section About Me (Bootstrap 5 + Vue JS)

```html
<section id="about" class="about">
  <div class="container-fluid px-4 px-lg-5">
    <div class="row g-5 mt-1">

      <!-- Kiri: Deskripsi + Pengalaman -->
      <div class="col-12 col-lg-6">
        <h2 class="section-title">Who Am <span class="accent">I?</span></h2>
        <p class="about-desc" v-for="(para, i) in aboutParagraphs" :key="i">{{ para }}</p>

        <div class="d-flex flex-column gap-3 mt-4">
          <div class="exp-card d-flex align-items-start gap-3 p-3"
               v-for="exp in experiences" :key="exp.title">
            <div class="exp-icon">{{ exp.icon }}</div>
            <div>
              <div class="exp-title">{{ exp.title }}</div>
              <div class="exp-org">{{ exp.org }}</div>
            </div>
          </div>
        </div>
      </div>

      <!-- Kanan: Skills -->
      <div class="col-12 col-lg-6">
        <h3 class="skills-title">Skills</h3>
        <div class="d-flex flex-column gap-4">
          <div class="skill-item" v-for="skill in skills" :key="skill.name">
            <div class="skill-header d-flex justify-content-between mb-2">
              <span>{{ skill.name }}</span>
              <span class="skill-pct">{{ skill.pct }}%</span>
            </div>
            <!-- Bootstrap Progress Bar -->
            <div class="progress custom-progress" style="height: 6px;">
              <div class="progress-bar custom-progress-bar"
                   role="progressbar"
                   :style="{ width: skill.pct + '%' }"
                   :aria-valuenow="skill.pct"
                   aria-valuemin="0" aria-valuemax="100">
              </div>
            </div>
          </div>
        </div>
      </div>

    </div>
  </div>
</section>
```

**Bootstrap 5:** `col-12 col-lg-6` membagi section menjadi dua kolom seimbang di layar besar. `progress` dan `progress-bar` adalah komponen Bootstrap untuk menampilkan progress bar. `d-flex`, `align-items-start`, `gap-3`, `p-3`, `justify-content-between`, `mb-2` adalah utility spacing dan flexbox dari Bootstrap.

**Vue JS:** `v-for="(para, i) in aboutParagraphs"` merender setiap paragraf deskripsi diri dari array. `v-for="exp in experiences"` merender setiap kartu pengalaman dari array `experiences`. `v-for="skill in skills"` merender setiap baris skill. `:style="{ width: skill.pct + '%' }"` binding lebar progress bar secara dinamis sesuai nilai persentase di `data()`.

---

### 🔷 Section Certificates (Bootstrap 5 + Vue JS)

```html
<section id="certificates" class="certificates">
  <div class="container-fluid px-4 px-lg-5">

    <h2 class="section-title">My <span class="accent">Certificates</span></h2>
    <p class="cert-intro">{{ certIntro }}</p>

    <!-- Bootstrap Grid -->
    <div class="row g-4">
      <div class="col-12 col-md-6 col-lg-4" v-for="cert in certificates" :key="cert.title">
        <div class="cert-card h-100">
          <div class="cert-img-wrap">
            <img :src="cert.img" :alt="cert.title" class="cert-img" />
            <div class="cert-img-placeholder">📜 {{ cert.title }}</div>
          </div>
          <div class="cert-info p-3">
            <span class="cert-tag">Certificate</span>
            <h4 class="cert-title mt-2">{{ cert.title }}</h4>
            <p class="cert-issuer">{{ cert.issuer }}</p>
          </div>
        </div>
      </div>
    </div>

  </div>
</section>
```

**Bootstrap 5:** `col-12 col-md-6 col-lg-4` membuat layout responsif: 1 kolom di mobile, 2 kolom di tablet (≥768px), dan 3 kolom di desktop (≥992px). `g-4` memberikan gap antar kolom. `h-100` memastikan semua kartu memiliki tinggi yang sama dalam satu baris.

**Vue JS:** `v-for="cert in certificates"` melakukan perulangan untuk merender setiap kartu sertifikat dari array `certificates` di `data()`. `:src="cert.img"` dan `:alt="cert.title"` adalah binding dinamis untuk atribut gambar. `{{ cert.title }}` dan `{{ cert.issuer }}` menampilkan teks dari data.

---

### 🔷 Vue JS — Struktur `data()` dan `.mount()`

```javascript
const { createApp } = Vue;

createApp({
  data() {
    return {
      logo:         'RG',
      fullName:     'Reswara Ganendra Rashi Dewa',
      nameParts:    ['Reswara', 'Ganendra', 'Rashi Dewa'],
      subtitle:     'Mahasiswa Sistem Informasi\n...',
      profilePhoto: 'images/dewa.jpeg',

      navLinks: [
        { href: '#home',         label: 'Home'         },
        { href: '#about',        label: 'About Me'     },
        { href: '#certificates', label: 'Certificates' },
      ],

      badges: ['Web Dev', 'Database', 'UI/UX'],

      aboutParagraphs: [ '...paragraf 1...', '...paragraf 2...' ],

      experiences: [
        { icon: '🕌', title: 'Penanggung Jawab', org: 'ROHIS — Rohani Islam' },
        { icon: '💼', title: 'Anggota Dept. Entrepreneurship', org: 'INFORSA' },
      ],

      skills: [
        { name: 'MySQL & Database', pct: 80 },
        { name: 'HTML & CSS',       pct: 75 },
        { name: 'Computer',         pct: 85 },
        { name: 'Teamwork',         pct: 90 },
        { name: 'Leadership',       pct: 70 },
      ],

      certIntro: 'Kumpulan sertifikat...',
      certificates: [
        { img: 'images/sertif_1.png', title: '...', issuer: '...' },
        { img: 'images/sertif_2.png', title: '...', issuer: '...' },
        { img: 'images/Sertif_3.png', title: '...', issuer: '...' },
      ],
    };
  },
}).mount('#app');
```

`createApp({...})` membuat instance aplikasi Vue baru. Fungsi `data()` mengembalikan objek berisi semua data statis yang digunakan di template HTML. `.mount('#app')` menghubungkan Vue ke elemen `<div id="app">` sehingga semua sintaks Vue (`{{ }}`, `v-for`, `:bind`) dapat bekerja di dalam elemen tersebut.

---

### 🔷 CSS Kustom — Variabel & Tema

```css
:root {
  --black:       #0a0a0a;
  --dark:        #111111;
  --yellow:      #f5c518;
  --yellow-dim:  rgba(245, 197, 24, 0.12);
  --yellow-glow: rgba(245, 197, 24, 0.25);
  --white:       #f0ece0;
  --gray:        #888888;

  --font-display: 'Bebas Neue', sans-serif;
  --font-body:    'DM Sans', sans-serif;
  --font-mono:    'Space Mono', monospace;
}
```

CSS Custom Properties (variabel) digunakan agar warna dan font konsisten di seluruh halaman. Tema hitam-kuning diimplementasikan melalui variabel `--black`, `--dark`, dan `--yellow` yang digunakan berulang di semua komponen.

---

## 🎨 Desain & Fitur Tambahan

- **Tema:** Hitam dominan dengan aksen kuning emas
- **Font:** Bebas Neue (judul besar), DM Sans (teks isi), Space Mono (label & kode)
- **Animasi:** Progress bar fill saat halaman dimuat, hover efek kartu sertifikat, animasi garis scroll
- **Responsif:** Tampilan menyesuaikan layar mobile, tablet, dan desktop menggunakan Bootstrap Grid
- **Navbar:** Fixed dengan efek blur glassmorphism, burger menu otomatis di mobile

---

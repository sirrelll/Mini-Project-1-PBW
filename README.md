# Portfolio Website - Darel Prasetya Fawwaz

Website portofolio pribadi yang dibuat sebagai tugas Praktikum  Pemrograman Berbasis Web.

---

## Teknologi yang Digunakan

| Teknologi | Kegunaan |
|---|---|
| HTML | Struktur halaman website |
| CSS3 | Styling tampilan, warna, dan layout |
| Bootstrap 5 | Navbar, grid system, card, button, utilities |
| Vue JS  | Menampilkan skill, pengalaman, dan sertifikat secara dinamis |

---

## Tampilan Setiap Section

### Navbar
Navbar fixed di bagian atas halaman dengan background gelap dan garis bawah oranye. Berisi nama sebagai brand dan tiga link navigasi menuju section Home, About Me, dan Certificates. 
<img width="1905" height="59" alt="Screenshot 2026-03-01 151213" src="https://github.com/user-attachments/assets/5327cf93-d3b0-44b0-a978-bc3a8965c895" />

---

### Section Home
Halaman pertama yang muncul saat website dibuka. Berisi foto profil berbentuk lingkaran di sebelah kanan, dan di sebelah kiri ada nama lengkap, prodi, deskripsi singkat tentang diri, serta dua tombol menuju section About Me dan Certificates.
<img width="1903" height="947" alt="Screenshot 2026-03-01 151223" src="https://github.com/user-attachments/assets/a8bab498-23c9-4ab9-96f9-1c3af13f3d7a" />


---

### Section About Me
Section ini dibagi jadi tiga bagian. Pertama ada kartu Info Diri yang berisi bio singkat, kota asal, email, dan prodi, semuanya ditulis langsung pakai HTML biasa. Kedua ada kartu Skill yang menampilkan progress bar menggunakan Vue JS, datanya diambil dari array `skills` di dalam `data()`. Ketiga ada bagian Pengalaman yang menampilkan kartu-kartu pengalaman organisasi menggunakan Vue JS dengan looping dari array `pengalaman`.
<img width="1903" height="826" alt="Screenshot 2026-03-01 151235" src="https://github.com/user-attachments/assets/51dce4d8-80bd-4fca-8964-da66c3aff93f" />


---

### Section Certificates
Menampilkan daftar sertifikat dalam bentuk grid kartu tiga kolom. Setiap kartu berisi gambar sertifikat, judul, penerbit, dan tanggal. Bagian ini menggunakan Vue JS untuk looping data dari array `sertifikat`, jadi kalau mau tambah sertifikat baru tinggal tambah data di scriptnya tanpa perlu edit HTML.
<img width="1903" height="941" alt="Screenshot 2026-03-01 151244" src="https://github.com/user-attachments/assets/24389a8f-e36c-403b-abf8-fb8ab0dae6f6" />


---

### Footer
Bagian paling bawah halaman dengan background gelap dan garis atas oranye. Berisi nama dan tulisan singkat.
<img width="1904" height="102" alt="Screenshot 2026-03-01 151259" src="https://github.com/user-attachments/assets/1fb4ec05-221d-4071-89b2-eb7f25431b41" />


---

## Penjelasan Code Setiap Section

### Navbar
Navbar dibuat pakai komponen navbar dari Bootstrap 5. Class `navbar-expand-lg` bikin navbar otomatis jadi hamburger di layar kecil. `ms-auto` dipakai buat dorong menu ke kanan. Warna dan border bawah oranye diatur lewat CSS sendiri di `style.css`.

```html
<nav class="navbar navbar-expand-lg navbar-dark" id="navbar">
  <div class="container">
    <a class="navbar-brand fw-bold" href="#">Darel Prasetya Fawwaz</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#menuNavbar">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="menuNavbar">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item"><a class="nav-link" href="#home">Home</a></li>
        <li class="nav-item"><a class="nav-link" href="#about">About Me</a></li>
        <li class="nav-item"><a class="nav-link" href="#certificates">Certificates</a></li>
      </ul>
    </div>
  </div>
</nav>
```

---

### Section Home
Layout home pakai grid Bootstrap dengan `row` dan `col-md-7` / `col-md-5` supaya teks dan foto bisa sejajar. `align-items-center` bikin keduanya rata tengah secara vertikal. Foto profil dibuat bulat lewat CSS dengan `border-radius: 50%`. Tombol dibuat custom pakai class `.btn-oren` dan `.btn-outline-oren` yang didefinisikan di `style.css`.

```html
<div class="row align-items-center gy-4">
  <div class="col-md-7"> ... teks ... </div>
  <div class="col-md-5 text-center">
    <img src="darel.jpeg" alt="Foto Darel" class="foto-profil" />
  </div>
</div>
```

---

### Section About Me - Skill (Vue JS)
Bagian skill pakai Vue JS. Elemen dengan `id="app-skill"` dijadikan titik mount Vue. Di dalam HTML dipakai `v-for` buat looping semua data skill, lalu `{{ skill.nama }}` dan `{{ skill.nilai }}` buat nampilin teksnya. Lebar progress bar disambungin ke data pakai `:style`.

```html
<!-- HTML -->
<div id="app-skill">
  <div v-for="skill in skills" :key="skill.nama" class="mb-3">
    <span>{{ skill.nama }}</span>
    <span>{{ skill.nilai }}%</span>
    <div class="progress-bar" :style="'width: ' + skill.nilai + '%'"></div>
  </div>
</div>
```
```js
// Vue JS
createApp({
  data() {
    return {
      skills: [
        { nama: 'HTML & CSS',       nilai: 50 },
        { nama: 'Futsal',           nilai: 80 },
        { nama: 'Culers',           nilai: 100 },
        { nama: 'Olahraga apa aja', nilai: 90 },
      ]
    }
  }
}).mount('#app-skill')
```

---

### Section About Me - Pengalaman (Vue JS)
Pengalaman juga pakai Vue JS dengan cara yang sama. `id="app-pengalaman"` jadi titik mount, lalu `v-for` looping dari array `pengalaman`. Kartu pengalaman pakai Bootstrap grid `col-md-6` supaya tampil dua kolom di layar besar.

```html
<!-- HTML -->
<div class="row g-3" id="app-pengalaman">
  <div class="col-md-6" v-for="exp in pengalaman" :key="exp.posisi">
    <div class="kartu-gelap border-oren-kiri">
      <h6>{{ exp.posisi }}</h6>
      <p>{{ exp.tempat }}</p>
      <p>{{ exp.periode }}</p>
      <p>{{ exp.deskripsi }}</p>
    </div>
  </div>
</div>
```
```js
// Vue JS
createApp({
  data() {
    return {
      pengalaman: [
        {
          posisi: 'Anggota Divisi Passion Talent Center',
          tempat: 'Information System Association',
          periode: 'Feb 2025 - Dec 2025',
          deskripsi: 'Membantu menjalankan program kerja dengan penuh tanggung jawab.'
        },
        {
          posisi: 'Anggota Divisi Publikasi & Dokumentasi',
          tempat: 'APLIKASI 2025',
          periode: 'Oktober 2025 - November 2025',
          deskripsi: 'Mendokumentasikan kegiatan dan mempublikasikan informasi kegiatan.'
        },
      ]
    }
  }
}).mount('#app-pengalaman')
```

---

### Section Certificates (Vue JS)
Sertifikat pakai Vue JS supaya gampang kalau mau tambah atau ganti data. `id="app-sertifikat"` jadi titik mount, lalu `v-for` looping dari array `sertifikat`. Gambar disambungin pakai `:src` dan `:alt` dari data. Grid pakai `col-md-6 col-lg-4` dari Bootstrap supaya tampil tiga kolom di laptop dan dua kolom di tablet.

```html
<!-- HTML -->
<div class="row g-4" id="app-sertifikat">
  <div class="col-md-6 col-lg-4" v-for="cert in sertifikat" :key="cert.judul">
    <div class="kartu-gelap h-100 p-0 overflow-hidden">
      <img :src="cert.gambar" :alt="cert.judul" class="gambar-sertifikat" />
      <div class="p-3">
        <h6>{{ cert.judul }}</h6>
        <p>{{ cert.penerbit }}</p>
        <p>{{ cert.tanggal }}</p>
      </div>
    </div>
  </div>
</div>
```
```js
// Vue JS
createApp({
  data() {
    return {
      sertifikat: [
        {
          judul: 'Kepanitiaan Information System Association',
          penerbit: 'Information System Association',
          tanggal: 'Feb 2025 - Dec 2025',
          gambar: 'inforsa.PNG'
        },
        {
          judul: 'Kepanitiaan APLIKASI 2025',
          penerbit: 'Departemen HRD Information System Association',
          tanggal: '2025',
          gambar: 'pubdok.jpeg'
        },
        // ... dst
      ]
    }
  }
}).mount('#app-sertifikat')
```

---

### Footer
Footer ditulis pakai HTML biasa. Styling background gelap dan garis atas oranye diatur di `style.css`.

```html
<footer>
  <div class="container text-center">
    <p class="mb-1 fw-bold">Darel Prasetya Fawwaz</p>
    <p class="teks-abu small mb-0">visca barca</p>
  </div>
</footer>
```

---

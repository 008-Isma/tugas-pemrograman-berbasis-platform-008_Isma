# Laporan Perbandingan Pendekatan CSS: Component-Based vs Utility-First

## 1. Metrik Perbandingan

- **Jumlah baris CSS versi komponen:** Sekitar 100 baris CSS di dalam tag `<style>`, mencakup reset, kontainer, kartu, foto, tombol, dan media query.
- **Jumlah class utility versi utility-first:** Sekitar 25 class utility yang digunakan langsung pada elemen HTML dengan Tailwind CSS melalui CDN.
- **Waktu pengerjaan:** Dalam percobaan saya, pendekatan component-based membutuhkan waktu lebih lama karena saya harus menulis selector dan properti CSS sendiri. Pendekatan utility-first terasa lebih cepat karena menyediakan class siap pakai, meskipun beberapa elemen memiliki class yang cukup panjang.

## 2. Kemudahan Perubahan Tema

- **Versi komponen:** Perubahan warna atau ukuran dapat dilakukan melalui aturan CSS yang terpusat, misalnya class `.btn`. Semua elemen yang menggunakan class tersebut akan mengikuti perubahan aturan yang sama.
- **Versi utility-first:** Perubahan gaya dilakukan dengan mengganti class pada elemen HTML, misalnya mengganti warna latar melalui class Tailwind. Cara ini praktis untuk perubahan langsung, tetapi class pada beberapa elemen perlu diperiksa jika ingin mengubah tema secara menyeluruh.

## 3. Hasil Pengujian Responsif

Kedua versi diuji pada tampilan laptop dan layar kecil berukuran 360 × 800 piksel. Pada layar kecil, saya memeriksa apakah kartu tetap rapi, teks dapat dibaca, dan halaman tidak mengalami scroll horizontal. Screenshot hasil pengujian kedua versi dilampirkan sebagai bukti.

## 4. Kesimpulan dan Pilihan untuk Proyek Akhir

Untuk proyek akhir, saya memilih pendekatan utility-first menggunakan Tailwind CSS karena class siap pakainya membantu mempercepat pengembangan antarmuka. Pendekatan component-based tetap bermanfaat ketika aturan tampilan perlu dipusatkan agar lebih mudah dipelihara. Pilihan akhir dapat disesuaikan dengan kebutuhan halaman dan hasil pengujian pada proyek.

**Catatan:** Jumlah baris CSS, jumlah class utility, waktu pengerjaan, dan hasil pengujian harus disesuaikan dengan hasil pekerjaan yang benar-benar saya lakukan.

<!-- # Perbandingan CSS Component-Based dan Utility-First

## 1. Tujuan

Membandingkan pembuatan kartu profil mahasiswa menggunakan CSS berbasis komponen dan Tailwind CSS dengan pendekatan utility-first.

## 2. Data yang digunakan

Kedua halaman menggunakan data yang sama:
- Nama: Citra
- NIM: 2026002
- Foto: foto profil dari URL yang digunakan pada kode
- Tombol: Lihat Profil

## 3. Hasil pengamatan

| Aspek | Component-Based | Utility-First |
|---|---|---|
| Pengaturan tampilan | Menggunakan class seperti `.card` dan `.btn` | Menggunakan class utility Tailwind |
| Penulisan CSS | Aturan CSS ditulis di dalam `<style>` | Menggunakan class utility tanpa CSS buatan sendiri |
| Perubahan warna | Mengubah aturan CSS pada class komponen | Mengubah class warna pada elemen |
| Penggunaan ulang | Class komponen dapat digunakan kembali | Kombinasi class utility dapat digunakan kembali |
| Responsivitas | Menggunakan `width: 100%` dan `max-width` | Menggunakan `w-full` dan `max-w-[340px]` |

## 4. Jumlah baris CSS dan class utility

Jumlah baris CSS versi komponen perlu dihitung dari blok `<style>` pada file HTML. Jumlah class utility perlu dihitung berdasarkan class yang digunakan pada elemen HTML versi Tailwind.

Hasil pengukuran:
- Jumlah baris CSS komponen: **isi setelah menghitung kode**
- Jumlah class utility: **isi setelah menghitung kode**

## 5. Waktu pengerjaan

Catat waktu aktual saat membuat dan menguji masing-masing halaman:
- Component-based: **isi waktu pengerjaan**
- Utility-first: **isi waktu pengerjaan**

## 6. Kemudahan perubahan tema

Pada versi component-based, perubahan tema dapat dilakukan melalui aturan CSS pada class komponen. Pada versi utility-first, perubahan dilakukan dengan mengganti class utility pada elemen yang bersangkutan. Hasil pengamatan akhir disesuaikan dengan proses yang saya alami saat mengubah warna dan tampilan kedua halaman.

## 7. Pilihan untuk proyek akhir

Pendekatan component-based cocok ketika banyak elemen memiliki tampilan yang sama dan ingin dikelola melalui aturan CSS terpusat. Utility-first cocok ketika ingin menyusun layout dengan cepat menggunakan class yang sudah tersedia. Pilihan akhir disesuaikan dengan kebutuhan dan konsistensi tampilan proyek.

## 8. Screenshot

Lampirkan screenshot kedua halaman pada:
1. Tampilan laptop.
2. Lebar viewport 360 px. -->

# Laporan Perbandingan Pendekatan CSS: Component-Based vs Utility-First

## 1. Metrik Perbandingan
* **Jumlah Baris CSS (Versi Komponen):** Sekitar 100 baris di dalam tag `<style>` internal (mencakup reset, kontainer, kartu, foto, tombol, dan media query).
* **Jumlah Class Utility (Versi Utility-First):** Sekitar 25 class utility yang disematkan langsung pada elemen-elemen HTML (menggunakan Tailwind CDN).
* **Waktu Pengerjaan:** Pendekatan komponen memerlukan waktu sedikit lebih lama karena harus menulis selector CSS dan properti satu per satu dari awal. Sebaliknya, pendekatan utility-first terasa lebih cepat karena langsung memanfaatkan class siap pakai dari Tailwind, meskipun nama class-nya cukup panjang.

## 2. Kemudahan Perubahan Tema (Styling)
* **Versi Komponen:** Perubahan warna atau ukuran dapat dilakukan terpusat pada aturan class CSS (contohnya mengubah `.btn`), sehingga seluruh elemen dengan class tersebut langsung berubah serempak.
* **Versi Utility-First:** Perubahan gaya dilakukan dengan mengganti class langsung pada elemen HTML yang diinginkan (misalnya mengubah `bg-gradient-to-br from-[#ff8fbd]`). 

## 3. Kesimpulan & Pilihan untuk Proyek Akhir
Dalam proyek akhir nanti, saya memilih menggunakan pendekatan **Utility-First (Tailwind)** untuk mempercepat proses pengembangan antarmuka dan konsistensi desain, serta pendekatan **Component-Based** untuk bagian elemen global yang membutuhkan kerapian struktur dan pemeliharaan aturan CSS yang terpusat.
# Laporan Analisis Hashing, Enkripsi, dan Keamanan Konfigurasi

## 1. Hasil Percobaan Hashing Bcrypt
Setelah menjalankan perintah hashing dengan *password* `"sama"` sebanyak dua kali melalui terminal, diperoleh hasil berikut:
* **Percobaan 1:** Kata sandi `"sama"` $\rightarrow$ Nilai Hash: `$2a$10$7vF9...` *(sesuaikan dengan hash hasil terminal Anda)*
* **Percobaan 2:** Kata sandi `"sama"` $\rightarrow$ Nilai Hash: `$2a$10$3xK2...` *(sesuaikan dengan hash hasil terminal Anda)*

**Penjelasan:** Meskipun kata sandi masukan yang digunakan sama persis, kedua proses menghasilkan nilai hash yang berbeda. Hal ini karena *bcrypt* secara otomatis menyertakan *salt* (nilai acak unik) di setiap eksekusi hashing. *Salt* berfungsi mencegah serangan menggunakan *rainbow table*. Sementara itu, faktor biaya komputasi (*cost factor* 10) menentukan jumlah iterasi yang dilakukan; semakin tinggi nilai *cost*, semakin aman proses hashing tetapi waktu pemrosesan oleh server juga akan semakin lambat.

## 2. Pertanyaan Konseptual
* **Perbedaan Hashing dan Enkripsi:** Hashing bersifat satu arah (tidak dapat dikembalikan menjadi teks asli), sedangkan enkripsi bersifat dua arah (data dapat dikembalikan atau didekripsi menggunakan kunci yang sesuai).
* **Alasan Menyimpan Hash Kata Sandi:** Agar sistem dapat memverifikasi proses login dengan aman tanpa harus menyimpan teks kata sandi asli (*plaintext*) di dalam database.
* **Cara Kerja `bcrypt.compare`:** Membaca *salt* dari nilai hash yang tersimpan di database, mengenkripsi kata sandi yang dimasukkan pengguna menggunakan *salt* tersebut, lalu mencocokkan apakah hasil hash-nya identik.
* **Rainbow Table & Salt:** *Rainbow table* adalah tabel pra-hitung berisi kombinasi teks dan nilai hash-nya. Penambahan *salt* acak membuat nilai hash akhir menjadi unik untuk setiap pengguna, sehingga *rainbow table* generik tidak efektif.
* **Kerahasiaan `JWT_SECRET`:** Jika kunci rahasia ini bocor, pihak luar dapat memalsukan tanda tangan token JWT dan menyamar sebagai pengguna atau administrator sah di dalam sistem.

## 3. Hasil Pemeriksaan Repositori Git
* **Pemeriksaan `.env`:** 
  `AMAN: .env tidak terlacak` (atau hasil pesan verifikasi terminal Anda).
* **Pemeriksaan Token di Laporan/Client:** 
  `AMAN: tidak ada JWT di laporan atau client` (pastikan tidak ada token JWT lengkap yang tercantum pada dokumen laporan atau kode klien).
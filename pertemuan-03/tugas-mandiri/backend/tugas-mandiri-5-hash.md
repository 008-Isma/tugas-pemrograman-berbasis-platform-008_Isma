# Tugas Mandiri 5 — Membandingkan Hashing dan Enkripsi serta Menjaga Kunci Rahasia

**Nama:** Ismawati  
**NIM:** 2024520008  
**Program Studi:** Informatika  
**Mata Kuliah:** Pemrograman Berbasis Platform

## 1. Percobaan Hashing dengan bcrypt

Percobaan dilakukan menggunakan library `bcryptjs` dengan kata sandi `sama` dan cost factor `10`.

Perintah yang digunakan:

```bash
node -e "console.log(require('bcryptjs').hashSync('sama', 10))"
```

### Hasil percobaan

**Percobaan pertama:**

```text
$2b$10$rYGtaBhYx2ZhkS5Gj/4dV.hkOCTv4UOzEd71oCxNUY41L1AJZsOSi
```

**Percobaan kedua:**

```text
$2b$10$KQJBLmbaLV3KKwiW4OA.CeVcsSH33E8CQ2dEqkVtSzzGrCxkaVZt6
```

### Analisis hasil

Kedua percobaan menggunakan kata sandi yang sama, yaitu `sama`, tetapi menghasilkan nilai hash berbeda. Hal ini terjadi karena bcrypt menggunakan salt yang berbeda pada setiap proses hashing. Salt membuat penggunaan tabel hash yang telah disiapkan sebelumnya menjadi kurang efektif.

Cost factor `10` menentukan tingkat beban komputasi yang digunakan bcrypt. Semakin tinggi cost factor, semakin banyak komputasi yang diperlukan sehingga proses hashing biasanya membutuhkan waktu lebih lama.

## 2. Perbedaan Hashing dan Enkripsi

Hashing merupakan proses satu arah yang mengubah data menjadi nilai hash sehingga data asli tidak dapat langsung dikembalikan dari nilai hash tersebut. Enkripsi mengubah data menjadi bentuk yang tidak mudah dibaca dan memungkinkan data asli dipulihkan melalui proses dekripsi dengan kunci yang sesuai.

## 3. Alasan Password Disimpan dalam Bentuk Hash

Password sebaiknya disimpan dalam bentuk hash agar kata sandi asli tidak langsung terbaca apabila database bocor. Algoritma khusus password seperti bcrypt membantu mengurangi risiko penyalahgunaan password.

## 4. Cara Kerja bcrypt.compare()

Fungsi `bcrypt.compare()` digunakan untuk membandingkan password yang dimasukkan pengguna dengan hash password yang tersimpan. Fungsi ini menggunakan informasi salt dan parameter yang terdapat pada hash untuk memeriksa kecocokan password, sehingga aplikasi tidak perlu menyimpan password asli dalam bentuk teks biasa.

## 5. Rainbow Table dan Fungsi Salt

Rainbow table adalah kumpulan data perhitungan hash yang dapat membantu penyerang menebak data asli dari nilai hash. Salt membuat password yang sama menghasilkan hash berbeda sehingga penggunaan tabel hash yang telah dibuat sebelumnya menjadi kurang efektif.

## 6. Menjaga Kerahasiaan JWT_SECRET

`JWT_SECRET` harus dirahasiakan karena digunakan untuk menandatangani dan memverifikasi token JWT. Jika kunci tersebut bocor, pihak lain dapat mencoba membuat token dengan tanda tangan yang valid. Karena itu, secret sebaiknya disimpan dalam file `.env` yang tidak dilacak Git atau menggunakan pengelolaan secret yang sesuai, bukan ditulis langsung dalam kode maupun laporan.

Agar secret tidak tersimpan dalam riwayat Git, file `.env` perlu dimasukkan ke `.gitignore` sebelum ditambahkan ke repository. Jika secret sudah pernah di-commit atau terungkap, secret tersebut perlu diganti dan riwayat Git ditangani sesuai kebutuhan.

## 7. Pemeriksaan Keamanan Repository

### 7.1 Pemeriksaan file `.env`

Perintah pemeriksaan:

```bash
git ls-files --error-unmatch backend/.env
```

**Hasil:**

```text
error: pathspec 'backend/.env' did not match any file(s) known to git
```

Hasil tersebut menunjukkan bahwa `backend/.env` tidak tercatat sebagai file yang dilacak Git. Pemeriksaan ini terbatas pada jalur tersebut dan tidak memastikan apakah file `.env` ada di lokasi lain.

### 7.2 Pemeriksaan token JWT

Perintah pemeriksaan:

```bash
git grep -nE 'eyJ[A-Za-z0-9_-]+\.[A-Za-z0-9_-]+\.[A-Za-z0-9_-]+'
```

**Hasil:** Tidak ada output yang ditemukan.

Hasil tersebut menunjukkan bahwa pencarian pola token JWT tidak menemukan kecocokan pada file yang dilacak Git. Pemeriksaan ini bukan jaminan bahwa semua bentuk token atau secret telah ditemukan.

## 8. Kesimpulan

Percobaan menunjukkan bahwa bcrypt menghasilkan hash berbeda untuk password yang sama karena penggunaan salt. Hashing berbeda dari enkripsi karena hashing dirancang sebagai proses satu arah, sedangkan enkripsi memungkinkan pemulihan data melalui dekripsi. Password perlu disimpan dalam bentuk hash, sementara `JWT_SECRET` harus dijaga kerahasiaannya. Pemeriksaan Git tidak menemukan file `backend/.env` terlacak maupun kecocokan pola JWT pada file yang dilacak.
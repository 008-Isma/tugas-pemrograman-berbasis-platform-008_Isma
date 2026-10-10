# Laporan Analisis Authentication dan Authorization SIPERPUS

## 1. Matriks Hak Akses Peran Pengguna

SIPERPUS (Sistem Informasi Perpustakaan) memiliki tiga peran pengguna, yaitu Anggota, Pustakawan, dan Pimpinan. Setiap peran memiliki hak akses yang berbeda sesuai dengan tugas dan tanggung jawabnya.

| Fitur | Anggota | Pustakawan | Pimpinan | Endpoint |
| :--- | :---: | :---: | :---: | :--- |
| Melihat katalog buku | ✅ | ✅ | ✅ | `GET /buku` |
| Melihat kategori buku | ✅ | ✅ | ✅ | `GET /kategori` |
| Menambah data buku | ❌ | ✅ | ❌ | `POST /buku` |
| Mengubah data buku | ❌ | ✅ | ❌ | `PUT /buku/:id` |
| Menghapus data buku | ❌ | ✅ | ❌ | `DELETE /buku/:id` |
| Menambah kategori buku | ❌ | ✅ | ❌ | `POST /kategori` |
| Mengelola data rak buku | ❌ | ✅ | ❌ | `POST /rak` |
| Melihat rekapitulasi stok buku | ❌ | ✅ | ✅ | `GET /laporan/stok` |

Tanda ✅ berarti peran tersebut diizinkan mengakses fitur, sedangkan tanda ❌ berarti akses ditolak dengan kode HTTP `403` apabila identitas pengguna sudah terverifikasi. Endpoint pada tabel merupakan rancangan hak akses untuk analisis SIPERPUS.

## 2. Analisis Kode Status HTTP 401 dan 403

Kode HTTP `401 Unauthorized` digunakan ketika pengguna mengakses endpoint yang dilindungi tanpa menyertakan token autentikasi atau menggunakan token yang tidak valid. Contohnya, permintaan untuk `POST /buku` tanpa token akan ditolak karena sistem belum dapat memverifikasi identitas pengguna melalui middleware `requireAuth`.

Kode HTTP `403 Forbidden` digunakan ketika pengguna memiliki token valid, tetapi tidak mempunyai hak akses terhadap fitur yang diminta. Contohnya, anggota yang sudah login mencoba mengakses `POST /buku` untuk menambah katalog, padahal fitur tersebut hanya diizinkan bagi pustakawan. Dalam keadaan ini, identitas anggota sudah diketahui, tetapi permintaannya tetap ditolak oleh pemeriksaan peran melalui `requireRole`.

## 3. Risiko Jika Endpoint Tidak Memeriksa Peran

Jika endpoint penambahan katalog hanya menggunakan `requireAuth` tanpa `requireRole`, sistem hanya memeriksa apakah pengguna sudah terautentikasi. Akibatnya, anggota yang sudah login berpotensi menambah atau mengubah data buku meskipun tidak memiliki izin tersebut. Oleh karena itu, endpoint yang dibatasi berdasarkan peran harus memeriksa identitas pengguna dan hak aksesnya.

## 4. Contoh Skenario Pemeriksaan Akses

| Keadaan | Pemeriksaan | Hasil yang Diharapkan |
| :--- | :--- | :--- |
| Anggota mengakses `POST /buku` tanpa token | Identitas belum terverifikasi | `401 Unauthorized` |
| Pustakawan menggunakan token valid untuk `POST /buku` | Identitas dan hak akses sesuai | Permintaan diizinkan |
| Anggota menggunakan token valid untuk `POST /buku` | Identitas valid, tetapi tidak memiliki izin | `403 Forbidden` |

## Kesimpulan

Autentikasi digunakan untuk memastikan identitas pengguna, sedangkan otorisasi digunakan untuk menentukan fitur yang boleh diakses oleh pengguna tersebut. SIPERPUS memerlukan kedua pemeriksaan tersebut agar pengelolaan buku, kategori, dan rak hanya dapat dilakukan oleh peran yang memiliki izin sesuai ketentuan.

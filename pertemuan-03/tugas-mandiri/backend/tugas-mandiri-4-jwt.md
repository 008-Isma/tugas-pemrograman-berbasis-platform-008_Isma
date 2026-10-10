# Laporan Analisis Struktur dan Validitas JSON Web Token (JWT)

## 1. Analisis Klaim Payload JWT
Berdasarkan hasil pengamatan token praktikum pada jwt.io, klaim-klaim utama yang menyusun payload token meliputi:
* **Klaim Pengguna (`sub` / `nim`):** Mengidentifikasi data unik atau nomor induk mahasiswa yang sedang aktif dan terautentikasi di dalam sistem.
* **Klaim Peran (`role`):** Digunakan oleh server untuk menentukan hak akses (*authorization*) terhadap endpoint tertentu yang dibatasi.
* **Waktu Terbit (`iat`) & Kedaluwarsa (`exp`):** Klaim `iat` (*Issued At*) mencatat waktu token diterbitkan, sedangkan `exp` (*Expiration Time*) menetapkan batas waktu kedaluwarsa sah token. Selisih waktu kedua klaim ini menentukan durasi masa aktif sesi pengguna.

## 2. Analisis Kegagalan Tanda Tangan (Signature Verification)
Ketika satu karakter pada bagian payload diubah tanpa memperbarui tanda tangan kriptografis pada bagian *signature*, integritas token menjadi rusak. Saat token yang telah dimodifikasi tersebut digunakan untuk mengakses endpoint terlindungi seperti `GET /auth/me`, server akan menolak permintaan karena kunci validasi tanda tangan tidak lagi cocok dengan isi token.

## 3. Tabel Hasil Pengujian Respons Server
| Token yang Diuji | Endpoint | Hasil yang Diharapkan | Hasil Pengujian Anda |
| :--- | :--- | :---: | :--- |
| Token asli yang masih berlaku | `GET /auth/me` | 200 | 200 OK (Mengembalikan data profil pengguna) |
| Token payload diubah (tanpa update signature) | `GET /auth/me` | 401 | 401 Unauthorized (Ditolak oleh server) |
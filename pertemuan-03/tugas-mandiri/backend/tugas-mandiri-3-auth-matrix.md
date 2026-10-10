# Laporan Analisis Autentikasi dan Otorisasi

## 1. Matriks Hak Akses Peran Pengguna
Berikut adalah matriks hak akses yang menghubungkan fitur aplikasi, peran pengguna, dan endpoint backend:

| Fitur | Mahasiswa | Dosen / Pengelola | Administrator | Endpoint |
| :--- | :---: | :---: | :---: | :--- |
| Mengajukan/Melihat KRS & Nilai | ✅ | ❌ | ❌ | `GET/POST /akademik/krs` |
| Mengunggah Materi & Tugas Kuliah | ❌ | ✅ | ✅ | `POST /perkuliahan/materi` |
| Memvalidasi Pengajuan Mahasiswa | ❌ | ✅ | ✅ | `PUT /akademik/validasi` |
| Mengubah Profil Mandiri | ✅ | ✅ | ✅ | `PUT /auth/profile` |
| Mengelola Data Pengguna Sistem | ❌ | ❌ | ✅ | `DELETE /admin/users/{id}` |
| Melihat Rekapitulasi Akademik | ❌ | ✅ | ✅ | `GET /admin/rekap` |

## 2. Analisis Penggunaan Kode Status HTTP (401 vs 403)
* **Kode 401 (Unauthorized):** Dikembalikan oleh server ketika permintaan tidak menyertakan token autentikasi sama sekali atau token yang dikirimkan sudah tidak valid/kedaluwarsa. Hal ini menandakan bahwa sistem belum dapat mengenali identitas pengguna (`requireAuth` gagal).
* **Kode 403 (Forbidden):** Dikembalikan ketika token valid dan identitas pengguna berhasil dikenali, namun akun tersebut tidak memiliki hak akses (*role*) yang sesuai untuk mengeksekusi endpoint tertentu (misalnya seorang "Mahasiswa" mencoba mengakses endpoint manajemen pengguna admin).

## 3. Risiko Tanpa Pemeriksaan Peran (Role)
Jika endpoint manajemen atau penambahan data hanya diperiksa melalui fungsi autentikasi identitas (`requireAuth`) tanpa disertai pemeriksaan peran (`requireRole`), maka setiap pengguna yang berhasil login (termasuk mahasiswa biasa) dapat mengakses, mengubah, atau merusak data sistem secara ilegal karena hak aksesnya tidak dibatasi.
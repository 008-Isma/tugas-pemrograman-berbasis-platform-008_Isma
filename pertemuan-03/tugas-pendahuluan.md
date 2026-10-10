Tugas Pendahuluan Pertemuan 03
CSS Framework dan Authentication
Nama: Ismawati
NIM: 202452008
Soal 1 — Bandingkan Bootstrap dan Tailwind
Bootstrap menggunakan class komponen seperti card, card-body, card-title, btn, dan btn-primary untuk membuat kartu dan tombol. Sementara itu, Tailwind CSS menggunakan class utility seperti rounded-xl, shadow-md, p-6, bg-blue-600, dan text-white untuk mengatur tampilan secara langsung.
Menurut saya, Bootstrap lebih mudah digunakan oleh pemula karena sudah menyediakan komponen siap pakai sehingga kita tidak perlu menulis banyak class untuk membuat tampilan dasar.
Soal 2 — Rancang Satu Kartu Biodata dengan Dua Pendekatan
Sketsa kartu biodata:
+-----------------------------+
|         [Foto]              |
|                             |
|         Ismawati            |
|         NIM: 202452008      |
|                             |
|        [ Lihat Profil ]     |
+-----------------------------+
A. Versi komponen (Bootstrap)
<div class="card" style="width: 18rem;">
  <img src="foto.jpg" class="card-img-top" alt="Foto">
  <div class="card-body">
    <h5 class="card-title">Ismawati</h5>
    <p class="card-text">NIM: 202452008</p>
    <a href="#" class="btn btn-primary">Lihat Profil</a>
  </div>
</div>
Class Bootstrap sudah memiliki aturan tampilan bawaan. Jika ingin membuat kartu dengan CSS sendiri, saya dapat menambahkan 5 aturan CSS, yaitu untuk kartu, foto, judul, teks biodata, dan tombol.
B. Versi utility (Tailwind CSS)
<div class="max-w-sm overflow-hidden rounded-xl bg-white shadow-md">
  <img src="foto.jpg"
       class="h-48 w-full object-cover"
       alt="Foto">
  <div class="p-6">
    <h2 class="text-xl font-bold text-gray-800">
      Ismawati
    </h2>
    <p class="mt-2 text-gray-600">
      NIM: 202452008
    </p>
    <button class="mt-4 rounded-lg bg-blue-600 px-4 py-2
                   font-semibold text-white hover:bg-blue-700">
      Lihat Profil
    </button>
  </div>
</div>
Pada contoh Tailwind tersebut terdapat 22 class utility, dihitung berdasarkan setiap nama class yang dipisahkan oleh spasi, termasuk class pada elemen gambar, teks, dan tombol.
Menurut saya, Tailwind lebih mudah diubah warnanya secara langsung karena cukup mengganti class warna, misalnya dari bg-blue-600 menjadi bg-green-600, tanpa perlu mengubah aturan CSS terpisah.
Soal 3 — Amati Isi Token
JWT yang diberikan terdiri dari 3 bagian yang dipisahkan oleh tanda titik (.), yaitu header, payload, dan signature. Pada payload terdapat tiga nama data, yaitu sub, name, dan iat.
Password tidak boleh disimpan di dalam payload JWT karena isi token dapat dibaca oleh pihak yang memperoleh token tersebut. Payload bukan data rahasia yang otomatis dienkripsi, sehingga password berisiko diketahui orang lain.
Soal 4 — Analogi Gerbang Kampus
Authentication dapat diibaratkan sebagai pemeriksaan identitas di gerbang UNIRA untuk memastikan bahwa orang yang masuk benar-benar mahasiswa, dosen, atau petugas yang terdaftar. Authorization adalah pemeriksaan izin di depan ruang server laboratorium untuk memastikan bahwa orang tersebut memiliki hak akses ke ruangan itu.
Contohnya, seorang mahasiswa berhasil menunjukkan kartu identitas yang valid, tetapi tetap tidak diperbolehkan masuk ke ruang server karena hanya teknisi laboratorium yang memiliki izin akses.





Soal 5 — Peran di Aplikasi Nyata
Saya memilih GitHub sebagai contoh aplikasi yang memiliki beberapa peran pengguna, yaitu:
Peran	Hak akses
Pengunjung	Melihat repository publik
Collaborator	Mengakses dan berkontribusi pada repository sesuai izin yang diberikan
Administrator repository	Mengelola pengaturan repository dan aturan akses
Fitur mengubah pengaturan repository hanya boleh digunakan oleh pengguna yang memiliki izin administratif.
Dua kondisi respons yang tepat adalah:
1.	HTTP 401 Unauthorized: diberikan ketika pengguna belum login atau belum memberikan kredensial autentikasi yang valid, karena identitasnya belum berhasil diverifikasi.
2.	HTTP 403 Forbidden: diberikan ketika pengguna sudah login tetapi tidak memiliki izin untuk mengakses fitur tertentu, karena identitasnya sudah diketahui tetapi hak aksesnya tidak mencukupi.



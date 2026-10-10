# Laporan Tata Letak Responsif dengan Class Utility

## 1. Struktur Halaman

Halaman dibuat menggunakan HTML dan Tailwind CSS melalui CDN. Halaman terdiri dari navbar, hero sebagai bagian pembuka, tiga kartu konten, dan footer.

## 2. Class Utility yang Digunakan

| Bagian | Class utama | Fungsi |
| :--- | :--- | :--- |
| Body | `min-h-screen flex flex-col` | Membuat halaman memenuhi tinggi layar dan menyusun bagian secara vertikal. |
| Navbar | `sticky top-0 z-50` | Menjaga navbar tetap berada di bagian atas saat halaman digulir. |
| Kontainer | `max-w-5xl mx-auto px-6` | Membatasi lebar konten, memusatkannya, dan memberi jarak horizontal. |
| Hero | `bg-gradient-to-r rounded-[24px] p-8` | Memberi latar gradasi, sudut membulat, dan ruang dalam. |
| Judul hero | `text-2xl md:text-3xl` | Mengubah ukuran judul pada layar yang lebih lebar. |
| Kumpulan kartu | `grid grid-cols-1 gap-6 md:grid-cols-3` | Menyusun kartu satu kolom pada layar kecil dan tiga kolom pada layar lebih lebar. |
| Kartu | `bg-white/90 border-2 p-6 rounded-[20px]` | Memberi latar, garis tepi, jarak dalam, dan sudut membulat. |
| Efek kartu | `hover:shadow-lg hover:-translate-y-1 transition` | Memberi efek bayangan dan sedikit gerakan saat kursor diarahkan ke kartu. |
| Footer | `mt-auto py-4 text-center` | Mendorong footer ke bagian bawah dan meratakan teks ke tengah. |

## 3. Pengujian Responsif

Halaman perlu diuji pada tampilan laptop dan viewport berukuran 360 × 800 piksel. Pada layar kecil, saya memeriksa susunan navbar, hero, tiga kartu, dan footer serta memastikan tidak ada scroll horizontal. Hasil pengujian dicatat berdasarkan tampilan halaman yang benar-benar saya amati.

## 4. Kesimpulan

Class utility Tailwind CSS membantu menyusun tampilan dengan cepat tanpa harus menulis banyak aturan CSS secara terpisah. Penggunaan grid responsif dan prefiks `md:` memungkinkan tiga kartu ditampilkan satu kolom pada layar kecil dan tiga kolom pada layar yang lebih lebar.

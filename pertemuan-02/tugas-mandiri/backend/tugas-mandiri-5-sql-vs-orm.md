# Tugas Mandiri 5 — Membandingkan SQL Mentah dan ORM

## 1. Tujuan

Tugas ini bertujuan untuk memahami perbedaan, kelebihan, serta kekurangan antara penggunaan **SQL Mentah (Raw SQL)** dan **ORM (Object-Relational Mapping)** dalam mengelola serta mengakses database pada aplikasi backend. Selain itu, tugas ini juga membahas aspek keamanan seperti risiko **SQL Injection** dan bagaimana parameter query serta ORM membantu mencegah celah keamanan tersebut.

---

## 2. Studi Kasus Operasi Database

Operasi database yang dipilih adalah **Mengambil satu data berdasarkan ID** pada tabel `jadwal`.

### Skema Tabel `jadwal`

| Column | Type | Constraints |
| :--- | :--- | :--- |
| `id` | INT / Serial | Primary Key, Auto Increment |
| `matakuliah` | VARCHAR(250) | Not Null |
| `hari` | VARCHAR(50) | Not Null |
| `jam` | VARCHAR(50) | Not Null |
| `ruangan` | VARCHAR(50) | Not Null |

---

## 3. Implementasi Operasi Database

### A. Pendekatan SQL Mentah (Raw SQL)

Menggunakan SQL secara langsung melalui driver library seperti `mysql2` atau `pg` di Node.js dengan teknik *Parameterized Query*.

```javascript
const mysql = require('mysql2/promise');

async function getJadwalById(id) {
  const connection = await mysql.createConnection({
    host: 'localhost',
    user: 'root',
    database: 'db_perkuliah'
  });

  // Query SQL Mentah dengan Parameter Prepared Statement (?)
  const query = 'SELECT * FROM jadwal WHERE id = ?';
  const [rows] = await connection.execute(query, [id]);

  await connection.end();
  return rows[0];
}

B. Pendekatan ORM (Object-Relational Mapping)
Menggunakan ORM seperti Prisma atau Drizzle ORM untuk mengakses data menggunakan sintaks berbasis objek JavaScript/TypeScript.
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();

async function getJadwalById(id: number) {
  // Operasi mengambil data berdasarkan ID menggunakan Prisma ORM
  const jadwal = await prisma.jadwal.findUnique({
    where: {
      id: id
    }
  });

  return jadwal;
}

## 4. Perbandingan SQL Mentah dan ORM

| Aspek | SQL Mentah (Raw SQL) | ORM (Object-Relational Mapping) |
| :--- | :--- | :--- |
| **Sintaks** | Ditulis dalam string SQL murni (`SELECT...`) | Ditulis menggunakan method/fungsi bahasa pemrograman (`prisma.jadwal.findUnique`) |
| **Kurva Pembelajaran** | Harus menguasai sintaks SQL dan skema database | Harus mempelajari API dan konsep ORM yang digunakan |
| **Type Safety** | Tidak ada *type checking* bawaan (kecuali dibuat manual) | *Auto-completion* dan *Type-safe* yang kuat (terutama pada TypeScript) |
| **Performa** | Sangat cepat karena langsung dieksekusi oleh database engine | Ada sedikit *overhead* abstraksi sebelum dikonversi menjadi SQL |
| **Portabilitas DB** | Terikat pada dialek database tertentu (MySQL, PostgreSQL, dsb.) | Mudah berpindah database hanya dengan mengubah konfigurasi driver |

---

## 5. Pembahasan dan Analisis

### 1. Apa perbedaan SQL mentah dan ORM?
SQL mentah adalah perintah kueri basis data yang ditulis secara langsung dalam bahasa SQL murni dan dieksekusi oleh *database engine*. Sementara itu, ORM adalah teknik/pustaka abstraksi yang mengonversi data dari tabel relational ke dalam bentuk objek pada bahasa pemrograman (misalnya JavaScript/TypeScript), sehingga programmer dapat mengelola database tanpa harus menulis kueri SQL secara manual.

### 2. Apa kelebihan SQL mentah?
- **Performa Lebih Optimal:** Tidak membutuhkan abstraksi tambahan sehingga eksekusi kueri lebih cepat.
- **Fleksibilitas Tinggi:** Bebas menulis kueri yang sangat kompleks seperti gabungan *multi-join*, subquery rumit, atau optimasi kueri khusus (*indexing*).
- **Kontrol Penuh:** Memiliki kendali penuh atas kueri persis apa yang dikirimkan ke database engine.

### 3. Apa kelebihan ORM?
- **Produktivitas Tinggi:** Mempercepat proses pengembangan aplikasi karena sintaks lebih sederhana dan konsisten.
- **Type Safety & Auto-completion:** Mencegah kesalahan ketik (*typo*) pada nama kolom atau tabel saat menggunakan TypeScript.
- **Pengelolaan Skema & Migrasi:** Menyediakan fitur *migration tool* bawaan untuk mengelola perubahan skema database secara terstruktur.
- **Abstraksi Database:** Memudahkan migrasi dari satu jenis basis data ke basis data lain (misalnya dari MySQL ke PostgreSQL) tanpa perlu merombak sintaks kueri secara keseluruhan.

### 4. Apa risiko SQL Injection?
SQL Injection adalah celah keamanan (*vulnerability*) yang terjadi ketika masukan dari pengguna (*user input*) dimasukkan secara langsung ke dalam string kueri SQL tanpa proses validasi atau sanitasi. Hal ini memungkinkan penyerang menyisipkan perintah SQL berbahaya untuk membaca, mengubah, menghapus data sensitif, bahkan mengambil alih kontrol hak akses database.

### 5. Mengapa penggunaan parameter query dapat mengurangi risiko SQL Injection?
Parameter query (*Prepared Statements*) memisahkan antara struktur logika perintah SQL dengan data masukan (*input*). Saat kueri dijalankan, database engine memperlakukan nilai masukan murni sebagai data biasa, bukan sebagai bagian dari sintaks/instruksi yang dieksekusi. Oleh karena itu, karakter berbahaya seperti `' OR '1'='1` tidak akan dianggap sebagai perintah logika tambahan oleh database.

### 6. Bagaimana ORM membantu programmer dalam mengakses database?
- **Menghilangkan Boilerplate Code:** Mengurangi kebutuhan menulis kueri string SQL secara repetitif untuk operasi CRUD dasar.
- **Keamanan Bawaan:** Sebagian besar ORM secara otomatis menggunakan *parameterized queries* saat menangani parameter masukan, sehingga meminimalisir risiko SQL Injection secara mendasar.
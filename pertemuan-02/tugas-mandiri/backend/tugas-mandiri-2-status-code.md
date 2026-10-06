# Tugas Mandiri 2 — Memahami HTTP Status Code

## 1. Tujuan

Tugas ini bertujuan untuk memahami arti dan fungsi HTTP status code yang diberikan oleh server. Pengujian dilakukan menggunakan **Postman** dengan layanan publik **HTTPBin**.

Endpoint yang digunakan:

```text
https://httpbin.org/status/:code
```

Pada pengujian ini dilakukan pengujian terhadap status code:

* 200
* 201
* 400
* 401
* 403
* 404
* 500

Setiap request menggunakan method `GET` dan tidak menggunakan request body maupun query parameter.

---

## 2. Hasil Pengujian

| Status Code | Arti                  | Hasil Pengujian                                         | Kapan Digunakan                                                                              |
| ----------: | --------------------- | ------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
|         200 | OK                    | Server mengembalikan status `200 OK`                    | Digunakan ketika request berhasil diproses.                                                  |
|         201 | Created               | Server mengembalikan status `201 Created`               | Digunakan ketika request berhasil membuat resource/data baru.                                |
|         400 | Bad Request           | Server mengembalikan status `400 Bad Request`           | Digunakan ketika request yang dikirim tidak valid atau memiliki format yang salah.           |
|         401 | Unauthorized          | Server mengembalikan status `401 Unauthorized`          | Digunakan ketika request membutuhkan autentikasi atau kredensial yang valid tidak diberikan. |
|         403 | Forbidden             | Server mengembalikan status `403 Forbidden`             | Digunakan ketika server memahami request tetapi menolak akses karena tidak memiliki izin.    |
|         404 | Not Found             | Server mengembalikan status `404 Not Found`             | Digunakan ketika resource yang diminta tidak ditemukan.                                      |
|         500 | Internal Server Error | Server mengembalikan status `500 Internal Server Error` | Digunakan ketika terjadi kesalahan pada sisi server saat memproses request.                  |

---

## 3. Detail Pengujian

### 3.1 Status Code 200 — OK

**Request:**

```text
GET https://httpbin.org/status/200
```

**Hasil:**

```text
200 OK
```

Request berhasil diproses oleh server. Status `200` merupakan status umum yang digunakan ketika request berhasil.

---

### 3.2 Status Code 201 — Created

**Request:**

```text
GET https://httpbin.org/status/201
```

**Hasil:**

```text
201 Created
```

Status `201` menunjukkan bahwa sebuah resource berhasil dibuat. Dalam aplikasi API, status ini umumnya digunakan setelah proses pembuatan data baru berhasil dilakukan.

---

### 3.3 Status Code 400 — Bad Request

**Request:**

```text
GET https://httpbin.org/status/400
```

**Hasil:**

```text
400 Bad Request
```

Status `400` menunjukkan bahwa request yang diterima server tidak valid. Kesalahan dapat terjadi karena format request salah atau data yang dikirim tidak memenuhi aturan yang ditentukan oleh server.

---

### 3.4 Status Code 401 — Unauthorized

**Request:**

```text
GET https://httpbin.org/status/401
```

**Hasil:**

```text
401 Unauthorized
```

Status `401` digunakan ketika request membutuhkan autentikasi, tetapi kredensial yang diperlukan tidak tersedia atau tidak valid.

Contohnya adalah ketika pengguna mencoba mengakses API yang membutuhkan token autentikasi tanpa memberikan token yang valid.

---

### 3.5 Status Code 403 — Forbidden

**Request:**

```text
GET https://httpbin.org/status/403
```

**Hasil:**

```text
403 Forbidden
```

Status `403` menunjukkan bahwa server memahami request yang diberikan, tetapi akses ke resource tersebut ditolak karena pengguna tidak memiliki izin yang diperlukan.

Contohnya adalah pengguna yang sudah login tetapi mencoba mengakses halaman atau endpoint yang hanya diperbolehkan untuk admin.

---

### 3.6 Status Code 404 — Not Found

**Request:**

```text
GET https://httpbin.org/status/404
```

**Hasil:**

```text
404 Not Found
```

Status `404` menunjukkan bahwa resource yang diminta tidak ditemukan oleh server.

Contohnya adalah ketika aplikasi meminta data berdasarkan ID yang tidak tersedia:

```text
GET /api/buku/999
```

Jika buku dengan ID `999` tidak ditemukan, server dapat mengembalikan status `404 Not Found`.

---

### 3.7 Status Code 500 — Internal Server Error

**Request:**

```text
GET https://httpbin.org/status/500
```

**Hasil:**

```text
500 Internal Server Error
```

Status `500` menunjukkan bahwa terjadi kesalahan pada sisi server ketika memproses request. Dalam aplikasi nyata, penyebabnya dapat berupa kesalahan program, database bermasalah, exception yang tidak ditangani, atau konfigurasi server.

Pada pengujian ini, HTTPBin memang sengaja mengembalikan status `500` karena endpoint `/status/500` digunakan untuk menguji status code tersebut.

---

## 4. Jawaban Pertanyaan

### 1. Apa perbedaan `400` dan `404`?

`400 Bad Request` menunjukkan bahwa request yang dikirim tidak valid atau tidak dapat diproses karena terdapat kesalahan pada request.

Sedangkan `404 Not Found` menunjukkan bahwa request dapat dipahami oleh server, tetapi resource yang diminta tidak ditemukan.

Contoh:

```text
400 → format atau data request bermasalah
404 → resource yang dicari tidak ditemukan
```

---

### 2. Apa perbedaan `401` dan `403`?

`401 Unauthorized` biasanya menunjukkan bahwa pengguna belum berhasil melakukan autentikasi atau kredensial yang diberikan tidak valid.

Sedangkan `403 Forbidden` menunjukkan bahwa server memahami dan dapat memproses request, tetapi pengguna tidak memiliki izin untuk mengakses resource tersebut.

Contoh:

```text
401 → belum memiliki autentikasi yang valid
403 → sudah dikenali tetapi tidak memiliki izin
```

---

### 3. Mengapa `500` menunjukkan masalah pada sisi server?

Status `500 Internal Server Error` menunjukkan bahwa server mengalami kesalahan ketika memproses request. Kesalahan tersebut biasanya terjadi karena masalah internal pada aplikasi atau server, seperti kesalahan kode program, database error, exception yang tidak ditangani, atau konfigurasi server.

Pada pengujian menggunakan HTTPBin, status `500` sengaja dibuat oleh endpoint `/status/500` sehingga dapat digunakan untuk mempelajari respons tersebut.

---

### 4. Apakah semua error HTTP berarti server mengalami kerusakan?

Tidak. Tidak semua error HTTP berarti server mengalami kerusakan.

Beberapa status error menunjukkan adanya masalah pada request atau hak akses dari client. Contohnya:

* `400` → request tidak valid.
* `401` → autentikasi diperlukan atau tidak valid.
* `403` → akses ditolak.
* `404` → resource tidak ditemukan.

Sementara `500` termasuk status yang menunjukkan adanya masalah pada sisi server.

Dengan demikian, status error HTTP tidak selalu berarti server mengalami kerusakan. Status tersebut digunakan untuk memberikan informasi mengenai masalah yang terjadi antara client dan server.

---

## 5. Screenshot Pengujian

### Screenshot Status 200

Masukkan screenshot hasil pengujian:

```text
GET https://httpbin.org/status/200
```

### Screenshot Status 400

Masukkan screenshot hasil pengujian:

```text
GET https://httpbin.org/status/400
```

### Screenshot Status 500

Masukkan screenshot hasil pengujian:

```text
GET https://httpbin.org/status/500
```

Ketiga screenshot tersebut menunjukkan hasil pengujian status code yang berbeda menggunakan Postman.
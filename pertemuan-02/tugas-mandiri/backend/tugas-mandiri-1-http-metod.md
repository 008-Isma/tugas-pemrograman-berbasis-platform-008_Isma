# Tugas Mandiri 1 — Mengenal HTTP Method dan Endpoint

## 1. Tujuan

Tugas ini bertujuan untuk memahami penggunaan HTTP method dan endpoint dalam komunikasi antara client dan server. Pengujian dilakukan menggunakan **Postman** dengan layanan publik **HTTPBin**.

HTTP method yang diuji meliputi:

* GET
* POST
* PUT
* PATCH
* DELETE

Base URL yang digunakan:

```text
https://httpbin.org
```

---

## 2. Hasil Pengujian

| No | Method | Endpoint  | Data yang Dikirim                               | Status | Hasil                                                                                    |
| -: | :----- | :-------- | :---------------------------------------------- | :----: | :--------------------------------------------------------------------------------------- |
|  1 | GET    | `/get`    | Query parameter `Nama=Ismawati`, `NIM=2024520008` | 200 OK | Server mengembalikan query parameter, header, origin, dan URL request dalam format JSON. |
|  2 | POST   | `/post`   | JSON `nama`, `nim`, `prodi`                     | 200 OK | Server menerima dan mengembalikan data JSON yang dikirim melalui request body.           |
|  3 | PUT    | `/put`    | JSON `nama`, `nim`, `status`                    | 200 OK | Server menerima dan mengembalikan data JSON yang dikirim melalui request body.           |
|  4 | PATCH  | `/patch`  | JSON `status`, `semester`                       | 200 OK | Server menerima dan mengembalikan data JSON yang dikirim melalui request body.           |
|  5 | DELETE | `/delete` | Tidak ada data/body                             | 200 OK | Server menerima request DELETE dan mengembalikan informasi request tanpa data JSON/body. |

---

## 3. Detail Pengujian

### 3.1 GET `/get`

**Method:**

```text
GET
```

**URL:**

```text
https://httpbin.org/get?Nama=Ismawati&NIM=2024520008
```

**Data yang dikirim:**

```text
Nama = Ismawati
NIM = 2024520008
```

Data dikirim sebagai **query parameter**, bukan melalui request body.

**Status:**

```text
200 OK
```

**Response:**

Server mengembalikan informasi request dalam format JSON. Pada bagian `args`, server mengembalikan query parameter yang dikirim:

```json
{
  "args": {
    "Nama": "Ismawati",
    "NIM": "2024520008"
  }
}
```

Selain query parameter, response juga berisi informasi header, origin, dan URL request.

**Kesimpulan:**

GET digunakan untuk melakukan request atau mengambil informasi. Pada pengujian ini, query parameter digunakan untuk melihat bagaimana parameter yang dikirim melalui URL diterima oleh server.

**Screenshot:**

> Masukkan screenshot hasil pengujian GET dari Postman di bagian ini.

---

### 3.2 POST `/post`

**Method:**

```text
POST
```

**URL:**

```text
https://httpbin.org/post
```

**Data yang dikirim:**

```json
{
  "nama": "Ismawati",
  "nim": "2024520008",
  "prodi": "Informatika"
}
```

Data dikirim melalui **request body** dengan format JSON.

**Status:**

```text
200 OK
```

**Response:**

HTTPBin mengembalikan data JSON yang dikirim pada bagian `json`:

```json
{
  "nama": "Ismawati",
  "nim": "2024520008",
  "prodi": "Informatika"
}
```

Response juga menunjukkan bahwa request menggunakan:

```text
Content-Type: application/json
```

**Kesimpulan:**

POST digunakan untuk mengirim data ke server melalui request body. Pada pengujian ini, data berupa nama, NIM, dan program studi berhasil diterima oleh HTTPBin.

**Screenshot:**

> Masukkan screenshot hasil pengujian POST dari Postman di bagian ini.

---

### 3.3 PUT `/put`

**Method:**

```text
PUT
```

**URL:**

```text
https://httpbin.org/put
```

**Data yang dikirim:**

```json
{
  "nama": "Ismawati",
  "nim": "2024520008",
  "status": "Mahasiswa Aktif"
}
```

**Status:**

```text
200 OK
```

**Response:**

Server mengembalikan data JSON yang dikirim:

```json
{
  "nama": "Ismawati",
  "nim": "2024520008",
  "status": "Mahasiswa Aktif"
}
```

**Kesimpulan:**

PUT digunakan untuk melakukan pembaruan data secara keseluruhan. Pada pengujian ini, HTTPBin menerima dan mengembalikan data JSON yang dikirim melalui request body.

---

### 3.4 PATCH `/patch`

**Method:**

```text
PATCH
```

**URL:**

```text
https://httpbin.org/patch
```

**Data yang dikirim:**

```json
{
  "status": "Mahasiswa Aktif",
  "semester": 3
}
```

**Status:**

```text
200 OK
```

**Response:**

Server mengembalikan data JSON yang dikirim:

```json
{
  "semester": 3,
  "status": "Mahasiswa Aktif"
}
```

**Kesimpulan:**

PATCH digunakan untuk melakukan pembaruan sebagian data. Pada pengujian ini, hanya informasi `status` dan `semester` yang dikirim melalui request body.

---

### 3.5 DELETE `/delete`

**Method:**

```text
DELETE
```

**URL:**

```text
https://httpbin.org/delete
```

**Data yang dikirim:**

Tidak ada request body.

**Status:**

```text
200 OK
```

**Response:**

HTTPBin mengembalikan informasi request. Karena tidak ada data yang dikirim melalui body, response menunjukkan:

```json
{
  "data": "",
  "json": null
}
```

**Kesimpulan:**

DELETE digunakan untuk melakukan request penghapusan data. Pada pengujian menggunakan HTTPBin, request DELETE berhasil diproses dan server mengembalikan informasi request tanpa data body.

---

## 4. Kesimpulan

Berdasarkan pengujian menggunakan Postman dan HTTPBin, kelima HTTP method berhasil dijalankan dengan status **200 OK**.

GET digunakan untuk mengirim request dengan query parameter, sedangkan POST, PUT, dan PATCH dapat mengirim data melalui request body dalam format JSON. DELETE dapat digunakan tanpa mengirim request body. Setiap request menghasilkan response dari server yang menunjukkan bagaimana server menerima dan memproses request tersebut.

Pengujian ini membantu memahami hubungan antara **HTTP method, endpoint, parameter, request, dan response** dalam komunikasi antara client dan server.

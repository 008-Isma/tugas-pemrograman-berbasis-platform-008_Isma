# Tugas Mandiri 4 — Pengujian API dengan Postman dan curl

## 1. Tujuan

Tugas ini bertujuan untuk melakukan pengujian API menggunakan dua alat, yaitu **Postman** dan **curl**. Pengujian dilakukan menggunakan layanan publik **HTTPBin** untuk memahami perbedaan request menggunakan Postman dan command line serta melihat informasi HTTP response.

Pengujian yang dilakukan meliputi:

- GET menggunakan Postman.
- POST menggunakan Postman.
- GET menggunakan `curl -i`.
- Pengujian status `404` menggunakan `curl -i`.
- GET menggunakan `curl -s`.
- Perbandingan antara `curl -s` dan `curl -i`.

---

## 2. Pengujian Menggunakan Postman

### 2.1 Pengujian GET

**Request:**
`GET https://httpbin.org/get`

Request tidak menggunakan query parameter dan request body.

**Hasil Response:**

```json
{
  "args": {},
  "headers": {
    "Accept": "*/*",
    "Accept-Encoding": "gzip, deflate, br",
    "Cache-Control": "no-cache",
    "Host": "httpbin.org",
    "Postman-Token": "b04ee407-e313-43b2-9d38-37a5266fed6d",
    "User-Agent": "PostmanRuntime/7.39.1",
    "X-Amzn-Trace-Id": "Root=1-6ac3b8b2-1d004fa62b0c83bc61e2baa2"
  },
  "origin": "112.215.240.205",
  "url": "[https://httpbin.org/get](https://httpbin.org/get)"
}
Hasil Pengujian:
Request berhasil diproses dengan status 200 OK. Karena tidak menggunakan query parameter, bagian args pada response bernilai kosong.

2.2 Pengujian POST
Request:
POST https://httpbin.org/post

Data JSON yang dikirim:

JSON
{
  "nama": "Ismawati",
  "prodi": "Informatika"
}
Hasil Response:

JSON
{
  "args": {},
  "data": "{\r\n  \"nama\": \"Ismawati\",\r\n  \"prodi\": \"Informatika\"\r\n}",
  "files": {},
  "form": {},
  "headers": {
    "Accept": "*/*",
    "Accept-Encoding": "gzip, deflate, br",
    "Cache-Control": "no-cache",
    "Content-Length": "51",
    "Content-Type": "application/json",
    "Host": "httpbin.org",
    "Postman-Token": "b553f7b4-e685-4dda-b595-73ea49a8a787",
    "User-Agent": "PostmanRuntime/7.39.1",
    "X-Amzn-Trace-Id": "Root=1-6ac3b972-7bcbffad446ce5130cef039d"
  },
  "json": {
    "nama": "Ismawati",
    "prodi": "Informatika"
  },
  "origin": "112.215.240.205",
  "url": "[https://httpbin.org/post](https://httpbin.org/post)"
}
Hasil Pengujian:
Request berhasil diproses dengan status 200 OK. Data JSON yang dikirim berhasil diterima oleh server dan ditampilkan kembali pada bagian json. Response juga menunjukkan bahwa request menggunakan Content-Type: application/json.

3. Perbandingan Response GET dan POST
Aspek	GET	POST
Endpoint	/get	/post
Method	GET	POST
Request Body	Tidak ada	JSON
Query Parameter	Tidak ada	Tidak ada
Data pada Response	args kosong	Data muncul pada json
Content-Type	Tidak digunakan untuk body	application/json
Status	200 OK	200 OK
Perbedaan utama adalah GET pada pengujian ini tidak mengirimkan data melalui request body, sedangkan POST mengirimkan data JSON melalui request body. HTTPBin kemudian menampilkan kembali data yang diterima pada response.

4. Pengujian Menggunakan curl
4.1 Pengujian curl -i /get
Perintah yang digunakan:

Bash
curl -i [https://httpbin.org/get](https://httpbin.org/get)
Hasil:

HTTP
HTTP/1.1 200 OK
Date: Mon, 05 Oct 2026 14:54:21 GMT
Content-Type: application/json
Content-Length: 257
Connection: keep-alive
Server: gunicorn/19.9.0
Access-Control-Allow-Origin: *
Access-Control-Allow-Credentials: true
Response Body:

JSON
{
  "args": {},
  "headers": {
    "Accept": "*/*",
    "Host": "httpbin.org",
    "User-Agent": "curl/8.19.0",
    "X-Amzn-Trace-Id": "Root=1-6ac3ba1d-33eb534520d356656cc0fddb"
  },
  "origin": "112.215.240.205",
  "url": "[https://httpbin.org/get](https://httpbin.org/get)"
}
Hasil Pengamatan:
Perintah curl -i menampilkan HTTP response header dan response body. Dari hasil pengujian terlihat status 200 OK, Content-Type: application/json, dan Content-Length: 257.

4.2 Pengujian curl -i /status/404
Perintah yang digunakan:

Bash
curl -i [https://httpbin.org/status/404](https://httpbin.org/status/404)
Hasil:

HTTP
HTTP/1.1 404 NOT FOUND
Date: Mon, 05 Oct 2026 15:02:46 GMT
Content-Type: text/html; charset=utf-8
Content-Length: 0
Connection: keep-alive
Server: gunicorn/19.9.0
Access-Control-Allow-Origin: *
Access-Control-Allow-Credentials: true
Hasil Pengamatan:
Server mengembalikan status 404 NOT FOUND. Nilai Content-Length: 0 menunjukkan bahwa response tidak memiliki isi body.

5. Pengujian curl -s
Perintah yang digunakan:

Bash
curl -s [https://httpbin.org/get](https://httpbin.org/get)
Hasil:

JSON
{
  "args": {},
  "headers": {
    "Accept": "*/*",
    "Host": "httpbin.org",
    "User-Agent": "curl/8.19.0",
    "X-Amzn-Trace-Id": "Root=1-6ac3be4f-02c205d171cefa670bb7ee46"
  },
  "origin": "112.215.240.205",
  "url": "[https://httpbin.org/get](https://httpbin.org/get)"
}
Hasil Pengamatan:
Perintah curl -s hanya menampilkan response body tanpa menampilkan informasi tambahan seperti progress meter dari curl. Pada hasil pengujian, response JSON langsung ditampilkan pada terminal.

6. Perbandingan curl -s dan curl -i
Perintah curl -s https://httpbin.org/get digunakan untuk menjalankan curl dalam mode silent, sehingga output tambahan dari curl tidak ditampilkan dan response body dapat ditampilkan dengan lebih bersih.

Sedangkan curl -i https://httpbin.org/get menampilkan HTTP response header sekaligus response body.

Opsi -s dapat digunakan ketika hanya membutuhkan isi response, misalnya saat melakukan pengujian API atau memproses hasil menggunakan script. Opsi -i digunakan ketika membutuhkan informasi HTTP seperti status code, Content-Type, dan Content-Length untuk melakukan pemeriksaan atau debugging response server.

7. Fungsi Opsi curl
Opsi	Fungsi
-s	Menjalankan curl dalam mode silent sehingga output tambahan seperti progress meter tidak ditampilkan.
-i	Menampilkan HTTP response header sebelum response body.
Contoh penggunaan:

Bash
curl -s [https://httpbin.org/get](https://httpbin.org/get)
Digunakan ketika ingin mendapatkan response body dengan output yang lebih bersih.

Bash
curl -i [https://httpbin.org/get](https://httpbin.org/get)
Digunakan ketika ingin melihat informasi HTTP response header sekaligus response body.

8. Kesimpulan
Berdasarkan pengujian yang telah dilakukan, Postman dan curl dapat digunakan untuk menguji API dan melihat response dari server. Pengujian menggunakan Postman menunjukkan perbedaan antara request GET yang tidak menggunakan body dan request POST yang mengirimkan data JSON melalui request body.

Pengujian menggunakan curl -i menunjukkan bahwa HTTP response terdiri dari status code, response header, dan response body. Sementara itu, penggunaan curl -s menghasilkan output yang lebih sederhana karena response ditampilkan tanpa informasi tambahan dari curl. Dengan demikian, curl -s cocok digunakan ketika hanya membutuhkan response body, sedangkan curl -i lebih sesuai ketika ingin memeriksa informasi HTTP response secara lengkap.
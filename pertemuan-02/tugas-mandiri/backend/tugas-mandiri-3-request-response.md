# Tugas Mandiri 3 — Memahami Request dan Response

## 1. Tujuan

Tugas ini bertujuan untuk memahami konsep **request** dan **response** dalam komunikasi antara client dan server menggunakan protokol HTTP. Pengujian dilakukan menggunakan **Postman** dengan layanan publik **HTTPBin**.

Pada pengujian ini digunakan dua endpoint:

```text
GET https://httpbin.org/get

dan

GET https://httpbin.org/headers

Endpoint /get digunakan untuk melihat informasi request yang dikirim, termasuk query parameter. Sedangkan endpoint /headers digunakan untuk melihat HTTP header yang diterima oleh server.

2. Hasil Pengujian
Endpoint	Method	Parameter	Hasil
/get	GET	nama=Ismawati, kelas=pemrograman berbasi platform	Server mengembalikan query parameter pada bagian args.
/headers	GET	Tidak ada	Server menampilkan HTTP header yang diterima dari client.
3. Detail Pengujian
3.1 Pengujian GET /get

Request:

GET https://httpbin.org/get

Query Parameter:

Key	Value
nama	Ismawati
kelas	pemrograman berbasi platform

Sehingga request yang dikirim menjadi:

GET https://httpbin.org/get?nama=Ismawati&kelas=pemrograman%20berbasi%20platform

Hasil Response:

{
  "args": {
    "kelas": "pemrograman berbasi platform",
    "nama": "Ismawati"
  },
  "headers": {
    "Accept": "*/*",
    "Accept-Encoding": "gzip, deflate, br",
    "Cache-Control": "no-cache",
    "Host": "httpbin.org",
    "Postman-Token": "3afec96b-84ab-4010-b389-7ba83469fe7b",
    "User-Agent": "PostmanRuntime/7.39.1",
    "X-Amzn-Trace-Id": "Root=1-6ac3ac9e-7ee093ab31fd078a2617f8e"
  },
  "origin": "112.215.240.205",
  "url": "https://httpbin.org/get?nama=Ismawati&kelas=pemrograman berbasi platform"
}

Hasil Pengamatan:

Berdasarkan hasil pengujian, query parameter nama dan kelas yang dikirim melalui URL berhasil diterima oleh server. Data tersebut ditampilkan pada bagian args pada response.

Pada response juga terdapat informasi headers, origin, dan url. Hal ini menunjukkan bahwa HTTPBin dapat menampilkan informasi request yang diterima oleh server.

3.2 Pengujian GET /headers

Request:

GET https://httpbin.org/headers

Request ini tidak menggunakan query parameter maupun request body.

Hasil Response:

{
  "headers": {
    "Accept": "*/*",
    "Accept-Encoding": "gzip, deflate, br",
    "Cache-Control": "no-cache",
    "Host": "httpbin.org",
    "Postman-Token": "2abeadb5-0432-471c-9271-c574b0526bf5",
    "User-Agent": "PostmanRuntime/7.39.1",
    "X-Amzn-Trace-Id": "Root=1-6ac3ae3c-7406281b7605bf1826f9e36a"
  }
}

Hasil Pengamatan:

Berdasarkan hasil pengujian, server menampilkan beberapa HTTP header yang diterima dari client. Beberapa header yang terlihat adalah Accept, Accept-Encoding, Cache-Control, Host, dan User-Agent.

Header User-Agent menunjukkan bahwa request dikirim menggunakan Postman dengan PostmanRuntime/7.39.1.

4. Alur Request dan Response

Proses komunikasi antara client dan server dapat digambarkan sebagai berikut:

Client / Postman
       |
       | HTTP Request
       | Method + URL + Header + Body
       v
     Server
    (HTTPBin)
       |
       | HTTP Response
       | Status Code + Header + Body
       v
Client / Postman

Pada pengujian ini, Postman bertindak sebagai client yang mengirimkan request kepada server HTTPBin. Server kemudian memproses request dan memberikan response kembali kepada Postman.

5. Jawaban Pertanyaan
6. Apa yang dimaksud request?

Request adalah permintaan yang dikirimkan oleh client kepada server untuk meminta data atau melakukan suatu proses. Request HTTP dapat terdiri dari method, URL, query parameter, HTTP header, dan request body.

Pada pengujian ini, Postman bertindak sebagai client yang mengirimkan request dengan method GET kepada server HTTPBin.

2. Apa yang dimaksud response?

Response adalah balasan yang diberikan oleh server setelah menerima dan memproses request dari client. Response dapat berisi status code, HTTP header, dan response body.

Pada pengujian ini, HTTPBin memberikan response yang berisi informasi mengenai request yang telah diterima oleh server.

3. Apa fungsi query parameter?

Query parameter berfungsi untuk mengirimkan data atau informasi tambahan melalui URL. Query parameter ditulis setelah tanda ? dan apabila terdapat lebih dari satu parameter, setiap parameter dipisahkan menggunakan tanda &.

Contohnya:

https://httpbin.org/get?nama=Ismawati&kelas=pemrograman%20berbasi%20platform

Pada contoh tersebut terdapat dua query parameter:

nama = Ismawati
kelas = pemrograman berbasi platform

HTTPBin kemudian menampilkan data tersebut pada bagian args dalam response.

4. Apa fungsi HTTP header?

HTTP header berfungsi untuk membawa informasi tambahan dalam komunikasi antara client dan server. Header dapat memberikan informasi mengenai jenis data yang diterima, jenis client yang digunakan, host tujuan, dan informasi lainnya.

Pada pengujian /headers, HTTPBin menampilkan beberapa header yang dikirim oleh Postman, seperti:

Accept
Accept-Encoding
Cache-Control
Host
User-Agent
5. Apa perbedaan data pada URL dengan data pada request body?

Data pada URL biasanya dikirim menggunakan query parameter dan dapat terlihat langsung pada URL.

Contohnya:

GET https://httpbin.org/get?nama=Ismawati&kelas=Informatika

Sedangkan data pada request body dikirim pada bagian isi request dan tidak ditampilkan sebagai bagian dari URL. Request body biasanya digunakan pada method seperti POST, PUT, dan PATCH.

Contoh data pada request body:

{
  "nama": "Ismawati",
  "nim": "2024520009"
}

Jadi, perbedaannya adalah data pada URL dikirim melalui query parameter, sedangkan data pada request body dikirim melalui isi request.

6. Screenshot Pengujian
Screenshot GET /get

Masukkan screenshot hasil pengujian:

GET https://httpbin.org/get

Screenshot menunjukkan query parameter:

nama = Ismawati
kelas = pemrograman berbasi platform

Gambar 1. Pengujian GET /get dengan query parameter.

Screenshot GET /headers

Masukkan screenshot hasil pengujian:

GET https://httpbin.org/headers

Screenshot menunjukkan HTTP header yang diterima oleh server HTTPBin.

Gambar 2. Pengujian GET /headers untuk melihat HTTP header.

7. Kesimpulan

Berdasarkan pengujian yang telah dilakukan menggunakan Postman dan HTTPBin, dapat dipahami bahwa request merupakan permintaan yang dikirim oleh client kepada server, sedangkan response merupakan balasan yang diberikan oleh server kepada client.

Pengujian endpoint /get menunjukkan bahwa query parameter dapat digunakan untuk mengirimkan data melalui URL dan data tersebut dapat diterima serta ditampilkan oleh server. Sementara itu, pengujian endpoint /headers menunjukkan informasi HTTP header yang diterima oleh server dari client.

Dengan demikian, request dan response merupakan bagian penting dalam komunikasi antara client dan server pada aplikasi berbasis HTTP. Pemahaman terhadap query parameter, HTTP header, URL, dan request body juga diperlukan dalam pengembangan aplikasi web dan API.
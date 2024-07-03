# project4

## Tugas:

Membuat pipeline untuk mentransfer data yang ada di database operational MySQL ke database data_warehouse di PostgreSQL

## Langkah pengerjaan:

1.	Menjalankan perintah `docker-compose up`

![image](https://github.com/dzzzzrca/project5/assets/153365739/49812ed3-2e8d-4de9-966a-d6e7a334ae0f)

Dalam hal ini, file docker-compose.yml berisi dua services: satu untuk MySQL dan satu untuk PostgreSQL.

 ![image](https://github.com/dzzzzrca/project5/assets/153365739/3f89cea0-34f7-475e-aee6-32dff8547c97)

Gambar diatas untuk memastikan bahwa container sudah terbuat dan berjalan.

2.	Memasuki terminal container db-mysql di Docker Dekstop

![image](https://github.com/dzzzzrca/project5/assets/153365739/00b00cae-728e-4ac6-88ab-08128bffa599)

Gambar diatas untuk masuk kedalam direktori yang sama dengan file csv berisikan data yang akan di import.

3.	Memasuki MySQL Database

![image](https://github.com/dzzzzrca/project5/assets/153365739/897dcba0-5c9e-4910-a894-96fdfea66cc8)

Gambar diatas langkah masuk ke database MySQL yang bernama operational menggunakan username=root dan password=mysql. Penjelasan kueri yang digunakan sebagai berikut:
-	`--local-infile=1`: Mengaktifkan pemuatan data dari file lokal ke dalam database.
-	`-uroot`: Menentukan nama pengguna root.
-	`-pmysql`: Menentukan kata sandi mysql.
-	`operational`: Menentukan nama database yang akan dihubungi.
 
4.	Membuat table youtube

a.	Menggunakan database operational dan mengaktifkan ulang local_infile agar dapat memuat data dari file lokal ke dalam database

b.  Karena belum ada table pada database operational, maka langkah selanjutnya membuat table dengan nama `youtube` sesuai query DDL yang ada pada file init.sql

5.	Mengimpor data ke dalam table youtube

a.	Karena table `youtube` masih kosong, langkah selanjutnya mengimpor data dari local dari pada file global_youtube_stat.csv

![image](https://github.com/dzzzzrca/project5/assets/153365739/144c70c3-b904-4154-bf25-6c331340e6e4)

b.	Mengimpor data ke dalam table `youtube`

 ![image](https://github.com/dzzzzrca/project5/assets/153365739/7d5cdc79-fdf6-4da0-886e-429de6b32853)

c.	Data berhasil di impor

 ![image](https://github.com/dzzzzrca/project5/assets/153365739/8f7d4fa0-f546-48fb-bf29-4b1d430fa216)

6.	Membuat database di PostgreSQL

![image](https://github.com/dzzzzrca/project5/assets/153365739/4b512fa9-287c-4fdb-b755-b3ef8b3b17c1)

Perintah `\l` bertujuan untuk menampilkan semua database yang tersedia dalam instansi PostgreSQL.

![image](https://github.com/dzzzzrca/project5/assets/153365739/b045333d-47cd-47d8-99c2-c622d1b6983a)

Perintah `create database data_warehouse` untuk membuat database baru dengan nama = data_warehouse.

7.	Mengimpor dan memverifikasi data dari MySQL ke PostrgeSQL

a.	Proses pengimporan data
Kode yang disediakan dalam file etl.py akan membaca data dari basis data MySQL dan menuliskannya ke basis data PostgreSQL. Kode tersebut menggunakan perpustakaan pandas untuk membaca dan menulis data, serta perpustakaan mysql.connector dan sqlalchemy untuk terhubung ke basis data. Kode pertama-tama terhubung ke basis data MySQL dan membaca data dari tabel youtube. Kemudian, ia terhubung ke basis data PostgreSQL dan menulis data ke tabel bernama youtube_etl. Jika terjadi pengecualian, kode menangkapnya dan mencetak pesan kesalahan.

![image](https://github.com/dzzzzrca/project5/assets/153365739/9f8b2a97-126e-4cf9-86a4-a9f7487cac17)

b.	Memverifikasi data
Setelah masuk kembali ke dalam PostgreSQL pada database data_warehouse, sudah terlihat ketika perintah `\d` dijalankan kembali terdapat table dengan nama youtube_etl.

![image](https://github.com/dzzzzrca/project5/assets/153365739/e386fbc0-02a3-4cb0-88a9-9f1c6c681690)

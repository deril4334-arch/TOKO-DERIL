# TOKO-DERIL

Apa itu JOIN?
-
JOIN adalah perintah di SQL untuk menggabungkan data dari dua tabel atau lebih berdasarkan kolom yang saling berhubungan (biasanya ID yang sama).
Digunakan supaya kita bisa mengambil data yang tersebar di beberapa tabel menjadi satu hasil.

Penjelasan INNER JOIN, LEFT JOIN, RIGHT JOIN :
-
INNER JOIN menampilkan hanya data yang memiliki pasangan di kedua tabel.
-
Artinya:
Jika data di tabel pertama tidak punya pasangan di tabel kedua → tidak ditampilkan.
Jika data di tabel kedua tidak punya pasangan di tabel pertama → juga tidak ditampilkan.
📌 Jadi yang muncul hanya data yang benar-benar cocok di kedua tabel.
Kapan dipakai?
Saat kita hanya ingin melihat data yang saling berhubungan saja.

LEFT JOIN menampilkan semua data dari tabel kiri, walaupun tidak punya pasangan di tabel kanan.
-
Artinya:
Semua data tabel kiri pasti tampil.
Jika tidak ada pasangan di tabel kanan, maka bagian tabel kanan akan bernilai NULL (kosong).
📌 Jadi tabel kiri selalu lengkap, tabel kanan mengikuti jika ada kecocokan.
Kapan dipakai?
Saat ingin melihat semua data utama, termasuk yang belum memiliki relasi.

RIGHT JOIN adalah kebalikan dari LEFT JOIN.
Menampilkan semua data dari tabel kanan, walaupun tidak punya pasangan di tabel kiri.
-
Artinya:
Semua data tabel kanan pasti tampil.
Jika tidak ada pasangan di tabel kiri, maka bagian tabel kiri akan bernilai NULL.
📌 Jadi tabel kanan selalu lengkap.
Kapan dipakai?
Saat tabel kanan dianggap sebagai data utama yang harus tampil semua

CMD TOKO : 
-
Setting environment for using XAMPP for Windows.
Deril@WORKPRO-LITE c:\xampp
# mysql -u root
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 10
Server version: 10.4.32-MariaDB mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> create database toko;
Query OK, 1 row affected (0.002 sec)

MariaDB [(none)]> use toko;
Database changed
MariaDB [toko]> create table pelanggan(
    -> id_pelanggan int primary key,
    -> nama varchar(50));
Query OK, 0 rows affected (0.045 sec)

MariaDB [toko]> insert into pelanggan
    -> (id_pelanggan, nama) values
    -> (1,'Andi'),
    -> (2,'Budi'),
    -> (3,'Sari');
Query OK, 3 rows affected (0.034 sec)
Records: 3  Duplicates: 0  Warnings: 0

MariaDB [toko]> select * from pelanggan;
+--------------+------+
| id_pelanggan | nama |
+--------------+------+
|            1 | Andi |
|            2 | Budi |
|            3 | Sari |
+--------------+------+
3 rows in set (0.001 sec)

MariaDB [toko]> create table pesanan(
    -> id_pesanan int primary key,
    -> id_pelanggan int,
    -> produk varchar(50));
Query OK, 0 rows affected (0.047 sec)

MariaDB [toko]> insert into pesanan
    -> (id_pesanan, id_pelanggan, produk) values
    -> (101,1,'Laptop'),
    -> (102,2,'Smartphone'),
    -> (103,1,'Headset');
Query OK, 3 rows affected (0.006 sec)
Records: 3  Duplicates: 0  Warnings: 0

MariaDB [toko]> select * from pesanan;
+------------+--------------+------------+
| id_pesanan | id_pelanggan | produk     |
+------------+--------------+------------+
|        101 |            1 | Laptop     |
|        102 |            2 | Smartphone |
|        103 |            1 | Headset    |
+------------+--------------+------------+
3 rows in set (0.001 sec)

MariaDB [toko]> select pelanggan.nama, pesanan.produk
    -> from pelanggan
    -> inner join pesanan on pelanggan.id_pelanggan = pesanan.id_pelanggan;
+------+------------+
| nama | produk     |
+------+------------+
| Andi | Laptop     |
| Budi | Smartphone |
| Andi | Headset    |
+------+------------+
3 rows in set (0.001 sec)

MariaDB [toko]> select pelanggan.nama, pesanan.produk
    -> from pelanggan
    -> left join pesanan on pelanggan.id_pelanggan = pesanan.id_pelanggan;
+------+------------+
| nama | produk     |
+------+------------+
| Andi | Laptop     |
| Budi | Smartphone |
| Andi | Headset    |
| Sari | NULL       |
+------+------------+
4 rows in set (0.001 sec)

MariaDB [toko]> select pelanggan.nama, pesanan.produk
    -> from pelanggan
    -> right join pesanan on pelanggan.id_pelanggan = pesanan.id_pelanggan;
+------+------------+
| nama | produk     |
+------+------------+
| Andi | Laptop     |
| Budi | Smartphone |
| Andi | Headset    |
+------+------------+
3 rows in set (0.050 sec)

MariaDB [toko]>


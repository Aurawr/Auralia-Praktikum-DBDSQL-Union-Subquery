# Laporan Praktikum Tugas 8 : Union & Subquery
Berikut adalah langkah-langkah praktikum materi Union dan Subquery yang telah dibuat.

## Langkah-Langkah Praktikum
## UNION
### 1. Tambahkan Data Pada Table Mahasiswa Sesuai dengan Data Pada Modul.
```
INSERT INTO mahasiswa values
	('155150404', 1,212,'JESSY',2016,'1999-2-10','BANDUNG','F'),
	('155150405', 2 ,219,'BAMBANG',2014,'1996-9-27','MAKASSAR','M');
```
![image](https://github.com/Aurawr/Auralia-Praktikum-DBDSQL-Union-Subquery/assets/133871441/746fcb5a-fad9-4a0f-a5a1-824e375f2785)

### 2. Buat Table mahasiswa_pindahan
Membuat table baru dengan perintaah `create table` dengan nama mahasiswa_pindahan untuk menampung data dari mahasiswa pindahan.
```
CREATE TABLE AKADEMIK.MAHASISWA_PINDAHAN(
NIM VARCHAR(15) NOT NULL PRIMARY KEY,
ID_SELEKSI_MASUK SMALLINT,
FOREIGN KEY (ID_SELEKSI_MASUK) REFERENCES
AKADEMIK.SELEKSI_MASUK(ID_SELEKSI_MASUK),
ID_PROGRAM_STUDI SMALLINT,
FOREIGN KEY (ID_PROGRAM_STUDI) REFERENCES
AKADEMIK.PROGRAM_STUDI(ID_PROGRAM_STUDI),
NAMA VARCHAR(45),
ANGKATAN SMALLINT,
TGL_LAHIR DATE,
KOTA_LAHIR VARCHAR(60),
JENIS_KELAMIN CHAR(1) CHECK (JENIS_KELAMIN IN ('M','F'))
);
```

### 3. Masukkan Data Baru Ke Table mahasiswa_pindahan
Setelah membuat table mahasiswa_pindahan, selanjutnya adalah memasukkan data baru ke table dengan menggunakan perintah `insert into namaTable values ();`.
```
INSERT INTO MAHASISWA_PINDAHAN VALUES 
	('155150500', 1 ,211,'BUDI', 2015,'1997-3-3','BANYUWANGI','M'),
	('155150501', 2,212,'ANDI',2015,'1997-2-21','JAKARTA','M'),
	('155150502', 2 ,211,'DIMAS', 2015,'1998-4-11','SURABAYA','M'),
	('155150503', 2 ,211,'DIDIN',2015,'1997-2-26','BANDUNG','M');
```
![image](https://github.com/Aurawr/Auralia-Praktikum-DBDSQL-Union-Subquery/assets/133871441/67570acc-f53a-4300-bdcf-570d0848c646)

### 4. Menampilkan Data Mahasiswa yang Memiliki Kota Lahir dengan Inisial B dan Mahasiswa Pindahan yang Memiliki Nama Inisial D
Menampilkan NIM, NAMA, JENIS_KELAMIN, KOTA LAHIR dan ANGKATAN dari Mahasiswa yang memiliki Kota Lahir dengan inisial B dan dari Mahasiswa_Pindahan yang memiliki Nama dengan inisial D. Urutkan berdasarkan NIM. Untuk menampilkan data tersebut dapat menggunakan kode sebagai berikut.
```
SELECT NIM, NAMA, JENIS_KELAMIN, KOTA_LAHIR, ANGKATAN
FROM mahasiswa
WHERE KOTA_LAHIR LIKE 'B%'
UNION
SELECT NIM, NAMA, JENIS_KELAMIN, KOTA_LAHIR, ANGKATAN
FROM Mahasiswa_Pindahan
WHERE NAMA LIKE 'D%'
ORDER BY NIM;
```
Perintah select from digunakan untuk memilih kolom mana saja yang ingin ditampilkan dan dari tabel mana, sedangkan perintah `where kota_lahir  like 'B%'` untuk menentukan kondisi data yang ingin ditampilkan yaitu menentukan dimana kita ingin menampilkan data mahasiswa yang memiliki kota_lahir dengan inisial 'B' begitu juga dengan perintah where yang lain. Sedangkan penggunaan perintah `union` digunakan untuk menggabungkan atau memasukkan table-table yang kita inginkan, namun apabila terdapat kolom yang memiliki nilai sama, maka hanya akan ditampilkan salah satunya saja. Kemudian `order by nim` digunakan untuk mengurutkan data berdasarkan nim.

![WhatsApp Image 2023-11-18 at 07 28 24_385d3d73](https://github.com/Aurawr/Auralia-Praktikum-DBDSQL-Union-Subquery/assets/133871441/7b8d98e2-6d4b-4fe3-a5ed-371e89817e0e)

### 5. Menampilkan Data Mahasiswa dan Mahasiswa Pindahan Angkatan 2015 dengan Pengecualian Mahasiswa Pindahan yang Memiliki Kota Lahir dengan Inisial M
Menampilkan NIM, NAMA, JENIS_KELAMIN, KOTA LAHIR dan ANGKATAN dari Mahasiswa Angkatan 2015 dan dari Mahasiswa_Pindahan tetapi kecuali Mahasiswa_Pindahan yang memiliki Kota Lahir dengan inisial M urutkan berdasarkan NIM. Data tersebut dapat ditampilkan dengan kode berikut.
```
SELECT NIM, NAMA, JENIS_KELAMIN, KOTA_LAHIR, ANGKATAN
FROM mahasiswa
WHERE ANGKATAN = 2015
UNION
SELECT NIM, NAMA, JENIS_KELAMIN, KOTA_LAHIR, ANGKATAN
FROM MAHASISWA_PINDAHAN
WHERE ANGKATAN = 2015 AND KOTA_LAHIR NOT LIKE 'M%'
ORDER BY NIM;
```
Pada kode ini juga menggunakan perintah `union` dan untuk bagian mahasiswa pindahan menggunakan perintah `where angkatan = 2015 and kota_lahir not like 'M%'` untuk memilah data mahasiswa pindahan angkatan 2015 yang juga tidak memiliki kota lahir dengan inisial 'M'. Kemudian perintah `order by nim;` digunakan untuk mengurutkan data berdasarkan nim.

![WhatsApp Image 2023-11-18 at 07 28 58_40e4a1ad](https://github.com/Aurawr/Auralia-Praktikum-DBDSQL-Union-Subquery/assets/133871441/71676953-1d4e-49a3-b843-bf4c8cf1daf5)

## SUBQUERY
### 6. Menampilkan Data Mahasiswa yang Memiliki Kota Lahir yang Sama dengan Mahasiswa Pindahan dengan Nama BUDI
Menampilkan NIM, Nama dan Angkatan dari Mahasiswa yang memiliki Kota Lahir yang sama dengan Mahasiswa Pindahan dengan nama BUDI. Data tersebut dapat ditampilkan dengan kode berikut.
```
SELECT M.NIM, M.NAMA, M.ANGKATAN
FROM mahasiswa M
JOIN MAHASISWA_PINDAHAN MP ON M.KOTA_LAHIR = MP.KOTA_LAHIR
WHERE MP.NAMA = 'BUDI';
```
Pada kode tersebut penggunaan subquery terdapat pada perintah `join mahasiswa_pindahan MP on kota_lahir = mp.kota.lahir` lebih tepatnya pada bagian `m.kota_lahir = mp.kota_lahir`

![WhatsApp Image 2023-11-18 at 08 10 13_e71f76e9](https://github.com/Aurawr/Auralia-Praktikum-DBDSQL-Union-Subquery/assets/133871441/359ae3dd-8d36-41e3-a6bc-821fb6d9a604)

### 7. Menampilkan Data dari Mahasiswa yang Memiliki Kota Lahir yang Sama dengan Seluruh Mahasiswa Pindahan
Menampilkan NIM, Nama dan Angkatan dari Mahasiswa yang memiliki Kota Lahir yang sama dengan seluruh Mahasiswa Pindahan.
```
select NIM, NAMA, ANGKATAN
from mahasiswa
where KOTA_LAHIR in (
    select KOTA_LAHIR
    from MAHASISWA_PINDAHAN
);
```
Pada kode tersebut pengunaan subquery terdapat pada perintah `where kota_lahir in ( select kota_lahir from mahasiswa_pindahan);` yang mana perintah tersebut digunakan untuk menyaring data kota lahir tabel mahasiswa yang juga memiliki nilai sama dengan kolom kota lahir pada tabel mahasiswa pindahan.

![WhatsApp Image 2023-11-18 at 08 10 34_99a85e6d](https://github.com/Aurawr/Auralia-Praktikum-DBDSQL-Union-Subquery/assets/133871441/af642ca0-bf07-44ce-9d1b-5c36de4988f0)

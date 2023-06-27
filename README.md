# DATABASEPENGELOLAAN_KAS_RT

**Oleh Kelompok 8**

- MUHAMMAD RIZKY RAKA PRATAMA
- BADRUL MUNIR
- AHMAD YUDA RAMADHAN
- SHOFWAN ASSYAUQY RAMADHAN

## **A. ER-D**

![gambar](gambar/database%20pengelolaan%20kas%20rt.png)

## **B. DDL**

```sql
CREATE DATABASE KAS_RT;
```

```sql
CREATE TABLE warga (
    -> id_warga VARCHAR(10) PRIMARY KEY NOT NULL,
    -> nama VARCHAR(45) NOT NULL,
    -> alamat VARCHAR(45) NOT NULL,
    -> no_kk VARCHAR(20) NOT NULL
    -> );
```

```sql
CREATE TABLE t_pembayaran (
    -> id_pembayaran VARCHAR(10) PRIMARY KEY NOT NULL,
    -> id_warga VARCHAR(10),
    -> id_iuran VARCHAR(10),
    -> tanggal DATE,
    -> jumlah DECIMAL(20) NOT NULL
    -> );
```

```sql
 CREATE TABLE iuran (
    -> id_iuran VARCHAR(10) PRIMARY KEY NOT NULL,
    -> jenis VARCHAR(25) NOT NULL,
    -> jumlah DECIMAL(20) NOT NULL
    -> );
```

```sql
CREATE TABLE l_transaksi (
    -> id_laporan VARCHAR(10) PRIMARY KEY NOT NULL,
    -> id_iuran VARCHAR(10),
    -> tanggal DATE NOT NULL,
    -> deskripsi VARCHAR(45)
    -> );
```

```sql
ALTER TABLE t_pembayaran
    -> ADD CONSTRAINT fk_p_warga
    -> FOREIGN KEY (id_warga) REFERENCES warga(id_warga);
```

```sql
ALTER TABLE t_pembayaran
    -> ADD CONSTRAINT fk_p_iuran
    -> FOREIGN KEY (id_iuran) REFERENCES iuran(id_iuran);
```

```sql
ALTER TABLE l_transaksi
    -> ADD CONSTRAINT fk_LT_iuran
    -> FOREIGN KEY (id_iuran) REFERENCES iuran(id_iuran);
```

```sql
DESC warga/iuran/t_pembayaran/l_transaksi;
```

## **C. SQL CRUD**

```sql
INSERT INTO warga (id_warga,nama,alamat,no_kk)
    -> VALUES ('W001','John Doe','Jalan ABC No.123','123456'),
    -> ('W002','Jane Smith','Jalan XYZ No.456','789652'),
    -> ('W003','Mark Johnson','Jalan PQR No.345','887766');
```

```sql
 INSERT INTO iuran (id_iuran,jenis,jumlah)
    -> VALUES ('I001','Iuran Bulanan','50000'),
    -> ('I002','Iuran Keamanan','100000'),
    -> ('I003','Iuran Sampah','30000');
```

```sql
 INSERT INTO t_pembayaran (id_pembayaran,id_warga,id_iuran,tanggal,jumlah)
    -> VALUES ('P001','W001','I001','2023-01-05','50000'),
    -> ('P002','W001','I002','2023-02-10','100000'),
    -> ('P003','W002','I001','2023-02-15','50000'),
    -> ('P004','W003','I001','2023-03-02','50000'),
    -> ('P005','W003','I003','2023-03-10','30000');
```

```sql
INSERT INTO l_transaksi (id_laporan,id_iuran,tanggal,deskripsi)
    -> VALUES ('L001','I001','2023-01-31','Laporan Bulanan Januari'),
    -> ('L002','I002','2023-02-28','Laporan Bulanan Februari'),
    -> ('L003','I003','2023-03-31','Laporan Bulanan Maret');
```

```sql
SELECT * FROM warga/iuran/t_pembayaran/l_transaksi;
```

```sql
UPDATE warga SET nama = 'yudha' WHERE id_warga = 'W005';
```

```sql
DELETE FROM warga WHERE nama = 'Yudha';
```

## **D. SQL JOIN**

```sql
SELECT t_pembayaran.*, warga.nama AS 'Nama Warga'
    -> FROM t_pembayaran
    -> JOIN warga ON t_pembayaran.id_warga = warga.id_warga;
```

```sql
SELECT t_pembayaran.*, iuran.jenis, warga.nama AS 'Nama Warga', iuran.jumlah AS 'Jumlah Iuran'
    -> FROM t_pembayaran
    -> INNER JOIN iuran ON t_pembayaran.id_iuran = iuran.id_iuran
    -> LEFT JOIN warga ON t_pembayaran.id_warga = warga.id_warga;
```
## **E. Laporan**

DATABASE KAS RT
![gambar](gambar/database%20pengelolaan%20kas%20rt.png)
Berdasarkan konsep er-d di atas dapat disimpulkan untuk tabel akan terdiri dari warga, transaksi pembayaran, iuran dan laporan transaksi, berikut adalah langkah-langkah dalam pembuatan database Pengelolaan KAS RT.

1. Membuat DATABASE
   - Syntax
     ```SQL
     CREATE DATABASE KAS RT;
     ```
2. dan Gunakan DATABASE yang sudah dibuat tadi
   - Syntax
     ```SQL
     USE KAS RT;
     ```
3. Membuat beberapa tabel sesuai konsep er-d diatas

- Tabel warga
  - Syntax
    ```sql
    CREATE TABLE warga (
        -> id_warga VARCHAR(10) PRIMARY KEY NOT NULL,
        -> nama VARCHAR(45) NOT NULL,
        -> alamat VARCHAR(45) NOT NULL,
        -> no_kk VARCHAR(20) NOT NULL
        -> );
    ```
  - Output
    ![gambar](gambar/DESC%20warga.png)
- Tabel transaksi pembayaran
  - Syntax
    ```sql
    CREATE TABLE t_pembayaran (
        -> id_pembayaran VARCHAR(10) PRIMARY KEY NOT NULL,
        -> id_warga VARCHAR(10),
        -> id_iuran VARCHAR(10),
        -> tanggal DATE,
        -> jumlah DECIMAL(20) NOT NULL
        -> );
    ```
  - Output
    ![gambar](gambar/DESC%20t_pembayaran.png)
- Tabel iuran
  - Syntax
    ```sql
     CREATE TABLE iuran (
        -> id_iuran VARCHAR(10) PRIMARY KEY NOT NULL,
        -> jenis VARCHAR(25) NOT NULL,
        -> jumlah DECIMAL(20) NOT NULL
        -> );
    ```
  - Output
    ![gambar](gambar/DESC%20iuran.png)
- Tabel laporan transaksi
  - Syntax
    ```sql
    CREATE TABLE l_transaksi (
        -> id_laporan VARCHAR(10) PRIMARY KEY NOT NULL,
        -> id_iuran VARCHAR(10),
        -> tanggal DATE NOT NULL,
        -> deskripsi VARCHAR(45)
        -> );
    ```
  - Output
    ![gambar](gambar/DESC%20l_transaksi.png)

4. Menambahkan FOREIGN KEY dan CONSTRAINT pada setiap tabel yang memiliki hubungan

- Tabel transaksi pembayaran
  - Syntax
    ```sql
    ALTER TABLE t_pembayaran
        -> ADD CONSTRAINT fk_p_warga
        -> FOREIGN KEY (id_warga) REFERENCES warga(id_warga);
    ```
- Tabel transaksi pembayaran
  - Syntax
    ```sql
    ALTER TABLE t_pembayaran
        -> ADD CONSTRAINT fk_p_iuran
        -> FOREIGN KEY (id_iuran) REFERENCES iuran(id_iuran);
    ```
- Tabel laporan transaksi
  - Syntax
    ```sql
    ALTER TABLE l_transaksi
        -> ADD CONSTRAINT fk_LT_iuran
        -> FOREIGN KEY (id_iuran) REFERENCES iuran(id_iuran);
    ```

5. Memasukan data pada setiap tabel

- Tabel warga
  - Syntax
    ```sql
    INSERT INTO warga (id_warga,nama,alamat,no_kk)
        -> VALUES ('W001','John Doe','Jalan ABC No.123','123456'),
        -> ('W002','Jane Smith','Jalan XYZ No.456','789652'),
        -> ('W003','Mark Johnson','Jalan PQR No.345','887766');
    ```
  - Output
    ![gambar](gambar/SELECT%20FROM%20warga.png)
- Tabel transaksi pembayaran
  - Syntax
    ```sql
     INSERT INTO iuran (id_iuran,jenis,jumlah)
        -> VALUES ('I001','Iuran Bulanan','50000'),
        -> ('I002','Iuran Keamanan','100000'),
        -> ('I003','Iuran Sampah','30000');
    ```
  - Output
    ![gambar](gambar/SELECT%20FROM%20t_pembayaran.png)
- Tabel iuran
  - Syntax
    ```sql
     INSERT INTO t_pembayaran (id_pembayaran,id_warga,id_iuran,tanggal,jumlah)
        -> VALUES ('P001','W001','I001','2023-01-05','50000'),
        -> ('P002','W001','I002','2023-02-10','100000'),
        -> ('P003','W002','I001','2023-02-15','50000'),
        -> ('P004','W003','I001','2023-03-02','50000'),
        -> ('P005','W003','I003','2023-03-10','30000');
    ```
  - Output
    ![gambar](gambar/SELECT%20FROM%20iuran.png)
- Tabel laporan transaksi
  - Syntax
    ```sql
    INSERT INTO l_transaksi (id_laporan,id_iuran,tanggal,deskripsi)
        -> VALUES ('L001','I001','2023-01-31','Laporan Bulanan Januari'),
        -> ('L002','I002','2023-02-28','Laporan Bulanan Februari'),
        -> ('L003','I003','2023-03-31','Laporan Bulanan Maret');
    ```
  - Output
    ![gambar](gambar/SELECT%20FROM%20l_transaksi.png)

6. Melakukan JOIN Tabel

- JOIN antara tabel Transaksi Pembayaran Iuran dan Warga (KK) berdasarkan ID Warga:
  - Syntax
    ```sql
    SELECT t_pembayaran.*, warga.nama AS 'Nama Warga'
        -> FROM t_pembayaran
        -> JOIN warga ON t_pembayaran.id_warga = warga.id_warga;
    ```
  - Output
    ![gambar](gambar/JOIN%201.png)
- JOIN antara tabel Transaksi Pembayaran Iuran, Jenis Iuran, dan Warga (KK) berdasarkan ID Iuran dan ID Warga:
  - Syntax
    ```sql
    SELECT t_pembayaran.*, iuran.jenis, warga.nama AS 'Nama Warga', iuran.jumlah AS 'Jumlah Iuran'
        -> FROM t_pembayaran
        -> INNER JOIN iuran ON t_pembayaran.id_iuran = iuran.id_iuran
        -> LEFT JOIN warga ON t_pembayaran.id_warga = warga.id_warga;
    ```
  - Output
    ![gambar](gambar/JOIN%202.png)

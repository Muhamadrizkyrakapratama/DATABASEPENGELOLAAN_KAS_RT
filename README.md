# DATABASEPENGELOLAAN_KAS_RT
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
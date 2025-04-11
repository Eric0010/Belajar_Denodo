
# Mini Project: Aggregate View Transaksi Pelanggan Multi-Source (Denodo)

## Tujuan
Membuat Aggregate View (Summary) yang menyajikan total transaksi per pelanggan, berdasarkan data dari 3 sumber berbeda:

- MySQL: Data pelanggan (`customers`)
- PostgreSQL: Data transaksi (`transactions`)
- CSV File: Data demografi (`demografi.csv`)

---

## 1. Struktur Tabel dan Data Dummy

### 📦 MySQL: Tabel `customers`

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100)
);

INSERT INTO customers (customer_id, name, email) VALUES
(1, 'Andi', 'andi@mail.com'),
(2, 'Budi', 'budi@mail.com'),
(3, 'Citra', 'citra@mail.com');
```

---

### 💰 PostgreSQL: Tabel `transactions`

```sql
CREATE TABLE transactions (
    transaction_id SERIAL PRIMARY KEY,
    customer_id INT,
    transaction_date DATE,
    amount NUMERIC(10, 2)
);

INSERT INTO transactions (customer_id, transaction_date, amount) VALUES
(1, '2024-01-10', 100000),
(2, '2024-02-15', 200000),
(1, '2024-03-01', 150000);
```

---

### 🗂️ CSV File: `demografi.csv`

```csv
customer_id,gender,age,city
1,Male,30,Jakarta
2,Female,25,Bandung
3,Female,40,Surabaya
```

---

## 2. Langkah-langkah di Denodo

### 2.1 Buat Data Source
- MySQL → JDBC Data Source → Import `customers`
- PostgreSQL → JDBC Data Source → Import `transactions`
- CSV → Delimited File → Import `demografi.csv`

### 2.2 Join Ketiganya
- Buat Join View → `customers` + `transactions` + `demografi`
- Gunakan `LEFT JOIN` agar pelanggan tanpa transaksi tetap muncul
- Simpan sebagai: `vw_data_pelanggan_lengkap`

---

## 3. Buat Selection View Agregat

### 3.1 Klik Kanan → New → Selection
Dari `vw_data_pelanggan_lengkap`

### 3.2 Pilih Kolom Output
- customer_id, name, email, gender, age, city
- `SUM(amount)` → total_amount
- `COUNT(transaction_id)` → jumlah_transaksi

### 3.3 Masukkan ke Group By:
- customer_id, name, email, gender, age, city

### 3.4 Simpan View
Misalnya beri nama: `vw_summary_transaksi_pelanggan`

---

## 4. Hasil Akhir yang Diharapkan

| customer_id | name  | email           | gender | age | city     | jumlah_transaksi | total_amount |
|-------------|-------|------------------|--------|-----|----------|------------------|--------------|
| 1           | Andi  | andi@mail.com    | Male   | 30  | Jakarta  | 2                | 250000       |
| 2           | Budi  | budi@mail.com    | Female | 25  | Bandung  | 1                | 200000       |
| 3           | Citra | citra@mail.com   | Female | 40  | Surabaya | 0                | NULL         |

---

## 5. Bonus: Expose as REST API

- Klik kanan `vw_summary_transaksi_pelanggan`
- `Publish → REST Web Service`
- Akses via URL seperti:

```
http://<host>:9090/server/admin/vw_summary_transaksi_pelanggan/?$format=json
```


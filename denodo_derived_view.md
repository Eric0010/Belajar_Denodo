
# 📘 Denodo - Pembuatan Derived View (tanpa parameter)

## 🧱 Base Views yang Digunakan

### 1. `pelanggan` (MySQL)
```sql
CREATE TABLE pelanggan (
  customer_id INT PRIMARY KEY,
  name VARCHAR(100),
  city VARCHAR(100),
  age INT
);

INSERT INTO pelanggan VALUES
(1, 'Andi', 'Jakarta', 30),
(2, 'Budi', NULL, 45),
(3, 'Citra', 'Surabaya', 22),
(4, 'Dedi', 'Bandung', 40),
(5, 'Eka', NULL, 28);
```

### 2. `transaksi` (PostgreSQL)
```sql
CREATE TABLE transaksi (
  transaction_id SERIAL PRIMARY KEY,
  customer_id INT,
  transaction_date DATE,
  amount NUMERIC(12,2)
);

INSERT INTO transaksi (customer_id, transaction_date, amount) VALUES
(1, '2024-01-01', 300000),
(1, '2024-02-01', 800000),
(2, '2024-01-15', 200000),
(4, '2024-01-20', 600000),
(5, '2024-03-10', 100000);
```

## 🛠 Derived View Tahap 1: `pelanggan_transaksi_view`

Gabungkan `pelanggan` dan `transaksi`:

```sql
SELECT 
  p.customer_id,
  p.name,
  p.city,
  p.age,
  t.transaction_date,
  t.amount
FROM pelanggan p
LEFT JOIN transaksi t ON p.customer_id = t.customer_id
```

Disimpan sebagai: `pelanggan_transaksi_view`

## 🧠 Derived View Tahap 2: `total_transaksi_per_pelanggan`

Menghitung total transaksi:

```sql
SELECT
  customer_id,
  name,
  city,
  age,
  SUM(amount) AS total_transaksi
FROM pelanggan_transaksi_view
GROUP BY customer_id, name, city, age
```

Disimpan sebagai: `total_transaksi_per_pelanggan`

## 🧠 Derived View Tahap 3: `laporan_status_pelanggan`

Menambahkan logika `CASE` dan `COALESCE`:

```sql
SELECT
  customer_id,
  name,
  COALESCE(city, 'Tidak Diketahui') AS kota,
  age,
  total_transaksi,
  CASE 
    WHEN total_transaksi >= 1000000 THEN 'Sangat Aktif'
    WHEN total_transaksi >= 500000 THEN 'Aktif'
    ELSE 'Pasif'
  END AS status_pelanggan
FROM total_transaksi_per_pelanggan
WHERE age > 25 AND total_transaksi > 500000
```

Disimpan sebagai: `laporan_status_pelanggan`

## ✅ Hasil Akhir Contoh:

| customer_id | name  | kota     | age | total_transaksi | status_pelanggan |
|-------------|-------|----------|-----|------------------|------------------|
| 1           | Andi  | Jakarta  | 30  | 1100000          | Sangat Aktif     |
| 4           | Dedi  | Bandung  | 40  | 600000           | Aktif            |

## 📝 Catatan
- Semua view dibuat lewat **Design Studio UI → Create Selection → Save as View**
- Tidak menggunakan parameter atau REST API

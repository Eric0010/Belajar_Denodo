
# Membuat Aggregate View di Denodo: Total Transaksi per Pelanggan

## Tujuan
Membuat tampilan (view) agregat yang menampilkan total transaksi dan jumlah transaksi per pelanggan berdasarkan data gabungan multi-source (MySQL, PostgreSQL, CSV).

---

## 1. Sumber Data

Gunakan hasil join dari 3 sumber sebagai input view:

- `customers` (MySQL)
- `transactions` (PostgreSQL)
- `demografi.csv` (CSV)

Contoh nama view gabungan: `vw_data_pelanggan_lengkap`

---

## 2. Langkah-langkah di Denodo Design Studio

### 2.1 Buat Selection View
- Klik kanan view `vw_data_pelanggan_lengkap` → `New → Selection`

### 2.2 Pilih Kolom Output
Centang atau tambahkan kolom berikut:
- `customer_id`
- `name`
- `email`
- `gender`
- `age`
- `city`
- `SUM(amount)` → beri alias: `total_amount`
- `COUNT(transaction_id)` → beri alias: `jumlah_transaksi`

### 2.3 Masukkan Kolom ke Group By
Pindah ke tab `Group By`, tambahkan kolom:
- `customer_id`
- `name`
- `email`
- `gender`
- `age`
- `city`

> Semua kolom non-agregat **wajib** masuk Group By!

### 2.4 Simpan View
- Misalnya beri nama: `vw_summary_transaksi_pelanggan`

---

## 3. Hasil yang Diharapkan

| customer_id | name  | email           | gender | age | city     | jumlah_transaksi | total_amount |
|-------------|-------|------------------|--------|-----|----------|------------------|--------------|
| 1           | Andi  | andi@mail.com    | Male   | 30  | Jakarta  | 2                | 250000       |
| 2           | Budi  | budi@mail.com    | Female | 25  | Bandung  | 1                | 200000       |
| 3           | Citra | citra@mail.com   | Female | 40  | Surabaya | 0                | NULL         |

---

## 4. Catatan Tambahan

- Gunakan `LEFT JOIN` pada join utama agar pelanggan yang belum pernah bertransaksi tetap muncul.
- Hasil ini bisa langsung di-*expose* sebagai REST API melalui `Publish → REST Web Service`.
- View ini juga bisa dikembangkan untuk menyertakan transaksi terakhir (`MAX(transaction_date)`), rata-rata, dsb.

---

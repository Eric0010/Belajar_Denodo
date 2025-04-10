
# Menambahkan Business Logic di Denodo View

## Tujuan
Panduan ini menjelaskan cara menambahkan business logic dalam Denodo menggunakan Selection View:
- Membuat calculated field (`total_price = quantity * price`)
- Menambahkan filter (`total_price > 50000`)
- Rename field agar lebih readable

---

## 1. Membuat Selection View

1. Klik kanan pada Base View (misalnya: `penjualan_sample`)
2. Pilih `New → Selection`
3. Akan terbuka editor Selection View

---

## 2. Menambahkan Calculated Field

1. Pindah ke tab `Output`
2. Klik tombol `+ New → New Field`
3. Isi kolom sebagai berikut:
   - **Field name**: `total_price`
   - **Field type**: `decimal` (atau biarkan default)
   - **Expression**: `quantity * price`
4. Klik `OK` untuk menyimpan field baru

---

## 3. Menambahkan Filter

1. Pindah ke tab `Where Conditions`
2. Klik tombol `+ Add Condition`
3. Masukkan ekspresi berikut:
   ```
   quantity * price > 50000
   ```

---

## 4. Rename Kolom (Opsional)

1. Di tab `Output`, klik ikon ✏️ pada kolom:
   - `quantity` → ubah menjadi `Jumlah`
   - `price` → ubah menjadi `Harga Satuan`
   - `total_price` → ubah menjadi `Total Pembelian`

---

## 5. Simpan View

- Klik `Save` (kanan atas)
- Beri nama View: `vw_penjualan_logikabisnis`

---

## 6. Alternatif: Query Langsung di VQL Shell

Jika ingin menggunakan langsung syntax VQL (mirip SQL), gunakan:

```sql
SELECT produk, quantity, price, quantity * price AS total_price
FROM admin.p_p_selling_sample
WHERE quantity * price > 50000
```

Gantilah `p_p_selling_sample` dengan nama view milikmu.

---

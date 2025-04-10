
# Menambahkan Business Logic di Denodo

## Tujuan
Dokumentasi ini menjelaskan cara menambahkan logika bisnis (business logic) dalam Denodo View agar lebih siap digunakan oleh pengguna akhir atau aplikasi. Fokus pada:

- Filter data
- Rename kolom
- Tambah kolom kalkulasi (calculated field)
- Data masking (untuk role-based access, secara umum)

---

## 1. Tambah Calculated Field (Kolom Hitungan)

Contoh: ingin menambahkan kolom `total_price = quantity * price`

### Langkah:

1. Klik kanan pada Base View, pilih `New → Selection`
2. Pindah ke tab `Output`
3. Klik `+ New → New Field`
4. Isi:
   - **Field name**: `total_price`
   - **Expression**: `quantity * price`
5. Klik `OK` dan `Save`

---

## 2. Filter Baris Tertentu

Contoh: hanya tampilkan data `total_price > 50000`

### Langkah:

1. Di dalam Selection View, buka tab `Where Conditions`
2. Klik `+ Add Condition`
3. Masukkan ekspresi:
   ```
   quantity * price > 50000
   ```
4. Klik `Save`

---

## 3. Rename Kolom

Agar nama kolom lebih mudah dibaca atau sesuai kebutuhan pengguna akhir.

### Langkah:

1. Di tab `Output`, klik ikon pensil pada kolom yang ingin diubah
2. Ganti:
   - `quantity` → `Jumlah`
   - `price` → `Harga Satuan`
   - `total_price` → `Total Pembelian`
3. Klik `Save`

---

## 4. (Opsional) Data Masking / Role-Based Access

Denodo mendukung masking data berdasarkan peran user (role) melalui fitur:
- **Row Restrictions**
- **Column Privileges**
- **Data Catalog Role Rules**

Pengaturan dilakukan melalui Denodo VDP Admin atau Data Catalog.

---

## 5. Simpan dan Uji View

1. Simpan hasil Selection View, beri nama: `vw_penjualan_logikabisnis`
2. Klik dua kali View → `Execution Panel` → klik `Execute`

---

## 6. Contoh Query Langsung (Opsional)

```sql
SELECT produk, quantity, price, quantity * price AS total_price
FROM admin.penjualan_sample
WHERE quantity * price > 50000
```

Gantilah `penjualan_sample` dengan nama View yang digunakan.

---

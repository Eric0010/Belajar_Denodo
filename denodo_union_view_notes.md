
# Denodo Union View: Gabungkan File CSV dan Excel

## Tujuan
Panduan ini menjelaskan cara membuat Union View di Denodo dengan menggabungkan file CSV dan Excel. Termasuk langkah upload file, setting Column Delimiter, dan membersihkan data header ganda.

---

## 1. Upload File CSV dan Excel

### A. Upload File CSV (`transaksi_2023.csv`)
1. Buka Denodo Design Studio
2. Klik `New → Data Source → Delimited File`
3. Pilih file `transaksi_2023.csv`
4. Isi kolom konfigurasi sebagai berikut:
   - **Name**: transaksi_2023
   - **Column Delimiter**: `,`
   - **First row contains headers**: dicentang (Yes)
5. Klik `Save`
6. Klik kanan pada data source → `Create Base View`

### B. Upload File Excel (`transaksi_2024.xlsx`)
1. Klik `New → Data Source → Excel`
2. Pilih file `transaksi_2024.xlsx`
3. Isi konfigurasi:
   - **Name**: transaksi_2024
   - Pilih sheet yang sesuai
4. Klik `Save`
5. Klik kanan pada data source → `Create Base View`

---

## 2. Membuat Union View

1. Klik `New → Union`
2. Tambahkan kedua Base View:
   - transaksi_2023
   - transaksi_2024
3. Pilih tipe Union:
   - Jika struktur kolom sama persis: pilih `UNION (Standard SQL)`
   - Jika struktur berbeda: pilih `UNION (Extended)`
4. Pastikan kolom termapping dengan benar
5. Klik `Next`, pilih kolom output
6. Klik `Save` → beri nama: `vw_union_transaksi`

---

## 3. Menangani Duplikat Header dari CSV/Excel

Jika hasil Union masih mengandung baris header seperti:
```
tanggal | produk | jumlah | total
```
Gunakan query berikut untuk menghapus baris tersebut:

```sql
SELECT *
FROM admin.transaksi_u_transaksi_2024
WHERE column0 <> 'tanggal'
CONTEXT ('cache_wait_for_load' = 'true')
TRACE
```

Catatan:
- Jika nama kolom sudah dikenali dengan benar, ganti `column0` menjadi `tanggal`:
  ```sql
  WHERE tanggal <> 'tanggal'
  ```

---

## 4. Validasi dan Preview

1. Klik view `vw_union_transaksi`
2. Klik tab `Execution Panel`
3. Klik `Execute` untuk melihat data hasil gabungan

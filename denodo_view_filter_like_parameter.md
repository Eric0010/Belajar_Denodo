
# Denodo - Membuat View dengan Filter LIKE dan Parameter (Web-Based Design Studio)

## Tujuan
Membuat view turunan dari `admin.kastamers_j_demografi_j_transactions` yang dapat menampilkan data berdasarkan filter kolom `city` menggunakan parameter dinamis dan operator LIKE.

## Sumber Data

View awal: `admin.kastamers_j_demografi_j_transactions`  
Kolom-kolom yang tersedia:

- `customer_id`
- `name`
- `email`
- `gender`
- `age`
- `city`
- `jumlah_transaksi`
- `total_amount`

## Langkah-langkah Pembuatan View dengan Filter LIKE

### 1. Membuat View Turunan dari GUI

1. Buka Denodo Design Studio:
   ```
   http://10.100.13.205:9090/denodo-design-studio/#/
   ```

2. Klik kanan pada view `admin.kastamers_j_demografi_j_transactions`
3. Pilih **New → Selection**

### 2. Menambahkan Parameter

1. Masuk ke tab **View Parameters**
2. Klik tombol **➕**
   - Name: `input_city`
   - Type: `text`
   - Centang "Mandatory" jika ingin parameter ini wajib diisi

### 3. Menambahkan Filter LIKE

1. Masuk ke tab **Where**
2. Tambahkan filter berikut:
   ```sql
   city LIKE '%' || input_city || '%'
   ```

### 4. Menyimpan View

- Simpan dengan nama: `admin.kastamers_by_city_like`

### 5. Preview dan Input Nilai Parameter

1. Klik kanan pada view `admin.kastamers_by_city_like`
2. Pilih **Preview**
3. Saat diminta, masukkan nilai parameter misalnya: `jak` → maka akan mencocokkan dengan `Jakarta`

## Contoh Output yang Diharapkan

| customer_id | name  | city     | masked_email     | total_amount |
|-------------|-------|----------|------------------|--------------|
| 1           | Andi  | Jakarta  | a***@mail.com    | 250000       |
| ...         | ...   | Jakarta  | ...              | ...          |

## Catatan Penting

- Gunakan operator `||` untuk menggabungkan string di Denodo (bukan `+` seperti SQL biasa)
- Untuk penanganan koneksi error (misalnya `Communications link failure`), pastikan database source online dan bisa dijangkau dari server Denodo
- Fitur parameterized filtering hanya bisa dibuat lewat GUI (bukan VQL Shell)
- Untuk sumber data yang tidak membutuhkan koneksi ke luar, gunakan file CSV yang di-upload ke Denodo sebagai data source alternatif

## Troubleshooting

Jika muncul error seperti:

```
JDBC ROUTE [CONNECTION_ERROR] Unexpected error creating a connection: Communications link failure
```

Pastikan:
- Service database aktif
- Host dan port yang digunakan benar
- Tidak ada firewall atau network rule yang menghalangi
- Gunakan fitur “Test Connection” di halaman data source Denodo

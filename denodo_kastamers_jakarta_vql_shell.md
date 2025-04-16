
# Denodo - Membuat View Filter Data Kota Menggunakan VQL Shell (Web-Based Design Studio)

## Tujuan
Membuat view baru `admin.kastamers_jakarta` dari `admin.kastamers_j_demografi_j_transactions` yang hanya menampilkan data pelanggan dari kota Jakarta. Proses dilakukan menggunakan perintah VQL langsung melalui VQL Shell di Denodo Design Studio versi web-based.

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

## Langkah-langkah

### 1. Buka VQL Shell

1. Akses Denodo Design Studio:
   ```
   http://10.100.13.205:9090/denodo-design-studio/#/
   ```

2. Masuk ke tab **VQL Shell** di bagian atas

### 2. Jalankan Perintah VQL

Tempel dan jalankan perintah berikut:

```sql
CREATE OR REPLACE VIEW admin.kastamers_jakarta AS
SELECT
  customer_id,
  name,
  email,
  gender,
  age,
  city,
  jumlah_transaksi,
  total_amount
FROM admin.kastamers_j_demografi_j_transactions
WHERE city = 'Jakarta';
```

### 3. Simpan dan Preview View Baru

1. Setelah perintah berhasil dijalankan, view `admin.kastamers_jakarta` akan muncul di folder `admin`
2. Klik kanan pada view tersebut
3. Pilih **Preview** untuk melihat hasil data yang difilter khusus kota Jakarta

## Output yang Diharapkan

| customer_id | name  | email            | gender | age | city    | jumlah_transaksi | total_amount |
|-------------|-------|------------------|--------|-----|---------|------------------|---------------|
| 1           | Andi  | andi@mail.com    | Male   | 30  | Jakarta | 2                | 250000        |
| ...         | ...   | ...              | ...    | ... | Jakarta | ...              | ...           |

## Catatan Tambahan

- View ini hanya menampilkan data pelanggan dengan `city = 'Jakarta'`
- Proses filter dilakukan langsung di query, tanpa menggunakan parameter
- Cocok digunakan saat ingin membatasi hasil berdasarkan kriteria tetap (bukan dinamis)
- Jika ingin membuat filter dinamis berdasarkan parameter, gunakan fitur **View Parameters** melalui GUI


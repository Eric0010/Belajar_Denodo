
# Denodo - Membuat View dengan Data Masking (Web-Based Design Studio)

## Tujuan
Membuat view baru dari `admin.kastamers_j_demografi_j_transactions` yang menerapkan masking pada kolom `email` dan membersihkan nilai `null` pada `total_amount`.

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

### 1. Buka Denodo Design Studio
Masuk ke alamat:
```
http://10.100.13.205:9090/denodo-design-studio/#/
```

### 2. Buka VQL Shell
Akses tab **VQL Shell** untuk mengeksekusi perintah langsung dalam format VQL.

### 3. Buat View Baru dengan Masking
Jalankan perintah berikut di VQL Shell:

```sql
CREATE OR REPLACE VIEW admin.kastamers_masked AS
SELECT
  customer_id,
  name,
  gender,
  age,
  city,
  jumlah_transaksi,

  -- Masking untuk kolom email
  substring(email, 1, 1) || '***@' || substring(email, instr(email, '@') + 1) AS masked_email,

  -- Penanganan nilai null pada total_amount
  case
    when total_amount is null then 0
    else total_amount
  end AS total_amount_clean

FROM admin.kastamers_j_demografi_j_transactions;
```

### 4. Simpan dan Preview View Baru
Setelah perintah berhasil dieksekusi, view baru `admin.kastamers_masked` akan tersedia di katalog.  
Klik kanan pada view tersebut → **Preview** untuk melihat hasilnya.

### 5. (Opsional) Publish ke REST API
Jika ingin mengakses view ini melalui REST API:
1. Klik kanan pada `admin.kastamers_masked`
2. Pilih **Publish** → **REST Web Service**
3. Ikuti petunjuk untuk mengaktifkan endpoint REST
4. Akses data via:
   ```
   http://<denodo-host>:9090/server/rest/<database-name>/admin/kastamers_masked
   ```

## Hasil Output yang Diharapkan

| customer_id | name  | gender | age | city     | jumlah_transaksi | masked_email     | total_amount_clean |
|-------------|-------|--------|-----|----------|------------------|------------------|---------------------|
| 1           | Andi  | Male   | 30  | Jakarta  | 2                | a***@mail.com    | 250000              |
| 2           | Budi  | Female | 25  | Bandung  | 1                | b***@mail.com    | 200000              |
| 3           | Citra | Female | 40  | Surabaya | 0                | c***@mail.com    | 0                   |

## Catatan Tambahan

- Fungsi `||` digunakan sebagai operator untuk menggabungkan teks (concat) di Denodo.
- Gunakan `case when ... then ... end` sebagai pengganti `ifnull()` untuk penanganan null.
- Anda juga dapat mengubah nama alias dari `masked_email` menjadi `email` jika ingin mengganti kolom aslinya.

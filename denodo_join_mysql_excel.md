
# Denodo Join: MySQL Table and Excel File

## Tujuan
Membuat join view di Denodo yang menggabungkan data dari dua sumber berbeda:
- Tabel dari database MySQL
- File Excel yang diupload ke Denodo

## Prasyarat
- Denodo Design Studio aktif
- Sudah ada koneksi ke MySQL dan file Excel sebagai Data Source
- Sudah dibuat Base View dari masing-masing sumber data

## Langkah-langkah

### 1. Siapkan Base View
- Base View dari MySQL: misalnya `customers`
- Base View dari Excel: misalnya `pelanggan_status`

Kedua view ini harus memiliki kolom join yang sama, misalnya `customer_id`.

### 2. Buat Join View
1. Klik menu `New` lalu pilih `Join`
2. Akan terbuka Join Editor

### 3. Tambahkan View ke Join Editor
- Drag & drop Base View `customers` dari MySQL
- Drag & drop Base View `pelanggan_status` dari Excel

### 4. Buat Join Condition
- Hubungkan kolom `customer_id` dari kedua view
- Secara otomatis akan muncul join condition:
  ```
  customers.customer_id = pelanggan_status.customer_id
  ```

- Pilih jenis join:
  - Inner Join: hanya data yang cocok di kedua sumber
  - Left Join: semua data dari MySQL, cocokkan jika ada di Excel

### 5. Pilih Kolom Output
- Pilih kolom-kolom yang ingin ditampilkan dari kedua view
  Contoh: `name`, `email`, `status`, `segment`

### 6. Simpan View
- Klik `Next`, lalu `Save`
- Beri nama view: `vw_customers_joined`

### 7. Preview Data
- Klik dua kali view `vw_customers_joined`
- Masuk ke tab `Execution Panel`
- Klik `Execute` untuk melihat hasil join

## Contoh Hasil
| customer_id | name  | email          | city     | status   | segment    |
|-------------|-------|----------------|----------|----------|------------|
| 1           | Andi  | andi@mail.com  | Jakarta  | Active   | Premium    |
| 2           | Budi  | budi@mail.com  | Bandung  | Inactive | Basic      |
| 3           | Citra | citra@mail.com | Surabaya | Active   | Enterprise |


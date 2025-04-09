
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

### A. Buat dan Isi Tabel MySQL

#### 1.1 Buat Tabel `customers`
Gunakan perintah SQL berikut di MySQL:

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100),
    city VARCHAR(50)
);
```

#### 1.2 Masukkan Data ke Tabel `customers`

```sql
INSERT INTO customers (customer_id, name, email, city) VALUES
(1, 'Andi', 'andi@mail.com', 'Jakarta'),
(2, 'Budi', 'budi@mail.com', 'Bandung'),
(3, 'Citra', 'citra@mail.com', 'Surabaya');
```

---

### B. Upload dan Import File Excel ke Denodo

#### 1.3 Buat File Excel
Buat file bernama `pelanggan_status.xlsx` dengan isi sebagai berikut:

| customer_id | status   | segment    |
|-------------|----------|------------|
| 1           | Active   | Premium    |
| 2           | Inactive | Basic      |
| 3           | Active   | Enterprise |

#### 1.4 Upload Excel ke Denodo

1. Masuk ke Denodo Design Studio
2. Klik `New → Data Source → Excel`
3. Beri nama (misalnya: `excel_status`)
4. Klik `Browse` dan upload file `pelanggan_status.xlsx`
5. Pilih sheet/tab yang berisi data
6. Klik `Save`
7. Setelah tersimpan, klik kanan pada data source → `Create Base View`
8. Pilih sheet dan klik `Create`

---

### C. Buat Base View dari MySQL

1. Klik kanan pada koneksi MySQL yang sudah dibuat sebelumnya
2. Pilih `Create Base View`
3. Pilih tabel `customers`
4. Klik `Create`

Sekarang kamu memiliki dua Base View:
- `customers` dari MySQL
- `pelanggan_status` dari Excel

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


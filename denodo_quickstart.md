
# 🚀 Denodo Quickstart Guide

## 🎯 Tujuan
Panduan ini membantu pengguna baru Denodo untuk:
1. Menghubungkan berbagai sumber data (MySQL, Excel/CSV, dsb)
2. Membuat **Base View**
3. Menyiapkan JDBC driver (MySQL `.jar`) yang dibutuhkan

---

## ✅ 1. Connect ke Data Source

### A. MySQL

#### 🔧 Persiapan
- Install & jalankan MySQL (local atau remote)
- Siapkan:
  - Hostname/IP
  - Port (default: `3306`)
  - Username & password
  - Nama database
- Download JDBC driver MySQL:  
  👉 [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

> File yang dibutuhkan: `mysql-connector-j-8.x.x.jar`

---

### 📦 Upload MySQL JDBC Driver ke Denodo

1. Buka **Design Studio**
2. Klik menu atas: `File → Extension Management`
3. Buka tab **Libraries**
4. Pilih adapter: `mysql-8`
5. Klik `Upload`, lalu pilih file:  
   `mysql-connector-j-8.3.0.jar`
6. Klik `Apply Changes`

> ⚠️ Jika tidak langsung terdeteksi, restart VDP Server via Denodo Platform Control Center.

---

### 🔗 Buat Data Source: MySQL

1. Klik `New → Data Source → JDBC`
2. Pilih adapter: `mysql-8`
3. Isi detail koneksi:
   ```
   Name: mysql_conn
   URI: jdbc:mysql://localhost:3306/namadb
   Username: root
   Password: *****
   ```
4. Klik **Test Connection**
5. Klik **Save**

---

### B. Excel / CSV

1. Klik `New → Data Source → Excel`
2. Upload file `.xlsx` atau `.csv`
3. Pilih sheet → klik **Create Base View**

---

## ✅ 2. Buat Base View

### 📥 Dari Tabel atau File
1. Setelah Data Source sukses, klik kanan → **Create Base View**
2. Pilih:
   - Tabel dari database
   - Sheet/tab dari Excel
3. Klik **Create**

### 🔍 Preview Data
- Klik 2x nama View → tab **Execution Panel**
- Klik `Execute` untuk lihat data

---

## 💡 Tips Tambahan:
- Gunakan `Create Base View from Query` jika ingin ambil data via SQL
- Semua data bersifat virtual — Denodo tidak menyimpan data
- Kamu bisa gabungkan (join), filter, dan expose sebagai REST API

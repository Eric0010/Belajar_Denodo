
# Expose Denodo View as REST API

## Tujuan
Membuat endpoint REST API dari Virtual View di Denodo agar bisa diakses dari aplikasi lain (frontend, backend, Postman, dsb).

---

## 1. Syarat Awal
- View sudah tersedia di Denodo (Base View atau Derived View)
- Denodo RESTful Web Services aktif (default di port 9090)

---

## 2. Langkah-langkah Publish REST API

### 2.1 Buka Denodo Design Studio
- Masuk ke Virtual Database (contoh: `admin`)

### 2.2 Klik Kanan View → Publish → REST Web Service
- Pilih View, misalnya: `transaksi_u_transaksi_2024`
- Klik `Publish → REST Web Service`

### 2.3 Carilah REST Web Service
- Di dalam sideview menu, terdapat REST Web Service (transaksi_u_transaksi_2024)
- Klik `3 dot → Launch Web Service URL`, lalu akan muncul URL seperti berikut:
  
  Contoh:
  ```
  http://10.100.13.205:9090/server/admin/transaksi_u_transaksi_2024/
  ```

---

## 3. Cara Akses dari Browser atau Postman

### 3.1 Akses via Browser
- Buka URL:
  ```
  http://10.100.13.205:9090/server/admin/transaksi_u_transaksi_2024/
  ```
- Masukkan username/password Denodo saat diminta

### 3.2 Akses dengan Output JSON
Tambahkan format di URL:
```
http://10.100.13.205:9090/server/admin/transaksi_u_transaksi_2024/?$format=json
```

### 3.3 Akses dengan Postman
1. Method: `GET`
2. URL:
   ```
   http://10.100.13.205:9090/server/admin/transaksi_u_transaksi_2024/?$format=json
   ```
3. Tab Authorization:
   - Type: Basic Auth
   - Username: `admin`
   - Password: (password Denodo)

---

## 4. Catatan Tambahan
- REST API Denodo bersifat read-only
- Output bisa diatur dalam format: JSON, XML, CSV
- Bisa ditambahkan parameter di URL sebagai filter
- Endpoint ini bisa digunakan untuk integrasi dengan aplikasi, reporting tools, bahkan AI Agent / LangChain

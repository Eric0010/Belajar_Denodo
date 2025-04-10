
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

## 3. Cara Akses dari Browser, Postman, dan curl

### 3.1 Akses via Browser
- Buka URL:
```
http://10.100.13.205:9090/server/admin/transaksi_u_transaksi_2024/
```
- Masukkan username/password Denodo saat diminta

### 3.2 Akses dengan Output JSON (curl)
```bash
curl -X 'GET' \
  'http://10.100.13.205:9090/server/admin/customers_j_excel_tes/views/customers_j_excel_tes?%24displayRESTfulReferences=true&%24format=JSON' \
  -H 'accept: application/xml;charset=UTF-8;subtype=denodo-9'
```

### 3.3 Akses dengan Output XML (curl)
```bash
curl -X 'GET' \
  'http://10.100.13.205:9090/server/admin/customers_j_excel_tes/views/customers_j_excel_tes?$format=xml' \
  -u admin:admin \
  -H 'Accept: application/xml'
```

---

## 4. Catatan Tambahan

- REST API Denodo bersifat **read-only secara default**
- Output bisa diatur dalam format: **JSON**, **XML**, **CSV**
- Bisa ditambahkan parameter di URL sebagai filter (misal: `?city=Jakarta`)
- Endpoint ini bisa digunakan untuk integrasi dengan aplikasi, reporting tools, bahkan AI Agent / LangChain

---

## 5. Reminder Mengenai Method POST

### POST hanya diperbolehkan untuk View yang berasal dari:
- **Base Table di Database** (MySQL, PostgreSQL, dll via JDBC)
- Telah dipublish sebagai REST Web Service dan **diaktifkan opsi `INSERT`**

### POST tidak diperbolehkan untuk:
- View dari **Excel, CSV, REST API**
- **Join View**, **Union View**, atau **Selection View**
- View yang berasal dari sumber **non-relational**

---

## 6. Contoh Method POST

### 6.1 POST JSON ke Tabel MySQL (View: users)
```bash
curl -X POST \
  "http://10.100.13.205:9090/server/admin/users/views/users" \
  -u admin:admin \
  -H "Content-Type: application/json" \
  -d '{
    "id": 5,
    "name": "andi"
}'
```

### 6.2 POST XML ke Tabel MySQL (View: users)
```bash
curl -X 'POST' \
  'http://10.100.13.205:9090/server/admin/users/views/users' \
  -H 'accept: */*' \
  -H 'Content-Type: application/xml' \
  -d '<?xml version="1.0" encoding="UTF-8"?>
<users xmlns="http://www.denodo.com/restful/admin/views/users">
    <id>0</id>
    <name>string</name>
</users>'
```

---

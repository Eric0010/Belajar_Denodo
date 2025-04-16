
# Denodo - REST API dengan Filtering Dinamis via Query Parameter

## Tujuan
Membuat dan mengakses REST API dari view `vw_kastamers_semantic` di Denodo, serta menggunakan query parameter pada URL untuk melakukan filtering data secara dinamis.

## Prasyarat
- View `vw_kastamers_semantic` telah tersedia di database `admin`
- View telah dipublish sebagai REST Web Service melalui Denodo Design Studio Web-Based
- Akses ke URL Denodo REST: `http://10.100.13.205:9090/server/admin/vw_kastamers_semantic`

## Struktur Data View
Kolom-kolom utama dari view:

- `IDPelanggan`
- `NamaLengkap`
- `AlamatEmail`
- `JenisKelamin`
- `Umur`
- `Kota`
- `TotalTransaksi`
- `TotalNilaiPembelian`

## Contoh Filter yang Berhasil

### 1. Filter berdasarkan kota

Command curl:
```bash
curl -G -H "Accept: application/json" \
--data-urlencode "Kota=Jakarta" \
"http://10.100.13.205:9090/server/admin/vw_kastamers_semantic/views/vw_kastamers_semantic"
```

Response JSON:
```json
{
  "name": "vw_kastamers_semantic",
  "elements": [
    {
      "IDPelanggan": 1,
      "NamaLengkap": "Andi",
      "AlamatEmail": "andi@mail.com",
      "JenisKelamin": "Male",
      "Umur": "30",
      "Kota": "Jakarta",
      "TotalTransaksi": 2,
      "TotalNilaiPembelian": 250000.00
    }
  ],
  "links": [
    {
      "rel": "self",
      "href": "http://10.100.13.205:9090/server/admin/vw_kastamers_semantic/views/vw_kastamers_semantic?Kota=Jakarta"
    }
  ]
}
```

## Catatan

- Denodo REST API hanya mendukung filter dalam bentuk `field=value`. 
- Tidak mendukung operator seperti `>`, `<`, `>=`, `LIKE` dalam parameter URL secara langsung.
- Jika filtering lebih kompleks dibutuhkan (misalnya `TotalNilaiPembelian >= 100000`), maka disarankan membuat view dengan input parameter (`input_min_amount`) melalui GUI (New → Selection View).

## Saran Penggunaan

- Gunakan `curl` atau Postman untuk pengujian manual
- Untuk digunakan di frontend/backend, pastikan parameter URL di-encode dengan benar (gunakan `%20` untuk spasi, `%3E` untuk >, dll)
- Hindari spasi dan karakter khusus pada nama kolom view jika ingin menggunakan REST API secara maksimal

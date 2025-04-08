# Instalasi Denodo di Linux

Pertama, pergilah ke web ini:

```
https://community.denodo.com/express/download
```

lalu pilih tombol linux64. Setelah itu tunggulah download sampai selesai.

Setelah download selesai, bukalah Visual Studio code sebagai alat pembantu untuk memindahkan file denodo platform ke tujuan yang diinginkan.

Pada kali ini saya ingin memindahkan ke server kantor ADI.

Setelah dipindahkan, maka file akan terlihat seperti gambar berikut dalam format .zip

![image](https://github.com/user-attachments/assets/0e5b49ab-b8e5-46bc-9a61-aac1e0f55407)

setelah dipindahkan, jalankan command berikut ini:

```
unzip /home/denodo/denodo-express-install-9-linux64.zip -d /home/denodo/
```

Langkah Selanjutnya: Generate Konfigurasi Auto-Installer

Masuk ke folder installer:

```
cd /home/denodo/denodo-install-9
chmod +x installer_cli.sh
./installer_cli.sh install --autoinstaller /home/denodo/install.properties
```

Lalu isi wizard seperti:

|Prompt |	Jawaban|
--------| -------|
Setup type	| express (tekan Enter aja)
Installation path	| misalnya /home/denodo/denodo-platform
License file path	| /home/denodo/denodo-express-lic-9-202504.lic
Locale	| us_cst atau tekan Enter
Virtual DataPort	| full

Setelah selesai generate:

Kalau semuanya lancar, saya akan punya folder seperti:

![image](https://github.com/user-attachments/assets/65c8a6ec-897b-4612-ad0d-87234fc4b138)

Lalu pergilah ke denodo-platform/bin dan saya akan menjalankan command untuk menjalankan seervice denodo:

```
./vqlserver_shutdown.sh && ./vqlserver_startup.sh
./scheduler_shutdown.sh && ./scheduler_startup.sh
./scheduler_webadmin_startup.sh
./webcontainer.sh stop && ./webcontainer.sh start
./diagnosticmonitoringtool_startup.sh
./datacatalog_startup.sh
./designstudio_startup.sh
```

Berikut command untuk mematikan service jika dibutuhkan:

```
./vqlserver_shutdown.sh
./scheduler_shutdown.sh
./scheduler_webadmin_shutdown.sh
./webcontainer.sh stop
./diagnosticmonitoringtool_shutdown.sh
./datacatalog_shutdown.sh
./designstudio_shutdown.sh
```

Setelah semua selesai, coba buka web ini di browser lokal:

Coba akses URL spesifik Denodo Web Tools

Langsung akses ini di browser:

🔧 Web Design Studio:

```
http://<ip-server>:9090/denodo-design-studio/
```

📚 Data Catalog:
```
http://<ip-server>:9090/denodo-data-catalog/
```

📊 Diagnostic & Monitoring Tool:

```
http://<ip-server>:9090/denodo-monitor/
```

Gantilah <ip-server> dengan IP server (misalnya 10.100.13.205 atau localhost kalau via browser lokal).

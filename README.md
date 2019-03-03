# TUTORIAL PEMBUATAN MODUL SHIPPING OPENCART 2.3.0.2

## Sekilas tentang Pengaturan File di Back-End

> “Prinsip utama penempatan file modul pada opencart adalah pada folder `admin` dan `catalog` di dalamnya terdapat folder `controller`, `model`, `view` dan `language` atau dikenal dengan prinsip MVC.”

Mari kita mulai dengan daftar file yang diperlukan di back-end. Kita akan menggunakan "**sicepat**" sebagai nama metode pengiriman yang baru yang akan dibuat.

------------


### Pada Bagian Folder Admin:
- [admin/controller/extension/shipping/sicepat.php](https://github.com/farindra/oc_2.3_shipping_sicepat/blob/master/admin/controller/extension/shipping/sicepat.php "admin/controller/extension/shipping/sicepat.php"): Ini adalah file controller di mana kita akan mengatur segala yang diperlukan untuk kontrol backend formulir konfigurasi.
- [admin/view/template/extension/shipping/sicepat.tpl](https://github.com/farindra/oc_2.3_shipping_sicepat/blob/master/admin/view/template/extension/shipping/sicepat.tpl "admin/view/template/extension/shipping/sicepat.tpl"): Ini adalah file view di mana kita akan mengatur segala yang diperlukan untuk tampilan formulir konfigurasi panel admin yaitu pada menu Extentions → Extensions → Shipping.
- [admin/language/en-gb/extension/shipping/sicepat.php](https://github.com/farindra/oc_2.3_shipping_sicepat/blob/master/admin/language/en-gb/extension/shipping/sicepat.php "admin/language/en-gb/extension/shipping/sicepat.php"): Ini adalah file bahasa di mana kita akan mendefinisikan bahasa default (english) kedalam variable yang akan digunakan pada controller/view admin.
- [admin/language/id-id/extension/shipping/sicepat.php](https://github.com/farindra/oc_2.3_shipping_sicepat/blob/master/admin/language/id-id/extension/shipping/sicepat.php "admin/language/id-id/extension/shipping/sicepat.php"): Ini adalah file bahasa di mana kita akan mendefinisikan bahasa opsional ( Indonesia ) kedalam variable yang akan digunakan pada controller/view admin.

---

### Pada Bagian Folder Catalog:
- [catalog/model/extension/shipping/sicepat.php](https://github.com/farindra/oc_2.3_shipping_sicepat/blob/master/catalog/model/extension/shipping/sicepat.php "catalog/model/extension/shipping/sicepat.php"): Ini adalah file model di mana kita akan mengatur segala yang diperlukan untuk kontrol backend  metode pengiriman Sicepat seperti mendefinisikan jenis pengiriman, menghitung tarif dan untuk kasus ini melakukan integrasi dengan API Vendor Sicepat.
- [catalog/view/javascript/sicepat_origin.json.php](https://github.com/farindra/oc_2.3_shipping_sicepat/blob/master/catalog/view/javascript/sicepat_origin.json "catalog/view/javascript/sicepat_origin.json.php"): Pada kasus ini kita membutuhkan data origin ( properti region pickup toko ) oleh karena itu perlu dibuatkan database statik berupa file json yang berisikan data origin yang telah diperoleh dari vendor untuk keperluan pengecekan tariff via API.
- [catalog/language/en-gb/extension/shipping/sicepat.php](https://github.com/farindra/oc_2.3_shipping_sicepat/blob/master/catalog/language/en-gb/extension/shipping/sicepat.php "catalog/language/en-gb/extension/shipping/sicepat.php"): Ini adalah file bahasa di mana kita akan mendefinisikan bahasa default (english) kedalam variable yang akan digunakan pada controller/view catalog bagian metode pengiriman.
- [catalog/language/id-id/extension/shipping/sicepat.php](https://github.com/farindra/oc_2.3_shipping_sicepat/blob/master/catalog/language/id-id/extension/shipping/sicepat.php "catalog/language/id-id/extension/shipping/sicepat.php"): Ini adalah file bahasa di mana kita akan mendefinisikan bahasa opsional ( Indonesia ) kedalam variable yang akan digunakan pada controller/view catalog metode pengiriman.

Jika semua file telah dipersiapkan, maka strukturnya akan terbentuk seperti berikut:

```bash
├── admin
│   ├── controller
│   │   └── extension
│   │       └── shipping
│   │           └── sicepat.php
│   ├── language
│   │   ├── en-gb
│   │   │   └── extension
│   │   │       └── shipping
│   │   │           └── sicepat.php
│   │   └── id-id
│   │       └── extension
│   │           └── shipping
│   │               └── sicepat.php
│   └── view
│       └── template
│           └── extension
│               └── shipping
│                   └── sicepat.tpl
├── catalog
│   ├── language
│   │   ├── en-gb
│   │   │   └── extension
│   │   │       └── shipping
│   │   │           └── sicepat.php
│   │   └── id-id
│   │       └── extension
│   │           └── shipping
│   │               └── sicepat.php
│   ├── model
│   │   └── extension
│   │       └── shipping
│   │           └── sicepat.php
│   └── view
│       └── javascript
│           └── sicepat_origin.json

```
---
### PENJELASAN ISI DARI SETIAP FILE
Berikut ini akan dijelaskan isi dari setiap file di atas, baik itu dari class, function dan logic  yang akan digunakan. Penjelasan hanya fokus terhadap bagian yang telah dimodifikasi, tidak akan membahas bagian umum dari fungsi default opencart, untuk referensi penjelasan lebih dalam tentang opencart bisa ditemukan disini <a href="http://docs.opencart.com/en-gb/introduction/" target="_blank"><img src="http://docs.opencart.com/image/opencart-logo.png" height="15" /></a> .

admin/controller/extension/shipping/sicepat.php

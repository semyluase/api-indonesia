# API Data Wilayah Indonesia

Repository ini berisi source code untuk generate (REST) API statis berisi data wilayah Indonesia
serta perintah untuk mendeploynya ke _static hosting_ [Github Page](https://pages.github.com/).

Demo: [https://semyluase.github.io/api-indonesia/](https://semyluase.github.io/api-indonesia/)

#### Apa yang dimaksud API statis?

API statis adalah API yang _endpoint_-nya terdiri dari file statis.

#### Keuntungan API statis?

- Dapat dihosting pada _static file hosting_ seperti Github Page, Netlify, dsb.
- Proses lebih cepat karena tidak membutuhkan server-side scripting.

#### Bagaimana cara kerjanya?

- Daftar provinsi, kab/kota, kecamatan, kelurahan/desa disimpan pada folder `data` berupa file `csv` (agar mudah diedit).
- Kemudian script `generate.php` dijalankan. Script ini akan membaca file `csv` didalam folder `data`, kemudian men-generate ribuan endpoint (file) kedalam folder `static/api`.
- API siap 'dihidangkan'.

## ENDPOINTS

#### 1. Mengambil Daftar Provinsi

```
GET https://semyluase.github.io/api-indonesia/static/api/provinces.json
```

Contoh Response:

```
[
  {
    "id": "11",
    "name": "ACEH"
  },
  {
    "id": "12",
    "name": "SUMATERA UTARA"
  },
  ...
]
```

#### 2. Mengambil Daftar Kab/Kota pada Provinsi Tertentu

```
GET https://semyluase.github.io/api-indonesia/static/api/regencies/{provinceId}.json
```

Contoh untuk mengambil daftar kab/kota di provinsi Jawa Tengah (ID = 33):

```
GET https://semyluase.github.io/api-indonesia/static/api/regencies/33.json
```

Contoh Response:

```
[
  {
      "id": "3301",
      "province_id": "33",
      "name": "KABUPATEN CILACAP"
  },
  {
      "id": "3302",
      "province_id": "33",
      "name": "KABUPATEN BANYUMAS"
  },
  ...
]
```

#### 3. Mengambil Daftar Kecamatan pada Kab/Kota Tertentu

```
GET https://semyluase.github.io/api-indonesia/static/api/districts/{regencyId}.json
```

Contoh untuk mengambil daftar kecamatan di Kota Semarang (ID = 3374):

```
GET https://semyluase.github.io/api-indonesia/static/api/districts/3374.json
```

Contoh Response:

```
[
  {
    "id": "3374010",
    "regency_id": "3374",
    "name": "MIJEN"
  },
  {
    "id": "3374020",
    "regency_id": "3374",
    "name": "GUNUNG PATI"
  },
  ...
]
```

#### 4. Mengambil Daftar Kelurahan pada Kecamatan Tertentu

```
GET https://semyluase.github.io/api-indonesia/static/api/villages/{districtId}.json
```

Contoh untuk mengambil daftar kelurahan di Mijen (ID = 3374010):

```
GET https://semyluase.github.io/api-indonesia/static/api/villages/3374010.json
```

Contoh Response:

```
[
  {
    "id": "3374010001",
    "district_id": "3374010",
    "name": "CANGKIRAN",
    "postal_code": "50216"
  },
  {
    "id": "3374010002",
    "district_id": "3374010",
    "name": "BUBAKAN",
    "postal_code": "57683"
  },
  ...
]
```

#### 5. Mengambil Data Provinsi berdasarkan ID Provinsi

```
GET https://semyluase.github.io/api-indonesia/static/api/province/{provinceId}.json
```

Contoh untuk mengambil data provinsi Jawa Tengah (ID = 33):

```
GET https://semyluase.github.io/api-indonesia/static/api/province/33.json
```

Contoh Response:

```
{
    "id": "33",
    "name": "JAWA TENGAH"
}
```

#### 6. Mengambil Data Kab/Kota berdasarkan ID Kab/Kota

```
GET https://semyluase.github.io/api-indonesia/static/api/regency/{regencyId}.json
```

Contoh untuk mengambil data kabupaten Kota Semarang (ID = 3374):

```
GET https://semyluase.github.io/api-indonesia/static/api/regency/3374.json
```

Contoh Response:

```
{
    "id": "3374",
    "province_id": "33",
    "name": "KOTA SEMARANG"
}
```

#### 7. Mengambil Data Kecamatan berdasarkan ID Kecamatan

```
GET https://semyluase.github.io/api-indonesia/static/api/district/{districtId}.json
```

Contoh untuk mengambil data kecamatan Mijen (ID = 3374010):

```
GET https://semyluase.github.io/api-indonesia/static/api/district/3374010.json
```

Contoh Response:

```
{
    "id": "3374010",
    "regency_id": "3374",
    "name": "MIJEN"
}
```

#### 8. Mengambil Data Kelurahan berdasarkan ID Kelurahan

```
GET https://semyluase.github.io/api-indonesia/static/api/village/{villageId}.json
```

Contoh untuk mengambil data kelurahan Jatibarang (ID = 3374010009):

```
GET https://semyluase.github.io/api-indonesia/static/api/village/3374010009.json
```

Contoh Response:

```
{
    "id": "3374010009",
    "district_id": "3374010",
    "name": "JATIBARANG",
    "postal_code": "50219"
}
```

## LIMITASI

Karena API ini dihosting di Github Page, Github Page sendiri memberikan batasan bandwith 100GB/bulan. Rata-rata endpoint disini memiliki ukuran 1KB/endpoint, jadi kurang lebih request yang dapat digunakan adalah 100.000.000 request per bulan, atau sekitar 3.000.000 request/hari.

Karena limitasi ini, disarankan untuk hosting API ini di github kamu sendiri.

Untuk lebih detail tentang limitasi Github Page, bisa dilihat [disini](https://help.github.com/en/articles/about-github-pages#usage-limits).

# Nested Easter Egg

## Deskripsi Soal

Pada challenge ini, kamu diminta untuk menemukan Easter Egg tersembunyi yang berada di dalam beberapa lapisan fitur aplikasi.

## Identifikasi Kerentanan

Aplikasi menyembunyikan Easter Egg di endpoint atau halaman yang tidak terlihat secara langsung oleh user biasa. Biasanya, akses ke Easter Egg memerlukan eksplorasi lebih dalam, seperti mengakses endpoint tersembunyi, melakukan manipulasi parameter, atau menggabungkan beberapa teknik eksploitasi.

## Langkah Penyelesaian

1. Telusuri source code aplikasi atau gunakan tools seperti Burp Suite untuk menemukan endpoint tersembunyi.
2. Coba akses endpoint yang tidak terdokumentasi, misal: `/easter-egg`, `/api/egg`, atau `/hidden/nested-egg`.

   ![Akses Endpoint]()

3. Jika endpoint meminta token atau parameter khusus, coba gunakan token dari fitur lain atau manipulasi parameter.

   ![Token Manipulasi]()

4. Jika berhasil, kamu akan menemukan pesan atau gambar Easter Egg.

   ![Easter Egg Ditemukan]()

5. Dokumentasikan proses dan payload yang digunakan.

## Payload/Tools yang Digunakan

- Burp Suite / Postman untuk eksplorasi endpoint
- Manipulasi parameter URL
- Token dari fitur lain aplikasi
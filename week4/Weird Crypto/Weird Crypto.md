# Weird Crypto

## Deskripsi Soal
Challenge ini mencari kelemahan pada implementasi kriptografi, khususnya pada penyimpanan password.

## Identifikasi Kerentanan

Aplikasi menggunakan hash MD5 untuk menyimpan password user. MD5 sudah tidak aman karena:
- Mudah terkena brute force dan collision.
- Tidak menggunakan salt.
- Banyak hash MD5 yang sudah ada di database publik.

## Langkah Penyelesaian

1. Ambil JWT dari cookie browser.
2. Decode JWT payload menggunakan Base64 decoder.

   ![JWT Decode]()

3. Temukan hash password user, misal: `"password":"0192023a7bbd73250516f069df18b500"`

   ![Password Hash]()

4. Cek hash tersebut di situs hash lookup publik (misal: https://crackstation.net/ atau https://md5decrypt.net/).

   ![Hash Lookup]()

5. Jika hash ditemukan dan password asli diketahui, berarti aplikasi rentan.

6. Laporkan kelemahan ini melalui contact form aplikasi.

   ![Report]()

## Payload/Tools yang Digunakan

- JWT dari cookie browser
- Base64 decoder
- Hash lookup (crackstation, md5decrypt)

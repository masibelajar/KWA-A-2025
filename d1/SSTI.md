# SSTI 1

## Deskripsi Soal

Pada challenge ini, diberikan sebuah aplikasi login admin yang rentan terhadap **Server-Side Template Injection (SSTI)**.

[SSTI1](SSTI1.png)

## Identifikasi Kerentanan

Aplikasi menggunakan template engine yang tidak melakukan sanitasi input dengan baik, sehingga memungkinkan terjadinya SSTI.

## Langkah Penyelesaian

1. Buka aplikasi dan temukan form login.
   
3. Coba input payload SSTI sederhana, misal: `{{7*7}}` pada field username atau password.
   
[Login](SSTI1.1.png)
4. Jika output pada halaman berubah menjadi `49`, maka aplikasi rentan SSTI.

[Output](SSTI1.2.png)

5. Lanjutkan eksploitasi dengan payload lain, misal untuk membaca file:
   ```
   {{config.__class__.__init__.__globals__['os'].popen('cat /etc/passwd').read()}}
   ```
6. Jika berhasil, Anda dapat membaca file sensitif pada server.
7. 
[Flag](SSTI1.3)

## Payload yang Digunakan

- `{{7*7}}`
- `{{config.__class__.__init__.__globals__['os'].popen('cat /etc/passwd').read()}}`

## Referensi

- [PayloadAllTheThings - SSTI](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection)

- [OWASP SSTI](https://owasp.org/www-community/vulnerabilities/Server-Side_Template_Injection)


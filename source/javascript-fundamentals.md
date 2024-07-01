<h1 align="center" style="text-align: center;">JavaScript Fundamentals</h1>

## Apa itu JavaScript?

JavaScript adalah bahasa pemrograman tingkat tinggi yang awalnya dikembangkan untuk membuat situs web lebih interaktif. Bersama dengan HTML dan CSS, JavaScript menjadi salah satu bahasa pemrograman paling populer untuk pengembangan aplikasi berbasis web. Bahasa ini memberikan logika tambahan pada situs web, sehingga situs tersebut menjadi lebih fungsional dan dinamis. JavaScript termasuk dalam kategori bahasa scripting, yang kodenya tidak memerlukan proses kompilasi untuk dijalankan, melainkan menggunakan interpreter untuk menerjemahkan kode agar dapat dipahami oleh mesin.

JavaScript diciptakan pada tahun 1995 oleh Brendan Eich, seorang programmer dari Netscape. Bahasa ini awalnya diberi nama "Mocha", kemudian berubah menjadi "LiveScript", dan akhirnya menjadi "JavaScript". Meskipun namanya mirip, JavaScript tidak berhubungan dengan bahasa pemrograman Java. Setelah digunakan di luar Netscape, JavaScript distandarisasi oleh European Computer Manufacturers Association (ECMA).

JavaScript sekarang sudah mengalahkan Java Applet dan Flash sebagai bahasa pemrograman untuk membuat halaman web menjadi lebih interaktif, hal ini dikarenakan kemudahan bahasanya dan juga secara default sekarang semua browser sudah bisa menjalankan JavaScript tanpa harus menginstall aplikasi tambahan seperti Java Applet dan Adobe Flash Player.

## JavaScript di Server

Awalnya JavaScript memang kebanyakan di gunakan untuk berjalan di client side (Browser). Namun, semenjak keluar teknologi NodeJS yang bisa digunakan untuk menjalankan JavaScript tanpa browser, sekarang akhirnya JavaScript juga banyak digunakan untuk membuat aplikasi di Server. Karena ini, akhirnya sekarang JavaScript dikenal dengan bahasa pemrograman Full-Stack karena bisa digunakan untuk membuat aplikasi Back-End dan aplikasi Front-End.

## JavaScript dan ECMAScript

Karena JavaScript sekarang hampir di adopsi oleh sebuah aplikasi browser, akhirnya dibuatlah sebuah standarisasi yang bernama ECMAScript. Organisasi yang melakukan standarisasi ECMAScript adalah ECMA International. Sekarang dengan adanya standarisasi, kita bisa pastikan bahwa kode program JavaScript, harus mengikuti standarisasi ECMAScript. Sekarang karena ECMAScript dan JavaScript sama, sekarang bisa dibilang ECMAScript dan JavaScript adalah dua nama untuk satu bahasa pemrograman yang sama. dokumentasi ECMAScript: https://www.ecma-international.org/

## JavaScript dan Java

Pemula programmer sering salah tentang JavaScript dan Java. Ada yang mengira bahwa Java dan JavaScript adalah bahasa pemrograman yang sama, padahal itu berbeda. Java adalah bahasa pemrograman lain, tidak ada hubungannya dengan JavaScript. Walaupun namanya ada kata "Java" nya, tapi dua bahasa pemrograman ini benar-benar berbeda, tidak ada hubungannya sama sekali.

## Development Tools

Saat kita belajar JavaScript, kita perlu menyiapkan beberapa perangkat lunak untuk membantu development. Browser, ini sudah pasti, karena kita perlu menjalankan kode program JavaScript menggunakan Browser. Text Editor atau Integrated Development Environment (IDE), ini digunakan untuk membuat kode program JavaScript.

## Membuat Kode JavaScript

Ada beberapa cara untuk membuat kode JavaScript. Bisa langsung di file HTML. Atau bisa menggunakan file .js (ekstensi untuk JavaScript), lalu di include di dalam file HTML. Pada praktek course ini kita akan menggunakan HTML langsung agar mudah membuat kode program-nya.

**index.html**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Belajar JavaScript</title>
  </head>
  <body>
    <h1>Belajar JavaScript</h1>
    <script>
      // Script JavaScript
      document.writeln("Hello World");
    </script>

    <!-- Include Script JavaScript -->
    <script src="js/script.js"></script>
  </body>
</html>
```

**script.js**

```js
// Script JavaScript
document.writeln("Hello World");
```

## Titik Koma

JavaScript mirip seperti bahasa pemrograman C/C++, dimana di akhir tiap statement kode program, kita perlu menambahkan ; (titik koma). Namun, di JavaScript tanda ; (titik koma) tidak wajib, jadi kita bisa menambahkan ataupun tidak. Sangat disarankan konsisten, jika ingin menggunakan titik koma, gunakan disemua tempat, jika tidak, jangan gunakan di semua tempat. Namun direkomendasikan untuk menggunakan titik koma.

## Komentar

Komentar adalah kode program yang tidak akan dieksekusi ketika dibaca. Komentar biasanya digunakan sebagai informasi tambahan atau petunjuk. Di JavaScript, kita bisa menambahkan kode komentar.

```js
// Komentar JavaScript satu baris
document.writeln("<p>Hello World</p>");

/* 
Komentar JavaScript lebih dari satu baris
 */
document.writeln("<p>Hello World Lagi</p>");
```

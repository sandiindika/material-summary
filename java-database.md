<h1 style="text-align: center;">Java Database</h1>

## Pengenalan JDBC

JDBC (Java Database Connectivity) merupakan spesifikasi API standar untuk mengakses database. Untuk terhubung ke database apapun, cara kerjanya sama dan hanya berbeda query SQL yang digunakan. JDBC hanya berisi interface-interface kontrak untuk berinteraksi dengan database. JDBC perlu implementasi, atau bisa disebut dengan Driver, seperti MySQL Driver, PostgreSQL Driver, OracleDB Driver, dan lain-lain. Semua interface API JDBC terdapat di package java.sql dan javax.sql.

## Cara Kerja JDBC

![Cara Kerja JDBC](images/java_database/cara_kerja_jdbc.png)

Dari aplikasi (APP) yang dibuat menggunakan Java lalu terhubung ke JDBC yang kemudian menggunakan Driver untuk terhubung ke database, tergantung dengan jenis databasenya.

## JUnit 5

Belajar Java Database menggunakan unit test, dengan menambahkan dependency JUnit 5 di project.

Source junit-jupiter di https://search.maven.org/


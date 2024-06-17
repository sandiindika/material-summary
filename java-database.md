<h1 style="text-align: center;">Java Database</h1>

## Pengenalan JDBC

JDBC (Java Database Connectivity) merupakan spesifikasi API standar untuk mengakses database. Untuk terhubung ke database apapun, cara kerjanya sama dan hanya berbeda query SQL yang digunakan. JDBC hanya berisi interface-interface kontrak untuk berinteraksi dengan database. JDBC perlu implementasi, atau bisa disebut dengan Driver, seperti MySQL Driver, PostgreSQL Driver, OracleDB Driver, dan lain-lain. Semua interface API JDBC terdapat di package java.sql dan javax.sql.

## Cara Kerja JDBC

![Cara Kerja JDBC](images/java_database/cara_kerja_jdbc.png)

Dari aplikasi (APP) yang dibuat menggunakan Java lalu terhubung ke JDBC yang kemudian menggunakan Driver untuk terhubung ke database, tergantung dengan jenis databasenya.

## JUnit 5

Belajar Java Database menggunakan unit test, dengan menambahkan dependency JUnit 5 di project.

Source junit-jupiter di https://search.maven.org/

## Driver

Driver adalah jembatan penghubung antara JDBC dan Database Management System yang akan digunakan. Sebenarnya Driver itu berisikan class-class implementasi dari interface yang terdapat di JDBC. Tanpa menggunakan Driver, JDBC tidak bisa terkoneksi ke DBMS. Driver di JDBC direpresentasikan oleh interface java.sql.Driver.

Dokumentasi (Java Doc): https://docs.oracle.com/en/java/javase/17/docs/api/java.sql/java/sql/Driver.html

## PostgreSQL Driver

Untuk menghubungkan aplikasi Java dengan PostgreSQL menggunakan JDBC, kita memerlukan driver PostgreSQL JDBC. Langkah-langkah untuk mengunduh dan menggunakan driver PostgreSQL JDBC:

1. Unduh Driver PostgreSQL JDBC dari situs resmi PostgreSQL atau dari repository Maven. Lihat [sumber](https://jdbc.postgresql.org/download)

2. Tambahkan Driver ke Proyek Java.
    
    - Menggunakan Maven

        Jika menggunakan Maven untuk manajemen proyek, tambahkan dependensi berikut ke dalam file `pom.xml`:
        ```xml
        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <version>42.7.3</version>
        </dependency>
        ```
        Untuk memeriksa versi terbaru, cek sumber [disini](https://central.sonatype.com/artifact/org.postgresql/postgresql)

    - Menggunakan Gradle

        Jika menggunakan Gradle untuk manajemen proyek, tambahkan dependensi berikut ke dalam file `build.gradle`:
        ```gradle
        dependencies {
            implementation 'org.postgresql:postgresql:42.7.3'
        }
        ```

    - Manual Download

        Jika tidak menggunakan sistem manajemen dependensi seperti Maven atau Gradle, kita bisa mengunduh file `.jar` dari situs resmi dan menambahkannya ke classpath proyek kita.

        - Jalankan IntellJ IDE.
        - Buat atau buka proyek Java.
        - Klik kanan pada nama proyek dan pilih **Open Module Settings**.
        - Setelah itu, pilih **Libraries** pada tab **Project Settings** dan klik **New Project Library (+)**.
        - Kemudian, pilih file PostgreSQL Database Driver seperti `postgresql-42.7.3.jar`.
        - Info lengkap ada [disini](https://postgresqltutorial.com/postgresql-jdbc/connecting-to-postgresql-database)

## Source:

- [Programmer Zaman Now](https://github.com/ProgrammerZamanNow)
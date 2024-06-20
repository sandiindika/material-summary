<h1 style="text-align: center;">Java Apache Maven</h1>

## Pengenalan Build Automation

Build Automation adalah proses meng-otomatisasi tahapan pembuatan software dan hal-hal yang berhubungan dengannya, seperti kompilasi: source code menjadi binary code, mem-package binary code menjadi distribution file, membuat dokumentasi, menjalankan automated test sampai manajemen dependency.

Jadi seperti saat membuat aplikasi menggunakan Java, kita harus meng-compile source code-nya. Jika kita menggunakan IDE, kita akan dibantu dalam hal compile. Namun, pada kenyataannya kita tidak mungkin membawa IDE ke dalam server untuk meng-compile source code Java. Sehingga kita harus meng-compile source code Java menjadi binary code. Kemudian melakukan packaging binary code menjadi distribution file seperti dari `.class` menjadi `.jar` (Java ARchive). Jadi Build Automation akan meng-otomatisasi semua proses tersebut sehingga tidak perlu dilakukan secara manual.

## Kompilasi Source Code

![Kompilasi Source Code](/images/java_apache_maven/kompilasi_source_code.png)

Proses compile seperti gambar dilakukan secara manual saat kita tidak menggunakan IDE.

## Mem-package Binary File

![Mem-package Binary File](/images/java_apache_maven/package_binary_file.png)

Dari binary file `.class` di package menjadi distribution file seperti `.jar` (Java ARchive), `.war` (Web ARchive), `.ear` (Enterprise ARchive), dan lain sebagainya.

## Membuat Dokumentasi

![Membuat Dokumentasi](/images/java_apache_maven/membuat_dokumentasi.png)

Kemampuan Java untuk compile source code menjadi dokumentasi (Java Doc). Java Doc adalah hasil compile dari source code.

## Menjalankan Automated Test

![Menjalankan Automated Test](/images/java_apache_maven/menjalankan_automated_test.png)

Proses otomatisasi test dengan menggunakan build automation. Pada kenyataannya saat kita membuat aplikasi, kita juga pasti akan membuat test code juga (unit test) yang nanti dapat dijalankan secara otomatis sehingga kita bisa melihat test resultnya.

## Management Dependency

![Management Dependency](/images/java_apache_maven/management_dependency.png)

Saat membuat aplikasi kita selalu membutuhkan framework yang sudah ada, sehingga kita harus mendownload secara manual kemudian disimpan dan di compile bersama sehingga menjadi ribet. Dengan build automation kita dapat meringkas proses-proses tersebut secara otomatis.

## Contoh Build Automation Tool

- Apache Maven (Populer di Programmer Java)
- Apache Ivy
- Gradle (Banyak digunakan oleh Programmer Kotlin dan Android)

## Pengenalan Apache Maven

Apache Maven salah satu build automation yang free dan open source. Apache menggunakan XML untuk mendefinisikan build script-nya. Apache Maven running menggunakan JVM (Java Virtual Machine) sebagai fondasi dasar.

## Teknologi yang Didukung

Apache Maven mendukung build automation untuk banyak teknologi, seperti:

- Java
- Kotlin
- Groovy
- Scala

## Menginstal Apache Maven

1. Download Maven: https://maven.apache.org/download.cgi
2. Instalasi Apache Maven adalah proses sederhana, yakni dengan mengekstraksi arsip (archive) dan menambahkan direktori `bin` ke `PATH`.
3. Setting `PATH` di Linux. Open file `.bashrc` atau `.bash_profile` dan tambahkan perintah berikut:
   ```bash
   export JAVA_HOME="/path/to/maven/home/3,x,x"
   export PATH="$JAVA_HOME/bin:$PATH"
   ```
4. Konfirmasi instalasi dengan mengetikan `mvn -v`

## Archetype

Maven mendukung pembuatan berbagai macam project dengan mudah. Pembuatan project di maven menggunakan archetype yang merupakan template project. Jadi kita dapat menggunakan template yang telah disediakan atau bahkan membuat template archetype sendiri.

Dokumentasi archetype: https://maven.apache.org/guides/introduction/introduction-to-archetypes.html

## Membuat Java Project menggunakan Maven

Gunakan perintah berikut:

- `mvn archetype:generate`
- `maven-archetype-quickstart` (Template Java Project sederhana)

## Lifecycle

Maven bekerja dalam konsep lifecycle. Untuk menjalankan lifecycle, kita bisa menggunakan perintah: `mvn namalifecycle`. Lifecycle akan menjalankan banyak plugin, entah bawaan maven, atau bisa dari tambahan plugin lain.

Dokumentasi lifecycle: https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html

## Contoh Lifecycle

- `clean`, menghapus folder target (tempat menyimpan hasil kompilasi)
- `compile`, meng-compile source code
- `test-compile`, meng-compile test code
- `test` (optional), menjalankan test
- `package` (optional), membuat distribusi binary file
- `install` (optional), meng-install distribusi binary file
- `deploy` (optional), deploy distribusi binary file ke remote repository server

## Build Project

Saat kita membuat project, biasanya akan ada 2 jenis kode yang dibuat, kode programnya (source code) dan kode testing-nya (test code). Maven mendukung kedua hal tersebut. Untuk menjalankan kompilasi program gunakan perintah: `mvn compile` dan untuk test gunakan: `mvn test` sedangkan untuk mem-package project gunakan: `mvn package`. Langkah praktis untuk meringkas semua proses dapat digunakan perintah berikut: `mvn clean compile test package`.

## Dependency

Proyek aplikasi jarang sekali berdiri sendiri, biasanya membutuhkan dukungan dari pihak lain, seperti tool atau library. Tanpa build tool seperti Apache Maven, untuk menambahkan library dari luar, kita harus melakukannya secara manual. Apache Maven mendukung dependency management, dimana kita tidak perlu me-manage secara manual proses penambahan dependency (tool atau library) ke dalam proyek aplikasi.

## Dependency Scope

Saat kita menambahkan dependency ke project Maven, kita harus menentukan scope dependency tersebut, ada banyak scope yang ada di Maven, namun sebenarnya hanya beberapa saja yang sering kita gunakan, seperti:

- `compile`: dependency dengan scope compile adalah default dan tersedia di semua fase dari compile, test, dan runtime.

  ```xml
  <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>5.3.9</version>
  </dependency>
  ```

- `provided`: dependency yang harus disediakan oleh JDK atau container/runtime di mana aplikasi berjalan. Dependency ini digunakan saat kompilasi dan pengujian, tetapi tidak dikemas ke dalam artefak akhir (misalnya, jar atau war).

  ```xml
  <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>4.0.1</version>
      <scope>provided</scope>
  </dependency>
  ```

- `runtime`: dependency ini tidak diperlukan saat kompilasi, tetapi diperlukan saat menjalankan aplikasi.

  ```xml
  <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.26</version>
      <scope>runtime</scope>
  </dependency>
  ```

- `test`: dependency ini hanya digunakan untuk kompilasi dan menjalankan tes, tetapi tidak termasuk dalam artefak yang diproduksi.

  ```xml
  <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.13.2</version>
      <scope>test</scope>
  </dependency>
  ```

- `system`: mirip dengan `provided`, tetapi Anda harus secara eksplisit menentukan lokasi jar dengan elemen `systemPath`. Scope ini jarang digunakan karena mengharuskan dependensi berada di jalur yang tetap.

  ```xml
  <dependency>
      <groupId>com.h2database</groupId>
      <artifactId>h2</artifactId>
      <version>1.4.200</version>
      <scope>system</scope>
      <systemPath>${basedir}/lib/h2-1.4.200.jar</systemPath>
  </dependency>
  ```

## Source untuk Mencari Dependency

- https://search.maven.org/
- https://mvnrepository.com/

## Repository

Saat kita menambahkan dependency, terdapat istilah repository yaitu lokasi file .jar itu tersedia (default repository Maven).

![Repository Dependency](/images/java_apache_maven/management_dependency.png)

## Menambahkan Repository Baru

Untuk menambahkan repository baru miliki pribadi atau perusahaan sendiri yaitu dengan menambahkan repository baru di `pom.xml`.

```xml
<repositories>
    <repository>
        <id>bintray-bliblidotcom-maven</id>
        <name>bintray</name>
        <url>https://dl.bintray.com/bliblidotcom/maven</url>
    </repository>
</repositories>
```

## Maven Properties

Maven mendukung properties untuk menyimpan data konfigurasi. Fitur ini akan sangat memudahkan kita kedepannya, dibandingkan melakukan hardcode di konfigurasi maven.

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
    <junit.version>4.11</junit.version>
    <gson.version>2.8.6</gson.version>
</properties>
```

## Menggunakan Properties

```xml
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>${junit.version}</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

## Membuat Distribution File

Secara default, maven mendukung pembuatan distribution file menggunakan lifecycle package. Hanya saja, hasil distribution file-nya berupa file `.jar` yang berisikan binary code dari project kita. Dependency lainnya tidak dimasukkan, sehingga tidak bisa langsung dijalankan.

## Menggunakan Assembly Plugin

Salah satu plugin yang bisa kita gunakan untuk membuat distribution file beserta dependency yang kita butuhkan adalah Assembly Plugin.

Detail: https://maven.apache.org/plugins/maven-assembly-plugin/usage.html

Untuk membuat distribution file, kita bisa menggunakan perintah berikut: `mvn package assembly:single`

## Multi Module Project

Saat aplikasi kita sudah sangat besar, kadang ada baiknya kita buat aplikasi dalam bentuk modular. Misal kita pisahkan module model, controller, view, service, repository, dan lain-lain. Maven kini telah mendukung pembuatan project multi module.

## Membuat Module Baru

Untuk membuat module baru, di dalam project yang sudah ada, kita hanya tinggal membuat folder baru, lalu menambahkan setting pom.xml di folder tersebut. Module harus memiliki parent, dimana parent-nya adalah project di atas folder tersebut. Selanjutnya, di parent-nya pun, module harus di include.

## Konfigurasi Module

```xml
<parent>
    <artifactId>belajar-apache-maven</artifactId>
    <groupId>sandi-indika</groupId>
    <version>1.0-SNAPSHOT</version>
</parent>
<modelVersion>4.0.0</modelVersion>

<artifactId>belajar-apache-maven-data</artifactId>
```

More detail: https://youtu.be/VYA7NzIZFdg?t=3100

## Dependency Management

Saat project kita sudah besar, kadang kita sering menggunakan banyak dependency. Masalah dengan banyak dependency adalah, jika kita salah menggunakan dependency yang sama namun versinya berbeda-beda. Maven mendukung fitur dependency management, dimana kita bisa memasukkan daftar dependency di parent module beserta versinya, lalu menambahkan dependency tersebut di module tanpa harus menggunakan versinya. Secara otomatis versi dependency akan sama dengan yang ada di dependency management di parent module.

Mode detail: https://youtu.be/VYA7NzIZFdg?t=3646

## Source:

- [Programmer Zaman Now](https://github.com/ProgrammerZamanNow)
<h1 align="center" style="text-align: center;">Jakarta Persistence API</h1>

Sebagai sebuah spesifikasi, Jakarta Persistence API (sebelumnya Java Persistence API) berkaitan dengan persistensi, yang secara umum berarti mekanisme apapun yang memungkinkan object Java bertahan lebih lama dari proses aplikasi yang membuatnya. Tidak semua object Java perlu dipersistenkan, tetapi sebagian besar aplikasi mempersistenkan object bisnis utama. Spesifikasi JPA memungkinkan kita mendefinisikan object mana yang harus dipersistenkan, dan bagaimana mereka dipersistenkan dalam aplikasi Java kita.

JPA sendiri bukanlah suatu tool atau framework; sebaliknya, ia mendefinisikan serangkaian konsep yang memandu para pembuat. Meskipun model Object-Relational Mapping (ORM) JPA awalnya didasarkan pada Hibernate, JPA telah berkembang sejak saat itu. Demikian pula, meskipun JPA awalnya dimaksudkan untuk digunakan dengan relational database, beberapa implementasi JPA telah diperluas untuk digunakan dengan database non-relational, seperti NoSQL. Salah satu kerangka kerja populer yang mendukung JPA dengan NoSQL adalah EpclipseLink, implementasi referensi untuk JPA 3.

Ide inti di balik JPA, berbeda dengan Java Database Connectivity (JDBC), yaitu bahwa sebagian besar JPA memungkinkan kita menghindari kebutuhan untuk "berpikir secara relasional". Dalam JPA, kita dapat mendefinisikan aturan persistensi kita dalam ranah kode dan object Java, sementara JDBC mengharuskan kita menerjemahkan secara manual dari kode ke tabel relasional dan sebaliknya.

## JPA dan Hibernate

Karena sejarahnya yang saling terkait, Hibernate dan JPA sering kali dikonflasikan. Namun, seperti spesifikasi Java Servlet, JPA telah melahirkan banyak tools dan frameworks yang kompatibel. Hibernate hanyalah salah satu dari banyak tools JPA.

Dikembangkan oleh Gavin King dan pertama kali dirilis pada awal 2002, Hibernate adalah library untuk Java. King mengembangkan Hibernate sebagai alternatif untuk entity beans dalam hal persistensi. Framework ini begitu populer, dan sangat dibutuhkan pada saat itu, sehingga banyak idenya diadopsi dan dikodifikasi dalam spesifikasi JPA pertama.

Saat ini, Hibernate ORM adalah salah satu implementasi JPA yang paling matang, dan masih menjadi pilihan populer untuk ORM di Java. Tool tambahan Hibernate termasuk Hibernate Search, Hibernate Validator, dan Hibernate OGM, yang mendukung persistensi model domain untuk NoSQL.

**JPA dan EJB**

> Seperti yang telah disebutkan sebelumnya, JPA diperkenalkan sebagai subset dari Enterprise JavaBeans (EJB) 3.0, tetapi sejak berkembangnya menjadi menjadi spesifikasinya sendiri. EJB adalah spesifikasi dengan fokus yang berbeda dari JPA, dan diimplementasikan dalam kontainer EJB. Setiap kontainer EJB mencakup lapisan persistensi, yang didefinisikan oleh spesifikasi JPA.

## Apa itu Java ORM?

Meskipun berbeda dalam pelaksanaannya, setiap implementasi JPA menyediakan semacam lapisan ORM. Untuk memahami JPA dan tools yang kompatibel dengan JPA, kita perlu memiliki pemahaman yang baik tentang ORM.

Object-relational mapping adalah suatu konsep yang memungkinkan kita mendefinisikan bagaimana object Java ditangani pada database. Framework seperti ORM atau EclipseLink mengkodifikasi tugas menjadi sebuah library atau framework, yaitu ORM layer. Sebagai bagian dari arsitektur aplikasi, ORM layer bertanggung jawab untuk mengelolan konversi object perangkat lunak agar dapat berinteraksi dengan tabel dan kolom dalam relational database. Di Java, ORM layer mengonversi class dan object Java sehingga mereka dapat disimpan dan dikelola dalam relational database.

Secara default, nama object yang dipresistenkan akan menjadi nama tabel, dan field-nya menjadi kolom. Setelah tabel disiapkan, setiap baris tabel seusai dengan object dalam aplikasi. Pemetaan object dapat dikonfigurasi, tetapi pengaturan default cenderung berfungsi, dan dengan tetap menggunakan default, kita dapat terhindar dari keharusan mempertahankan metadata konfigurasi.

**JPA dengan NoSQL**

> Hingga baru-baru ini, non-relational database adalah curiosities yang jarang ditemukan. Gerakan NoSQL mengubah semua itu, dan sekarang berbagai NoSQL database tersedia bagi pengembang Java. beberapa implementasi JPA telah berkembang untuk mengakomodasi NoSQL, termasuk Hibernate OGM dan EclipseLink.

Ilustrasi peran JPA dan ORM layer dalam pengembangan aplikasi.

<p align="center">
<img src="https://images.idgesg.net/images/article/2022/05/what-is-jpa.drawio-1-100928128-orig.jpg?auto=webp&quality=85,70" alt="JPA dan Java ORM Layer">
</p>

## Konfigurasi Java ORM Layer

Ketika kita menyiapkan project baru untuk menggunakan JPA, kita perlu mengonfigurasi datastore dan JPA provider. Kita akan mengonfigurasi konektor datastore untuk terhubung ke database pilihan kita (SQL atau NoSQL). Kita juga akan menyertakan dan mengonfigurasi JPA provider, yang merupakan framework seperti Hibernate atau EclipseLink. Meskipun kita dapat mengonfigurasi JPA secara manual, banyak pengembang memilih untuk menggunakan dukungan bawaan dari Spring. Kita akan melihat pengaturan dan instalasi JPA secara manual dan berbasis Spring sebentar lagi.

**Java Data Objects**

> Java Data Objects (JDO) adalah framework persistensi standar yang berbeda dari JPA terutama karena mendukung logika persistensi dalam object, dan karena dukungannya yang sudah lama untuk bekerja dengan non-relational data stores. JPA dan JDO cukup mirip sehingga penyedia JDO sering juga mendukung JPA. Lihat [Apache JDO Project](http://db.apache.org/jdo/why_jdo.html) untuk mempelajari lebih lanjut tentang JDO dalam kaitannya dengan standar persistensi lainnya seperti JPA dan JDBC.

## Persistensi Data di Java

Dari perspektif pemrograman, ORM layer adalah lapisan adaptop: ia mengadaptasi bahasa grafik objek ke bahasa SQL dan relational tables. ORM layer memungkinkan pengembang berorientasi objek untuk membangun perangkat lunak yang mempersistenkan data tanpa meninggalkan paradigma berorientasi objek.

Ketika kita menggunakan JPA, kita membuat peta dari datastore ke objek model data aplikasi kita. Alih-alih mendefinisikan bagaimana objek disimpan dan diambil, kita mendefinisikan pemetaan antara object dan database kita, kemudian memanggil JPA untuk mempersistenkannya. Jika kita menggunakan relational database, banyak dari koneksi aktual antara kode aplikasi kita dan database akan ditangani oleh JDBC.

Sebagai sebuah spesifikasi, JPA menyediakan metadata annotations, yang kita gunakan untuk mendefinisikan pemetaan antara objek dan database. Setiap implementasi JPA menyediakan mesinnya sendiri untuk JPA annotations. Spesifikasi JPA juga menyediakan PersistenceManager atau EntityManager, yang merupakan titik kontak utama dengan sistem JPA (dimana kode logika bisnis kita memberi tahu sistem apa yang harus dilakukan dengan objek yang dipetakan).

**Untuk membuat semuanya lebih konkret, kita buat class data sederhana untuk memodelkan seorang musisi.**

```java
public class Musician {
    private Long id;
    private String name;
    private Instrument mainInstrument;
    private ArrayList performances = new ArrayList();

    public Musician (Long id, String name) {
        /* constructor setters... */
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getName() {
        return this.name;
    }

    public void setMainInstrument(Instrument instr) {
        this.instrument = instr;
    }

    public Instrument getMainInstrument() {
        return this.instrument;
    }

    // ...Other getters and setters
}
```

Class Musician dalam kode di atas digunakan untuk menyimpan data. Class ini dapat berisi data primitif seperti field nama. Class ini juga dapat menyimpan relasi ke kelas lain seperti mainInstrument dan performances.

Alasan keberadaan Musician adalah untuk menyimpan data. Jenis class ini terkadang dikenal sebagai DTO, atau data transfer object. DTO adalah fitur umum dalam pengembangan perangkat lunak. Meskipun mereka menyimpan berbagai jenis data, mereka tidak mengandung logika bisnis apapun. Mempertahankan object data adalah tantangan yang umum dalam pengembangan perangkat lunak.

## Persistensi Data dengan JDBC

Salah satu cara untuk menyimpan instance dari class Musician ke dalam relational database adalah dengan menggunakan library JDBC. JDBC adalah lapisan abstraksi yang memungkinkan aplikasi mengeluarkan perintah SQL tanpa harus memikirkan implementasi database yang mendasarinya.

**JDBC inserting a record**

```java
Musician georgeHarrison = new Musician(0, "George Harrison");
String myDriver = "org.gjt.mm.mysql.Driver";
String myUrl = "jdbc:mysql://localhost/test";

Class.forName(myDriver);
Connection conn = DriverManager.getConnection(myUrl, "root", "");

String query = " insert into users (id, name) values (?, ?)";
PreparedStatement preparedStmt = conn.prepareStatement(query);

preparedStmt.setInt (1, 0);
preparedStmt.setString (2, "George Harrison");
preparedStmt.setString (2, "Rubble");
preparedStmt.execute();
conn.close();
// Error handling removed for brevity
```

Object `georgeHarrison` dapat berasal dari mana saja (front-end submit, external service, dll), dan memiliki field ID dan nama yang telah diset. Field pada object kemudian digunakan untuk memberikan nilai pada pernyataan SQL insert. (Class `PreparedStatement` adalah bagian dari JDBC, dengan menawarkan cara yang lebih aman untuk menerapkan nilai ke query SQL.)

Meskipun JDBC menyediakan kontrol yang datang dengan konfigurasi manual, hal ini menjadi merepotkan dibandingkan dengan JPA. Untuk memodifikasi database, kita perlu membuat query SQL yang memetakan object Java kita ke dalam relational database. Kemudian kita harus memodifikasi SQL setiap kali signature object berubah. Dengan JDBC, pemeliharaan SQL menjadi tantangan tugas tersendiri.

## Persistensi Data dengan JPA

```java
Musician georgeHarrison = new Musician(0, "George Harrison");
musicianManager.save(georgeHarrison);
```

Kode di atas menggantikan SQL manual hanya dengan satu baris, `musicianManager.save()` yang menginstruksikan JPA untuk mempersistensikan object. Setelah itu, framework akan menangani konversi SQL, sehingga kita tidak perlu keluar dari paradigma object-oriented.

## Metadata annotations di JPA

Pada kode sebelumnya, hasil dari konfigurasi yang dibuat menggunakan anotasi JPA. Pengembang menggunakan anotasi untuk memberi tahu JPA object mana yang harus dipersistensikan dan bagaimana mereka harus dipersistensikan.

**Class Musician dengan Anotasi JPA**

```java
import javax.persistence.Entity;

@Entity
class Musician {
    // ..class body
}
```

Object yang dipersistensikan terkadang disebut sebagai entitas (entities). Melampirkan anotasi `@Entity` pada class Musician, memberi tahu JPA bahwa class ini dan object-object-nya harus dipersistensikan.

**Konfigurasi Berbasis XML vs. Anotasi**

> JPA juga memungkinkan kita menggunakan file XML eksternal untuk mendefinisikan metadata class, sebagai alternatif dari anotasi. Namun, mengapa kita mau melakukan itu pada kita sendiri? Konfigurasi berbasis anotasi lebih intuitif dan terintegrasi langsung dengan kode, sehingga lebih mudah dipelihara dan dipahami. <br /><br /> Anotasi memungkinkan pengembang untuk langsung melihat bagaimana entitas dipetakan ke database, tanpa harus mencari konfigurasi di file lain.

## Mengonfigurasi JPA

Seperti kebanyakan framework modern, JPA mengadopsi pengkodean berdasarkan konvensi (juga dikenal sebagai convertion over configuration), dimana framework menyediakan konfigurasi default berdasarkan praktik terbaik yang diterapkan. Sebagai contoh, class `Musician` secara default akan dipetakan ke tabel database yang disebut `Musician`.

Konfigurasi konvensional ini menghemat waktu, dan dalam banyak kasus bekerja dengan baik. Kita juga dapat menyesuaikan JPA kita. Sebagai contoh, kita dapat menggunakan anotas `@Table` dari JPA untuk menentukan tabel tempat class `Musician` harus disimpan.

```java
@Entity
@Table(name = "musician")
class Musician {
    // ..class body
}
```

Kode di atas memberi tahu JPA untuk mempersistensikan class Musician ke tabel `musician`.

## Primary Key

Dalam JPA, primary key adalah field yang digunakan untuk mengidentifikasi setiap object secara unik dalam database. Primary key berguna untuk mereferensikan dan menghubungkan object dengan entitas lain. Setiap kali kita menyimpan object ke dalam tabel, kita juga akan menentukan field yang akan digunakan sebagai primary key.

Kita dapat memberi tahu JPA, field mana yang akan digunakan sebagai primary key untuk `musician`.

```java
@Entity
@Table(name = "musician")
class Musician {
    @Id
    private Long id;
    // ..class body
}
```

Dalam kasus ini, kita menggunakan anotasi `@Id` dari JPA untuk menentukan fiela `id` sebagai primary key untuk `musician`. Secara default, konfigurasi ini mengasumsikan bahwa primary key akan ditetapkan oleh database- misalnya, ketika field diatur untuk auto-increment pada tabel.

JPA mendukung strategi lain untuk menghasilkan primary key object. JPA juga memiliki anotasi untuk mengubah nama field individual. Secara umum, JPA cukup fleksibel untuk beradaptasi dengan pemetaan persistensi apa pun yang kita butuhkan.

## Operasi CRUD

Setelah kita memetakan sebuah class ke tabel database dan menetapkan primary key-nya, kita memiliki semua yang kita butuhkan untuk membuat, mengambil, menghapus, dan memperbarui class tersebut dalam database. Memanggil `entityManager.persist()` akan membuat atau memperbarui class yang ditentukan, tergantung pada apakah field primary key-nya adalah null atau berlaku untuk entitas yang sudah ada. Memanggil `entityManager.remove()` akan menghapus class yang ditentukan.

## Hubungan antar Entitas (Entity Relationship)

Mempertahankan objek dengan field primitif hanya setengah dari persamaan. JPA juga memungkinkan kita mengelola entitas dalam kaitannya satu sama lain. Empat jenis hubungan entitas dimungkinkan dalam tabel dan objek:

- One-to-one
- One-to-many
- Many-to-one
- Many-to-many

Setiap jenis hubungan menjelaskan bagaimana sebuah entitas berhubungan dengan entitas lainnya. Sebagai contoh, entitas `Musician` dapat memiliki hubungan one-to-many dengan `Performance`, sebuah entitas yang diwakili oleh koleksi seperti `List` atau `Set`.

Jika `Musician` menyertakan field `Band`, hubungan antara entitas ini bisa menjadi many-to-one, yang menyiratkan koleksi `Musician` pada class `Band` tunggal. (Dengan asumsi setiap musisi hanya tampil di satu band.)

Jika `Musician` memiliki field `BandMates`, itu bisa mewakili hubungan many-to-many dengan entitas `Musician` lainnya.

Terakhir, `Musician` mungkin memiliki hubungan one-to-one dengan entitas `Quote`, yang digunakan untuk mewakili kutipan terkenal: `Quote famousQuote = new Quote()`.

## Mendefinisikan jenis Relationship

JPA memiliki anotasi untuk masing-masing jenis pemetaan hubungannya. Potongan kode berikut menunjukkan bagaimana kita bisa memberikan anotasi pada hubungan one-to-many antara `Musician` dan `Performances`.

**Anotasi one-to-many relationship**

```java
public class Musician {
    @OneToMany
    @JoinColumn(name = "musician_id")
    private List performances = new ArrayList();
    // ...
}
```

Satu hal yang perlu diperhatikan bahwa `@JoinColumn` memberi tahu JPA kolom mana pada tabel `Performance` yang akan dipetakan ke entitas `Musician`. Setiap performance akan dikatikan dengan satu `Musician`, yang dilacak oleh kolom ini. Ketika JPA memuat `Musician` atau `Performances` ke dalam database, JPA akan menggunakan informasi ini untuk merekonstruksi grafik object.

## Entity states dan detached entities

Entitas adalah nama umum untuk object yang persistensinya dipetakan dengan ORM. Entitas dalam aplikasi yang sedang berjalan akan selalu berada dalam salah satu dari empat keadaan: _transient_, _managed_, _detached_, dan _removed_.

Salah satu situasi yang akan kita temui di JPA adalah entitas yang detached. Ini berarti objek yang kita hadapi telah terlepas dari apa yang ada di datastore yang mendukungnya, dan sesi yang mendukungnya telah ditutup. Dengan kata lain, JPA ingin menjaga object tetap terkini, tetapi tidak bisa. Kita dapat menyambungkan kembali entitas yang _detached_ dengan memanggil `entityManager.merge()` pada entitas tersebut.

Object apa pun yang tidak persisten adalah _transient_. Object tersebut hanya merupakan entitas potensial pada saat itu. Setelah `entityManager.persist()` dipanggil, object tersebut menjadi entitas persisten.

Object yang _managed_ adalah entitas persisten.

Ketika entitas telah dihapus dari datastore, tetapi masih ada sebagai object aktif, dikatakan berada dalam keadaan _removed_.

Vlad Mihalcea telah menulis diskusi yang baik tentang [status entitas](https://vladmihalcea.com/jpa-persist-merge-hibernate-save-update-saveorupdate), bersama dengan perbedaan halus antara class EntityManager miliki JPA dan class Seassion miliki Hibernate untuk mengelolanya.

## Apa Tujuan dari EntityManager.flush()?

Banyak pengembang baru di JPA bertanya-tanya tentang tujuan dari method `EntityManager.flush()`. Manajer JPA akan menyimpan operasi yang diperlukan untuk menjaga keadaan persisten entitas agar konsisten dengan database, dan mengelompokkannya untuk efisiensi.

Namun, terkadang kita perlu secara manual untuk membuat framework JPA menjalankan operasi yang diperlukan untuk melakukan push entitas ke database. Misalnya, ini bisa dilakukan untuk menjalankan pemicu database. Dalam kasus itu, kita bisa menggunakan method `flush()`, dan semua status entitas yang belum dipersistenkan akan segera dikirim ke database.

## Strategi Fetching

Selain mengetahui di mana menempatkan entitas terkait dalam database, JPA perlu mengetahui bagaimana kita ingin memuatnya. Strategi fetching memberi tahu JPA cara memuat entitas terkait. Saat memuat dan menyimpan object, framework JPA juga menyediakan kemampuan untuk menyesuaikan cara menangani grafik object. Misalnya, jika class `Musician` memiliki field `bandMate`, memuat george bisa menyebabkan seluruh tabel `Musician` dimuat dari database!

Kita perlu dapat mendefinisikan lazy loading untuk entitas terkati, dengan memahami bahwa hubungan dalam JPA bisa eager atau lazy. Kita dapat menggunakan anotasi untuk menyesuaikan strategi fetching kita, tetapi konfigurasi default JPA sering kali berfungsi langsung tanpa perubahan:

- One-to-many: Lazy
- Many-to-one: Eager
- Many-to-many: Lazy
- One-to-one: Eager

**Transactions di JPA**

> Meskipun di luar cakupan pengantar singkat ini, transaction memungkinkan pengembang menulis ke database. Kita dapat mencapai transaction sederhana dengan baris: `em.getTransaction().commit();`. Transaction dapat didefinisikan dalam berbagai cara, mulai dari interaksi eksplisit melalui API, hingga menggunakan anotasi untuk mendefinisikan batasan transaction, hingga menggunakan Spring AOP untuk mendefinisikan transaction.

## Instalasi dan Setup JPA

Kita akan mengakhiri dengan melihat cepat cara menginstal dan mengatur JPA untuk aplikasi Java kita. Untuk demonstrasi ini, kita akan menggunakan EclipseLink, implementasi referensi JPA.

Cara umum untuk menginstal JPA adalah dengan memasukkan penyedia JPA ke dalam proyek. Masukkan EclipseLink sebagai dependensi dalam file Maven `pom.xml` kita.

```xml
<dependency>
    <groupId>org.eclipse.persistence</groupId>
    <artifactId>eclipselink</artifactId>
    <version>4.0.0-M3</version>
</dependency>
```

Kita juga perlu menyertakan driver untuk database kita

```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.29</version>
</dependency>
```

Selanjutnya, kita perlu memberi tahu sistem tentang database dan penyedia yang kita gunakan. Ini dilakukan dalam file `persistence.xml`.

```xml
<persistence xmlns="http://xmlns.jcp.org/xml/ns/persistence"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence
                                 http://xmlns.jcp.org/xml/ns/persistence/persistence_2_2.xsd"
             version="2.2">
    <persistence-unit name="myPersistenceUnit">
        <provider>org.eclipse.persistence.jpa.PersistenceProvider</provider>
        <class>com.example.Musician</class>
        <properties>
            <property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/myDatabase"/>
            <property name="javax.persistence.jdbc.user" value="username"/>
            <property name="javax.persistence.jdbc.password" value="password"/>
            <property name="javax.persistence.jdbc.driver" value="com.mysql.cj.jdbc.Driver"/>
            <property name="eclipselink.logging.level" value="FINE"/>
        </properties>
    </persistence-unit>
</persistence>

```

Ada cara lain untuk menyediakan informasi ini kepada sistem, termasuk secara programatik. Saya merekomendasikan menggunakan file `persistence.xml` karena menyimpan dependensi dengan cara ini membuatnya sangat mudah untuk memperbarui aplikasi kamu tanpa mengubah kode.

## Konfigurasi Spring untuk JPA

Menggunakan Spring akan sangat memudahkan integrasi JPA ke dalam aplikasi kita. Sebagai contoh, meletakkan anotasi `@SpringBootApplication` di header aplikasi kita menginstruksikan Spring untuk secara otomatis memindai kelas dan menyuntikkan EntityManager sesuai kebutuhan, berdasarkan konfigurasi yang telah kita tentukan.

Berikut adalah dependensi Maven yang harus kita tambahkan jika ingin mendapatkan dukungan JPA dari Spring untuk aplikasi kita:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <version>2.6.7</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
    <version>2.6.7</version>
</dependency>
```

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
<h1 style="text-align: center;">Java Persistence API</h1>

## Apa itu JPA?

JPA (Java Persistence API) adalah sebuah spesifikasi dalam bahasa pemrograman Java yang digunakan untuk mengelola data yang disimpan dalam basis data relasional. Dengan JPA, kamu bisa menghubungkan aplikasi Java dengan basis data tanpa harus menulis kode SQL secara langsung.

## Kegunaan JPA

1. Menyimpan Data: JPA memungkinkan kita menyimpan objek Java ke dalam tabel di basis data.
2. Mengambil Data: JPA memungkinkan kita untuk mengambil data dari basis data dan mengubahnya menjadi objek Java.
3. Mengupdate Data: JPA memungkinkan kita untuk mengupdate data di basis data.
4. Menghapus Data: JPA memungkinkan kita untuk menghapus data di basis data.

## Konsep Utama dalam JPA

1. Entity: Entity adalah kelas Java yang dipetakan ke tabel di basis data. Setiap instance dari kelas ini mewakili satu baris di tabel.
2. Entity Manager: Entity Manager adalah objek yang mengatur operasi CRUD (Create, Read, Update, dan Delete) pada entitas.
3. Persistence Context: Persistence Context adalah lingkungan yang mengelola entitas yang sedang dikelola oleh Entity Manager.
4. Persistence Unit: Persistence Unit adalah definisi konfigurasi yang mengelola sekumpulan entitas. Biasanya didefinisikan dalam file `persistence.xml`.

## Cara Kerja JPA

1. Pemodelan Data dengan Entity: Kamu membuat kelas Java yang mewakili tabel di basis data.
2. Konfigurasi Koneksi Basis Data: Kamu menyiapkan koneksi ke basis data melalui konfigurasi dalam file `persistence.xml`.
3. Menggunakan Entity Manager: Kamu menggunakan Entity Manager untuk melakukan operasi pada entitas, seperti menyimpan, mengambil, mengupdate, dan menghapus data.

## Keuntungan Menggunakan JPA

1. Mengurangi Kode SQL: JPA mengabstraksi detail SQL sehingga kamu bisa fokus pada logika bisnis aplikasi.
2. Portabilitas: Karena JPA adalah spesifikasi, kamu bisa berpindah antara berbagai implementasi JPA (seperti Hibernate, EclipseLink) tanpa mengubah kode.
3. Pengelolaan Transaksi Otomatis: JPA mengelola transaksi secara otomatis, yang memudahkan pengelolaan data dalam basis data.

## Contoh Implementasi Sederhana

1. Konfigurasi Proyek

   Untuk menggunakan JPA, kamu biasanya perlu beberapa dependensi di dalam proyekmu. Jika kamu menggunakan Maven, tambahkan dependensi berikut dalam pom.xml:

   ```xml
   <dependencies>
       <!-- JPA API -->
       <dependency>
           <groupId>javax.persistence</groupId>
           <artifactId>javax.persistence-api</artifactId>
           <version>2.2</version>
       </dependency>
       <!-- Hibernate sebagai implementasi JPA -->
       <dependency>
           <groupId>org.hibernate</groupId>
           <artifactId>hibernate-core</artifactId>
           <version>5.4.10.Final</version>
       </dependency>
       <!-- JDBC driver untuk database yang kamu gunakan (contoh untuk MySQL) -->
       <dependency>
           <groupId>mysql</groupId>
           <artifactId>mysql-connector-java</artifactId>
           <version>8.0.19</version>
       </dependency>
   </dependencies>
   ```

2. Buat Kelas Entity

   Misalkan kita ingin menyimpan informasi pengguna. Kita buat kelas `User` sebagai entity.

   ```java
   package com.example.model;

   import javax.persistence.Entity;
   import javax.persistence.Id;
   import javax.persistence.GeneratedValue;
   import javax.persistence.GenerationType;

   @Entity
   public class User {

       @Id
       @GeneratedValue(strategy = GenerationType.IDENTITY)
       private Long id;
       private String name;
       private String email;

       // Getter dan Setter
   }
   ```

3. Konfigurasi `persistence.xml`

   File `persistence.xml` berisi informasi koneksi ke basis data.

   ```xml
   <persistence xmlns="http://xmlns.jcp.org/xml/ns/persistence" version="2.2">
       <persistence-unit name="example-unit">
           <class>com.example.model.User</class>
           <properties>
               <property name="javax.persistence.jdbc.driver" value="com.mysql.cj.jdbc.Driver"/>
               <property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/mydb"/>
               <property name="javax.persistence.jdbc.user" value="root"/>
               <property name="javax.persistence.jdbc.password" value="password"/>
               <property name="hibernate.dialect" value="org.hibernate.dialect.MySQLDialect"/>
               <property name="hibernate.hbm2ddl.auto" value="update"/>
           </properties>
       </persistence-unit>
   </persistence>
   ```

4. Menggunakan Entity Manager untuk Operasi CRUD

   Kita menggunakan Entity Manager untuk melakukan operasi CRUD.

   ```java
   package com.example;

   import com.example.model.User;

   import javax.persistence.EntityManager;
   import javax.persistence.EntityManagerFactory;
   import javax.persistence.Persistence;

   public class Main {
       public static void main(String[] args) {
           EntityManagerFactory emf = Persistence.createEntityManagerFactory("example-unit");
           EntityManager em = emf.createEntityManager();

           // Mulai transaksi
           em.getTransaction().begin();

           // Membuat dan menyimpan entitas User
           User user = new User();
           user.setName("John Doe");
           user.setEmail("john.doe@example.com");

           em.persist(user);

           // Commit transaksi
           em.getTransaction().commit();

           // Mengambil data User berdasarkan ID
           User foundUser = em.find(User.class, user.getId());
           System.out.println("Found User: " + foundUser.getName());

           // Menutup Entity Manager dan Entity Manager Factory
           em.close();
           emf.close();
       }
   }
   ```

## Relasi Antar Entitas

- One-to-One: Satu entitas berhubungan dengan satu entitas lainnya.
- One-to-Many: Satu entitas berhubungan dengan banyak entitas lainnya.
- Many-to-One: Banyak entitas berhubungan dengan satu entitas lainnya.
- Many-to-Many: Banyak entitas berhubungan dengan banyak entitas lainnya.

Contoh relasi One-to-Many:

```java
@Entity
public class Department {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;

    @OneToMany(mappedBy = "department")
    private List<Employee> employees;

    // Getters dan Setters
}

@Entity
public class Employee {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;

    @ManyToOne
    @JoinColumn(name = "department_id")
    private Department department;

    // Getters dan Setters
}
```

## JPQL (Java Persistence Query Language)

JPQL adalah bahasa query yang mirip dengan SQL, namun beroperasi pada objek Java daripada tabel basis data.

Contoh query JPQL:

```java
TypedQuery<User> query = em.createQuery("SELECT u FROM User u WHERE u.name = :name", User.class);
query.setParameter("name", "John Doe");
List<User> users = query.getResultList();
```

## Named Queries

Named Queries adalah query yang didefinisikan secara statis pada entitas.

```java
@Entity
@NamedQuery(name = "User.findByName", query = "SELECT u FROM User u WHERE u.name = :name")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;
    
    // Getters dan Setters
}
```

Penggunaan Named Query:

```java
TypedQuery<User> query = em.createNamedQuery("User.findByName", User.class);
query.setParameter("name", "John Doe");
List<User> users = query.getResultList();
```

## Criteria API

Criteria API adalah cara lain untuk membuat query secara programatik yang memberikan fleksibilitas dan keamanan tipe.

```java
CriteriaBuilder cb = em.getCriteriaBuilder();
CriteriaQuery<User> cq = cb.createQuery(User.class);
Root<User> user = cq.from(User.class);
cq.select(user).where(cb.equal(user.get("name"), "John Doe"));
TypedQuery<User> query = em.createQuery(cq);
List<User> users = query.getResultList();
```

## Lifecycle Callbacks

JPA menyediakan mekanisme untuk menangani event lifecycle entitas, seperti `@PrePersist`, `@PostPersist`, `@PreUpdate`, `@PostUpdate`, `@PreRemove`, dan `@PostRemove`.

```java
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;

    @PrePersist
    public void prePersist() {
        System.out.println("About to persist user: " + name);
    }

    // Getters dan Setters
}
```

## Inheritance Mapping

JPA mendukung pemetaan pewarisan, di mana satu entitas bisa mewarisi properti dan perilaku dari entitas lain. Contoh:

```java
@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn(name = "dtype")
public class Vehicle {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String manufacturer;
    // Getters dan Setters
}

@Entity
public class Car extends Vehicle {
    private int numOfDoors;
    // Getters dan Setters
}

@Entity
public class Bike extends Vehicle {
    private boolean hasCarrier;
    // Getters dan Setters
}
```

## Cascading Operations

Cascading menentukan apakah operasi tertentu (persist, merge, remove, refresh, detach) harus diteruskan ke entitas terkait.

```java
@OneToMany(mappedBy = "department", cascade = CascadeType.ALL)
private List<Employee> employees;
```
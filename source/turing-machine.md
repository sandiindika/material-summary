<h1 style="text-align: center;">Computational Theory: Turing Machines</h1>

## Sejarah Mesin Turing

Diusulkan pada tahun 1936 oleh Alan Turing, seorang matematikawan Inggris sebagai model matematis sederhana sebuah komputer. Meskipun sederhana, Mesin Turing memiliki kemampuan untuk menggambarkan perilaku komputer _general-purpose_. Mesin Turing dapat digunakan untuk menghitung kelas fungsi bilangan bulat yang dikenal sebagai fungsi rekursif sebagian (_partial recursive function_).

## Model Mesin Turing

Sebuah mesin Turing terdiri dari komponen-komponenL

1. Pengendali berhingga (finite control)
2. Pita masukan dengan sifat:
   - Panjangnya tidak berhingga (ujung kiri terbatas, ujung kanan tidak terbatas) dapat dibaca maupun ditulis
   - Sel yang tidak berisi simbol masukan akan berisi simbol kosong (blank = $B$)

Pada keadaan awal, $n$ sel pertama dari pita masukan berisi rangkaian simbol yang harus dikenali (dinyatakan sebagai $a_1$, $a_2$, ..., $a_n$). Sel di sebelah kanan rangkaian simbol berisi $B$.

## Perbedaan Mesin Turing dengan FSA dan PDA

| FSA/PDA                                  | Mesin Turing                                                                                    |
| :--------------------------------------- | :---------------------------------------------------------------------------------------------- |
| Pita masukan hanya dapat dibaca          | Pita masukan dapat dibaca dan ditulis                                                           |
| _Head_ hanya dapat digerakkan ke kanan   | _Head_ dapat digerakkan ke kanan maupun kiri                                                    |
| Pita masukan hanya berisi string masukan | Pita masukan juga berfungsi sebagai tempat penyimpanan yang pada pengaksesannya tidak dibatasi. |

## Aksi Mesin Turing

Perilaku mesin Turing bergantung pada simbol masukan yang berada pada posisi _Head_, baca/tulis dan status dari _Finite Control_. Dalam setiap gerakannya, mesin Turing dapat melakukan salah satu dari aksi berikut:

- Berubah status.
- Menuliskan simbol pada pita masukan. Aksi penulisan ini mengubah simbol yang sebelumnya berada pada sel tersebut.
- Menggerakkan _Head_ ke kiri atau ke kanan.

## Definisi Formal Mesin Turing

Sebuah mesin Turing $M$ dilambangkan dengan notasi formal sebagai berikut:

$$
M = (Q, \Sigma, \Gamma, \delta, S, B, F)
$$

- $Q$ = himpunan state
- $\Sigma$ = himpunan simbol input, termasuk $B$
- $\Gamma$ = simbol-simbol yang muncul di pita, termasuk $\Sigma$
- $\delta$ = fungsi transisi yang memetakan $Q \times \Gamma \to Q \times \Gamma \times \{L, R\}$
- $S$ = state awal, $S \in Q$
- $B$ = simbol blank, $B \in \Gamma$
- $F$ = himpunan final state, $F \subseteq Q$

## Contoh

Mesin Turing $M$ akan digunakan untuk mengenali bahasa $L=\{0^n1^n|n\geq1\}$. Contoh string di dalam L misalnya: 01, 0011, 000111, 00001111, dan seterusnya.

<p align="center">
<img src="/images/turing_machine/pita-awal.png" alt="Pita Awal">
</p>

Cara kerja mesin Turing untuk mengenali bahasa $L$ dinyatakan dengan algoritma berikut:

1. Ganti simbol `0` paling kiri dengan simbol `X`.
2. Gerakkan _Head_ ke kanan hingga dijumpai simbol `1`.
3. Ganti simbol `1` paling kiri dengan simbol `Y`.
4. Gerakkan _Head_ ke kiri hingga dijumpai simbol `X`.
5. Gerakkan _Head_ ke kanan (hingga menemukan simbol `0`). Kemudian, ganti simbol `0` paling kiri dengan simbol `X`.
6. Kemudian kembali ke langkah no 2, dan seterusnya.

Syarat:

- Jika pada saat bergerak ke kanan untuk mencari `1`, mesin Turing `M` menjumpai simbol `B`, maka berarti banyaknya `0` lebih dari banyaknya `1`. Kesimpulannya, string masukan tidak dikenali.
- Jika pada saat bergerak ke kiri `M` tidak menjumpai lagi `0`, maka `M` akan memeriksan apakah masih ada `1`. Bila habis maka string diterima (dikenali).
- Jika sebuah string diterima (dikenali), maka mesin Turing `M` berhenti. Untuk string yang tidak dikenali (ditolak) ada kemungkinan `M` tidak berhenti (looping).

**String masukan adalah 000111**

<p align="center">
<img src="/images/turing_machine/string-masukan.png" alt="String Masukan">
</p>

Model Kerja:

<p align="center">
<img src="/images/turing_machine/cara-kerja.png" alt="Cara Kerja Turing Machine">
</p>

Pada gambar, terlihat ada lima modus kerja yang berbeda dari mesin Turing:

| State | Action | Description                                   |
| :---: | :----: | :-------------------------------------------- |
|   a   | Find 0 | Find symbol `0`                               |
|   b   | Find 1 | Find symbol `1` in the right                  |
|   c   | Find X | Find symbol `X` in the left                   |
|   d   | Remain | Check the remaining symbols on the input tape |

Dalam setiap modus kerja (state), aksi yang dilakukan mesin Turing mungkin menerima/membaca berbagai simbol pada pita. Aksi yang dilakukan dalam setiap modus kerja (state) dapat berbeda-beda.

Sehingga dapat dibuat tabel transisi seperti berikut:

|                  |               0                |               1               |          X          |          Y          |               B               |
| :--------------: | :----------------------------: | :---------------------------: | :-----------------: | :-----------------: | :---------------------------: |
| Find 0 (State a) | State b, Write `X`, Move Right |                               |                     | State d, Move Right |                               |
| Find 1 (State b) |           Move Right           | State c, Write `Y`, Move :eft |                     |     Move Right      |                               |
| Find X (State c) |           Move Left            |                               | State a, Move Right |      Move Left      |                               |
| Remain (State d) |                                |                               |                     |     Move Right      | State _e (empty)_, Move Right |

Notasi yang lebih ringkas:

Dengan penulisan _Tripel_ $(q, a, D)$ menyatakan aksi bahwa mesin berubah ke state $q$, menuliskan/membaca simbol $a$, dan menggerakkan $Head$ ke arah $D$.

|     |      0      |      1      |      X      |      Y      |      B      |
| :-: | :---------: | :---------: | :---------: | :---------: | :---------: |
|  a  | $(b, X, R)$ |             |             | $(d, Y, R)$ |             |
|  b  | $(b, 0, R)$ | $(c, Y, L)$ |             | $(b, Y, R)$ |             |
|  c  | $(c, 0, L)$ |             | $(a, X, R)$ | $(c, Y, L)$ |             |
|  d  |             |             |             | $(d, Y, R)$ | $(e, B, R)$ |

Dengan menggunakan notasi formalnya, maka mesin Turing pengenal bahasa $L = \{0^n1^n | n\geq1\}$ dapat ditulis sebagai berikut:

$M = (Q, \Sigma, \Gamma, \delta, S, B, F)$

yang dalam hal ini,

- $Q$ = $\{a, b, c, d, e\}$
- $\Sigma$ = $\{0, 1, B\}$
- $\Gamma$ = $\{0, 1, X, Y, B\}$
- $S$ = $a$
- $B$ = $B$
- $F$ = $\{e\}$

Sehingga dihasilkan fungsi transisi ($\delta$) berikut:

$\delta(a, 0) = (b, X, R);$ <br />
$\delta(a, Y) = (d, Y, R);$ <br />
$\delta(b, 0) = (b, 0, R);$ <br />
$\delta(b, 1) = (c, Y, L);$ <br />
$\delta(b, Y) = (b, Y, R);$ <br />
$\delta(c, 0) = (c, 0, L);$ <br />
$\delta(c, X) = (a, X, R);$ <br />
$\delta(c, Y) = (c, Y, L);$ <br />
$\delta(d, Y) = (d, Y, R);$ <br />
$\delta(d, B) = (e, B, R);$ <br />

## Deskripsi Sesaat/Seketika

Keadaan sebuah Mesin Turing setiap saat dicirikan oleh tiga hal:

1. State sekarang ($q$)
2. Simbol yang sedang diterima/dibaca
3. Posisi _Head_ ("nomor sel" yang sedang dibaca) pada pita.

|            |                           |                   |
| :--------: | :-----------------------: | ----------------- |
|            | $\longleftarrow \alpha_2$ | $\longrightarrow$ |
| $\alpha_1$ |             a             | $\beta$           |
|            |        $\uparrow$         |                   |
|            |             q             |                   |

Jika $\alpha_2 = a\beta$, maka konfigurasi sesaat mesin Turing pada gambar di atas dapat dinyatakan secara tekstual oleh deskripsi sesaat (_instantaneous description_):

$$
\alpha_1 q \alpha_2
$$

yang artinya:

- mesin sedang berada pada state q
- $\alpha_1\alpha_2$ adalah string yang tertera pada pita
- mesin sedang membaca simbol paling kiri dari $\alpha_2$

Saat membuat deskripsi sesaat, kita memerlukan notasi formal dengan menggunakan tanda $\vdash $ sebagai pemisah, dan tanda $\_$ sebagai tuntunan state (_Head_).

> Contoh gerakan ke kiri oleh $\delta(p, Xi)=(q, Y, L):$ <br/>
>
> $$
> X_1X_2...X_{i-1}\:\underline{p}\:X_iX_{i+1}...X_n\vdash X_1X_2...\:\underline{q}\:X_{i-1}YX_{i+1}...X_n
> $$

> Contoh gerakan ke kanan oleh $\delta(p, Xi)=(q, Y, R):$ <br/>
>
> $$
> X_1X_2...X_{i-1}\:\underline{p}\:X_iX_{i+1}...X_n\vdash X_1X_2...X_{i-1}Y\:\underline{q}\:X_{i+1}...X_n
> $$

Sebuah string (kalimat) diterima oleh mesin Turing. $M = (Q, \Sigma, \Gamma, \delta, q_0, B, F)$, jika mesin tersebut mencapai status akhir. Dengan kata lain, suatu kalimat `w` diterima oleh $M$ jika terdapat rangkaian deskripsi sesaat:

$$
q_0\:w\vdash a_1\:p\:a_2
$$

yang dalam hal ini $p\in F\:dan\:a_1\:a_2\in\Gamma^\ast$

## Contoh

- $Q = \{a, b, c, d, e\}$
- $\Gamma = \{0, 1, X, Y, B\}$
- $\Sigma = \{0, 1, B\}$
- $q_0 = a$
- $F = \{e\}$

Gunakan tabel transisi yang telah dibuat sebelumnya.

Maka komputasi String `0011` pada mesin turing:

$\underline{a}0011\:\vdash  X\underline{b}011\:\vdash  X0\underline{b}11\:\vdash  X\underline{c}0Y1\:\vdash  \underline{c}X0Y1\:\vdash  X\underline{a}0Y1\:\vdash  XX\underline{b}Y1\:\vdash  XXY\underline{b}1\:\vdash  XX\underline{c}YY\:\vdash  X\underline{c}XYY\:\vdash  XX\underline{a}YY\:\vdash  XXY\underline{d}Y\:\vdash  XXYY\underline{d}\:\vdash  XXYYB\underline{e} \quad (Diterima)$

## Unrestricted Grammar -> Mesin Turing

Misalkan `w` adalah kalimat yang dihasilkan oleh tata Bahasa $G=(N,T,S,P)$. Mesin Turing $M$ yang menerima `w` bekerja dengan cara mensimulasikan proses penurunan `w` dari simbol awal $S$ oleh tata bahasa $G$. Input awal yang dibaca oleh $M$ adalah $w \# S\#$. $M$ menerapkan aturan produksi yang ada di $P$ dengan mengubah string yang terletak di antara `#` sehingga pita masukan suatu saat diperoleh $w\#w\#$.

Contoh:

- $S \rightarrow ACaB$ <br/>
- $Ca \rightarrow aaC$ <br/>
- $CB \rightarrow DB$ <br/>
- $CB \rightarrow E$ <br/>
- $aD \rightarrow Da$ <br/>
- $AD \rightarrow AC$ <br/>
- $aE \rightarrow Ea$ <br/>
- $AE \rightarrow \varepsilon$ <br/>

Misal:

$aaaa \# S \#$

Maka:

$ aaaa \# S \# \Rightarrow aaaa \# ACaB \# \Rightarrow aaaa \# AaaCB \Rightarrow aaaa \# AaaDB \# \Rightarrow aaaa \# AaDaB \# \Rightarrow aaaa \# ADaaB \# \Rightarrow aaaa \# ACaaB \# \Rightarrow aaaa \# AaaCaB \# \Rightarrow aaaa \# AaaaaCB \# \Rightarrow aaaa \# AaaaaE \# \Rightarrow aaaa \# AaaaEa \# \Rightarrow aaaa \# AaaEaa \# \Rightarrow aaaa \# AaEaaa \# \Rightarrow aaaa \# AEaaaa \# \Rightarrow aaaa \# aaaa \# $

## Source:

- [bringITonUNPAS](https://youtube.com/@bringitonunpas4027)

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
| ---------------------------------------- | ----------------------------------------------------------------------------------------------- |
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
M = (Q, \Sigma, \Gamma, \Delta, S, B, F)
$$

- $Q$ = himpunan state
- $\Sigma$ = himpunan simbol input, termasuk $B$
- $\Gamma$ = simbol-simbol yang muncul di pita, termasuk $\Sigma$
- $\Delta$ = fungsi transisi yang memetakan $Q \times \Gamma \to Q \times \Gamma \times \{L, R\}$
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

Model Kerja

<p align="center">
<img src="/images/turing_machine/cara-kerja.png" alt="Cara Kerja Turing Machine">
</p>

<h1 style="text-align: center;">Computational Theory: Concepts of Language and Automata</h1>

## Pengenalan Teori Automata dan Bahasa Formal

Teori automata berkaitan dengan definisi dan properti dari model-model matematika komputasi. Model pertama disebut *finite automata* yang dapat digunakan dalam *text processing*, *compilers*, dan *hardware design*. Model yang lainnya disebut *context free grammar* yang digunakan dalam bahasa pemrograman dan *Artificial Intelligence* (AI). Model yang lainnya disebut juga dengan *turing machines* yang banyak diteliti saat ini. Teori komputabilitas dan kompleksitas komputasi memerlukan definisi yang tepat mengenai komputasi.

Tata bahasa merupakan kumpulan dari himpunan variabel ($V$), simbol terminal ($T$), simbol awal ($S$) yang dibatasi oleh aturan produksi ($P$), sehingga Tata Bahasa ($G$) tersebut dapat dinyatakan:

$$
G = (V, T, S, P)
$$

dimana:
- $V$ = simbol variabel adalah simbol yang masih dapat diartikan.
- $T$ = simbol terminal adalah simbol yang sudah tidak dapat diturunkan kembali.
- $S$ = simbol awal adalah simbol yang merupakan anggota dari $V$, atau $S \in V$.
- $P$ = aturan produksi yang dinyatakan dengan $\alpha \rightarrow \beta$ (\* dibaca: "$\alpha \: menurunkan \: \beta$").

**VARIABEL** disimbolkan dengan huruf besar/kapital. Sedangkan **terminal** disimbolkan dengan huruf kecil. $\alpha$ merupakan ruas kiri dan $\beta$ merupakan ruas kanan.

## Hirarki Chomsky

Tingkatan bahasa menurut Chomsky (Hirarki Chomsky):

| Kelas Bahasa | Mesin Automata | Bahasa Aturan Produksi |
|---|---|---|
| Reguler | FSA (*Finite State Automaton*) | Ruas kiri: 1 simbol variabel <br /> Ruas kanan: maksimal memiliki 1 simbol variabel yang diletakkan diposisi paling kanan |
| Bebas Konteks | PDA (*Push Down Automata*) | Ruas kiri: 1 simbol variabel |
| Konteks Sensitif | LBA (*Linear Bounded Automata*) | Panjang ruas kiri harus lebih kecil sama dengan (<=) panjang ruas kanan, dan ruas kirinya harus memiliki paling sedikit 1 simbol variabel |
| Bahasa Alami | Mesin Turing | Tidak ada batasan |

- Panjang ruas kiri = banyaknya simbol (baik itu simbol variabel maupun simbol terminal) yang ada di ruas kiri.
- Panjang ruas kanan = banyak simbol (baik itu simbol variabel maupun simbol terminal) yang ada di ruas kanan.
- Contoh: $A \rightarrow aBCd$
    - Panjang ruas kiri = 1, karena di ruas kiri hanya ada 1 simbol variabel, yaitu A.
    - Panjang ruas kanan = 4, karena di ruas kanan ada 2 simbol variabel, yaitu B dan C, dan ada 2 simbol termina, yaitu a dan d, maka jumlah simbolnya adalah 4.
- Tata Bahasa Bebas Konteks = *Context Free Grammar* (CFG)
- Bahasa Alami = *Natural Language*

## Penulisan Reguler

$$
A \rightarrow aB
$$

**Termasuk** dalam **Bahasa Reguler**, karena:
- Ruas kiri: 1 simbol variabel, yaitu $A$.
- Ruas kanan: maksimal memiliki 1 simbol variabel yang diletakkan diposisi paling kanan, yaitu $B$.

$$
A \rightarrow a
$$

**Termasuk** dalam **Bahasa Reguler**, karena:
- Ruas kiri: 1 simbol variabel, yaitu $A$.
- Ruas kanan: maksimal memiliki 1 simbol variabel, artinya ruas kanannya boleh tidak memiliki simbol variabel atau semua ruas kanannya adalah simbol terminal.

$$
a \rightarrow aB
$$

**Bukan termasuk** dalam **Bahasa Reguler**, karena:
- Ruas kiri: tidak memiliki variabel sama sekali.

$$
A \rightarrow Ba
$$

**Bukan termasuk** dalam **Bahasa Reguler**, karena:
- Ruas kiri: 1 simbol variabel, yaitu $A$.
- Ruas kanan: memiliki 1 simbol variabel namun tidak terletak pada posisi paling kanan, yaitu $B$ sedangkan simbol terminal $a$ terletak pada posisi paling kanan.

$$
A \rightarrow aBC
$$

**Bukan termasuk** dalam **Bahasa Reguler**, karena:
- Ruas kiri: 1 simbol variabel, yaitu $A$.
- Ruas kanan: memiliki 2 simbol variabel sehingga melanggar aturan, yaitu $BC$.

$$
AB \rightarrow ab
$$

**Bukan termasuk** dalam **Bahasa Reguler**, karena:
- Ruas kiri: memiliki lebih dari 1 simbol variabel, yaitu $AB$.

## Bebas Konteks

$$
A \rightarrow aB
$$

**Termasuk** dalam **Bahasa Bebas Konteks**, karena:
- Ruas kiri: memiliki 1 simbol variabel, yaitu $A$.

$$
A \rightarrow a
$$

**Termasuk** dalam **Bahasa Bebas Konteks**, karena:
- Ruas kiri: memiliki 1 simbol variabel, yaitu $A$.

$$
A \rightarrow Ba
$$

**Termasuk** dalam **Bahasa Bebas Konteks**, karena:
- Ruas kiri: memiliki 1 simbol variabel, yaitu $A$.

$$
A \rightarrow aBC
$$

**Termasuk** dalam **Bahasa Bebas Konteks**, karena:
- Ruas kiri: memiliki 1 simbol variabel, yaitu $A$.

$$
a \rightarrow aB
$$

**Bukan termasuk** dalam **Bahasa Bebas Konteks**, karena:
- Ruas kiri: bukan simbol variabel tapi simbol terminal, yaitu $a$.

$$
AB \rightarrow aB
$$

**Bukan termasuk** dalam **Bahasa Bebas Konteks**, karena:
- Ruas kiri: memiliki lebih dari 1 simbol variabel, yaitu $AB$.

## Konteks Sensitif

$$
A \rightarrow aB
$$

**Termasuk** dalam **Bahasa Konteks Sensitif**, karena:
- Aturan 1: panjang ruas kiri kurang dari sama dengan panjang ruas kanan, yaitu 1 <= 2.
- Aturan 2: ruas kiri memiliki setidaknya 1 simbol variabel, yaitu $A$.

$$
A \rightarrow a
$$

**Termasuk** dalam **Bahasa Konteks Sensitif**, karena:
- Aturan 1: panjang ruas kiri kurang dari sama dengan panjang ruas kanan, yaitu 1 <= 1.
- Aturan 2: ruas kiri memiliki setidaknya 1 simbol variabel, yaitu $A$.

$$
AB \rightarrow aBC
$$

**Termasuk** dalam **Bahasa Konteks Sensitif**, karena:
- Aturan 1: panjang ruas kiri kurang dari sama dengan panjang ruas kanan, yaitu 2 <= 3.
- Aturan 2: ruas kiri memiliki 2 simbol variabel, yaitu $AB$.

$$
Ab \rightarrow BaC
$$

**Termasuk** dalam **Bahasa Konteks Sensitif**, karena:
- Aturan 1: panjang ruas kiri kurang dari sama dengan panjang ruas kanan, yaitu 2 <= 3.
- Aturan 2: ruas kiri memiliki 1 simbol variabel, yaitu $A$.

$$
ABC \rightarrow ab
$$

**Bukan termasuk** dalam **Bahasa Konteks Sensitif**, karena:
- Aturan 1: panjang ruas kiri kurang dari sama dengan panjang ruas kanan, yaitu 3 <= 2.

$$
ab \rightarrow aBCD
$$

**Termasuk** dalam **Bahasa Konteks Sensitif**, karena:
- Aturan 1: panjang ruas kiri kurang dari sama dengan panjang ruas kanan, yaitu 2 <= 4.
- Aturan 2: ruas kiri tidak memiliki simbol variabel sama sekali.

## Mekanisme Kerja Automata

<p align="center">
<img src="/images/concepts_of_language_and_automata/mekanisme_kerja_automata.png" alt="Cara Kerja JDBC">
</p>

- Terdiri atas sejumlah state berhingga, yang dianggap sebagai memori mesin.
- Input merupakan bahasa yang harus dikenali oleh mesin.
- Membuat keputusan yang mengindikasikan sebuah input diterima atau tidak.
- Dapat digunakan untuk menghasilkan bahasa yang aturannya ditentukan oleh aturan bahasa itu sendiri.

## Source

- [bringITonUNPAS](https://youtube.com/@bringitonunpas4027)
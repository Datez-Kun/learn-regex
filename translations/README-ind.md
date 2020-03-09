<p align="center">
    <br/>
    <a href="https://github.com/ziishaned/learn-regex">
        <img src="https://i.imgur.com/bYwl7Vf.png" alt="Learn Regex">
    </a>
    <br /><br />
    <p>
        <a href="https://twitter.com/ziishaned">
            <img src="https://img.shields.io/twitter/follow/ziishaned.svg?style=social" />
        </a>
        <a href="https://github.com/ziishaned">
            <img src="https://img.shields.io/github/followers/ziishaned.svg?label=Follow%20%40ziishaned&style=social" />
        </a>
    </p>
</p>

## Terjemahan:

* [Indonesian](translations/README-ind.md)
* [English](README.md)
* [Español](translations/README-es.md)
* [Français](translations/README-fr.md)
* [Português do Brasil](translations/README-pt_BR.md)
* [中文版](translations/README-cn.md)
* [日本語](translations/README-ja.md)
* [한국어](translations/README-ko.md)
* [Turkish](translations/README-tr.md)
* [Greek](translations/README-gr.md)
* [Magyar](translations/README-hu.md)
* [Polish](translations/README-pl.md)
* [Русский](translations/README-ru.md)
* [Tiếng Việt](translations/README-vn.md)
* [فارسی](translations/README-fa.md)

## Apa itu Ekspresi Reguler?

 > Ekspresi reguler adalah sekelompok karakter atau simbol yang digunakan untuk menemukan pola tertentu dari sebuah teks.

 Ekspresi reguler adalah pola yang cocok dengan string subjek dari
 kiri ke kanan.  Ekspresi reguler digunakan untuk mengganti teks dalam string,
 memvalidasi bentuk, ekstrak substring dari string berdasarkan kecocokan pola,
 dan masih banyak lagi.  Kata "Ekspresi reguler" adalah suap, jadi biasanya Anda akan melakukannya
 temukan istilah yang disingkat "regex" atau "regexp".

 Bayangkan Anda sedang menulis aplikasi dan Anda ingin menetapkan aturan ketika a
 pengguna memilih nama pengguna mereka.  Kami ingin membolehkan nama pengguna mengandung surat,
 angka, garis bawah dan tanda hubung.  Kami juga ingin membatasi jumlah karakter
 di username sehingga tidak terlihat jelek.  Kami menggunakan ekspresi reguler berikut untuk
 memvalidasi nama pengguna:

<br/><br/>
<p align="center">
  <img src="./img/regexp-en.png" alt="Regular expression">
</p>

Ekspresi reguler di atas dapat menerima string `john_doe`,` jo-hn_doe` dan
 `john12_as`.  Itu tidak cocok dengan `Jo` karena string itu berisi huruf besar
 surat dan juga terlalu pendek.

 ## Daftar Isi

- [Pencocokan Dasar](#1-basic-matchers)
- [Karakter Meta](#2-meta-characters)
  - [Titik](#21-full-stop)
  - [Set karakter](#22-character-set)
    - [Kumpulan karakter yang dinegasikan](#221-negated-character-set)
  - [Pengulangan](#23-repetitions)
    - [Bintang](#231-the-star)
    - [Plus](#232-the-plus)
    - [Tanda Tanya](#233-the-question-mark)
  - [Kawat gigi](#24-braces)
  - [Grup Karakter](#25-character-group)
  - [Alternasi](#26-alternation)
  - [Melarikan karakter khusus](#27-escaping-special-character)
  - [Jangkar](#28-anchors)
    - [Tanda sisipan](#281-caret)
    - [Dolar](#282-dollar)
- [Kumpulan Karakter Singkat](#3-shorthand-character-sets)
- [Terlihat](#4-lookaround)
  - [Lihat kedepan Positif](#41-positive-lookahead)
  - [Lihat kedepan Negatif](#42-negative-lookahead)
  - [Tampilan Positif](#43-positive-lookbehind)
  - [Tampilan Negatif](#44-negative-lookbehind)
- [Bendera](#5-flags)
  - [Huruf Besar-Kecil](#51-case-insensitive)
  - [Pencarian global](#52-global-search)
  - [Multiline](#53-multiline)
- [Pencocokan serakah vs malas](#6-greedy-vs-lazy-matching)

## 1. Pencocokan Dasar

 Ekspresi reguler hanyalah pola karakter yang kami gunakan untuk tampil
 cari dalam teks.  Misalnya, ekspresi reguler `the` berarti: huruf
 `t`, diikuti oleh huruf` h`, diikuti oleh huruf `e`.

<pre>
"the" => The fat cat sat on <a href="#learn-regex"><strong>the</strong></a> mat.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/dmRygT/1)

 Ekspresi reguler `123` cocok dengan string` 123`.  Ekspresi regulernya adalah
 cocok dengan string input dengan membandingkan setiap karakter secara reguler
 ekspresi setiap karakter dalam string input, satu demi satu.  Reguler
 ekspresi biasanya case-sensitive sehingga ekspresi reguler `The` akan
 tidak cocok dengan string `the`.

<pre>
"The" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on the mat.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/1paXsy/1)

## 2. Karakter Meta

 Karakter met adalah blok bangunan dari ekspresi reguler.  Meta
 karakter tidak berdiri sendiri tetapi ditafsirkan dalam beberapa
 cara spesial.  Beberapa karakter meta memiliki makna khusus dan ditulis di dalamnya
 kurung kotak.  Karakter meta adalah sebagai berikut:

 |Karakter Meta|Deskripsi|
 |:----:|----|
 |. | Periode cocok dengan karakter tunggal apa pun kecuali jeda baris. |
 | [] | Kelas karakter.  Cocok dengan karakter apa pun yang terkandung di antara tanda kurung siku. |
 | [^] | Kelas karakter yang dinegasikan.  Cocok dengan karakter apa pun yang tidak terdapat di antara tanda kurung | |
 | * | Mencocokkan 0 atau lebih pengulangan dari simbol sebelumnya. |
 | + | Mencocokkan 1 atau lebih pengulangan dari simbol sebelumnya
 |? | Membuat simbol sebelumnya opsional. |
 | {n, m} | Kawat Gigi.  Cocok dengan setidaknya pengulangan "n" tetapi tidak lebih dari "m" dari simbol sebelumnya
 | (xyz) | Grup karakter.  Cocok dengan karakter xyz dalam urutan yang tepat. |
 ||| Alternatif.  Cocok dengan karakter sebelum atau karakter setelah simbol. |
 | \ | Mengosongkan karakter berikutnya.  Ini memungkinkan Anda untuk mencocokkan karakter yang dipesan <code> [] () {}.  * +?  ^ $ \ | </code> |
 | ^ | Cocok dengan awal input. |
 | $ | Cocok dengan akhir input. |

 ## 2.1 Pemberhentian penuh

 Pemberhentian penuh `.` adalah contoh paling sederhana dari karakter meta.  Karakter meta `.`
 cocok dengan karakter apa pun.  Itu tidak akan cocok dengan karakter baris kembali atau baru.
 Misalnya, ekspresi reguler `.ar` berarti: karakter apa saja, diikuti oleh
 huruf `a`, diikuti dengan huruf` r`.

<pre>
".ar" => The <a href="#learn-regex"><strong>car</strong></a> <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/xc9GkU/1)

## 2.2 Kumpulan karakter

 Set karakter juga disebut kelas karakter.  Kurung kotak digunakan untuk
 tentukan set karakter.  Gunakan tanda hubung di dalam rangkaian karakter untuk menentukan
 rentang karakter.  Urutan rentang karakter di dalam tanda kurung siku
 tidak masalah.  Misalnya, ekspresi reguler `[Tt] he` berarti: huruf besar
 `T` atau huruf kecil` t`, diikuti oleh huruf `h`, diikuti oleh huruf` e`.
 
<pre>
"[Tt]he" => <a href="#learn-regex"><strong>The</strong></a> car parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/2ITLQ4/1)

Namun, suatu periode di dalam rangkaian karakter berarti periode literal.  Biasa
 ekspresi `ar [.]` berarti: karakter huruf kecil `a`, diikuti oleh huruf` r`,
 diikuti oleh karakter `.` periode.

<pre>
"ar[.]" => A garage is a good place to park a c<a href="#learn-regex"><strong>ar.</strong></a>
</pre>

[Uji ekspresi reguler](https://regex101.com/r/wL3xtE/1)

### 2.2.1 Kumpulan karakter yang dinegasikan

 Secara umum, simbol tanda sisipan mewakili awal dari string, tetapi ketika itu
 diketik setelah tanda kurung siku pembukaan meniadakan set karakter.  Untuk
 contoh, ekspresi reguler `[^ c] ar` berarti: karakter apa pun kecuali` c`,
 diikuti oleh karakter `a`, diikuti oleh huruf` r`.

<pre>
"[^c]ar" => The car <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/nNNlq3/1)

## 2.3 Pengulangan

 Karakter meta berikut `+`, `*` atau `?` Digunakan untuk menentukan berapa kali a
 subpola dapat terjadi.  Karakter meta ini bertindak secara berbeda dalam berbeda
 situasi.

 ### 2.3.1 Bintang

 Simbol `*` cocok dengan nol atau lebih pengulangan dari pencocokan sebelumnya.  Itu
 ekspresi reguler `a *` berarti: nol atau lebih pengulangan dari huruf kecil sebelumnya
 karakter `a`.  Tetapi jika itu muncul setelah set karakter atau kelas maka ia menemukan
 pengulangan set karakter keseluruhan.  Misalnya, ekspresi reguler
 `[a-z] *` berarti: sejumlah huruf kecil berurutan.

<pre>
"[a-z]*" => T<a href="#learn-regex"><strong>he</strong></a> <a href="#learn-regex"><strong>car</strong></a> <a href="#learn-regex"><strong>parked</strong></a> <a href="#learn-regex"><strong>in</strong></a> <a href="#learn-regex"><strong>the</strong></a> <a href="#learn-regex"><strong>garage</strong></a> #21.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/7m8me5/1)

 Simbol `*` dapat digunakan dengan karakter meta `.` untuk mencocokkan string
 karakter `. *`.  Simbol `*` dapat digunakan dengan karakter spasi putih `\ s`
 untuk mencocokkan string karakter spasi putih.  Misalnya ungkapan
 `\ s * cat \ s *` berarti: nol atau lebih banyak spasi, diikuti oleh karakter huruf kecil `c`,
 diikuti oleh karakter huruf kecil `a`, diikuti oleh karakter huruf kecil` t`,
 diikuti oleh nol atau lebih banyak ruang.

<pre>
"\s*cat\s*" => The fat<a href="#learn-regex"><strong> cat </strong></a>sat on the con<a href="#learn-regex"><strong>cat</strong></a>enation.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/gGrwuz/1)

### 2.3.2 The Plus

 Simbol `+` cocok dengan satu atau lebih pengulangan dari karakter sebelumnya.  Untuk
 contoh, ekspresi reguler `c. + t` berarti: huruf kecil` c`, diikuti oleh
 setidaknya satu karakter, diikuti oleh karakter huruf kecil

<pre>
"c.+t" => The fat <a href="#learn-regex"><strong>cat sat on the mat</strong></a>.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/Dzf9Aa/1)

### 2.3.3 Tanda Tanya

 Dalam ekspresi reguler, karakter meta `?` Membuat karakter sebelumnya
 pilihan.  Simbol ini cocok dengan nol atau satu instance dari karakter sebelumnya.
 Misalnya, ekspresi reguler `[T]? He` berarti: Opsional huruf besar
 huruf `T`, diikuti oleh karakter huruf kecil` h`, diikuti oleh huruf kecil
 karakter `e`.

<pre>
"[T]he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in the garage.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/cIg9zm/1)

<pre>
"[T]?he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in t<a href="#learn-regex"><strong>he</strong></a> garage.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/kPpO2x/1)

## 2.4 Kawat gigi

 Dalam kurung ekspresi reguler yang juga disebut quantifiers digunakan
 tentukan berapa kali suatu karakter atau sekelompok karakter dapat
 ulang.  Misalnya, ekspresi reguler `[0-9] {2,3}` berarti: Paling tidak cocok
 2 digit tetapi tidak lebih dari 3 (karakter dalam kisaran 0 hingga 9).

<pre>
"[0-9]{2,3}" => The number was 9.<a href="#learn-regex"><strong>999</strong></a>7 but we rounded it off to <a href="#learn-regex"><strong>10</strong></a>.0.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/juM86s/1)

Kita bisa meninggalkan nomor kedua.  Misalnya, ekspresi reguler
 `[0-9] {2,}` berarti: Cocokkan 2 digit atau lebih.  Jika kami juga menghapus koma
 ekspresi reguler `[0-9] {3}` berarti: Sama persis dengan 3 digit.

<pre>
"[0-9]{2,}" => The number was 9.<a href="#learn-regex"><strong>9997</strong></a> but we rounded it off to <a href="#learn-regex"><strong>10</strong></a>.0.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/Gdy4w5/1)

<pre>
"[0-9]{3}" => The number was 9.<a href="#learn-regex"><strong>999</strong></a>7 but we rounded it off to 10.0.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/Sivu30/1)

## 2.5 Menangkap Grup

 Grup penangkap adalah sekelompok sub-pola yang ditulis di dalam tanda kurung
 `(...)`.  Seperti yang kita bahas sebelumnya bahwa dalam ekspresi reguler jika kita meletakkan quantifier
 setelah karakter maka itu akan mengulangi karakter sebelumnya.  Tetapi jika kita menempatkan quantifier
 setelah grup penangkap maka mengulangi seluruh kelompok penangkap.  Sebagai contoh,
 ekspresi reguler `(ab) *` cocok dengan nol atau lebih pengulangan karakter
 "ab".  Kita juga bisa menggunakan karakter meta alternation `di dalam grup capturing.
 Misalnya, ekspresi reguler `(c | g | p) ar` berarti: karakter huruf kecil` c`,
 `g` atau` p`, diikuti oleh karakter `a`, diikuti oleh karakter` r`.

<pre>
"(c|g|p)ar" => The <a href="#learn-regex"><strong>car</strong></a> is <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/tUxrBG/1)

Perhatikan bahwa menangkap grup tidak hanya cocok tetapi juga menangkap karakter untuk digunakan dalam
 bahasa induk.  Bahasa induk dapat berupa python atau javascript atau hampir apa saja
 bahasa yang mengimplementasikan ekspresi reguler dalam definisi fungsi.

 ### 2.5.1 Grup yang tidak menangkap

 Grup yang tidak menangkap adalah grup yang menangkap yang hanya cocok dengan karakter, tetapi
 tidak menangkap grup.  Grup yang tidak menangkap ditandai dengan `?` Diikuti oleh `:`
 dalam kurung `(...)`.  Misalnya, ekspresi reguler `(?: C | g | p) ar` mirip dengan
 `(c | g | p) ar` karena cocok dengan karakter yang sama tetapi tidak akan membuat grup tangkap.

<pre>
"(?:c|g|p)ar" => The <a href="#learn-regex"><strong>car</strong></a> is <a href="#learn-regex"><strong>par</strong></a>ked in the <a href="#learn-regex"><strong>gar</strong></a>age.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/Rm7Me8/1)

Grup yang tidak menangkap dapat berguna saat digunakan dalam fungsi temukan-dan-ganti atau
 ketika dicampur dengan menangkap grup untuk menjaga ikhtisar saat memproduksi segala jenis output lainnya.
 Lihat juga [4.Lookaround](# 4-lookaround).

 ## 2.6 Alternatif

 Dalam ekspresi reguler, bilah vertikal `|` digunakan untuk menentukan pergantian.
 Alternatif seperti pernyataan ATAU antara banyak ekspresi.  Sekarang kamu mungkin
 berpikir bahwa rangkaian karakter dan pergantian bekerja dengan cara yang sama.  Tapi yang besar
 Perbedaan antara set karakter dan pergantian adalah set karakter berfungsi
 level karakter tetapi pergantian bekerja pada level ekspresi.  Misalnya,
 ekspresi reguler `(T | t) he | car` berarti: baik (karakter huruf besar` T` atau huruf kecil
 `t`, diikuti oleh karakter huruf kecil` h`, diikuti oleh karakter huruf kecil `e`) ATAU
 (karakter huruf kecil `c`, diikuti oleh karakter huruf kecil` a`, diikuti oleh
 huruf kecil `r`).  Perhatikan bahwa saya menempatkan tanda kurung untuk kejelasan, untuk menunjukkan bahwa ekspresi baik
 dalam tanda kurung dapat dipenuhi dan itu akan cocok.

<pre>
"(T|t)he|car" => <a href="#learn-regex"><strong>The</strong></a> <a href="#learn-regex"><strong>car</strong></a> is parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/fBXyX0/1)

## 2.7 Melarikan karakter khusus

 Backslash `\` digunakan dalam ekspresi reguler untuk keluar dari karakter berikutnya.  Ini
 memungkinkan kita untuk menentukan simbol sebagai karakter yang cocok termasuk yang disediakan
 karakter `{} [] / \ + *.  $ ^ |  ? `.  Untuk menggunakan karakter khusus sebagai pasangan
 karakter mendahului `\` sebelumnya.

 Misalnya, ekspresi reguler `.` digunakan untuk mencocokkan karakter apa pun kecuali
 garis baru.  Sekarang untuk mencocokkan `.` dalam string input ekspresi reguler
 `(f | c | m) di \.?` berarti: huruf kecil `f`,` c` atau `m`, diikuti oleh huruf kecil
 karakter `a`, diikuti dengan huruf kecil` t`, diikuti oleh opsional `.`
 karakter.

<pre>
"(f|c|m)at\.?" => The <a href="#learn-regex"><strong>fat</strong></a> <a href="#learn-regex"><strong>cat</strong></a> sat on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[Uji ekspresi reguler](https://regex101.com/r/DOc5Nu/1)

## 2.8 Jangkar

 Dalam ekspresi reguler, kami menggunakan jangkar untuk memeriksa apakah simbol yang cocok adalah
 simbol awal atau simbol akhir dari string input.  Jangkar terdiri dari dua jenis:
 Tipe pertama adalah Caret `^` yang memeriksa apakah karakter yang cocok adalah awal
 karakter input dan tipe kedua adalah Dolar `$` yang memeriksa apakah cocok
 karakter adalah karakter terakhir dari string input.

 ### 2.8.1 Caret

 Simbol Caret `^` digunakan untuk memeriksa apakah karakter yang cocok adalah karakter pertama
 dari string input.  Jika kita menerapkan ungkapan reguler berikut ini `^ a` (jika a adalah
 simbol awal) untuk memasukkan string `abc` cocok dengan` a`.  Tetapi jika kita melamar
 ekspresi reguler `^ b` pada string input di atas tidak cocok dengan apa pun.
 Karena dalam string input `abc`" b "bukan simbol awal.  Mari lihat
 di ekspresi reguler lain `^ (T | t) he` yang berarti: karakter huruf besar` T` atau
 karakter huruf kecil `t` adalah simbol awal dari string input, diikuti oleh
 huruf kecil `h`, diikuti oleh huruf kecil` e`.

<pre>
"(T|t)he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in <a href="#learn-regex"><strong>the</strong></a> garage.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/5ljjgB/1)

<pre>
"^(T|t)he" => <a href="#learn-regex"><strong>The</strong></a> car is parked in the garage.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/jXrKne/1)

### 2.8.2 Dolar

 Simbol dolar `$` digunakan untuk memeriksa apakah karakter yang cocok adalah karakter terakhir
 dari string input.  Misalnya, ekspresi reguler `(at \.) $` Berarti: a
 huruf kecil `a`, diikuti oleh huruf kecil` t`, diikuti oleh `.`
 karakter dan pencocokan harus menjadi ujung string.

<pre>
"(at\.)" => The fat c<a href="#learn-regex"><strong>at.</strong></a> s<a href="#learn-regex"><strong>at.</strong></a> on the m<a href="#learn-regex"><strong>at.</strong></a>
</pre>

[Uji ekspresi reguler](https://regex101.com/r/y4Au4D/1)

<pre>
"(at\.)$" => The fat cat. sat. on the m<a href="#learn-regex"><strong>at.</strong></a>
</pre>

[Uji ekspresi reguler](https://regex101.com/r/t0AkOd/1)

## 3. Set Karakter Singkat

 Ekspresi reguler memberikan singkatan untuk set karakter yang umum digunakan,
 yang menawarkan singkatan yang mudah digunakan untuk ekspresi reguler yang umum digunakan.  Itu
 set karakter steno adalah sebagai berikut:

 |Singkatan|Deskripsi|
 |:----:|----|
 |. | Karakter apa pun kecuali baris baru |
 | \ w | Mencocokkan karakter alfanumerik: `[a-zA-Z0-9_]` |
 | \ W | Mencocokkan karakter non-alfanumerik: `[^ \ w]` |
 | \ d | Angka yang cocok: `[0-9]` |
 | \ D | Cocok dengan non-digit: `[^ \ d]` |
 | \ s | Cocok dengan karakter spasi putih: `[\ t \ n \ f \ r \ p {Z}]` |
 | \ S | Cocok dengan karakter non-spasi putih: `[^ \ s]` |

 ## 4. Mencari-cari

 Lookbehind dan lookahead (juga disebut lookaround) adalah tipe tertentu
 *** Grup yang tidak menangkap *** (digunakan untuk mencocokkan pola tetapi tidak termasuk dalam pencocokan
 daftar).  Penelusuran digunakan ketika kami memiliki kondisi pola ini
 didahului atau diikuti oleh pola tertentu lainnya.  Sebagai contoh, kami ingin mendapatkan semuanya
 angka yang diawali dengan karakter `$` dari string input berikut
 `$ 4,44 dan $ 10,88`.  Kami akan menggunakan ekspresi reguler berikut ini `(? <= \ $) [0-9 \.] *`
 yang berarti: dapatkan semua angka yang mengandung karakter `.` dan didahului
 oleh karakter `$`.  Berikut ini adalah lookaround yang digunakan secara teratur
 ekspresi:

 |Simbol|Deskripsi|
 |:----:|----|
 |? = | Positif Penampilan |
 |?! | Pencarian Negatif |
 |? <= | Tampilan Positif |
 |? <! | Tampilan Negatif |

 ### 4.1 Pencarian Positif

 Lookahead positif menyatakan bahwa bagian pertama dari ekspresi harus
 diikuti oleh ekspresi lookahead.  Pencocokan yang dikembalikan hanya berisi teks
 yang dicocokkan dengan bagian pertama dari ekspresi.  Untuk mendefinisikan positif
 lihatlah, kurung digunakan.  Di dalam tanda kurung itu, tanda tanya dengan
 tanda sama digunakan seperti ini: `(? = ...)`.  Ekspresi lookahead ditulis setelah
 tanda sama dengan di dalam tanda kurung.  Misalnya, ekspresi reguler
 `(T | t) he (? = \ Sfat)` berarti: secara opsional cocok dengan huruf kecil `t` atau huruf besar
 huruf `T`, diikuti oleh huruf` h`, diikuti oleh huruf `e`.  Dalam tanda kurung kita
 mendefinisikan lookahead positif yang memberitahu mesin ekspresi reguler untuk mencocokkan `The`
 atau `the` yang diikuti oleh kata` fat`.

<pre>
"(T|t)he(?=\sfat)" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on the mat.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/IDDARt/1)

### 4.2 Pencarian Negatif

 Lookahead negatif digunakan ketika kita perlu mendapatkan semua kecocokan dari string input
 yang tidak diikuti oleh suatu pola.  Lookahead negatif didefinisikan sama seperti yang kita definisikan
 lookahead positif tetapi satu-satunya perbedaan adalah bukan sama dengan karakter `=` kita
 gunakan negasi `!` character i.e. `(?! ...)`.  Mari kita simak yang berikut ini
 ekspresi reguler `(T | t) he (?! \ sfat)` yang berarti: dapatkan semua kata `The` atau` the`
 dari string input yang tidak diikuti oleh kata `fat` diawali oleh spasi
 karakter.

<pre>
"(T|t)he(?!\sfat)" => The fat cat sat on <a href="#learn-regex"><strong>the</strong></a> mat.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/V32Npg/1)

### 4.3 Pandangan Positif

 Tampilan positif di belakang digunakan untuk mendapatkan semua pertandingan yang didahului oleh a
 pola tertentu.  Tampilan positif di belakang dilambangkan dengan `(? <= ...)`.  Misalnya,
 ekspresi reguler `(? <= (T | t) he), (fat | mat)` berarti: dapatkan semua kata `fat` atau` mat`
 dari string input yang setelah kata `The` atau` the`.

<pre>
"(?<=(T|t)he\s)(fat|mat)" => The <a href="#learn-regex"><strong>fat</strong></a> cat sat on the <a href="#learn-regex"><strong>mat</strong></a>.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/avH165/1)

### 4.4 Tampilan Negatif

 Tampilan negatif di belakang digunakan untuk mendapatkan semua pertandingan yang tidak didahului oleh a
 pola tertentu.  Tampilan negatif di belakang dilambangkan dengan `(? <! ...)`.  Misalnya,
 ekspresi reguler `(? <! (T | t) he \ s) (cat)` berarti: dapatkan semua kata `cat` dari input
 string yang tidak setelah kata `The` atau` the`.

<pre>
"(?&lt;!(T|t)he\s)(cat)" => The cat sat on <a href="#learn-regex"><strong>cat</strong></a>.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/8Efx5G/1)

## 5. Bendera

 Bendera juga disebut pengubah karena mereka memodifikasi keluaran reguler
 ekspresi.  Bendera ini dapat digunakan dalam urutan atau kombinasi apa pun, dan merupakan
 bagian integral dari RegExp.

 |Bendera|Deskripsi|
 |:----:|----|
 | i | Peka huruf besar kecil: Mengatur pencocokan menjadi huruf besar-kecil
 | g | Pencarian Global: Mencari pola di seluruh string input. |
 | m | Multiline: Karakter meta jangkar bekerja di setiap baris. |

 ### 5.1 Tidak Peka Huruf

 Pengubah `i` digunakan untuk melakukan pencocokan case-insensitive.  Misalnya,
 ekspresi reguler `/ The / gi` berarti: huruf besar` T`, diikuti oleh huruf kecil
 karakter `h`, diikuti oleh karakter` e`.  Dan di akhir ekspresi reguler
 bendera `i` memberitahu mesin ekspresi reguler untuk mengabaikan case.  Sebisa kamu
 lihat kami juga menyediakan flag `g` karena kami ingin mencari pola di
 seluruh string input.

<pre>
"The" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on the mat.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/dpQyf9/1)

<pre>
"/The/gi" => <a href="#learn-regex"><strong>The</strong></a> fat cat sat on <a href="#learn-regex"><strong>the</strong></a> mat.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/ahfiuh/1)

### 5.2 Pencarian global

 Pengubah `g` digunakan untuk melakukan kecocokan global (temukan semua kecocokan alih-alih
 berhenti setelah pertandingan pertama).  Misalnya, ekspresi reguler` /. (At) / g`
 berarti: karakter apa pun kecuali baris baru, diikuti oleh karakter huruf kecil `a`,
 diikuti oleh karakter huruf kecil `t`.  Karena kami menyediakan flag `g` di akhir
 ekspresi reguler sekarang akan menemukan semua kecocokan dalam string input, bukan hanya yang pertama (yang merupakan perilaku default).

<pre>
"/.(at)/" => The <a href="#learn-regex"><strong>fat</strong></a> cat sat on the mat.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/jnk6gM/1)

<pre>
"/.(at)/g" => The <a href="#learn-regex"><strong>fat</strong></a> <a href="#learn-regex"><strong>cat</strong></a> <a href="#learn-regex"><strong>sat</strong></a> on the <a href="#learn-regex"><strong>mat</strong></a>.
</pre>

[Uji ekspresi reguler](https://regex101.com/r/dO1nef/1)

### 5.3 Multiline

 Pengubah `m` digunakan untuk melakukan pencocokan multi-garis.  Seperti yang kita bahas sebelumnya
 jangkar `(^, $)` digunakan untuk memeriksa apakah pola adalah awal dari input atau
 akhir dari string input.  Tetapi jika kita ingin agar jangkar bekerja pada setiap baris yang kita gunakan
 bendera `m`.  Misalnya, ekspresi reguler `/ at (.)? $ / Gm` berarti: huruf kecil
 karakter `a`, diikuti oleh karakter huruf kecil` t`, opsional apa pun kecuali
 garis baru.  Dan karena flag `m` sekarang mesin ekspresi reguler cocok dengan pola
 di akhir setiap baris dalam sebuah string.

<pre>
"/.at(.)?$/" => The fat
                cat sat
                on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[Uji ekspresi reguler](https://regex101.com/r/hoGMkP/1)

<pre>
"/.at(.)?$/gm" => The <a href="#learn-regex"><strong>fat</strong></a>
                  cat <a href="#learn-regex"><strong>sat</strong></a>
                  on the <a href="#learn-regex"><strong>mat.</strong></a>
</pre>

[Uji ekspresi reguler](https://regex101.com/r/E88WE2/1)

## 6. Pencocokan serakah vs malas
 Secara default regex akan melakukan pencocokan serakah yang artinya akan cocok selama
 bisa jadi.  Kita dapat menggunakan `?` Untuk mencocokkan dengan cara malas yang artinya sesingkat mungkin.

<pre>
"/(.*at)/" => <a href="#learn-regex"><strong>The fat cat sat on the mat</strong></a>. </pre>


[Uji ekspresi reguler](https://regex101.com/r/AyAdgJ/1)

<pre>
"/(.*?at)/" => <a href="#learn-regex"><strong>The fat</strong></a> cat sat on the mat. </pre>


[Uji ekspresi reguler](https://regex101.com/r/AyAdgJ/2)


## Kontribusi

 * Buka permintaan tarik dengan perbaikan
 * Diskusikan ide dalam masalah
 * Sebarkan berita
 * Jangkau dengan umpan balik [![Twitter URL](https://img.shields.io/twitter/url/https/twitter.com/ziishaned.svg?style=social&label=Follow%20%40ziishaned)](https://twitter.com/ziishaned)

## Lisensi
 MIT & salin; [Zeeshan Ahmad](https://twitter.com/ziishaned)

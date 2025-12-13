---
obsidianUIMode: preview
materi: Conventional Commit 1.0.0
sumber:
  - https://www.conventionalcommits.org/en/v1.0.0/
datetime: 2025-12-13T10:03:00
tags:
  - git
  - github
---
---
# Conventional Commits 1.0.0

## Ringkasan

Spesifikasi Conventional Commits adalah konvensi _lightweight_ (ringan) di atas pesan _commit_. Spesifikasi ini menyediakan seperangkat aturan mudah untuk menciptakan riwayat _commit_ yang eksplisit; yang membuatnya lebih mudah untuk menulis alat otomatis di atasnya. Konvensi ini sangat cocok dengan **SemVer** (Semantic Versioning), dengan mendeskripsikan fitur, perbaikan, dan perubahan yang merusak (_breaking changes_) yang dibuat dalam pesan _commit_.

Pesan _commit_ harus distrukturkan sebagai berikut:

```
<tipe>[cakupan-opsional]: <deskripsi>

[body-opsional]

[footer-opsional(s)]
```

_Commit_ tersebut berisi elemen-elemen struktural berikut, untuk mengkomunikasikan maksud kepada pengguna _library_ Anda:

- **`fix`**: _Commit_ dengan **tipe** `fix` menambal (_patches_) _bug_ di basis kode Anda (ini berkorelasi dengan **PATCH** dalam Semantic Versioning).
    
- **`feat`**: _Commit_ dengan **tipe** `feat` memperkenalkan fitur baru pada basis kode (ini berkorelasi dengan **MINOR** dalam Semantic Versioning).
    
- **`BREAKING CHANGE`**: _Commit_ yang memiliki _footer_ **`BREAKING CHANGE:`**, atau menambahkan tanda seru **`!`** setelah tipe/cakupan, memperkenalkan perubahan API yang merusak (_breaking API change_) (berkorelasi dengan **MAJOR** dalam Semantic Versioning). `BREAKING CHANGE` dapat menjadi bagian dari _commit_ dengan **tipe** apa pun.
    
- **Tipe** selain `fix:` dan `feat:` diizinkan, misalnya, `@commitlint/config-conventional` (berdasarkan konvensi Angular) merekomendasikan `build:`, `chore:`, `ci:`, `docs:`, `style:`, `refactor:`, `perf:`, `test:`, dan lainnya.
    
- **Footer** selain `BREAKING CHANGE: <deskripsi>` dapat disediakan dan mengikuti konvensi yang mirip dengan format _git trailer_.

Tipe tambahan tidak diamanatkan oleh spesifikasi Conventional Commits, dan tidak memiliki efek implisit dalam Semantic Versioning (kecuali jika menyertakan `BREAKING CHANGE`). **Cakupan** (scope) dapat diberikan pada tipe _commit_, untuk memberikan informasi kontekstual tambahan dan dimuat dalam tanda kurung, misalnya, `feat(parser): add ability to parse arrays`.

## Contoh

### Pesan commit dengan deskripsi dan breaking change footer

```
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files
```

### Pesan commit dengan `!` untuk menarik perhatian pada breaking change

```
feat!: send an email to the customer when a product is shipped
```

### Pesan commit dengan cakupan (scope) dan `!` untuk menarik perhatian pada breaking change

```
feat(api)!: send an email to the customer when a product is shipped
```

### Pesan commit dengan kedua `!` dan BREAKING CHANGE footer

```
chore!: drop support for Node 6

BREAKING CHANGE: use JavaScript features not available in Node 6.
```

### Pesan commit tanpa body

```
docs: correct spelling of CHANGELOG
```

### Pesan commit dengan cakupan (scope)

```
feat(lang): add Polish language
```

### Pesan commit dengan body multi-paragraf dan beberapa footer

```
fix: prevent racing of requests

Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

Remove timeouts which were used to mitigate the racing issue but are
obsolete now.

Reviewed-by: Z
Refs: #123
```


## Spesifikasi Conventional Commits (RFC 2119 Compliance)

Kata kunci "MUST" (HARUS), "MUST NOT" (TIDAK HARUS), "REQUIRED" (DIPERLUKAN), "SHALL" (WAJIB), "SHALL NOT" (TIDAK WAJIB), "SHOULD" (SEBAIKNYA), "SHOULD NOT" (SEBAIKNYA TIDAK), "RECOMMENDED" (DIREKOMENDASIKAN), "MAY" (BOLEH), dan "OPTIONAL" (OPSIONAL) dalam dokumen ini diinterpretasikan sebagaimana dijelaskan dalam RFC 2119.

- _Commit_ **HARUS** diawali dengan sebuah **tipe**, yang terdiri dari kata benda (_noun_), seperti `feat`, `fix`, dll., diikuti oleh _scope_ **OPSIONAL**, tanda seru `!` **OPSIONAL**, dan **DIPERLUKAN** titik dua (kolon) dan spasi di akhir.
    
- Tipe **`feat`** **HARUS** digunakan ketika _commit_ menambahkan fitur baru ke aplikasi atau _library_ Anda.
    
- Tipe **`fix`** **HARUS** digunakan ketika _commit_ merepresentasikan perbaikan _bug_ untuk aplikasi Anda.
    
- Sebuah **scope** **BOLEH** disediakan setelah sebuah tipe. _Scope_ **HARUS** terdiri dari kata benda yang mendeskripsikan bagian basis kode yang dikelilingi oleh tanda kurung, misalnya, `fix(parser):`.
    
- Sebuah **deskripsi** **HARUS** segera mengikuti titik dua dan spasi setelah awalan tipe/scope. Deskripsi adalah ringkasan singkat dari perubahan kode, misalnya, `fix: array parsing issue when multiple spaces were contained in string`.
    
- _Body_ _commit_ yang lebih panjang **BOLEH** disediakan setelah deskripsi singkat, memberikan informasi kontekstual tambahan tentang perubahan kode. _Body_ **HARUS** dimulai satu baris kosong setelah deskripsi.
    
- _Body_ _commit_ bersifat _free-form_ (bentuk bebas) dan **BOLEH** terdiri dari sejumlah paragraf yang dipisahkan oleh _newline_.
    
- Satu atau lebih **footer** **BOLEH** disediakan satu baris kosong setelah _body_. Setiap _footer_ **HARUS** terdiri dari _token_ kata, diikuti oleh pemisah berupa `:<spasi>` atau `<spasi>#`, diikuti oleh nilai _string_ (ini terinspirasi oleh konvensi _git trailer_).
    
- _Token_ _footer_ **HARUS** menggunakan tanda `-` sebagai pengganti karakter spasi, misalnya, `Acked-by` (ini membantu membedakan bagian _footer_ dari _body_ multi-paragraf). Pengecualian dibuat untuk `BREAKING CHANGE`, yang **BOLEH** juga digunakan sebagai _token_.
    
- Nilai _footer_ **BOLEH** berisi spasi dan _newline_, dan _parsing_ **HARUS** dihentikan ketika pasangan _token_/pemisah _footer_ valid berikutnya diamati.
    
- **Perubahan yang merusak (_Breaking changes_)** **HARUS** diindikasikan di awalan tipe/scope dari _commit_, atau sebagai entri di _footer_.
    
- Jika dimasukkan sebagai _footer_, perubahan yang merusak **HARUS** terdiri dari teks huruf kapital **BREAKING CHANGE**, diikuti oleh titik dua, spasi, dan deskripsi, misalnya, `BREAKING CHANGE: environment variables now take precedence over config files`.
    
- Jika dimasukkan dalam awalan tipe/scope, perubahan yang merusak **HARUS** diindikasikan dengan tanda seru **`!`** segera sebelum `:`. Jika `!` digunakan, `BREAKING CHANGE:` **BOLEH** dihilangkan dari bagian _footer_, dan deskripsi _commit_ **WAJIB** digunakan untuk mendeskripsikan perubahan yang merusak.
    
- Tipe selain `feat` dan `fix` **BOLEH** digunakan dalam pesan _commit_ Anda, misalnya, `docs: update ref docs`.
    
- Unit-unit informasi yang membentuk Conventional Commits **TIDAK HARUS** diperlakukan sebagai sensitif huruf besar/kecil oleh implementor, dengan pengecualian `BREAKING CHANGE` yang **HARUS** berupa huruf kapital.
    
- `BREAKING-CHANGE` **HARUS** bersinonim dengan `BREAKING CHANGE`, ketika digunakan sebagai _token_ di _footer_.
    

## Mengapa Menggunakan Conventional Commits

- Menghasilkan _CHANGELOG_ secara otomatis.
    
- Secara otomatis menentukan kenaikan versi semantik (_semantic version bump_) (berdasarkan tipe _commit_ yang masuk).
    
- Mengkomunikasikan sifat perubahan kepada rekan tim, publik, dan pemangku kepentingan lainnya.
    
- Memicu proses _build_ dan _publish_.
    
- Mempermudah orang untuk berkontribusi pada proyek Anda, dengan memungkinkan mereka menjelajahi riwayat _commit_ yang lebih terstruktur.


## Tanya Jawab (FAQ) Conventional Commits

### Bagaimana saya harus menangani pesan _commit_ di fase pengembangan awal?

Kami merekomendasikan Anda untuk melanjutkan seolah-olah Anda sudah merilis produk. Biasanya **seseorang**, bahkan jika itu adalah rekan pengembang _software_ Anda, sedang menggunakan _software_ Anda. Mereka pasti ingin tahu apa yang diperbaiki (_fixed_), apa yang rusak (_breaks_), dll.

### Apakah tipe dalam judul _commit_ menggunakan huruf besar atau huruf kecil?

Penggunaan huruf besar/kecil apa pun **diperbolehkan**, tetapi yang terbaik adalah **konsisten**.

### Apa yang harus saya lakukan jika _commit_ sesuai dengan lebih dari satu tipe _commit_?

Kembalilah dan buat **beberapa _commit_** jika memungkinkan. Salah satu manfaat dari Conventional Commits adalah kemampuannya mendorong kita untuk membuat _commit_ dan _Pull Request_ (PR) yang lebih terorganisir.

### Apakah ini tidak menghalangi pengembangan cepat dan iterasi cepat?

Ini menghalangi bergerak cepat dengan cara yang **tidak terorganisir**. Ini membantu Anda untuk dapat bergerak cepat dalam jangka panjang di berbagai proyek dengan kontributor yang beragam.

### Mungkinkah Conventional Commits membuat pengembang membatasi jenis _commit_ yang mereka buat karena mereka akan berpikir dalam tipe yang tersedia?

Conventional Commits mendorong kita untuk membuat lebih banyak tipe _commit_ tertentu seperti perbaikan (_fixes_). Selain itu, fleksibilitas Conventional Commits memungkinkan tim Anda membuat tipe mereka sendiri dan mengubah tipe tersebut dari waktu ke waktu.

### Bagaimana ini berhubungan dengan SemVer (Semantic Versioning)?

_Commit_ tipe **`fix`** harus diterjemahkan menjadi rilis **PATCH**. _Commit_ tipe **`feat`** harus diterjemahkan menjadi rilis **MINOR**. _Commit_ dengan **`BREAKING CHANGE`** di dalamnya, terlepas dari tipenya, harus diterjemahkan menjadi rilis **MAJOR**.

### Bagaimana saya seharusnya membuat versi ekstensi saya untuk Spesifikasi Conventional Commits, misalnya, `@jameswomack/conventional-commit-spec`?

Kami merekomendasikan penggunaan SemVer untuk merilis ekstensi Anda sendiri pada spesifikasi ini (dan kami mendorong Anda untuk membuat ekstensi ini!)

### Apa yang harus saya lakukan jika saya tidak sengaja menggunakan tipe _commit_ yang salah?

- **Ketika Anda menggunakan tipe yang termasuk dalam spesifikasi tetapi bukan tipe yang benar (misalnya, `fix` alih-alih `feat`):** Sebelum me-_merge_ atau merilis kesalahan tersebut, kami merekomendasikan penggunaan `git rebase -i` untuk mengedit riwayat _commit_. Setelah dirilis, proses pembersihan akan berbeda sesuai dengan alat dan proses yang Anda gunakan.
    
- **Ketika Anda menggunakan tipe yang _tidak_ termasuk dalam spesifikasi (misalnya, `feet` alih-alih `feat`):** Dalam skenario terburuk, tidak masalah besar jika _commit_ yang tidak memenuhi spesifikasi Conventional Commits masuk. Itu hanya berarti _commit_ tersebut akan dilewatkan oleh alat yang didasarkan pada spesifikasi.
    

### Apakah semua kontributor saya perlu menggunakan spesifikasi Conventional Commits?

Tidak! Jika Anda menggunakan alur kerja berbasis _squash_ di Git, pengelola utama dapat membersihkan pesan _commit_ saat digabungkan—tanpa menambah beban kerja pada _committer_ kasual. Alur kerja umum untuk ini adalah meminta sistem Git Anda secara otomatis me-_squash_ _commit_ dari _pull request_ dan menyajikan formulir bagi pengelola utama untuk memasukkan pesan _git commit_ yang sesuai untuk _merge_.

### Bagaimana Conventional Commits menangani _revert commits_?

Mengembalikan kode (_reverting code_) bisa rumit: apakah Anda mengembalikan beberapa _commit_? Jika Anda mengembalikan fitur, apakah rilis berikutnya harus berupa _patch_?

Conventional Commits tidak membuat upaya eksplisit untuk mendefinisikan perilaku _revert_. Sebaliknya, kami menyerahkannya kepada pembuat alat untuk menggunakan fleksibilitas **tipe** dan **footer** untuk mengembangkan logika mereka dalam menangani _revert_.

Satu rekomendasi adalah menggunakan tipe **`revert`**, dan _footer_ yang mereferensikan SHA _commit_ yang sedang dikembalikan:

```
revert: let us never again speak of the noodle incident

Refs: 676104e, a215868
```

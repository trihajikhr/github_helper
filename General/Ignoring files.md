---
obsidianUIMode: preview
materi: Ignoring files
sumber:
  - docs.github.com
datetime: 2026-01-12T23:06:00
tags:
  - gitignore
---
Link Sumber: [Ignoring files - GitHub Docs](https://docs.github.com/en/get-started/git-basics/ignoring-files)

---
# Ignoring files

Anda dapat mengonfigurasi Git untuk mengabaikan file yang tidak ingin Anda masukkan (_check in_) ke GitHub.

## Mengonfigurasi file yang diabaikan untuk satu repository

Anda dapat membuat file _.gitignore_ di root directory repository Anda untuk memberi tahu Git file dan directories mana yang harus diabaikan saat Anda membuat sebuah _commit_. Untuk membagikan aturan pengabaian (_ignore rules_) dengan pengguna lain yang melakukan _clone repository_, lakukan _commit_ pada file _.gitignore_ ke dalam repository Anda.

GitHub mengelola daftar resmi file _.gitignore_ yang direkomendasikan untuk banyak operating systems, environments, dan bahasa pemrograman populer di _public repository_ "github/gitignore". Anda juga dapat menggunakan gitignore.io untuk membuat file _.gitignore_ bagi _operating system_, bahasa pemrograman, atau _IDE_ Anda. Untuk informasi lebih lanjut, lihat [github/gitignore](https://github.com/github/gitignore) dan situs [gitignore.io](https://www.gitignore.io/).

1. Buka Git Bash.
2. Navigasikan ke lokasi Git repository Anda.
3. Buat file .gitignore untuk repository Anda.

```bash
touch .gitignore
```

4. Jika perintah berhasil, tidak akan ada _output_.

Untuk contoh file _.gitignore_, lihat [Some common .gitignore configurations](https://gist.github.com/octocat/9257657) di _repository_ Octocat.

Jika Anda ingin mengabaikan file yang sudah terlanjur masuk (checked in), Anda harus menghapus pelacakan (untrack) file tersebut sebelum Anda menambahkan aturan untuk mengabaikannya. Dari terminal Anda, lakukan untrack pada file tersebut.

```bash
git rm --cached FILENAME
```

## Mengonfigurasi file yang diabaikan untuk semua repository di komputer Anda

Anda dapat memberi tahu Git untuk selalu mengabaikan file atau _directories_ tertentu saat Anda membuat _commit_ di Git repository mana pun di komputer Anda. Sebagai contoh, Anda dapat menggunakan fitur ini untuk mengabaikan file cadangan sementara (_temporary backup files_) apa pun yang dibuat oleh _text editor_ Anda.

Untuk selalu mengabaikan file atau _directory_ tertentu, tambahkan hal tersebut ke file bernama _ignore_ yang terletak di dalam _directory_ `~/.config/git`. Secara standar (_by default_), Git akan mengabaikan file dan _directories_ apa pun yang tercantum dalam file konfigurasi global (_global configuration file_) `~/.config/git/ignore`. Jika _directory_ _git_ dan file _ignore_ belum ada, Anda mungkin perlu membuatnya.

## Mengecualikan file lokal tanpa membuat file .gitignore

Jika Anda tidak ingin membuat file _.gitignore_ untuk dibagikan dengan orang lain, Anda dapat membuat aturan yang tidak di-_commit_ bersama _repository_. Anda dapat menggunakan teknik ini untuk file yang dihasilkan secara lokal (_locally-generated files_) yang tidak Anda harapkan dihasilkan oleh pengguna lain, seperti file yang dibuat oleh editor Anda.

Gunakan _text editor_ favorit Anda untuk membuka file bernama `.git/info/exclude` di dalam _root_ dari Git repository Anda. Aturan apa pun yang Anda tambahkan di sini tidak akan dimasukkan (_checked in_), dan hanya akan mengabaikan file untuk _local repository_ Anda.

1. Buka Git Bash.
2. Navigasikan ke lokasi Git repository Anda.
3. Menggunakan _text editor_ favorit Anda, buka file `.git/info/exclude`.


## Bacaan Lebih Lanjut

- [Ignoring files](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository#_ignoring) dalam dokumentasi Git
- [.gitignore](https://git-scm.com/docs/gitignore) dalam dokumentasi Git
- [Koleksi templat .gitignore](https://github.com/github/gitignore) yang berguna dalam _repository_ github/gitignore
- Situs [gitignore.io](https://www.gitignore.io/)

## Format penulisan .gitignore

Berikut adalah materi mengenai berbagai cara mengonfigurasi aturan pengabaian (_ignore rules_) pada file `.gitignore`. Materi ini mencakup berbagai pola, mulai dari yang sederhana hingga yang spesifik menggunakan **glob patterns**.

Dalam file `.gitignore`, setiap baris menentukan pola untuk file atau _directory_ yang ingin diabaikan. Berikut adalah berbagai cara penerapannya:

### 1. Mengabaikan File dengan Nama Tertentu

Jika Anda ingin mengabaikan file spesifik tanpa peduli di mana letaknya dalam _repository_.

- `config.log` — Mengabaikan semua file bernama `config.log`.
- `debug.txt` — Mengabaikan semua file bernama `debug.txt`.

### 2. Mengabaikan File dengan Ekstensi Tertentu

Gunakan karakter _wildcard_ (`*`) untuk mengabaikan semua file berdasarkan jenis ekstensinya.

- `*.log` — Mengabaikan semua file yang berakhiran `.log`.
- `*.tmp` — Mengabaikan semua file sementara dengan ekstensi `.tmp`.
- `*.pdf` — Mengabaikan semua dokumen PDF.

### 3. Mengabaikan Semua Isi Folder (Directory)

Untuk mengabaikan seluruh folder beserta semua isinya, tambahkan tanda garis miring (`/`) di akhir nama folder.

- `node_modules/` — Mengabaikan folder `node_modules` dan semua file/subfolder di dalamnya.
- `bin/` — Mengabaikan folder hasil kompilasi.
- `temp/` — Mengabaikan folder penyimpanan sementara.

### 4. Mengabaikan Jalur Spesifik (Root Specific)

Jika Anda hanya ingin mengabaikan file di _root directory_, namun membiarkan file dengan nama yang sama di subfolder lain tetap terlacak.

- `/todo.txt` — Hanya mengabaikan `todo.txt` di folder utama (_root_). File `pribadi/todo.txt` tidak akan diabaikan.

### 5. Mengabaikan Berdasarkan Pola Karakter (Glob Patterns)

Anda bisa menggunakan pola yang lebih fleksibel untuk menangkap variasi nama file.

- `test?.txt` — Mengabaikan file seperti `test1.txt`, `testA.txt`, namun tidak `test12.txt` (tanda `?` mewakili tepat satu karakter).
- `results.[0-9]` — Mengabaikan `results.0`, `results.1`, dst.

### 6. Mengabaikan File di Folder Mana Pun (Double Asterisk)

Gunakan simbol `**` untuk mencocokkan _directories_ secara rekursif.

- `**/logs/*.txt` — Mengabaikan semua file `.txt` di dalam folder bernama `logs` di mana pun folder itu berada (misal: `/logs/a.txt` atau `/src/app/logs/b.txt`).
- `docs/**/*.pdf` — Mengabaikan semua file PDF di bawah folder `docs` dan seluruh subfolder di bawahnya.

### 7. Pengecualian Aturan (Negation)

Jika Anda mengabaikan seluruh kategori file tetapi ingin tetap melacak satu file spesifik, gunakan tanda seru (`!`).

- `*.log`
- `!important.log` (Artinya: Abaikan semua file .log, KECUALI` important.log`).

### 8. Mengabaikan File dengan Nama yang Sama tetapi Berbeda Huruf Besar/Kecil

Secara _default_, Git biasanya bersifat _case-sensitive_ tergantung pada sistem operasi. Namun, untuk memastikan keamanan, Anda bisa menuliskan pola seperti ini:

- `[Bb]ackup.zip` — Mengabaikan baik `Backup.zip` maupun `backup.zip`.


### Ringkasan Tabel Referensi Cepat

|**Pola**|**Deskripsi**|
|---|---|
|`filename.txt`|Mengabaikan file dengan nama tersebut di folder mana pun.|
|`*.ext`|Mengabaikan semua file dengan ekstensi tertentu.|
|`directory/`|Mengabaikan seluruh folder dan isinya.|
|`/file.txt`|Hanya mengabaikan file di _root directory_.|
|`dir/**/*.txt`|Mengabaikan semua file `.txt` di dalam `dir` dan seluruh subfoldernya.|
|`!file.txt`|Menandakan pengecualian (file ini tidak akan diabaikan).|

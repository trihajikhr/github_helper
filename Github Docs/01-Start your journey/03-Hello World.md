---
obsidianUIMode: preview
materi: Hello World
sumber:
  - docs.github.com
datetime: 2025-11-08T11:10:00
tags:
  - git
  - github
---
Link Sumber: [Hello World - GitHub Docs](https://docs.github.com/en/get-started/start-your-journey/hello-world)

---
# Hello World

## Pendahuluan

Tutorial ini mengajarkan hal-hal penting GitHub seperti repository, branches, commits, dan pull requests. Anda akan membuat repositori **Hello World** Anda sendiri dan mempelajari alur kerja pull request GitHub, cara populer untuk membuat dan meninjau kode.

Dalam panduan singkat ini, Anda akan:

* Membuat dan menggunakan repository.
* Memulai dan mengelola branch baru.
* Membuat perubahan pada file dan push ke GitHub sebagai commits.
* Membuka dan merge pull request

### Prasyarat

Anda harus sudah memiliki akun GitHub. Untuk informasi lebih lanjut, [Creating an account on GitHub](https://docs.github.com/en/get-started/start-your-journey/creating-an-account-on-github).

Anda tidak perlu tahu cara membuat kode, menggunakan command line, atau menginstal Git (perangkat lunak kontrol versi yang menjadi dasar dibangunnya GitHub).

---

## Langkah 1: Membuat Repositori

Hal pertama yang akan kita lakukan adalah membuat repository. Anda dapat menganggap repository sebagai **folder** yang berisi item-item terkait, seperti file, gambar, video, atau bahkan folder lainnya. Repository biasanya mengelompokkan item yang termasuk dalam "proyek" yang sama atau hal yang sedang Anda kerjakan.

Seringkali, repositori menyertakan berkas **README**, yaitu berkas yang berisi informasi tentang proyek Anda. Berkas README ditulis dalam **Markdown**, yang merupakan bahasa yang mudah dibaca dan mudah ditulis untuk memformat teks biasa. Kita akan mempelajari lebih lanjut tentang Markdown di tutorial berikutnya, [Setting up your profile](https://docs.github.com/en/get-started/start-your-journey/setting-up-your-profile).

GitHub memungkinkan Anda menambahkan berkas README pada saat yang sama ketika Anda membuat repository baru. GitHub juga menawarkan opsi umum lainnya seperti berkas lisensi, tetapi Anda tidak perlu memilih salah satunya sekarang.

Repository *hello-world* Anda dapat menjadi tempat di mana Anda menyimpan ide, sumber daya, atau bahkan berbagi dan mendiskusikan berbagai hal dengan orang lain.

1. Di sudut kanan atas halaman mana pun, pilih ikon **+**, lalu klik **New repository**.

	![](~src/03-Hello%20World.png)

2. Di kotak "**Repository name**", ketik **hello-world**.
3. Di kotak "**Description**", ketik deskripsi singkat. Contohnya, ketik "This repository is for practicing the GitHub Flow."
4. Pilih apakah repositori Anda akan **Public** atau **Private**.
5. Pilih opsi **Add a README file**.
6. Klik **Create repository**.


---

## Langkah 2: Membuat *Branch*

*Branching* (pencabangan) memungkinkan Anda memiliki versi repository yang berbeda pada satu waktu.

Secara *default*, repository Anda memiliki satu branch bernama `main` yang dianggap sebagai branch definitif (utama). Anda dapat membuat branch tambahan dari `main` di repository Anda.

*Branching* sangat membantu ketika Anda ingin menambahkan fitur baru ke sebuah proyek tanpa mengubah sumber kode utama. Pekerjaan yang dilakukan pada branch yang berbeda tidak akan muncul pada branch utama sampai Anda *merge*, yang akan kita bahas nanti dalam panduan ini. Anda dapat menggunakan branch untuk bereksperimen dan membuat pengeditan sebelum menerapkan *commit* perubahan tersebut ke `main`.

Ketika Anda membuat branch dari branch `main`, Anda membuat salinan, atau cuplikan (*snapshot*), dari `main` pada saat itu. Jika orang lain membuat perubahan pada branch `main` saat Anda sedang mengerjakan branch Anda, Anda dapat  *pull* pembaruan tersebut.

Diagram ini menunjukkan:

* Cabang `main`.
* Cabang baru yang disebut `feature`.
* Perjalanan yang dilalui `feature` melalui tahapan "**Commit changes**" (Komit perubahan), "**Submit pull request**" (Kirim permintaan tarik), dan "**Discuss proposed changes**" (Diskusikan perubahan yang diusulkan) sebelum dimerged ke dalam `main`.

![](~src/03-Hello%20World-1.png)



### Membuat Branch

1.  Klik *tab* **Code** pada repository `hello-world` Anda.
2.  Di atas daftar berkas, klik menu *dropdown* yang bertuliskan `main`.
   
	   ![](~src/03-Hello%20World-2.png)
   
3.  Ketik nama cabang, `readme-edits`, ke dalam kotak teks.
4.  Klik **Create branch: readme-edits from main**.

	![](~src/03-Hello%20World-3.png)

Sekarang Anda memiliki dua cabang, `main` dan `readme-edits`. Saat ini, keduanya terlihat persis sama. Selanjutnya, Anda akan menambahkan perubahan pada cabang baru `readme-edits`.

---

## Langkah 3: Membuat Perubahan dan Melakukan Commit

Ketika Anda membuat branch baru pada langkah sebelumnya, GitHub membawa Anda ke halaman kode untuk cabang `readme-edits` Anda yang baru, yang merupakan salinan dari `main`.

Anda dapat membuat dan menyimpan perubahan pada berkas di repository Anda. Di GitHub, perubahan yang tersimpan disebut **commits**. Setiap *commit* memiliki pesan *commit* terkait, yaitu deskripsi yang menjelaskan mengapa perubahan tertentu dibuat. Pesan *commit* mencatat riwayat perubahan Anda sehingga kontributor lain dapat memahami apa yang telah Anda lakukan dan alasannya.

1.  Di bawah cabang `readme-edits` yang Anda buat, klik berkas `README.md`.
2.  Untuk mengedit berkas, klik ikon pensil ✏️
3.  Di editor, tulis sedikit tentang diri Anda.
4.  Klik **Commit changes** (Terapkan perubahan).
5.  Di kotak "Commit changes", tulis pesan *commit* yang mendeskripsikan perubahan Anda.
6.  Klik **Commit changes** (Terapkan perubahan).

Perubahan ini hanya akan dilakukan pada berkas README di cabang `readme-edits` Anda, sehingga sekarang cabang ini berisi konten yang berbeda dari `main`.

---

Tentu, ini terjemahan untuk Langkah 4: Membuka *Pull Request*:

## 📬 Langkah 4: Membuka *Pull Request*

Setelah Anda memiliki perubahan pada cabang yang merupakan turunan dari **main**, Anda dapat membuka *pull request* (permintaan tarik).

*Pull request* adalah inti dari kolaborasi di GitHub. Ketika Anda membuka *pull request*, Anda mengajukan perubahan Anda dan meminta seseorang untuk meninjau dan menarik (*pull*) kontribusi Anda dan menggabungkannya (*merge*) ke dalam cabang mereka. *Pull request* menunjukkan *diffs* (perbedaan), atau perbedaan konten dari kedua cabang. Perubahan, penambahan, dan pengurangan ditampilkan dalam warna yang berbeda.

Segera setelah Anda membuat *commit*, Anda dapat membuka *pull request* dan memulai diskusi, bahkan sebelum kodenya selesai.

Pada langkah ini, Anda akan membuka *pull request* di repositori Anda sendiri dan kemudian menggabungkannya sendiri. Ini adalah cara yang bagus untuk melatih alur GitHub sebelum mengerjakan proyek yang lebih besar.

1.  Klik *tab* **Pull requests** pada repositori **hello-world** Anda.
2.  Klik **New pull request** (Pull request baru).
3.  Di kotak **Example Comparisons** (Perbandingan Contoh), pilih cabang yang Anda buat, **readme-edits**, untuk dibandingkan dengan **main** (aslinya).
4.  Periksa perubahan Anda di bagian *diffs* pada halaman Bandingkan (*Compare*), pastikan perubahan tersebut adalah yang ingin Anda kirimkan.

![](~src/03-Hello%20World-4.png)


Tentu, ini terjemahan langkah-langkah berikutnya, termasuk proses tinjauan (*review*):

## 📝 Menyelesaikan *Pull Request*

1.  Klik **Create pull request** (Buat *pull request*).
2.  Berikan **judul** pada *pull request* Anda dan tulis **deskripsi singkat** tentang perubahan Anda. Anda dapat menyertakan emoji, serta menarik dan meletakkan (*drag and drop*) gambar dan GIF.
3.  Klik **Create pull request** (Buat *pull request*).

### Meninjau *Pull Request*

Ketika Anda mulai berkolaborasi dengan orang lain, inilah saatnya Anda akan meminta tinjauan mereka. Ini memungkinkan kolaborator Anda untuk mengomentari, atau mengusulkan perubahan pada, *pull request* Anda sebelum Anda menggabungkan (*merge*) perubahan tersebut ke dalam cabang **main**.

Kami tidak akan membahas peninjauan *pull request* dalam tutorial ini, tetapi jika Anda tertarik untuk mempelajari lebih lanjut, lihat **Tentang tinjauan *pull request***. Atau, coba kursus **GitHub Skills** "Meninjau *pull request*".

---

Langkah terakhir dari tutorial ini adalah menggabungkan (*merging*) *pull request* tersebut. Apakah Anda ingin melanjutkan terjemahan?

Tentu, berikut adalah terjemahan untuk Langkah 5 dan Kesimpulan dari tutorial tersebut:

## 5️⃣ Langkah 5: Menggabungkan (*Merge*) *Pull Request* Anda

Pada langkah terakhir ini, Anda akan menggabungkan (*merge*) cabang **readme-edits** Anda ke dalam cabang **main**. Setelah Anda menggabungkan *pull request* Anda, perubahan pada cabang **readme-edits** Anda akan dimasukkan ke dalam **main**.

Terkadang, *pull request* dapat memperkenalkan perubahan kode yang **berkonflik** dengan kode yang sudah ada di **main**. Jika ada konflik, GitHub akan memberi tahu Anda tentang kode yang berkonflik dan mencegah penggabungan sampai konflik diselesaikan. Anda dapat membuat *commit* yang menyelesaikan konflik atau menggunakan komentar di *pull request* untuk mendiskusikan konflik dengan anggota tim Anda.

Dalam panduan ini, Anda seharusnya tidak memiliki konflik apa pun, jadi Anda siap untuk menggabungkan cabang Anda ke dalam cabang utama.

1.  Di bagian bawah *pull request*, klik **Merge pull request** (Gabungkan *pull request*) untuk menggabungkan perubahan ke dalam **main**.
2.  Klik **Confirm merge** (Konfirmasi penggabungan). Anda akan menerima pesan bahwa permintaan berhasil digabungkan dan permintaan ditutup.
3.  Klik **Delete branch** (Hapus cabang). Sekarang *pull request* Anda sudah digabungkan dan perubahan Anda ada di **main**, Anda dapat menghapus cabang **readme-edits** dengan aman. Jika Anda ingin membuat lebih banyak perubahan pada proyek Anda, Anda selalu dapat membuat cabang baru dan mengulangi proses ini.
4.  Klik kembali ke *tab* **Code** (Kode) repositori **hello-world** Anda untuk melihat perubahan Anda yang telah dipublikasikan di **main**.

## ✅ Kesimpulan

Dengan menyelesaikan tutorial ini, Anda telah belajar membuat proyek dan membuat *pull request* di GitHub.

Sebagai bagian dari itu, kita telah belajar bagaimana:

* Membuat repositori.
* Memulai dan mengelola cabang baru.
* Mengubah berkas dan menerapkan (*commit*) perubahan tersebut ke GitHub.
* Membuka dan menggabungkan *pull request*.

### Langkah Selanjutnya

Lihat profil GitHub Anda dan Anda akan melihat pekerjaan Anda tercermin pada grafik kontribusi Anda.

Jika Anda ingin melatih keterampilan yang telah Anda pelajari dalam tutorial ini lagi, coba kursus **GitHub Skills** "Pengantar GitHub (*Introduction to GitHub*)".

Dalam tutorial berikutnya, **Menyiapkan profil Anda (*Setting up your profile*)**, Anda akan belajar cara mempersonalisasi profil Anda dan Anda juga akan mempelajari beberapa sintaks dasar **Markdown** untuk menulis di GitHub.

---

Semua teks yang Anda berikan telah selesai diterjemahkan! Apakah ada hal lain yang bisa saya bantu, mungkin terkait penggunaan GitHub atau terjemahan lainnya?
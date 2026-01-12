---
obsidianUIMode: preview
materi: About Git
sumber:
  - docs.github.com
datetime: 2025-11-08T11:48:00
tags:
  - git
  - github
---
Link Sumber: [About Git - GitHub Docs](https://docs.github.com/en/get-started/using-git/about-git)

---
# About Git

## Tentang Kontrol Versi (*version control*) dan *Git*

Sistem kontrol versi, atau *VCS* (*Version Control System*), melacak riwayat perubahan saat orang dan tim berkolaborasi dalam suatu proyek. Saat *developer* membuat perubahan pada proyek, setiap versi awal dari proyek tersebut dapat dipulihkan kapan saja.

Para *developer* dapat meninjau riwayat proyek untuk mengetahui:

* Perubahan apa yang dibuat?
* Siapa yang membuat perubahan?
* Kapan perubahan itu dibuat?
* Mengapa perubahan itu diperlukan?

*VCS* memberikan setiap kontributor pandangan yang terpadu dan konsisten terhadap suatu proyek, menampilkan pekerjaan yang sudah berjalan. Melihat riwayat perubahan yang transparan, siapa yang membuatnya, dan bagaimana perubahan tersebut berkontribusi pada pengembangan proyek membantu anggota tim tetap selaras saat bekerja secara mandiri.

Dalam sistem kontrol versi terdistribusi (*distributed version control system*), setiap *developer* memiliki salinan lengkap dari proyek dan riwayat proyek. Berbeda dengan sistem kontrol versi terpusat yang pernah populer, *DVCS* (*Distributed Version Control System*) tidak memerlukan koneksi konstan ke *repository* pusat. *Git* adalah sistem kontrol versi terdistribusi yang paling populer. *Git* umumnya digunakan untuk pengembangan *software* sumber terbuka (*open source*) dan komersial, dengan manfaat signifikan bagi individu, tim, dan bisnis.

*Git* memungkinkan *developer* melihat seluruh linimasa perubahan, keputusan, dan perkembangan proyek apa pun di satu tempat. Sejak saat mereka mengakses riwayat proyek, *developer* memiliki semua konteks yang mereka butuhkan untuk memahaminya dan mulai berkontribusi.

Para *developer* bekerja di setiap zona waktu. Dengan *DVCS* seperti *Git*, kolaborasi dapat terjadi kapan saja sambil menjaga integritas kode sumber. Menggunakan *branches*, *developer* dapat dengan aman mengusulkan perubahan pada kode produksi.

Bisnis yang menggunakan *Git* dapat mendobrak hambatan komunikasi antar tim dan membuat mereka fokus pada pekerjaan terbaik mereka. Selain itu, *Git* memungkinkan untuk menyelaraskan para ahli di seluruh bisnis untuk berkolaborasi dalam proyek-proyek besar.

---

## Tentang *Repositories*

Sebuah *repository*, atau proyek *Git*, mencakup seluruh koleksi *files* (berkas) dan *folders* (folder) yang terkait dengan sebuah proyek, beserta riwayat revisi setiap *file*. Riwayat *file* muncul sebagai cuplikan waktu yang disebut *commits*. *Commits* dapat diorganisir menjadi beberapa lini pengembangan yang disebut *branches*. Karena *Git* adalah *DVCS*, *repositories* adalah unit yang mandiri (*self-contained*) dan siapa pun yang memiliki salinan *repository* dapat mengakses seluruh *codebase* dan riwayatnya. Menggunakan *command line* atau antarmuka yang mudah digunakan lainnya, sebuah *Git repository* juga memungkinkan untuk: interaksi dengan riwayat, *cloning* *repository*, membuat *branches*, *committing*, *merging*, membandingkan perubahan di seluruh versi kode, dan banyak lagi.

Melalui *platform* seperti *GitHub*, *Git* juga memberikan lebih banyak peluang untuk transparansi dan kolaborasi proyek. *Repositories* publik membantu tim bekerja sama untuk membangun produk akhir terbaik.

---

## Cara Kerja *GitHub*

*GitHub* menghosting *Git repositories* dan menyediakan *tools* bagi *developer* untuk mengirimkan kode yang lebih baik melalui fitur *command line*, *issues* (diskusi berulir), *pull requests*, *code review*, atau penggunaan koleksi aplikasi gratis dan berbayar di *GitHub Marketplace*. Dengan lapisan kolaborasi seperti *GitHub flow*, komunitas yang terdiri dari 100 juta *developer*, dan ekosistem dengan ratusan integrasi, *GitHub* mengubah cara *software* dibuat.

*GitHub* membangun kolaborasi secara langsung ke dalam proses pengembangan. Pekerjaan diatur ke dalam *repositories* di mana *developer* dapat menguraikan persyaratan atau arahan dan menetapkan ekspektasi untuk anggota tim. Kemudian, menggunakan *GitHub flow*, *developer* cukup membuat *branch* untuk mengerjakan *updates*, *commit* perubahan untuk menyimpannya, membuka *pull request* untuk mengusulkan dan mendiskusikan perubahan, dan *merge* *pull requests* setelah semua orang sepakat. Untuk informasi lebih lanjut, lihat [GitHub flow](https://docs.github.com/en/get-started/using-github/github-flow).

Untuk paket dan biaya *GitHub*, lihat [GitHub Pricing](https://github.com/pricing). Untuk informasi tentang perbandingan *GitHub Enterprise* dengan opsi lain, lihat [Comparing GitHub to other DevOps solutions](https://resources.github.com/devops/tools/compare/).

---
---

## *GitHub* dan *Command Line*

### Perintah Dasar *Git*

Untuk menggunakan *Git*, *developer* menggunakan perintah spesifik untuk menyalin, membuat, mengubah, dan menggabungkan kode. Perintah-perintah ini dapat dieksekusi langsung dari *command line* atau dengan menggunakan aplikasi seperti *GitHub Desktop*. Berikut adalah beberapa perintah umum untuk menggunakan *Git*:

* `git init` menginisialisasi *Git repository* yang benar-benar baru dan mulai melacak *directory* yang sudah ada. Ini menambahkan subfolder tersembunyi di dalam *directory* yang ada yang menampung struktur data internal yang diperlukan untuk kontrol versi.

* `git clone` membuat salinan lokal dari proyek yang sudah ada secara *remotely* (jarak jauh). *Clone* ini mencakup semua *files*, riwayat, dan *branches* proyek.

* `git add` menahapkan (*stages*) sebuah perubahan. *Git* melacak perubahan pada *codebase* seorang *developer*, tetapi perlu menahapkan dan mengambil *snapshot* dari perubahan tersebut untuk memasukkannya ke dalam riwayat proyek. Perintah ini melakukan penahapan (*staging*), bagian pertama dari proses dua langkah itu. Setiap perubahan yang ditahapkan akan menjadi bagian dari *snapshot* berikutnya dan bagian dari riwayat proyek. Penahapan dan *committing* secara terpisah memberikan *developer* kontrol penuh atas riwayat proyek mereka tanpa mengubah cara mereka membuat kode dan bekerja.

* `git commit` menyimpan *snapshot* ke riwayat proyek dan menyelesaikan proses pelacakan perubahan. Singkatnya, *commit* berfungsi seperti mengambil foto. Apa pun yang telah ditahapkan dengan `git add` akan menjadi bagian dari *snapshot* dengan `git commit`.

* `git status` menunjukkan status perubahan, apakah *untracked* (tidak terlacak), *modified* (dimodifikasi), atau *staged* (ditahapkan).

* `git branch` menunjukkan *branches* yang sedang dikerjakan secara lokal.

* `git merge` menggabungkan lini pengembangan. Perintah ini biasanya digunakan untuk menggabungkan perubahan yang dibuat pada dua *branches* yang berbeda. Misalnya, seorang *developer* akan melakukan *merge* ketika mereka ingin menggabungkan perubahan dari *feature branch* ke dalam *main branch* untuk *deployment*.

* `git pull` memperbarui lini pengembangan lokal dengan *updates* dari rekannya yang *remote*. *Developer* menggunakan perintah ini jika rekan satu tim telah membuat *commits* ke *branch* di *remote*, dan mereka ingin mencerminkan perubahan tersebut di lingkungan lokal mereka.

* `git push` memperbarui *remote repository* dengan setiap *commits* yang dibuat secara lokal ke sebuah *branch*.

Untuk informasi lebih lanjut, lihat [full reference guide to Git commands](https://git-scm.com/docs).



---
obsidianUIMode: preview
materi: Github Workflow Management
sumber:
  - gemini.google.com
datetime: 2025-12-13T09:23:00
tags:
  - git
  - github
---
Link Sumber: 

---

# Github Workflow Management

Dalam pengembangan perangkat lunak modern, repositori Git (khususnya di GitHub) bukan hanya tempat penyimpanan kode, melainkan jantung kolaborasi tim. Namun, seiring bertambahnya anggota tim dan kompleksitas proyek, histori _commit_ proyek—atau yang sering kita sebut **Network Commit**—dapat dengan cepat berubah menjadi labirin yang rumit dan kacau. Tanpa strategi yang jelas, _network_ akan dipenuhi cabang mati, _merge commit_ berulang, dan histori yang sulit dilacak, yang pada akhirnya memperlambat _code review_, meningkatkan risiko konflik _merge_, dan mempersulit proses _debugging_. Oleh karena itu, menguasai **GitHub Manajemen Alur Kerja (Workflow Management)** bukanlah pilihan, melainkan keharusan untuk memastikan proyek berjalan dengan efisien, stabil, dan _scalable_.

Berikut diberikan beberapa penjelasan untuk workflow management Github yang rapi.

## 1 | Branch utama cuma satu: `main`

- **Detail Penjelasan:**
    
    - **Tujuan:** Untuk menjaga agar hanya ada **satu sumber kebenaran (Single Source of Truth)** yang selalu merepresentasikan kode yang _siap_ atau _sedang digunakan_ (production).
        
    - **Masalah dengan Banyak Branch Permanen:** Ketika Anda memiliki branch seperti `main`, `development`, dan `staging`, Anda secara efektif menciptakan tiga versi permanen dari proyek. Ini akan memperumit alur kerja:
        
        1. Ketika sebuah fitur selesai di `development`, Anda harus me-_merge_-nya ke `staging`.
            
        2. Setelah diuji di `staging`, Anda harus me-_merge_-nya lagi ke `main`.
            
        3. Jika ada _hotfix_ di `main`, Anda harus me-_merge_-nya mundur ke `development` dan `staging` agar ketiganya tetap sinkron.
            
    - **Efek pada Network:** Setiap _merge_ antar branch permanen ini akan menciptakan titik-titik percabangan (merge commits) yang permanen, membuat _network graph_ (visualisasi histori commit) menjadi kusut seperti "mie instan" atau "spageti" yang sulit dilacak.
        
    - **Solusi Terbaik:** Hanya `main` sebagai branch permanen. Gunakan branch fitur (_feature branch_) yang pendek dan cepat mati untuk semua pekerjaan baru.


## 2 | Setiap fitur = 1 branch kecil, pendek, dan cepat mati

- **Detail Penjelasan:**
    
    - **Filosofi:** Ini adalah inti dari **Git Flow Sederhana** atau **GitHub Flow**. Semua pekerjaan baru (fitur, perbaikan, refactoring) dilakukan di _branch_ terpisah dari `main`.
        
    - **Mengapa Pendek dan Cepat Mati:** Branch fitur seharusnya hanya hidup selama pengerjaan fitur tersebut. Setelah di-_merge_ ke `main` (melalui _Pull Request_), branch tersebut **wajib dihapus** (lihat Poin 6).
        
    - **Manfaat Branching Kecil:**
        
        - **Isolasi:** Pekerjaan yang sedang berlangsung tidak merusak kode di `main`.
            
        - **Review Mudah:** PR dari branch kecil lebih mudah direview.
            
        - **Network Rapi:** Karena branch dihapus, _network graph_ hanya menampilkan _commit_ fitur tersebut dan _merge commit_-nya, tanpa sisa cabang yang tidak perlu.
            
    - **Naming Convention:** Menggunakan awalan seperti `feat/`, `fix/`, `refactor/` (disebut juga **Conventional Commits** untuk branch) membantu mengidentifikasi tujuan branch dengan cepat.

## 3 | Selalu sync dulu sebelum mulai kerja

- **Detail Penjelasan:**
    
    - **Pentingnya Sinkronisasi:** `main` (di server `origin`) adalah _source of truth_. Sebelum Anda membuat branch fitur baru atau melanjutkan pekerjaan di branch fitur yang sudah ada, Anda harus memastikan _local main_ Anda **sama persis** dengan _remote main_.
        
    - **Alasan Perintah:**
        
        - `git fetch origin`: Mengambil semua informasi terbaru dari _remote_ (termasuk _commit_ baru di `main`) tanpa mengubah _working directory_ lokal Anda.
            
        - `git pull origin main`: Mengambil _commit_ terbaru dari `origin/main` dan menggabungkannya ke _local main_ Anda.
            
    - **Risiko Tanpa Sync:** Jika Anda membuat branch dari `main` yang "3 minggu di masa lalu," _commit_ pertama Anda di branch fitur akan didasarkan pada kode yang sudah _outdated_. Ini hampir pasti akan menyebabkan **konflik besar** dan membuat PR Anda sulit di-_merge_ karena Anda bekerja di atas versi yang salah.


## 4 | JANGAN merge main ke branch fitur berkali-kali

- **Detail Penjelasan:**
    
    - **Masalah Merge Berulang:** Ketika Anda sering `git merge main` ke branch fitur, setiap operasi _merge_ akan menghasilkan _merge commit_ baru di branch fitur Anda. Ini menciptakan percabangan dan penyatuan yang berulang-ulang, membuat histori _commit_ dari satu fitur menjadi berantakan dan sulit diikuti. Inilah yang menciptakan histori "bercabang kayak pohon beringin" atau "spageti".
        
    - **Solusi 1: Rebase (Disarankan untuk Pekerja Mandiri/Ketika Branch Tidak Dibagikan):**
        
        - **Cara Kerja Rebase:** `git rebase main` akan memindahkan (_re-base_) semua _commit_ fitur Anda **ke ujung terbaru** dari branch `main`. Ini menghasilkan histori yang **linier**, seolah-olah Anda baru mulai bekerja hari ini.
            
        - **Manfaat:** Menjaga _network graph_ tetap lurus dan bersih.
            
        - **Catatan Keamanan:** **JANGAN** pernah me-_rebase_ _commit_ yang sudah Anda _push_ ke _remote_ dan dibagikan dengan orang lain (aturan emas Git: **Never Rebase Public History**).
            
    - **Solusi 2: Merge Sekali di Akhir (Disarankan untuk Kerja Tim):**
        
        - **Alasan:** Dalam tim, _merge_ lebih aman karena ia mempertahankan _commit_ histori yang "asli" (tidak ditimpa seperti rebase) dan mencatat _merge commit_ yang jelas, memudahkan pelacakan jika terjadi masalah. Sinkronisasi dengan _main_ cukup dilakukan sekali atau hanya ketika benar-benar diperlukan dan dilakukan menggunakan `rebase` secara lokal (jika aman) atau _pull_ biasa.


## 5 | Pull request harus bersih & kecil

- **Detail Penjelasan:**
    
    - **Definisi PR Kecil:** PR idealnya fokus pada satu tujuan tunggal (satu fitur, satu perbaikan) dan memiliki _line changes_ yang minimal (50–200 baris perubahan).
        
    - **Mengapa PR Besar Buruk:**
        
        - **Reviewer Overload:** _Reviewer_ akan kesulitan mencerna 2000 baris kode sekaligus, membuat proses _review_ menjadi lambat dan rawan _bug_ lolos.
            
        - **Konflik:** Semakin lama branch fitur hidup dan semakin banyak perubahan di dalamnya, semakin besar kemungkinan terjadi konflik dengan `main`. PR besar dan lama adalah resep untuk **konflik _merge_ yang kacau balau**.
            
    - **Action Plan:** Pecah fitur besar menjadi serangkaian PR kecil yang mandiri. Contoh: Daripada "Buat Fitur Akun Pengguna Lengkap," pecah menjadi:
        
        1. PR 1: `feat/setup-user-model-db`
            
        2. PR 2: `feat/add-login-api`
            
        3. PR 3: `feat/ui-dashboard-refactor`
            

## 6. Hapus branch setelah merge

- **Detail Penjelasan:**
    
    - **Prinsip Kebersihan:** Setelah kode di branch fitur berhasil di-_merge_ ke `main`, branch fitur tersebut sudah tidak relevan lagi. Pekerjaannya sudah selesai dan _commit_-nya sudah menjadi bagian dari histori `main`.
        
    - **Masalah Branch Tidak Dihapus:**
        
        - **Kekacauan Visual:** _Network graph_ akan penuh dengan cabang-cabang yang "mati," membuat visualisasi histori menjadi berantakan.
            
        - **Kebingungan:** Anggota tim dapat bingung, apakah sebuah branch masih aktif, apakah _commit_-nya sudah masuk `main`, atau apakah branch itu harus dihapus.
            
    - **Mekanisme:** GitHub (dan GitLab/Bitbucket) menyediakan opsi otomatis untuk menghapus branch setelah _merge_ PR, yang sangat disarankan untuk diaktifkan dan digunakan.


## 7 | Hindari merge antar branch feature

- **Detail Penjelasan:**
    
    - **Apa yang Terjadi:** Jika `feature-A` me-_merge_ `feature-B`, berarti _feature-A_ sekarang mengandung _commit_ dari _feature-B_. Jika _feature-A_ di-_merge_ duluan ke `main`, berarti _feature-B_ juga ikut masuk ke `main` **sebelum waktunya** (sebelum PR _feature-B_ disetujui).
        
    - **Indikasi Desain Buruk:** Ketergantungan seperti ini sering menunjukkan bahwa desain atau pembagian tugas awal terlalu terikat. Idealnya, setiap fitur harus **independen**.
        
    - **Solusi:** Jika memang ada ketergantungan:
        
        - Pastikan fitur dasar (`feature-B`) diselesaikan, di-_review_, dan di-_merge_ ke `main` **terlebih dahulu**.
            
        - Setelah `feature-B` ada di `main`, `feature-A` bisa melakukan `git pull origin main` dan melanjutkan pekerjaannya.

## 8 | Gunakan PROTECTED BRANCHES

- **Detail Penjelasan:**
    
    - **Keamanan Kode:** **Protected Branches** adalah fitur di GitHub (dan Git hosting lainnya) yang memungkinkan Anda mengatur batasan ketat pada branch-branch penting (seperti `main`).
        
    - **Aturan Kunci yang Ditetapkan:**
        
        - **Require Pull Request:** Melarang _push_ langsung ke `main`. Semua perubahan harus melalui _Pull Request_ (PR).
            
        - **Require Review:** Membutuhkan setidaknya satu (atau lebih) _approving review_ dari anggota tim sebelum PR dapat di-_merge_.
            
        - **Require Passing Status Checks:** Memastikan semua _test_ otomatis (CI/CD) lulus sebelum _merge_.
            
    - **Manfaat:** Mencegah _commit_ yang belum teruji atau tidak sengaja langsung merusak kode yang sedang berjalan, sehingga menjaga kestabilan dan kebersihan `main`.
        

## 9 | Commit message jelas dan konsisten

- **Detail Penjelasan:**
    
    - **Pentingnya Sejarah:** _Commit message_ adalah narasi dari sejarah proyek Anda. Ketika _network graph_ sudah lurus (berkat aturan di atas), _commit message_ adalah yang membantu tim dan diri Anda di masa depan untuk mengerti **mengapa** perubahan dibuat.
        
    - **Standardisasi:** Menggunakan format seperti **Conventional Commits** (`type: subject`) sangat membantu.
        
        - `feat`: Fitur baru.
            
        - `fix`: Perbaikan _bug_.
            
        - `refactor`: Perubahan kode tanpa mengubah fungsionalitas.
            
        - `docs`: Perubahan dokumentasi saja.
            
    - **Manfaat:** Memudahkan pembuatan _changelog_ otomatis dan membuat proses _review_ PR menjadi lebih cepat karena _commit_ di dalamnya sudah jelas tujuannya.

## 10 | Jangan kerja di branch yang sama lebih dari 1 orang

- **Detail Penjelasan:**
    
    - **Masalah Utama:** Jika dua orang _push_ ke branch fitur yang sama, mereka akan terus-menerus saling menimpa pekerjaan (walaupun Git bisa mengatasinya), dan yang lebih penting: _network graph_ dari branch tersebut akan menjadi sangat tidak stabil (percobaan _merge_, _pull_, _push force_, dll.).
        
    - **Prinsip:** Setiap orang harus bekerja di **branch fitur pribadi** mereka sendiri, yang berasal dari `main`.
        
    - **Solusi (Jika Kolaborasi Harus Dilakukan):**
        
        - Pecah fitur menjadi dua bagian yang terpisah, dan setiap orang membuat branch-nya sendiri.
            
        - Jika terpaksa harus berkolaborasi, gunakan _pair programming_ atau komunikasikan secara ketat, dan gunakan `git pull --rebase` untuk menjaga histori _commit_ linier sebelum _push_.

## 11 | Gunakan Fitur SQUASH and MERGE

- **Detail Penjelasan:**
    
    - **Tujuan:** Membuat _network graph_ di branch `main` tetap super linier dan bersih dari _commit_ detail yang tidak perlu.
        
    - **Masalah:** Selama pengerjaan sebuah fitur, Anda mungkin memiliki 15 _commit_ kecil di branch fitur Anda (`fix: typo`, `test: nambah console log`, `chore: hapus file`, dll.). Jika Anda menggunakan _Standard Merge_, ke-15 _commit_ ini akan masuk ke `main`, membuat histori menjadi berisik.
        
    - **Solusi: Squash Merge:** Saat me-_merge_ _Pull Request_ (PR) di GitHub, gunakan opsi **Squash and Merge**. Opsi ini akan:
        
        1. Menggabungkan (squash) semua _commit_ dari branch fitur (misalnya, 15 _commit_) menjadi **satu _commit_ tunggal**.
            
        2. _Commit_ tunggal ini yang kemudian di-_merge_ ke `main`.
            
    - **Efek pada Network:** Histori `main` Anda akan terlihat rapi, di mana setiap fitur diwakili oleh **satu _commit_** yang jelas dan bermakna.


## 12 | Hindari Commit “WIP” (Work In Progress)

- **Detail Penjelasan:**
    
    - **WIP Commit:** Ini adalah _commit_ yang Anda buat hanya untuk menyelamatkan pekerjaan atau sebelum makan siang, tetapi kodenya masih rusak, tidak lengkap, atau tesnya gagal.
        
    - **Masalah:** Jika _commit_ ini masuk ke `main` (melalui _merge_ yang salah atau rebase yang tidak hati-hati), itu akan merusak histori. Bahkan jika tidak masuk ke `main`, ia mengotori _history_ branch fitur Anda dan PR Anda (lihat Poin 5: PR harus bersih).
        
    - **Solusi:**
        
        - **Saat Sedang Bekerja:** Gunakan `git stash` jika Anda perlu beralih branch atau menyimpan pekerjaan sementara tanpa membuat _commit_ yang buruk.
            
        - **Sebelum PR:** Selalu gunakan **Interactive Rebase** (`git rebase -i HEAD~N`) untuk membersihkan, menggabungkan (_squash_), dan mengedit _commit_ Anda sebelum Anda membuat PR atau sebelum di-_merge_. Ini memastikan _commit_ yang dilihat oleh _reviewer_ adalah _commit_ yang _atomic_ (unit perubahan yang utuh).
            

## 13 | Gunakan Pre-Commit Hooks (Linting & Testing)

- **Detail Penjelasan:**
    
    - **Tujuan:** Mencegah _commit_ yang buruk atau melanggar standar kode masuk ke repositori Anda, sehingga menjaga kualitas kode dan histori.
        
    - **Mekanisme:** _Git hooks_ adalah _script_ yang dijalankan pada titik-titik tertentu dalam operasi Git. **Pre-commit hook** adalah _script_ yang dijalankan _sebelum_ Git mengizinkan sebuah _commit_ dibuat.
        
    - **Implementasi:** Anda dapat menggunakan alat seperti **Husky** atau **Lint-Staged** untuk mengatur _hook_ ini.
        
    - **Contoh:**
        
        - Menjalankan _formatter_ (seperti Prettier) untuk memastikan semua kode diformat secara konsisten.
            
        - Menjalankan _linter_ untuk memeriksa kesalahan sintaks dan gaya.
            
        - Menjalankan _unit test_ cepat untuk memastikan _commit_ yang dibuat tidak merusak fungsionalitas inti.
            

## 14 | Selalu Gunakan `--no-ff` pada Merge Manual (Jika Tidak Menggunakan Squash)

- **Detail Penjelasan:**
    
    - **Apa itu Fast-Forward (FF):** Secara _default_, jika _main_ belum memiliki _commit_ baru sejak branch fitur dibuat, Git akan melakukan **Fast-Forward Merge** ketika Anda melakukan `git merge`. Ini hanya memindahkan pointer `main` ke _commit_ terbaru branch fitur, **tanpa membuat _merge commit_**.
        
    - **Masalah FF:** Jika _Fast-Forward_ terjadi, Anda kehilangan informasi penting bahwa _commit_ tersebut adalah bagian dari _branch_ fitur tertentu. Ini membuat debugging dan pelacakan historis menjadi lebih sulit.
        
    - **Solusi: `--no-ff`:** Jika Anda me-_merge_ secara manual (bukan melalui UI GitHub), selalu gunakan:
        
        Bash
        
        ```
        git merge --no-ff nama-branch-fitur
        ```
        
        Perintah ini **memaksa** Git untuk membuat _merge commit_, bahkan jika _Fast-Forward_ dimungkinkan. _Merge commit_ ini bertindak sebagai penanda yang jelas di _network graph_ yang mengatakan: "Di sinilah fitur X selesai dan diintegrasikan."
        

## 15 | Manfaatkan Issue Tracking dalam Commit Message

- **Detail Penjelasan:**
    
    - **Tujuan:** Menghubungkan _commit_ (dan _merge commit_) Anda secara langsung ke pekerjaan yang sedang dilakukan di sistem _issue tracking_ (misalnya, GitHub Issues, Jira).
        
    - **Cara Kerja:** Sertakan referensi ke nomor _issue_ yang terkait di bagian akhir _commit message_ atau di deskripsi PR.
        
    - **Contoh Format Commit:**
        
        ```
        feat: tambahkan validasi form login [skip ci]
        
        Tambahkan validasi sisi klien untuk form login.
        Jika email tidak valid, akan muncul pesan error.
        
        Refs: #42
        ```
        
    - **Manfaat:**
        
        - **Traceability:** Saat melihat _network graph_ atau histori _commit_, Anda dapat langsung melihat _issue_ (masalah/fitur) mana yang dipecahkan oleh _commit_ tersebut.
            
        - **Otomatisasi:** Menggunakan kata kunci seperti `Fixes #42` atau `Closes #42` di deskripsi PR akan membuat GitHub **secara otomatis menutup _issue_ #42** ketika PR tersebut di-_merge_. Ini adalah cara yang sangat rapi untuk mengelola alur kerja.

## 16 | Perhatikan `.gitignore` dan Hindari Commit File Hasil Build

- **Detail Penjelasan:**
    
    - **Tujuan:** Menjaga repositori (dan histori _commit_) tetap ringan dan bersih dari _file_ yang tidak perlu dilacak oleh Git.
        
    - **Masalah:** Banyak pemula lupa menambahkan _file_ hasil _build_ (`dist/`, `build/`), _file_ dependensi (`node_modules/`, `.venv/`), _file_ log, atau _file_ konfigurasi lokal (`.env.local`) ke dalam `.gitignore`. Jika _file-file_ ini di-_commit_, ukuran repositori akan membengkak, dan _commit_ yang tidak relevan akan muncul di _network_.
        
    - **Solusi:** Pastikan _file_ `.gitignore` sudah komprehensif. Jika Anda tidak sengaja meng-_commit_ _file_ besar, Anda harus menggunakan alat seperti `git rm --cached` dan, jika _file_ tersebut sudah di-_commit_ ke histori, Anda mungkin perlu menggunakan **`git filter-repo`** (alat tingkat lanjut) untuk menghapus _file_ tersebut dari seluruh sejarah Git Anda.
        

## 17 | Pilih Strategi Merge yang Konsisten (Squash vs Rebase vs Standard)

- **Detail Penjelasan:**
    
    - **Tujuan:** Menciptakan histori _network_ yang mudah dibaca dan diprediksi oleh semua anggota tim.
        
    - **Konsistensi adalah Kunci:** Meskipun Poin 4 dan Poin 11 menyarankan _rebase_ (untuk kebersihan linier) atau _squash_ (untuk histori bersih per fitur), hal terpenting adalah tim **memilih satu strategi** dan menggunakannya secara seragam.
        
    - **Rekomendasi Umum:**
        
        - Gunakan **Squash and Merge** untuk PR ke `main` (memberikan histori linier di mana setiap fitur adalah satu _commit_).
            
        - Atau, gunakan **Rebase Merge** (membuat histori linier, mempertahankan semua _commit_ kecil).
            
    - **Peringatan:** Mencampur strategi _merge_ dalam satu repositori (kadang _standard_, kadang _squash_, kadang _rebase_) akan menghasilkan _network graph_ yang membingungkan dan tidak konsisten. Terapkan aturan ini melalui **Protected Branch Settings** di GitHub.
        

## 18 | Gunakan Reflog untuk Kesalahan Fatal

- **Detail Penjelasan:**
    
    - **Tujuan:** Menyelamatkan pekerjaan Anda ketika Anda melakukan kesalahan _fatal_ dengan perintah yang mengubah histori, seperti _rebase_ yang salah atau _hard reset_ yang keliru.
        
    - **Reflog Itu Apa?** `git reflog` adalah "Log Referensi" lokal Anda. Ia mencatat **setiap tindakan** yang Anda lakukan pada HEAD repositori Anda (setiap _commit_, _merge_, _checkout_, _rebase_, _reset_). Data ini disimpan secara lokal dan tidak di-_push_ ke _remote_.
        
    - **Cara Pakai:** Jika Anda baru saja me-_rebase_ dan merusak _commit_ Anda, Anda bisa menjalankan `git reflog`. Cari _hash_ _commit_ sebelum kesalahan terjadi, lalu gunakan:
        
        Bash
        
        ```
        git reset HEAD@{indeks_reflog_yang_benar}
        # Contoh: git reset HEAD@{5}
        ```
        
    - **Manfaat:** Memastikan bahwa tidak ada pekerjaan yang benar-benar hilang karena kesalahan _command line_, sehingga Anda bisa memperbaiki _network commit_ lokal Anda tanpa panik.
        

## 19 | Tetapkan Aturan untuk _Force Push_ dan Rebase Publik

- **Detail Penjelasan:**
    
    - **Tujuan:** Mencegah _force push_ yang tidak disengaja merusak pekerjaan anggota tim lain, yang dikenal sebagai "Rewriting Public History."
        
    - **Masalah _Force Push_ (Wajib Diikuti dari Poin 4):** Setelah Anda me-_push_ _commit_ ke _remote_ (misalnya branch fitur Anda), _commit_ tersebut menjadi "publik." Jika Anda kemudian me-_rebase_ _commit_ tersebut secara lokal dan melakukan `git push --force`, Anda akan menimpa histori yang sudah dilihat atau ditarik oleh rekan tim, menyebabkan kekacauan _network_ di mesin mereka.
        
    - **Aturan yang Ditetapkan:**
        
        1. **Dilarang _Force Push_** ke `main` (dijamin oleh _Protected Branches_).
            
        2. **Dilarang _Force Push_** ke branch fitur yang sedang digunakan atau dibagikan oleh orang lain.
            
        3. _Force Push_ **hanya diperbolehkan** pada branch fitur pribadi Anda **setelah Anda membersihkan (_squash_/edit) _commit_ lokal Anda** dan Anda yakin tidak ada rekan tim lain yang sedang bekerja di atas _commit_ lama Anda.
            

## 20 |  Manfaatkan Branch Protection untuk Pemeriksaan Kualitas (CI/CD)

- **Detail Penjelasan:**
    
    - **Tujuan:** Menjamin bahwa _network commit_ di `main` hanya berisi kode yang sudah diuji secara otomatis dan lulus standar kualitas.
        
    - **Integrasi CI/CD:** Hubungkan sistem Integrasi Berkelanjutan/Deployment Berkelanjutan (CI/CD) Anda (seperti GitHub Actions, Jenkins, CircleCI) ke GitHub.
        
    - **Setting Protected Branch:**
        
        - Di pengaturan branch `main`, wajibkan **"Require status checks to pass before merging."**
            
        - Tambahkan _checks_ dari sistem CI/CD Anda (misalnya, _Test Run Complete_, _Linting Passed_).
            
    - **Efek pada Network:** PR tidak akan menampilkan tombol _Merge_ sampai semua pemeriksaan otomatis lulus. Ini berarti setiap _merge commit_ baru di `main` adalah **commit yang terjamin berfungsi**, mencegah kerusakan _network_ akibat _commit_ yang rusak.

## 21 | Tulis Deskripsi Pull Request (PR) yang Detail

- **Detail Penjelasan:**
    
    - **Tujuan:** Deskripsi PR adalah jembatan komunikasi utama antara pengembang dan _reviewer_. PR yang baik menjelaskan mengapa perubahan ini dilakukan, bukan hanya apa yang berubah.
        
    - **Standar Minimum:** Deskripsi PR harus mencakup:
        
        1. **Masalah yang Dipecahkan:** (Misalnya: "Memperbaiki bug di halaman checkout yang gagal saat diskon diterapkan.")
            
        2. **Solusi yang Diterapkan:** (Misalnya: "Mengubah perhitungan pajak dari integer menjadi float dan menambahkan validasi sisi server.")
            
        3. **Bukti Pengujian (Screenshots/Video):** Tunjukkan bahwa perubahan berfungsi.
            
        4. **Referensi _Issue_:** Selalu kaitkan dengan _issue_ terkait (misalnya, `Closes #123`).
            
    - **Efek pada Network:** PR yang jelas memfasilitasi _review_ cepat. _Review_ yang cepat berarti branch fitur Anda mati lebih cepat (Poin 2), mengurangi risiko konflik dan menjaga _network_ tetap efisien.
        

## 22 | Gunakan `git blame` dan `git log` untuk Belajar, Bukan Menyalahkan

- **Detail Penjelasan:**
    
    - **Tujuan:** Mendorong budaya tim yang menggunakan alat Git untuk memahami histori, bukan untuk mencari siapa yang membuat kesalahan.
        
    - **`git blame`:** Perintah ini menunjukkan siapa _commit_ terakhir yang mengubah setiap baris kode.
        
    - **`git log`:** Menunjukkan histori _commit_ secara rinci.
        
    - **Penerapan:** Gunakan `git blame` untuk mengidentifikasi konteks historis ketika Anda melihat _bug_ lama (misalnya, untuk melihat mengapa suatu baris ditambahkan atau diubah), sehingga Anda dapat memperbaiki masalah dengan pemahaman penuh, bukan hanya menebak. Pendekatan ini memastikan setiap orang menghargai kejelasan _commit message_ (Poin 9) karena histori yang bersih akan memudahkan proses _blame_ dan _log_ yang konstruktif.
        

## 23 | Dokumentasikan Alur Kerja Git Tim Anda

- **Detail Penjelasan:**
    
    - **Tujuan:** Menghilangkan ambiguitas dan memastikan setiap anggota tim, terutama anggota baru, mengikuti aturan yang sama persis.
        
    - **Isi Dokumentasi:** Buatlah dokumen internal yang mencantumkan:
        
        - Strategi _Branching_ Resmi (Misalnya: "Kami menggunakan GitHub Flow dengan Squash Merge").
            
        - Aturan _Commit Message_ Wajib (Misalnya: "Harus menggunakan Conventional Commits").
            
        - Aturan _Force Push_ (Poin 19).
            
        - Prosedur _Merge_ dan _Delete Branch_ (Poin 6).
            
    - **Manfaat:** Konsistensi adalah kunci _network_ yang bersih. Dokumentasi adalah cara terbaik untuk mencapai konsistensi di seluruh tim, menghindari interpretasi yang berbeda yang dapat merusak _network_ seiring waktu.
        

## 24 | Lakukan Pemeriksaan Kesehatan Repo Secara Periodik

- **Detail Penjelasan:**
    
    - **Tujuan:** Secara proaktif membersihkan _network_ dan _repo_ dari sampah yang tidak disengaja.
        
    - **Tindakan yang Dapat Dilakukan:**
        
        1. **Hapus Branch Lokal Mati:** Secara berkala, gunakan `git fetch --prune` untuk menghapus semua referensi branch _remote_ yang sudah dihapus dari lokal Anda.
            
        2. **Bersihkan Sampah Git:** Gunakan `git gc` (Garbage Collection) secara berkala di mesin lokal Anda untuk mengoptimalkan _repo_ dan menghapus _object_ yang tidak terjangkau (tetapi ini biasanya dilakukan Git secara otomatis).
            
        3. **Audit Branch di Remote:** Tetapkan jadwal untuk melihat semua _branch_ di GitHub dan hapus secara manual _branch_ fitur yang _stale_ (tua dan tidak di-_merge_) yang ditinggalkan.
            
    - **Efek pada Network:** Menghapus sampah ini membuat _local clone_ dan visualisasi _network_ tetap bersih dan efisien.
        

## 25 | Prioritaskan Code Review di atas Pengembangan Baru

- **Detail Penjelasan:**
    
    - **Tujuan:** Mempercepat _Time-to-Merge_ dan menjaga alur kerja tetap lancar.
        
    - **Mengapa Penting:** _Pull Request_ adalah _bottleneck_ utama dalam _Git Workflow_. Jika PR dibiarkan tertunda, branch fitur akan menjadi _stale_ dan jauh dari `main`, meningkatkan kemungkinan konflik _merge_ yang rumit (Poin 5) dan merusak _network_.
        
    - **Aturan Tim:** Dorong tim untuk menjadikan _Code Review_ sebagai prioritas tertinggi kedua (setelah _hotfix_ kritis). Jika ada PR yang menunggu, setiap pengembang harus mengulasnya terlebih dahulu sebelum memulai pekerjaan _commit_ baru.
        
    - **Hasil:** Branch fitur hidup pendek dan mati cepat, menghasilkan _network_ yang selalu linier, terkini, dan bebas konflik.

## 26 | Jadikan Feature Toggle sebagai Alternatif Feature Branch Jangka Panjang

- **Detail Penjelasan:**
    
    - **Tujuan:** Mengatasi skenario di mana fitur baru membutuhkan waktu pengembangan yang sangat lama (berbulan-bulan) tanpa merusak aturan _branching_ pendek (Poin 2).
        
    - **Masalah:** Jika fitur membutuhkan waktu 3 bulan, membuat _feature branch_ selama 3 bulan akan menyebabkan _branch_ tersebut jauh dari `main` dan seringkali menyebabkan konflik _merge_ besar saat akhirnya _merge_.
        
    - **Solusi: Feature Toggle (atau Feature Flags):**
        
        1. Pengembang tetap bekerja di _branch_ kecil, meng-_merge_ _commit_ mereka ke `main` secara bertahap (harian/mingguan).
            
        2. Namun, semua kode fitur baru di-bungkus di balik _toggle_ atau _flag_ yang **dinonaktifkan** secara _default_ di produksi.
            
        3. Fitur baru tidak akan terlihat oleh pengguna akhir sampai _flag_ diaktifkan melalui _dashboard_ manajemen (bukan melalui _deployment_ kode baru).
            
    - **Dampak pada Network:** Strategi ini memungkinkan tim untuk mengadopsi model **Trunk-Based Development** yang sangat bersih, di mana `main` selalu _deployable_ (siap dirilis), dan _network commit_ tetap linier tanpa adanya _branch_ fitur yang berumur panjang dan bermasalah. Ini adalah puncak dari manajemen alur kerja yang efisien.
        

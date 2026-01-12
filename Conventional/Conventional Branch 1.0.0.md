---
obsidianUIMode: preview
materi: Conventional Branch 1.0.0
sumber:
  - conventional-branch.github.io
datetime: 2025-12-13T10:40:00
tags:
  - branch
  - conventional
---
Link Sumber: [Conventional Branch](https://conventional-branch.github.io/)

---
# Conventional Branch 1.0.0

> [!CAUTION] 
> Secara resmi **tidak ada standar bernama _Conventional Branch_** seperti halnya _Conventional Commits_; yang sering disebut “conventional branch” itu sebenarnya hanyalah **kebiasaan penamaan branch** yang disamakan polanya dengan tipe commit (seperti `feature/`, `fix/`, `refactor/`) demi kerapian dan konsistensi tim, bukan sebuah spesifikasi baku. 
> 
> Alasannya simpel dan logis: **branch bersifat sementara dan kontekstual** (dibuat, dipakai, lalu dihapus), sementara **commit adalah artefak permanen** yang membentuk histori, changelog, dan bahkan menentukan semver serta proses rilis, sehingga commit perlu distandardisasi ketat, sedangkan branch dibiarkan fleksibel agar bisa menyesuaikan workflow tim tanpa jadi beban aturan yang kaku.

## Ringkasan

Conventional Branch mengacu pada konvensi penamaan yang terstruktur dan terstandardisasi untuk _branch_ Git yang bertujuan untuk membuat nama _branch_ lebih mudah dibaca dan ditindaklanjuti (_actionable_). Kami menyarankan beberapa awalan _branch_ yang mungkin ingin Anda gunakan, tetapi Anda juga dapat menentukan konvensi penamaan Anda sendiri. Konvensi penamaan yang konsisten memudahkan untuk mengidentifikasi _branch_ berdasarkan tipenya.

## Poin Utama

- **Nama _Branch_ Berbasis Tujuan:** Setiap nama _branch_ harus secara jelas menunjukkan tujuannya, membuatnya mudah bagi semua pengembang untuk memahami _branch_ tersebut digunakan untuk apa.
    
- **Integrasi dengan CI/CD:** Dengan menggunakan nama _branch_ yang konsisten, ini dapat membantu sistem otomatis (seperti _pipeline_ Continuous Integration/Continuous Deployment) untuk memicu tindakan spesifik berdasarkan tipe _branch_ (misalnya, _auto-deployment_ dari _branch_ rilis).
    
- **Kolaborasi Tim:** Ini mendorong kolaborasi di dalam tim dengan membuat tujuan _branch_ menjadi eksplisit, mengurangi kesalahpahaman, dan mempermudah anggota tim untuk beralih antar tugas tanpa kebingungan.
    

## Spesifikasi

### Awalan Penamaan Branch

Spesifikasi _branch_ ini mendukung awalan berikut dan **sebaiknya** distrukturkan sebagai:

```
<tipe>/<deskripsi>
```

|**Awalan (Tipe)**|**Tujuan**|**Contoh Penamaan**|
|---|---|---|
|**`main`**|_Branch_ pengembangan utama (_e.g., main, master, or develop_).|Tidak ada awalan, ini adalah _branch_ inti.|
|**`feature/`** (atau `feat/`)|Untuk fitur baru (_e.g., feature/add-login-page, feat/add-login-page_).|`feature/add-login-page`|
|**`bugfix/`** (atau `fix/`)|Untuk perbaikan _bug_ (_e.g., bugfix/fix-header-bug, fix/header-bug_).|`fix/header-bug`|
|**`hotfix/`**|Untuk perbaikan mendesak (_e.g., hotfix/security-patch_).|`hotfix/security-patch`|
|**`release/`**|Untuk _branch_ yang mempersiapkan rilis (_e.g., release/v1.2.0_).|`release/v1.2.0`|
|**`chore/`**|Untuk tugas non-kode seperti dependensi, _update_ dokumen (_e.g., chore/update-dependencies_).|`chore/update-dependencies`|

### Aturan Dasar

- **Gunakan Alfanumerik Huruf Kecil, Tanda Hubung, dan Titik:** Selalu gunakan huruf kecil (a-z), angka (0-9), dan tanda hubung (`-`) untuk memisahkan kata. **Hindari karakter khusus, garis bawah (_underscore_), atau spasi.** Untuk _branch_ rilis, titik (`.`) **boleh** digunakan dalam deskripsi untuk merepresentasikan nomor versi (misalnya, `release/v1.2.0`).
    
- **Tidak Ada Tanda Hubung atau Titik Berurutan, di Awal, atau di Akhir:** Pastikan tanda hubung dan titik tidak muncul secara berurutan (misalnya, `feature/new--login`, `release/v1.-2.0`), atau di awal atau akhir deskripsi (misalnya, `feature/-new-login`, `release/v1.2.0.`).
    
- **Jaga Agar Tetap Jelas dan Ringkas:** Nama _branch_ harus deskriptif namun ringkas, secara jelas menunjukkan tujuan pekerjaan.
    
- **Sertakan Nomor Tiket:** Jika berlaku, sertakan nomor tiket dari alat manajemen proyek Anda untuk mempermudah pelacakan. Misalnya, untuk tiket `issue-123`, nama _branch_ bisa menjadi `feature/issue-123-new-login`.
    

## Kesimpulan

- **Komunikasi yang Jelas:** Nama _branch_ saja memberikan pemahaman yang jelas tentang tujuan perubahan kode.
    
- **Ramah Otomasi:** Mudah terhubung ke proses otomatisasi (misalnya, _workflow_ yang berbeda untuk `feature`, `release`, dll.).
    
- **Skalabilitas:** Bekerja dengan baik di tim besar di mana banyak pengembang mengerjakan tugas yang berbeda secara bersamaan.
    

Singkatnya, _conventional branch_ dirancang untuk meningkatkan organisasi proyek, komunikasi, dan otomatisasi dalam alur kerja Git.

## Tanya Jawab (FAQ)

### Mengapa tipe _branch_ tidak sedetail Conventional Commits (misalnya, `build`, `ci`, `docs`, `style`, `refactor`)?

_Branch_ berbeda dari _commit_—mereka bersifat sementara dan terutama digunakan sampai digabungkan (_merged_). Memperkenalkan terlalu banyak tipe untuk _branch_ akan tidak perlu dan akan membuatnya lebih sulit untuk dikelola dan diingat.

### Alat apa yang dapat digunakan untuk secara otomatis mengidentifikasi jika anggota tim tidak memenuhi spesifikasi ini?

Anda dapat menggunakan **`commit-check`** untuk memeriksa spesifikasi _branch_ atau **`commit-check-action`** jika kode Anda di-_host_ di GitHub.

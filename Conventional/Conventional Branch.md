---
obsidianUIMode: preview
materi: Conventional Branch
sumber:
  - gemini.google.com
  - conventional-branch.github.io
datetime: 2025-12-13T10:34:00
tags:
  - branch
  - conventional
---
Link Sumber: [Conventional Branch](https://conventional-branch.github.io/)

---
# Conventional Branching: Standar Penamaan Branch

Setelah Anda menetapkan standar untuk _commit message_, penting untuk menerapkan standar yang serupa pada penamaan _branch_ Anda. **Conventional Branching** adalah sistem sederhana yang memanfaatkan _tipe_ yang sama dari Conventional Commits untuk mengidentifikasi tujuan _branch_ dengan cepat.

Tujuan utama dari konvensi ini adalah agar setiap anggota tim dapat mengetahui **tujuan** dan **cakupan** dari sebuah _branch_ hanya dari namanya, bahkan sebelum melihat kodenya.

## 1 | Struktur Dasar Penamaan Branch

Nama _branch_ **sebaiknya** mengikuti struktur tiga bagian ini:

```
<tipe>/<scope-opsional>/<deskripsi-singkat>
```

- **Aturan Utama:** Gunakan tanda garis miring (`/`) sebagai pemisah, dan gunakan tanda hubung (`-`) sebagai pemisah kata dalam deskripsi.
    

## 2 | Tipe Branch yang Direkomendasikan

Tipe _branch_ harus konsisten dengan _tipe_ _commit_ utama Anda. Berikut adalah tipe yang paling umum dan direkomendasikan:

|**Tipe Branch**|**Tujuan Utama**|**Contoh Nama Branch**|**Catatan Penggunaan (Konsolidasi Tipe)**|
|---|---|---|---|
|**`main`**|**KODE UTAMA:** Sumber kebenaran, kode yang siap dirilis/sudah rilis.|N/A|**Branch permanen.** Dilarang _push_ langsung. Semua _merge_ harus melalui PR.|
|**`feature/`** (atau `feat/`)|**FITUR BARU:** Pengembangan fungsionalitas, _refactor_ besar, atau _spike_ eksplorasi.|`feature/user-profile-editor`|**Menggantikan `refactor/` dan `test/`.** Semua kode baru dan pembersihan besar masuk sini.|
|**`fix/`** (atau `bugfix/`)|**PERBAIKAN BUG:** Perbaikan _bug_ standar yang ditemukan saat pengembangan atau _staging_.|`fix/checkout-gagal-cache`|Untuk _bug_ rutin, bukan yang mendesak (_hotfix_). Harus berumur pendek.|
|**`hotfix/`**|**PERBAIKAN DARURAT:** Perbaikan yang harus segera di-_deploy_ ke lingkungan produksi.|`hotfix/security-patch-api`|Diprioritaskan. Biasanya dibuat langsung dari `main` dan di-_merge_ kembali ke `main`.|
|**`release/`**|**PERSIAPAN RILIS:** _Branch_ untuk _final testing_, _bugfix_ minor rilis, dan pembuatan _tag_ SemVer.|`release/v1.2.0`|Dibuat hanya menjelang rilis. Setelah rilis, _branch_ **sebaiknya** dihapus.|
|**`chore/`**|**PEMELIHARAAN:** Tugas non-fungsional, termasuk _docs_, _style_, _build_, _ci_, dan _update_ dependensi.|`chore/update-dependencies`|**Menggantikan `docs/`, `style/`, `test/` (jika hanya penambahan konfigurasi CI).** Detailnya dijelaskan di _commit message_ internal.|

## 3 | Komponen Penamaan Branch Lebih Lanjut

### A. Cakupan (Scope) Opsional

Mirip dengan _commit message_, _scope_ dapat digunakan untuk mengidentifikasi area kode yang terpengaruh. Ini sangat membantu di repositori besar.

- **Contoh Buruk:** `feat/new-button`
    
- **Contoh Baik:** `feat/ui-dashboard/tambah-button-export` (Jelas di mana pekerjaan dilakukan)
    

### B. Deskripsi Singkat

- **Wajib Singkat:** Deskripsi haruslah ringkas dan deskriptif.
    
- **Format:** Gunakan **huruf kecil** dan pisahkan kata dengan **tanda hubung (`-`)**. **Hindari spasi.**
    

## 4 | Branch Khusus: Nomor Issue (Opsional tapi Direkomendasikan)

Dalam tim yang menggunakan sistem _issue tracking_ (seperti GitHub Issues, Jira, atau Trello), seringkali _branch_ diberi awalan dengan nomor _issue_ untuk memudahkan pelacakan:

```
<tipe>/<nomor-issue>-<deskripsi-singkat>
```

- **Contoh:** `fix/101-perbaiki-gagal-login-cache`
    
- **Manfaat:** Otomatisasi: Sistem dapat secara otomatis menautkan _branch_ ke _issue_ yang sesuai segera setelah _branch_ di-_push_.
    

## 5 | Aturan Wajib untuk Kebersihan Branch

1. **Tidak Ada Karakter Aneh:** Hanya gunakan huruf kecil, angka, dan tanda hubung (`-`). **Hindari** spasi, huruf besar/kapital, atau karakter khusus lainnya.
    
2. **Jaga Agar Tetap Pendek:** Jangan membuat nama _branch_ terlalu panjang. Ingat, _branch_ ini harus berumur pendek dan cepat mati (seperti yang dibahas di materi sebelumnya).
    
3. **Tidak Ada Nama Pengguna:** Hindari menambahkan nama Anda sendiri ke nama _branch_ (`feat/andi-fix-login`). Konteks kepemilikan sudah jelas dari _commit_ atau PR.

---
obsidianUIMode: preview
materi: Conventional Branch
sumber:
  - gemini.google.com
datetime: 2025-12-13T10:34:00
tags:
  - git
  - github
---
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

|**Tipe Branch**|**Tujuan**|**Contoh Nama Branch**|
|---|---|---|
|**`feat`**|Mengembangkan fitur baru.|`feat/checkout-flow/tambah-metode-bayar`|
|**`fix`**|Memperbaiki _bug_ pada fungsionalitas yang ada.|`fix/api-user/perbaiki-filter-tanggal`|
|**`refactor`**|Perubahan kode yang meningkatkan struktur tanpa mengubah fungsionalitas.|`refactor/navbar/ubah-komponen-ke-ts`|
|**`docs`**|Perubahan pada dokumentasi (README, Wiki).|`docs/readme/perbarui-instruksi-install`|
|**`chore`**|Tugas rutin/pemeliharaan (misalnya, _update_ dependensi).|`chore/deps/update-react-router`|
|**`test`**|Menulis atau memodifikasi _test_ saja.|`test/auth/tambah-unit-test-login`|
|**`hotfix`**|Perbaikan mendesak langsung ke produksi (seringkali dilewatkan dari _staging_).|`hotfix/db/perbaiki-error-timeout`|

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

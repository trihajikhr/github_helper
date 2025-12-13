---
obsidianUIMode: preview
materi: Conventional Commit
sumber:
  - gemini.google.com
datetime: 2025-12-13T09:54:00
tags:
  - git
  - github
---
---
# Conventional Commit: Standar Message Commit
Dalam proyek kolaboratif, _commit message_ adalah kartu identitas dari setiap perubahan kode dan berfungsi sebagai narasi historis proyek. Namun, seringkali kita berhadapan dengan histori Git yang dipenuhi _commit_ berantakan, seperti "fix," "test," atau bahkan hanya "nyoba," yang membuat _debugging_ dan _code review_ menjadi mimpi buruk. Ketika sebuah masalah muncul, sulit untuk menentukan **apa** yang diubah, **mengapa** perubahan itu dibuat, dan **cakupan** mana yang terpengaruh. Strategi _Conventional Commits_ hadir sebagai solusi industri untuk mengatasi kekacauan komunikasi ini, menawarkan standar format yang ketat, konsisten, dan dapat dibaca baik oleh manusia maupun mesin.

## 1 | Mengapa Commit Message yang Jelas itu Penting?

Sebelum membahas strukturnya, penting untuk dipahami mengapa tim Anda harus berinvestasi dalam Conventional Commits:

- **1.1. Debugging Cepat:** Ketika _bug_ muncul di produksi, Anda bisa menggunakan `git blame` atau `git log` untuk segera mengidentifikasi _commit_ mana yang memperkenalkan masalah, dan yang terpenting, **mengapa** perubahan itu dibuat.
    
- **1.2. Review Kode Efisien:** _Reviewer_ dapat dengan cepat memahami _scope_ (cakupan) perubahan hanya dari judul _commit_, memungkinkan mereka fokus pada bagian kode yang paling relevan.
    
- **1.3. Automasi Changelog:** Conventional Commits memungkinkan _tools_ otomatis (seperti `standard-version`) untuk menghasilkan _Changelog_ (daftar perubahan) yang rapi untuk setiap rilis.
    
- **1.4. Penentuan Versi Semantik (SemVer):** Tipe _commit_ tertentu (`fix` atau `feat`) secara otomatis menentukan apakah rilis berikutnya adalah _patch_, _minor_, atau _major_ version.


## 2 | Struktur Dasar Conventional Commit

Setiap _commit message_ harus mengikuti format standar ini, terdiri dari Tipe, Cakupan (Scope) opsional, dan Deskripsi (Subject):

```
<tipe>[opsional-scope]: <deskripsi-singkat>

[opsional-body-panjang]

[opsional-footer/breaking-changes]
```

### A. Bagian Wajib: `<tipe>`

Ini adalah bagian terpenting, mendefinisikan sifat perubahan. Ini harus ditulis dalam huruf kecil dan diikuti titik dua (`:`).

|**Tipe**|**Deskripsi (Tujuan Commit)**|**Dampak SemVer**|
|---|---|---|
|**`feat`**|**FEATURE:** _Commit_ yang menambahkan fitur baru (misalnya, menambahkan _endpoint_ API baru).|**MINOR** (versi naik: 1.0.0 → 1.1.0)|
|**`fix`**|**FIX:** _Commit_ yang memperbaiki _bug_ (masalah yang salah/rusak).|**PATCH** (versi naik: 1.0.0 → 1.0.1)|
|`docs`|**DOCUMENTATION:** Hanya perubahan dokumentasi (README, JSDoc).|Tidak ada|
|`style`|**STYLE:** Perubahan yang tidak mempengaruhi makna kode (spasi, format, _semicolon_).|Tidak ada|
|`refactor`|**REFACTORING:** Perubahan kode yang tidak menambah fitur atau memperbaiki _bug_, tetapi meningkatkan struktur/kebersihan kode.|Tidak ada|
|`test`|**TESTS:** Menambahkan atau mengubah _test_ yang hilang.|Tidak ada|
|`chore`|**CHORES:** Perubahan pemeliharaan yang tidak terkait dengan logika aplikasi (misalnya, memperbarui konfigurasi CI).|Tidak ada|

### B. Bagian Opsional: `[opsional-scope]`

Digunakan untuk memberikan konteks di bagian mana kode Anda berubah. Ini ditulis dalam tanda kurung dan segera setelah Tipe.

- **Contoh:** `feat(auth): tambahkan validasi password`
    
    - _Scope_ di sini adalah **`auth`** (autentikasi).
        
- **Contoh:** `fix(ui-dashboard): perbaiki tabel pagination`
    
    - _Scope_ di sini adalah **`ui-dashboard`**.
        

### C. Bagian Wajib: `<deskripsi-singkat>` (Subject)

Ini adalah deskripsi singkat dan imperatif tentang perubahan tersebut (seperti perintah).

- **Aturan Wajib:**
    
    1. Tulis dalam **kalimat perintah** (imperatif): "tambahkan" bukan "menambahkan" atau "menambahkan".
        
    2. Maksimal **50-72 karakter** agar mudah dibaca di _tools_ Git.
        
    3. Jangan diakhiri dengan titik (.).
        
    4. Mulai dengan huruf kecil.

## 3 | Contoh Conventional Commit Lengkap

Berikut adalah perbandingan _commit_ buruk versus _commit_ yang bersih:

|**Commit Buruk**|**Commit Bersih (Conventional)**|
|---|---|
|`fix`|`fix(cart): perbaiki perhitungan diskon`|
|`nyoba login`|`feat(login): tambahkan fitur 'lupa password'`|
|`ganti text di dashboard`|`style(dashboard): ubah warna font menu utama`|

**Contoh Commit Multi-baris Terbaik:**

```
feat(api): implementasi endpoint GET /products

Tambahkan endpoint API untuk mengambil daftar semua produk.
Endpoint ini sudah mencakup filter berdasarkan kategori dan harga.

BREAKING CHANGE: Sebelumnya, semua produk diambil dari endpoint /items.
Endpoint lama /items telah dihapus. Harap gunakan /products.
Refs: #55
```

## 4 | Menandai Breaking Change (Perubahan Mayor)

Jika _commit_ Anda menghasilkan perubahan yang tidak kompatibel ke belakang (membutuhkan versi **MAJOR** baru), Anda **wajib** menandainya:

1. **Di Footer:** Tambahkan `BREAKING CHANGE:` (Huruf besar dan diakhiri titik dua).
    
2. **Di Subject (Alternatif):** Tambahkan tanda seru (`!`) setelah Tipe dan Scope.
    
    - Contoh: `feat(auth)!: hapus support untuk username`
        
        (Ini otomatis akan menaikkan versi MAJOR: 1.0.0 → 2.0.0)
        

## 5 | Strategi Implementasi dalam Tim

Untuk memastikan semua orang mengikutinya:

1. **Edukasi & Sosialisasi:** Jelaskan standar ini di _onboarding_ tim Anda (Poin 23 dari materi sebelumnya).
    
2. **Pre-commit Hook:** Gunakan alat seperti **Commitlint** yang terintegrasi dengan _Pre-commit Hook_ (Poin 13). Ini akan mencegah _user_ membuat _commit_ di mesin lokal mereka jika _message_ mereka tidak sesuai dengan format yang telah ditetapkan.
    
3. **Review PR:** Jadikan _commit message_ yang bersih sebagai persyaratan wajib dalam proses _Code Review_ (Poin 8).
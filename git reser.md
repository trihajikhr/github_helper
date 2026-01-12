---
obsidianUIMode: preview
materi:
sumber:
datetime:
tags:
---
Link Sumber: 



> apa itu git reset?

Oke, Git reset itu salah satu perintah paling powerful — dan sekaligus berbahaya kalau nggak dipahami. Aku jelasin lengkap, step by step.

---

## **1. Apa itu `git reset`**

- `git reset` **mengubah posisi HEAD** di branch saat ini.
    
- HEAD menunjuk ke commit terbaru di branch.
    
- Dengan reset, kamu bisa “memundurkan” branch ke commit sebelumnya atau ke commit tertentu.
    
- Ada **tiga mode utama**:
    

|Mode|Apa yang berubah|Kapan dipakai|
|---|---|---|
|`--soft`|HEAD dipindah, **staging/Index tetap**|Gabungkan commit terakhir ke staging untuk diubah atau squash|
|`--mixed` (default)|HEAD dipindah, **staging di-reset**, tapi **file lokal tetap**|Menghapus commit tapi simpan perubahan di working directory|
|`--hard`|HEAD dipindah, staging dan working directory ikut di-reset|Menghapus commit dan perubahan, _PERMANEN_ jika belum ada backup|

---

## **2. Contoh penggunaan**

### a. Reset commit terakhir, tapi simpan perubahan

```bash
git reset --soft HEAD~1
```

- Commit terakhir dihapus dari branch, tapi perubahan tetap di staging.
    
- Bisa commit ulang dengan pesan baru.
    

### b. Reset commit terakhir, hapus dari staging tapi simpan di working directory

```bash
git reset HEAD~1
# sama dengan --mixed
```

- Commit dihapus, file tetap ada di folder lokal tapi unstaged.
    
- Cocok kalau mau edit dulu sebelum commit ulang.
    

### c. Reset commit terakhir dan hapus semua perubahan

```bash
git reset --hard HEAD~1
```

- Commit terakhir dihapus, file lokal kembali ke kondisi commit sebelumnya.
    
- **PERINGATAN:** perubahan yang belum di-push akan hilang.
    

---

## **3. Reset ke commit tertentu**

```bash
git reset --hard <commit_id>
```

- `<commit_id>` bisa dari `git log --oneline`.
    
- HEAD, staging, dan working directory ikut kembali ke commit itu.
    

---

## **4. Hal penting yang harus diperhatikan**

1. **Force push jika sudah di remote:**  
    Kalau sudah push commit nakal dan pakai `reset --hard`, untuk sinkron di GitHub perlu:
    
    ```bash
    git push origin nama_branch --force
    ```
    
    Tapi ini bisa mengacaukan orang lain yang sudah pull branch itu.
    
2. **Gunakan revert untuk branch publik:**
    
    - Branch protected (misal main) sebaiknya pakai `git revert <commit>` daripada reset → aman, riwayat tetap utuh.
        
3. **Selalu cek log dulu:**
    

```bash
git log --oneline
```

- Pastikan commit yang di-reset benar.
    

---

Kalau mau, aku bisa buat **diagram visual `git reset`** yang menunjukkan HEAD, staging, dan working directory saat `--soft`, `--mixed`, dan `--hard`. Ini bikin lebih gampang ngerti bedanya.

Mau aku bikinkan diagram itu?
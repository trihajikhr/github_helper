---
obsidianUIMode: preview
materi:
sumber:
datetime:
tags:
---
Link Sumber: 

---
> apa itu git re3vert

Oke, `git revert` itu agak beda sama `git reset`, dan justru lebih aman buat branch publik. Mari kita bedah detailnya.

---

## **1. Pengertian `git revert`**

- `git revert` **membuat commit baru** yang membatalkan perubahan dari commit tertentu.
    
- **Tidak menghapus commit lama**, tapi menambahkan commit baru yang “mengembalikan keadaan” file seperti sebelum commit itu.
    
- Ideal untuk branch publik atau branch yang dilindungi karena riwayat tetap utuh.
    

---

## **2. Perbedaan utama `git revert` vs `git reset`**

|Fitur|git reset|git revert|
|---|---|---|
|Riwayat commit|Bisa dihapus / diubah|Tetap utuh|
|Aman di branch publik?|Tidak, bisa mengacaukan orang lain|Aman|
|Cara kerjanya|Memindahkan HEAD ke commit sebelumnya|Membuat commit baru yang membatalkan commit target|
|Efek di remote|Perlu force push jika sudah push|Bisa push normal|

---

## **3. Contoh penggunaan**

### a. Revert commit terakhir

```bash
git revert HEAD
```

- Membuat commit baru yang **membatalkan commit terakhir**.
    

### b. Revert commit tertentu

```bash
git log --oneline
# misal commit nakal id: abc123
git revert abc123
```

- Commit `abc123` dibatalkan dengan commit baru.
    
- File akan kembali ke kondisi sebelum commit itu, tapi **commit nakal tetap ada di log**.
    

### c. Revert beberapa commit sekaligus

- Bisa revert **range commit** atau gunakan **revert interaktif**:
    

```bash
git revert <commit_id1>^..<commit_id2>
```

- Membuat beberapa commit baru sekaligus untuk membatalkan range commit.
    

---

## **4. Kapan pakai `git revert`**

1. **Branch publik / protected**
    
    - Misal `main` atau branch tim, agar riwayat tetap aman.
        
2. **Ada commit nakal / bug**
    
    - Daripada hapus dengan reset → revert membuat commit yang membatalkan.
        
3. **Tidak ingin mengacaukan orang lain**
    
    - Semua kolaborator tetap bisa pull tanpa konflik karena riwayat tidak diubah.
        

---

## **5. Tips**

- Setelah revert, commit baru bisa langsung di-push ke remote:
    

```bash
git push origin nama_branch
```

- Bisa dicombine dengan PR supaya ada review sebelum merge.
    

---

Kalau mau, aku bisa buat **diagram visual perbedaan git revert vs reset**, dari commit log, HEAD, dan working directory, supaya gampang dipahami siapa yang hilang atau dibatalkan.

Mau aku buatkan diagram itu?
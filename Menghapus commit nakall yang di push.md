---
obsidianUIMode: preview
materi:
sumber:
datetime:
tags:
---
Link Sumber: 

---
Ah, ini situasi klasik: ada commit “nakal” yang masuk ke branch tim, dan kamu ingin **menghapus atau membatalkannya**. Di Git/GitHub ada beberapa cara, tergantung apakah commit itu sudah di-push ke remote (`origin`) atau belum, dan apakah branch itu dilindungi.

---

## **1. Commit belum di-push (lokal)**

Kalau commit masih di lokal:

- **Hapus commit terakhir:**
    

```bash
git reset --hard HEAD~1
```

`HEAD~1` artinya hapus 1 commit terakhir.

- **Hapus beberapa commit terakhir:**
    

```bash
git reset --hard HEAD~3
```

- Commit hilang dari branch lokal, belum menyentuh remote.
    

---

## **2. Commit sudah di-push ke remote**

Jika commit sudah di-push ke GitHub, cara menghapusnya tergantung branch protection:

### a. **Branch tidak protected**

- Kamu bisa pakai **force push** (beresiko!):
    

```bash
git reset --hard <commit_id_sebelum_nakal>
git push origin nama_branch --force
```

- `<commit_id_sebelum_nakal>` bisa dilihat dengan `git log`.
    
- Ini **menghapus commit nakal dari remote**, tapi hati-hati:
    
    - Semua orang yang sudah pull branch ini harus sinkron ulang (`git fetch` + `git reset`)
        
    - Bisa bikin konflik kalau mereka sudah kerja di atas commit yang dihapus.
        

### b. **Branch protected**

- Kalau branch dilindungi di GitHub (branch protection rules):
    
    - **Force push biasanya diblokir**.
        
    - Solusinya: buat **revert commit** → membuat commit baru yang membatalkan commit nakal:
        

```bash
git revert <commit_id_nakal>
git push origin nama_branch
```

- Ini aman, tidak mengubah riwayat branch, tetap tercatat siapa yang revert.
    

---

## **3. Cara aman untuk branch tim**

1. **Gunakan revert** jika branch penting (misal `main` atau branch orang lain).
    
2. **Jangan pakai force push** kecuali semua kolaborator sudah diberi tahu.
    
3. **Cek commit log sebelum push**: `git log --oneline` atau `git diff` untuk review.
    
4. **Atur branch protection rules**:
    
    - Restrict push hanya untuk owner atau PR.
        
    - Jadi kolaborator nakal **tidak bisa langsung push** ke branch orang lain.
        

---

Kalau mau, aku bisa buatkan **diagram alur menangani commit nakal**: mulai dari commit lokal → push → revert atau reset, termasuk opsi aman di branch terproteksi.

Mau aku buatkan diagram itu?
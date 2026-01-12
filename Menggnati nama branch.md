---
obsidianUIMode: preview
materi:
sumber:
datetime:
tags:
---
Link Sumber: 

---
> Apakah bisa mengagnati nama branch?

Bisa banget, branch di Git itu fleksibel. Ada dua cara tergantung branch **lokal** atau **remote**:

---

### 1. **Ganti nama branch lokal**

```bash
# Pastikan berada di branch yang mau diganti namanya
git branch -m nama_baru
```

Contoh:

```bash
git checkout fitrah
git branch -m fitrah-baru
```

Sekarang branch lokal namanya sudah berubah.

---

### 2. **Push branch baru ke remote dan hapus branch lama**

```bash
# Push branch baru ke remote
git push origin nama_baru

# Set upstream supaya branch lokal nge-track remote branch baru
git push --set-upstream origin nama_baru

# Hapus branch lama di remote (opsional)
git push origin --delete nama_lama
```

---

⚠️ Catatan:

- Kalau ada orang lain sudah nge-pull branch lama, mereka perlu update branch baru di lokal mereka.
    
- Kalau branch itu **branch yang dilindungi di GitHub**, kamu harus ubah **branch protection rules** ke nama branch baru juga.
    

Kalau mau, aku bisa kasih langkah **lengkap pindah nama branch yang sudah diproteksi di GitHub** supaya aman tanpa ganggu PR atau kolaborator. Mau aku buatkan?

> nah, sekarang kollabotraotr harus ngapain nih supaya mereka aman?


Oke, setelah kamu ubah nama branch dan setup branch protection, langkah selanjutnya supaya **kolaborator aman dan tidak “nabrak” branch orang lain** adalah ini:

---

### 1. **Update branch lokal mereka**

Kolaborator harus sinkronisasi branch baru di lokal mereka:

```bash
# Ambil update branch dari remote
git fetch origin

# Ganti nama branch lokal lama (misal "fitrah") sesuai remote
git branch -m fitrah fitrah-baru

# Set upstream ke branch remote baru
git push --set-upstream origin fitrah-baru
```

Sekarang branch lokal mereka **ngehubung ke branch remote baru** dan siap push/commit lagi.

---

### 2. **Hindari push ke branch lain**

- Jangan push langsung ke branch orang lain. Kalau mereka coba push ke branch selain miliknya, **GitHub akan menolak push** karena protection rules.
    
- Kalau ingin kontribusi ke branch lain → **buat Pull Request (PR)**.
    

---

### 3. **Selalu tarik update dari main**

Untuk menghindari konflik dan supaya branch mereka tetap up-to-date:

```bash
git checkout main
git pull origin main

git checkout fitrah-baru
git rebase main
# atau git merge main
```

Ini bikin branch mereka aman dari perubahan di `main`.

---

### 4. **Gunakan PR untuk merge ke branch lain**

- Kalau kolaborator ingin merge perubahan ke branch lain (misal fitur bersama), **selalu pakai PR**.
    
- Branch protection rules akan memastikan PR direview sebelum bisa merge.
    

---

Kalau mau, aku bisa bikin **checklist step-by-step untuk kolaborator** supaya mereka langsung tahu apa yang harus dilakukan setelah nama branch diganti dan proteksi diaktifkan. Ini bakal bikin tim lebih rapi.

Mau aku bikinkan checklist itu?
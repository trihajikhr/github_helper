---
obsidianUIMode: preview
materi:
sumber:
datetime:
tags:
---
Link Sumber: 

---
> kalau aku reset ke branch si fitrah misal, terus dia pull nanti lansgung ikut juga atau ngga?

Ah, ini penting banget buat dipahami sebelum kamu main **reset + force push**. Jawabannya: **nggak otomatis ikut** kalau user lain sudah nge‑pull branch itu sebelumnya. Mari gue jelasin step by step.

---

## **1. Kondisi awal**

- Branch: `fitrah`
    
- Kamu sebagai admin melakukan:
    

```bash
git reset --hard <commit_sebelum_nakal>
git push origin fitrah --force
```

- Ini **mengubah history di remote**.
    

---

## **2. Apa yang terjadi kalau user lain pull?**

### a. Jika user belum pernah pull branch itu

- Saat dia pertama kali pull:
    

```bash
git pull origin fitrah
```

- Branch lokal mereka akan **sinkron langsung** dengan remote → ikut reset.
    

### b. Jika user sudah pull branch itu sebelum reset

- Branch lokal mereka **menjadi diverged** karena remote history sudah berubah.
    
- Kalau dia coba pull:
    

```bash
git pull origin fitrah
```

- Git akan kasih **error**:
    

```
! [rejected]        fitrah -> fitrah (non-fast-forward)
```

- Mereka harus melakukan **reset lokal juga** atau merge manual, misal:
    

```bash
git fetch origin
git reset --hard origin/fitrah
```

- Setelah itu branch mereka **sinkron lagi dengan remote**.
    

---

## **3. Dampak terhadap workflow**

- **Reset + force push** itu aman untuk **One Branch One Man**, karena setiap branch cuma dipakai satu user.
    
- Satu-satunya efek ke user lain:
    
    - Mereka harus **sinkron ulang** branch mereka.
        
    - Kalau branch itu benar-benar milik user itu, **mereka nggak merasa dirugikan** karena branch mereka memang “dimiliki sendiri”.
        

---

## **4. Ringkasnya**

|Kondisi|Apa yang terjadi|
|---|---|
|User belum pull branch → reset|Otomatis ikut saat pull pertama|
|User sudah pull branch → reset|Perlu manual reset lokal → diverged history|
|Branch hanya dipakai satu orang|Aman, tinggal admin reset|
|Branch dipakai banyak orang|Bisa bikin konflik → hati-hati|

---

Kalau mau, aku bisa buat **diagram alur reset + force push untuk One Branch One Man**, dari remote → lokal user → apa yang terjadi kalau mereka pull setelah reset.

Mau aku bikinkan diagram itu?
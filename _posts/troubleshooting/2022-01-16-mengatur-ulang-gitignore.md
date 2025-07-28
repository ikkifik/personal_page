---
layout: posts
title: "Mengatur ulang .gitignore (Untrack)"
category: Troubleshooting
---

_Solusi ini berasal dari [stackoverflow](https://stackoverflow.com/questions/1139762/ignore-files-that-have-already-been-committed-to-a-git-repository )_

Untuk mengatur ulang file .gitignore yang telah terekam di git repository agar bisa men-untrack semua file yang sengaja diabaikan dengan cara menghapus git cache, caranya sebagai berikut.

1. Commit file yang telah dibuat terlebih dahulu.  

        git add .
        git commit -m “pesan commit”

2. Hapus cache dari git.  

        git rm -r --cached .

3. Seluruh file akan kembali seperti awal kita menginisialiasi git, lakukan commit ulang.  

        git add .
        git commit -m ".gitignore is now working"

----

Selain itu kita juga bisa menghapus tracking (cache) file satu per satu dengan perintah,  

        git rm --cached nama_file

Lalu lakukan hal yang sama dengan men-commit git.  

        git add filename
        git commit -m “pesan commit”
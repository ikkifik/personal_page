---
layout: posts
title: Fix high memory usage in Windows 11 (while idle)
date: 2025-07-26
category: Troubleshooting
---
Source: [Fossbytes](https://fossbytes.com/how-to-fix-high-ram-and-cpu-usage-of-windows-10-system-ntoskrnl-exe-process/)

Beberapa waktu ke belakang, saya sering mengalami kendala memori penuh 80% padahal sedang tidak sedang menjalankan program apapun. Solusi awal adalah restart komputer, dengan asumsi segala macam background task pasti akan tertutup, akan tetapi ketika baru pertama kali boot dan posisi masih idle pun ternyata memory masih saja penuh 80%. Padahal startup application juga sudah sangat minim yang diaktifkan.

Lalu saya menemunkan solusi ini dari Fossbyte untuk mengubah konfigurasi Regedit, dengan langkah-langkah di bawah ini:
- Tekan shortcut **Win Key + R**, untuk membuka Run command.
- Ketik “Regedit” lalu tekan Enter.
- Lalu pergi ke `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management`, untuk mudahnya copy-paste saja path tersebut pada address bar.
- Cari `ClearPageFileAtShutDown`, klik 2x, lalu ubah `Value Data`-nya menjadi 1
- Restart computer.

Dengan cara di atas, memory (RAM) pada komputer saya berhasil diredam menyisakan system usage saja sekitar memory +/- 28%, pada saat awal boot (idle).


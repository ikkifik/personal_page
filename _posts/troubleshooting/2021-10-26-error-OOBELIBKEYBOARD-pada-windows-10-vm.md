---
layout: posts
title: "Error OOBE pada Windows 10 VM"
category: Troubleshooting
---

Pernah saya diminta oleh Pakde(tetangga) yang berprofesi sebagai dosen di salah satu perguruan tinggi kedinasan untuk membantu merapikan dokumen laporannya. Pada saat itu posisi sistem operasi yang sedang saya gunakan single boot Linux Ubuntu, dengan software office menggunakan LibreOffice. Sedangkan mayoritas pekerja kantoran pasti menggunakan sistem operasi windows dengan sofware office microsoft office.  

Karena tidak mau membuang banyak waktu karena harus mengedit ulang di laptop Pakde dan tidak mau ambil risiko kalau semisal layout yang sudah ditata sedemikian rupa di laptop saya malah hancur ketika di laptop Pakde. Akhirnya memutuskan untuk mencoba menginstall sistem operasi windows di virtual machine(VM).  

Percobaan ini sebenarnya sudah lama ingin saya lakukan karena mengingat ketika membuat paper jurnal, template yang digunakan hancur tampilannya ketika masuk di LibreOffice. Asumsi awal karena LibreOffice dioptimasi untuk pengolahan dokumen berformat .odt, sedangkan template paper jurnal berformat .doc/.docx plus font berbasis windows. Di samping itu juga ada niatan tidak ingin menyusahkan dosen pembimbing ketika harus menata ulang layoutnya.  

----

## Troubleshooting

Awal membuat VM saya hanya memperhatikan berapa besar RAM yang digunakan, karena RAM laptop saya 8gb maka saya coba ambil setengahnya(4gb) untuk VM windows 10 ini. Instalasi berjalan lancar sampai selesai dan VM restart awal setelah instalasi.  

Ketika akan masuk ke halaman greeting(mengisi username, password, dll), muncul error:

> Something went wrong  
> But you can try again  
> OOBEKEYBOARD  

Jika diklik tombol try again, error berganti:

> Something went wrong  
> But you can try again  
> OOBEREGION

----

Error OOBE ini saya temukan solusinya di forum [virtualbox](https://forums.virtualbox.org/viewtopic.php?f=2&t=96726). Error ini muncul karena windows 10 mewajibkan hardware memiliki setidaknya processor(CPU) sebanyak 2 core, maka solusinya hanya menambah core dengan menggeser slider pada settingan VM(di sini saya menggunakan Virtualbox).

![VirtualBox CPU settings](/assets/images/posts/troubleshooting/error-OOBELIBKEYBOARD-pada-windows-10-vm.png "Menambah core pada CPU VM"){: .post-figure}

Begitu saja sudah bisa menyelesaikan masalah, terimakasih.
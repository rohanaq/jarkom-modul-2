# 2. Web Server
Web Server adalah perangkat yang menyediakan layanan akses kepada pengguna melalui protokol HTTP atau HTTPS melalui aplikasi web.

### 2.1 Instalasi apache2
Install Web Server Apache pada PUCANG yang sebelumnya sudah diupdate dengan mengetikkan __apt-get install apache2__. Setelah proses instalasi selesai, coba akses __IP_PUCANG_TIAP_KELOMPOK__ pada browser maka akan muncul seperti gambar di bawah:

![Pucang1](images/01.png)

### 2.2 Instalasi PHP pada PUCANG
Supaya web server dapat menjalankan perintah PHP, maka kita perlu menginstall PHP pada PUCANG dengan mengetikkan __apt-get install php__

![Pucang2](images/02.png)

Setelah proses instalasi selesai, untuk mengetahui apakah instalasi PHP berhasil atau tidak, silahkan membuat file PHP yang diletakkan di __/var/www/html__
```
cd /var/www/html
nano ini.php
```

Kemudian isikan pada file __ini.php__:
```
<?php phpinfo(); ?>
```

Setelah selesai membuat file __ini.php__, untuk mencoba membukanya akses dengan __IP_PUCANG_TIAP_KELOMPOK/ini.php__ maka akan muncul seperti gambar di bawah:

![Pucang3](images/03.png)

Untuk membuat sebuah halaman atau website, kita dapat menambahkannya pada direktori __/var/www/html__. Langkah-langkahnya sama seperti saat membuat halaman __ini.php__.

Sekarang bayangkan ketika kita ingin mengakses sebuah halaman web kita harus mengetikkan alamat IPnya terlebih dahulu. Ribet kan? Maka kita akan membuatnya menjadi mudah, silahkan lakukan konfigurasi sehingga ketika kita mengakses __klampis.com__ akan diarahkan ke halaman web yang sudah kita buat. 

![Pucang4](images/04.png)

Jika lupa caranya, silahkan buka lagi modul sebelumnya yang membahas tentang [DNS](https://github.com/rohanaq/jarkom2/tree/master/DNS).

### 2.3 Mengubah Direktori Default
Cobalah membuat sebuah halaman web di luar direktori __/var/www/html__ sebagai contoh kita akan membuat halaman __coba.php__ pada direktori __/var/www__. Maka ketika diakses akan muncul seperti gambar di bawah:

![Pucang5](images/05.png)

Tulisan yang ditampilkan pada browser adalah __NOT FOUND__, karena secara default web server apache akan mengakses file-file yang ada pada direktori __/var/www/html__. Namun halaman __coba.php__ tetap bisa diakses dengan cara mengubah direktori default dengan mengetikkan:
```
nano /etc/apache2/sites-enabled/000-default.conf
```

Setelah itu ubah __DocumentRoot__ menjadi __/var/www/__ seperti gambar di bawah ini:

![Pucang6](images/06.png)

Setelah itu restart apache2 dengan perintah `service apache2 restart` dan coba akses kembali halaman __coba.php__ pada browser anda.

## Latihan
1. Download halaman web di 10.151.36./web2.tar.gz dan taruh di /var/www
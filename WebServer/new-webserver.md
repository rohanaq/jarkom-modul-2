# Web Server

## C. Dasar Teori
### 1. Web Server
Web Server adalah perangkat yang menyediakan layanan akses kepada pengguna melalui protokol HTTP atau HTTPS melalui aplikasi web.
### 2. Apache Web Server
Apache adalah sebuah nama web server yang bertanggung jawab pada request-response HTTP dan logging informasi secara detail

## D. Instalasi Apache
1. Buka uml **Pucang** dan jalankan perintah

    `apt-get install apache2 `
    
    ![](/WebServer/gambar/1.PNG)
    
2. Buka browser laptop/komputer masing-masing dan buka web **IP Pucang Masing-Masing Kelompok** sampai muncul halaman Apache

    ![](/WebServer/gambar/2.PNG)

## E. Instalasi PHP
1. Buka uml **Pucang** dan jalankan perintah
    `apt-get install php`
    
    ![](/WebServer/gambar/3.PNG)

2. Test apakah **php** sudah terinstall dengan menjalankan perintah

    `php -v`
    
    ![](/WebServer/gambar/4.PNG)

## F. Apache Basic
Webserver Apache memiliki folder untuk konfigurasi yang berada di **/etc/apache2**

![](/WebServer/gambar/5.PNG)

Pada folder **/etc/apache2** terdapat berbagai file dan folder untuk konfigurasi

Penting untuk diketahui:
1. **apache2.conf** adalah file konfigurasi utama apache2.
2. **ports.conf** adalah file konfigurasi port yang digunakan untuk webserver.
3. **sites-available** adalah folder tempat konfigurasi website (virtual host) yang tersedia.
4. **sites-enabled** adalah folder tempat konfigurasi website (virtual host) yang tersedia dan sudah aktif.
5. **mods-available** adalah folder tempat modul-modul apache2 yang tersedia.
6. **mods-enabled** adalah folder tempat modul-modul apache2 yang tersedia dan sudah aktif.

## G. Konfigurasi Apache
### G.1. Penggunaan Sederhana
1. Buka folder **/etc/apache2/sites-available**

    ![](/WebServer/gambar/6.PNG)
    
    Pada folder **/etc/apache2/sites-availabke** terdapat dua buah file,
    a. **000-default.conf** adalah file konfigurasi website default apache untuk http.
    b. **default-ssl.conf** adalah file konfigurasi website default apache untuk https.

2. Buka file **000-default.conf**

    ![](/WebServer/gambar/7.PNG)
3. Pada file **000-default.conf** berisi contoh konfigurasi,

    a. port berapa yang digunakan.
    
        <VirtualHost *:80> # Menggunakan port 80
        
    b. domain
    
        # ServerName www.example.com
        
    c. folder tempat website
    
        DocumentRoot /var/www/html
     
4. Buka folder tempat website pada file konfigurasi default yaitu **/var/www/html** dan buat file **index.php** yang berisi

        <?php
            phpinfo();
        ?>

5. Buka browser dan masukkan alamat **http://[IP Pucang]/index.php**

    ![](/WebServer/gambar/8.PNG)
    
    * **Catatan**:
        Apabila tampilan web tidak muncul seperti gambar diatas dan hanya muncul plain text isi file **index.php**, silahkan install **libapache2-mod-php7.0** dengan menjalankan perintah 
        
        `apt-get install libapache2-mod-php7.0`
        
        dan restart apache dengan perintah
        
        `service apache2 restart`
        
### G.2. Membuat Konfigurasi Website Menggunakan Port 8080
1. Pindah ke folder **/etc/apache2/sites-available** dan copy file **000-default.conf** menjadi file **default-8080.conf**.

    ![](/WebServer/gambar/9.PNG)
    
2. Buka file **default-8080.conf**, kemudian ubah ubah port yang digunakan yang awalnya **80 **menjadi **8080 **dan ubah tempat menaruh file/folder web yang awalnya **/var/www/html** menjadi **/var/www/web-8080**.

    ![](/WebServer/gambar/10.PNG)

3. Tambahkan port 8080 pada file **ports.conf**

    ![](/WebServer/gambar/11.PNG)

4. Untuk mengaktifkan konfigurasi **default-8080.conf** jalankan perintah

    `a2ensite`

    dan ketik nama **file konfigurasi tanpa .conf**
    
    ![](/WebServer/gambar/12.PNG)
    
    kemudian tekan enter.

5. Restart apache menggunakan perintah **service apache2 restart**
6. Pindah ke folder **/var/www** dan buat folder baru dengan nama **web-8080**
7. Masuk ke folder **web-8080** dan buat file **index.php** yang berisi
        <?php
            echo "Hello ini port 8080";
        ?>
    
    
        
8. 




    
    

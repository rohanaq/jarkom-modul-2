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
3. **sites-available** adalah folder tempat konfigurasi website yang tersedia.
4. **sites-enabled** adalah folder tempat konfigurasi website yang tersedia dan sudah aktif.
5. **mods-available** adalah folder tempat modul-modul apache2 yang tersedia.
6. **mods-enabled** adalah folder tempat modul-modul apache2 yang tersedia dan sudah aktif.

## G. Konfigurasi Apache
### 1. Penggunaan Sederhana
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
        Apabila tampilan web tidak muncul seperti gambar diatas dan hanya muncul plain text isi file **index.php**, silahkan install libapache2-mod-php7.0 dengan menjalankan perintah 
        
        `apt-get install libapache2-mod-php7.0`
        
        dan restart apache dengan perintah
        
        `service apache2 restart`
        
        

    
    

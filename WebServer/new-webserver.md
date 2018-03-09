# Web Server

## A. Persyaratan Tambahan Mengikuti Sesilab
1. Record A dan PTR pada klampis.com mengarah ke IP Pucang

## B. Penting Untuk Dibaca
1. Pastikan Semua UML bisa connect ke internet baik dapat melakukan koneksi keluar maupun dapat ping dari luar (Khusus DMZ).
2. Pastikan Pucang dan Klampis sudah memiliki memory 256M


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

## F. Mengenal Apache
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

## G. Konfigurasi Apache Sederhana
### G.1. Penggunaan Sederhana
1. Pindah ke folder **/etc/apache2/sites-available**

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
     
4. Pindah ke folder tempat website pada file konfigurasi default yaitu **/var/www/html** dan buat file **index.php** yang berisi

        <?php
            phpinfo();
        ?>

5. Buka browser dan akses alamat **http://[IP Pucang]/index.php**

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
    
    ![](/WebServer/gambar/13.PNG)
        
8. Buka browser dan akses alamat http://[IP Pucang]:8080

    ![](/WebServer/gambar/14.PNG)

## H. Mari Berimajinasi
### H.1. Setting Domain Pada Apache
Nia adalah seorang mahasiswi Departemen Infomatika yang sedang ingin membuat website dengan domain **klampis.com**. Dia memiliki **teman** yang bernama Udin kebetulan mempunyai server yang bisa digunakan untuk tempat host websitenya.

Maka yang harus dilakukan Udin adalah:

1. Pindah ke folder **/etc/apache2/sites-available** dan copy file     **000-default.conf** menjadi **klampis.com.conf**

    ![](/WebServer/gambar/15.PNG)
    
2. Buka file **klampis.com.com**, kemudian

    2.1. Uncomment **ServerName** dan ganti **www.example.com** menjadi **klampis.com**.
    
    2.2. Tambahkan
    
        ServerAlias www.klampis.com
    agar dapat mengakses **www.klampis.com**
         
    2.3. Ganti tempat **DocumentRoot** yang awalnya **/var/www/html** menjadi **/var/www/klampis.com**
    
    ![](/WebServer/gambar/16.PNG)
    
3. Aktifkan konfigurasi **klampis.com.conf** dengan menjalankan
 `a2ensite klampis.com`
 
     ![](/WebServer/gambar/17.PNG)
 
4. Restart apache dengan menjalankan
`service apache2 restart`
5. Pindah ke folder **/var/www** dan buat folder baru dengan nama **klampis.com**
6. Buat file **index.php** dengan isi file

        <?php
            echo "Hello ini klampis.com";
        ?>
    
    ![](/WebServer/gambar/18.PNG)

7. Ganti DNS laptop/komputer sesuai **IP Klampis** masing-masing.
8. Buka browser dan akses **klampis.com**

    ![](/WebServer/gambar/19.PNG)

### H.2. Directory Listing
Di dalam folder **/var/www/klampis.com** terdapat folder sebagai berikut

        /var/www/klampis.com
                            /download
                                    /lagu
                            /assets
                                    /javascript
                            /private-digest
                            /private-basic

Karena folder **download** terdapat file-file yang bisa didownload oleh pengunjung website **klampis.com**, Nia ingin folder tersebut dapat menampilkan list file yang ada. Tetapi untuk folder **assets**, Nia tidak ingin ada yang tahu apa isi folder tersebut ketika diakses oleh pengunjung websitenya.

Maka yang harus dilakukan Udin adalah:

1. Buat folder **download**, **private** ,**assets**, **data** dan **assets/javascript** pada **/var/www/klampis.com** dengan menjalankan perintah berikut

        mkdir -p /var/www/klampis.com/data
        mkdir -p /var/www/klampis.com/download
        mkdir -p /var/www/klampis.com/download/lagu
        mkdir -p /var/www/klampis.com/assets
        mkdir -p /var/www/klampis.com/assets/javascript

#### H.2.1 Mengaktifkan Directory Listing

1. Pindah ke folder **/etc/apache2/sites-available** kemudian buka file **klampis.com** dan tambahkan
    
        <Directory /var/www/klampis.com/download>
            Options +Indexes #Untuk mengaktifkan directory listing
        </Directory>
    
    agar folder **download** menampilkan isi folder.
    
    ![](/WebServer/gambar/20.PNG)
    
2. Simpan dan restart apache.
3. Buka Browser dan akses **http://klampis.com/download**

    ![](/WebServer/gambar/21.PNG)


**Keterangan**:
  1. Untuk mengatur folder pada sebuah web, menggunakan
  
  `<Directory /x> ... </Directory>`
  
Contoh untuk mengatur /var/www/klampis.com/download
    
    <Directory /var/www/klampis.com/download>
        
    </Directory>

#### H.2.2 Mematikan Directory Listing

1. Pindah ke folder **/etc/apache2/sites-available** kemudian buka file **klampis.com** dan tambahkan
    
        <Directory /var/www/klampis.com/assets>
            Options -Indexes #Untuk mematikan directory listing
        </Directory>
    
    agar folder **assets** tidak menampilkan isi folder.
    
    ![](/WebServer/gambar/22.PNG)
    
2. Simpan dan restart apache.
3. Buka Browser dan akses **http://klampis.com/assets**

    ![](/WebServer/gambar/23.PNG)
  
### H.3 Directory Alias
Karena dirasa **http://[IP Klampis]/assets/javascript** terlalu panjang url-nya, maka Udin mencoba membuat directory alias menjadi **http://[IP Klampis]/assets/js**

Maka yang dilakukan Udin adalah

1. Pindah ke folder **/etc/apache2/sites-available** kemudian buka file **klampis.com** dan tambahkan

        Alias "/assets/js" "/var/www/klampis.com/assets/javascript"
                
        <Directory /var/www/klampis.com/assets/javascript>
            Require all granted # Mengizinkan akses ke semua pengguna
            Options +Indexes
        </Directory>
        
 ![](/WebServer/gambar/24.PNG)
        
2. Restart apache2
3. Pindah ke folder **/var/www/klampis.com/assets/javascript** dan buat file **app.js** dengan perintah 
`touch app.js`
    ![](/WebServer/gambar/25.PNG)

4. Buka browser dan akses **http://klampis.com/assets/js**

    ![](/WebServer/gambar/26.PNG)

### H.4. Module Rewrite

### H.4.1. Mengaktifkan Module Rewrite
Setelah dipikir-pikir ternyata **http://klampis.com/index.php** ternyata kurang cantik untuk penulisan url. Maka Udin berinisiatif untuk mengaktifkan module rewrite agar ketika mengakses file php tidak usah menambahkan ekstensi .php.

Maka yang dilakukan Udin adalah

1. Menjalankan perintah `a2enmod` dan menuliskan **rewrite** untuk mengaktikan module rewrite.

    ![](/WebServer/gambar/27.PNG)

2. Restart apache

### H.4.2. Membuat file .htaccess

Biasanya semua konfigurasi terhadap sebuah website diatur pada file di folder **/etc/apache2/sites-available**. Namun terkadang ada sebuah kasus bahwa kita tidak memiliki hak akses root untuk edit file konfigurasi yang berada di folder **/etc/apache2/sites-available** atau kita tidak ingin user lain untuk mengedit file konfigurasi yang berada di folder **/etc/apache2/sites-available**. 
Untuk mengatasi masalah tersebut kita dapat membuat file **.htaccess** pada folder dimana kita ingin atur. Untuk contoh kasus diatas kita ingin mengatur mod rewrite dari **http://klampis.com** agar saat mengakses file php tanpa ekstensi file. 

Maka yang dilakukan adalah 
Step 1. Pindah ke folder **/var/www/klampis.com** dan buat file **.htaccess** dengan isi file

    RewriteEngine On
    RewriteCond %{SCRIPT_FILENAME} !-d #Aturan tidak akan jalan ketika yang diakses adalah folder
    RewriteRule ^([^.]+)$ $1.php [NC,L]
    
![](/WebServer/gambar/28.PNG)

Keterangan

    * RewriteEngine On = Untuk flag bahwa menggunakan module rewrite
    * RewriteCond %{SCRIPT_FILENAME} !-d = aturan tidak akan jalan ketika yang diakses adalah folder (d)
    * RewriteRule ^([^.]+)$ $1.php [NC,L] = $1 adalah parameter input yang akan dicari oleh webserver
    * Info cek [Klik Disini](https://httpd.apache.org/docs/2.4/rewrite/flags.html)
    
Step 2. Buat file aboutus.php dengan isi


        <?php
        
            echo "ini halaman About Us"
        ?>
    
   ![](/WebServer/gambar/29.PNG)

Step 3. Pindah ke folder **/etc/apache2/sites-available** kemudian buka file **klampis.com** dan tambahkan

    <Directory /var/www/klampis.com>
        AllowOverride All
    </Directory>

![](/WebServer/gambar/30.PNG)

Keterangan : 
`AllowOverride All` ditambahkan agar konfigurasi **.htaccess** dapat berjalan.

Step 4. Restart apache

Step 5. Buka browser dan akses **http://klampis.com/aboutus**

![](/WebServer/gambar/31.PNG)

### H.5 Otorisasi

Pada web **http://klampis.com** terdapat path **/data** yang tidak boleh dibuka sembarang orang. Nia ingin **/data** hanya boleh di akses oleh pengguna yang memiliki ip **10.151.252.0/255.255.252.0**.

Maka yang dilakukan Udin adalah

Step 1. Pindah ke folder **/etc/apache2/sites-available** kemudian buka file **klampis.com** dan tambahkan

    <Directory /var/www/klampis.com/data>
        Options +Indexes
        Order deny,allow
        Deny from all
        Allow from 10.151.252.0/255.255.252.0
    </Directory>

![](/WebServer/gambar/32.PNG)

Keterangan:

* `Order deny,allow` merupakan urutan hak akses. Terdapat dua jenis tipe order yaitu:

    1. deny,allow : Bagian *Deny* harus dideclare terlebih dahulu sebelum _Allow_
    2. allow, deny : Bagian *Allow* harus dideclare terlebih dahulu sebelum _Deny_

* `Deny from all` berarti semua pengguna ditolak
* `Allow from 10.151.252.0/255.255.252.0` berarti apabila pengguna memiliki ip nid 10.151.252.0/22 diperbolehkan mengakses halaman.

* Info lebih lanjut [Klik Disini](https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html)

Step 2. Restart apache
Step 3. Buka browser dan akses **http://klampis.com/data**

![](/WebServer/gambar/33.PNG)

Gambar diatas ketika pengguna **tidak memiliki ip nid 10.151.252.0/22**


![](/WebServer/gambar/34.png)

Gambar diatas ketika pengguna **memiliki ip nid 10.151.252.0/22**






 
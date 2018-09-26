# **PENTING UNTUK DIBACA**
1. Pastikan UML KLAMPIS dan PUCANG Memory yang sebelumnya **96 diganti 256** pada file topologi.sh.
2. Jalankan **iptables -t nat .....** agar NGINDEN dan NGAGEL bisa terhubung ke internet.
3. Ketika ingin mengakses internet pastikan sudah mengexport proxy terlebih dahulu. **syntaxnya cek modul pengenalan UML** .
4. Jangan melakukan apapun sebelum asisten memberikan perintah.
5. Ikuti apa yang asisten arahkan.
6. Ketika point 4 dan 5 tidak ditaati **resiko tanggung sendiri!!!**

# 1. DNS (Domain Name System)



------



## 1.1 Teori

### 1.1.A Pengertian

DNS (_Domain Name System_) adalah sistem penamaan untuk semua device (smartphone, computer, atau
network) yang terhubung dengan internet. DNS Server berfungsi menerjemahkan nama domain menjadi alamat IP. DNS dibuat guna untuk menggantikan sistem penggunaan file host yang dirasa tidak efisien.

### 1.1.B Cara Kerja

![DNS](gambar/1.jpg)

Client akan meminta alamt IP dari suatu domain ke DNS server. Jika pada DNS server data alamat IP dari DNS server tersebut ada maka akan di return alamat IP nya kembali menuju client. Jika DNS server tersebut tidak memiliki alamat IP dari domain tersebut maka dia akan bertanya kepada DNS server yang lain sampai alamat domain itu ditemukan.

### 1.1.C Aplikasi DNS Server

Untuk praktikum jarkom kita menggunakan aplikasi BIND9 sebagai DNS server, karena BIND(Berkley Internet Naming Daemon) adalah DNS server yang paling banyak digunakan dan juga memiliki fitur-fitur yang cukup lengkap.

### 1.1.D List DNS Record
| Tipe          | Deskripsi                     |
| ------------- |:-----------------------------|
| A             | Memetakan nama domain ke alamat IP (IPv4) dari komputer hosting domain|
| AAAA          | AAAA record hampir mirip A record, tapi mengarahkan domain ke alamat Ipv6|
| CNAME         | Alias ​​dari satu nama ke nama lain: pencarian DNS akan dilanjutkan dengan mencoba lagi pencarian dengan nama baru|
| NS            | Delegasikan zona DNS untuk menggunakan authoritative name servers yang diberikan|
| PTR           | Digunakan untuk Reverse DNS (Domain Name System) lookup|
| SOA           | Mengacu server DNS yang mengediakan otorisasi informasi tentang sebuah domain Internet|
| TXT           | Mengijinkan administrator untuk memasukan data acak ke dalam catatan DNS, catatan ini juga digunakan di spesifikasi Sender Policy Framework|

### 1.1.E SOA (Start of Authority)

Adalah informasi yang dimiliki oleh suatu DNS zone.

| Nama          | Deskripsi                     |
| ------------- |:-----------------------------|
| Serial        | Jumlah revisi dari file zona ini. Kenaikan nomor ini setiap kali file zone diubah sehingga perubahannya akan didistribusikan ke server DNS sekunder manapun|
| Refresh       | Jumlah waktu dalam detik bahwa nameserver sekunder harus menunggu untuk memeriksa salinan baru dari zona DNS dari nameserver utama domain. Jika file zona telah berubah maka server DNS sekunder akan memperbarui salinan zona tersebut agar sesuai dengan zona server DNS utama|
| Retry         | Jumlah waktu dalam hitungan detik bahwa nameserver utama domain (atau server) harus menunggu jika upaya refresh oleh nameserver sekunder gagal sebelum mencoba refresh zona domain dengan nameserver sekunder itu lagi|
| Expire        | Jumlah waktu dalam hitungan detik bahwa nameserver sekunder (atau server) akan menahan zona sebelum tidak lagi mempunyai otoritas|
| Minimum       | Jumlah waktu dalam hitungan detik bahwa catatan sumber daya domain valid. Ini juga dikenal sebagai TTL minimum, dan dapat diganti oleh TTL catatan sumber daya individu|
| TTL           | (waktu untuk tinggal) - Jumlah detik nama domain di-cache secara lokal sebelum kadaluarsa dan kembali ke nameserver otoritatif untuk informasi terbaru|



------



## 1.2 Praktik

### 1.2.A Buat Topologi Berikut

![Topologi](gambar/2.PNG)

Referensi 

[Modul Pengenalan UML](https://github.com/rohanaq/Modul-Pengenalan-UML "Modul Pengenalan UML")

### 1.2.A Instalasi bind

- Buka *KATSU* dan update package lists dengan menjalankan command:

	```
	apt-get update
	```

![Klampis1](image/1.PNG)

- Setalah melakukan update silahkan install aplikasi bind9 pada *KATSU* dengan perintah:

	```
	apt-get install bind9 -y
	```

![Klampis2](image/2.PNG)

### 1.2.B Pembuatan Domain
Pada sesilab ini kita akan membuat domain **jarkomtc.com**.

- Lakukan perintah pada *KATSU*. Isikan seperti berikut:

  ```
   nano /etc/bind/named.conf.local
  ```

- Isikan configurasi domain jarkomtc.com sesuai dengan syntax berikut:

  ```
  zone "jarkomtc.com" {
  	type master;
  	file "/etc/bind/jarkom/jarkomtc.com";
  };
  ```

![Klampis3](image/3.PNG)

- Buat folder **jarkom** di dalam **/etc/bind**

  ```
  mkdir /etc/bind/jarkom
  ```


![Klampis4](image/4.PNG)

- Copykan file **db.local** pada path **/etc/bind** ke dalam folder **jarkom** yang baru saja dibuat dan ubah namanya menjadi **jarkomtc.com**

  ```
  cp /etc/bind/db.local /etc/bind/jarkom/jarkomtc.com
  ```

![Klampis5](image/5.PNG)

- Kemudian buka file **jarkomtc.com** dan edit seperti gambar berikut dengan IP *KATSU* masing-masing kelompok:

  ```
  nano /etc/bind/jarkom/jarkomtc.com
  ```

![Klampis6](image/6.PNG)

- Restart bind9 dengan perintah 

  ```
  service bind9 restart
  
  ATAU
  
  named -g //Bisa digunakan untuk restart sekaligus debugging
  ```



### 1.2.C Setting nameserver pada client

Domain yang kita buat tidak akan langsung dikenali oleh client oleh sebab itu kita harus merubah settingan nameserver yang ada pada client kita.

- Pada client *SOTO* dan *KARI* arahkan nameserver menuju IP *KATSU* dengan mengedit file _resolv.conf_ dengan mengetikkan perintah 

	```
	nano /etc/resolv.conf
	```

![Klampis7](image/7.PNG)

- Untuk mencoba koneksi DNS, lakukan ping domain **jarkomtc.com** dengan melakukan  perintah berikut pada client *SOTO* dan *KARI*

  ```
  ping jarkomtc.com
  ```

![Klampis8](image/8.PNG)

### 1.2.D Reverse DNS (Record PTR)
Jika pada pembuatan domain sebelumnya DNS server kita bekerja menerjemahkan string domain **jarkomtc.com** kedalam alamat IP agar dapat dibuka, maka Reverse DNS atau Record PTR digunakan untuk menerjemahkan alamat IP ke alamat domain yang sudah diterjemahkan sebelumnya.

- Edit file **/etc/bind/named.conf.local** pada KLAMPIS

  ```
  nano /etc/bind/named.conf.local
  ```

- Lalu tambahkan konfigurasi berikut ke dalam file **named.conf.local**

  ```
  zone "74.151.10.in-addr.arpa {
      type master;
      file "/etc/bind/jarkom/74.151.10.in-addr.arpa";
  };
  ```

![Klampis9](image/9.PNG)

- Copykan file **db.local** pada path **/etc/bind** ke dalam folder **jarkom** yang baru saja dibuat dan ubah namanya menjadi **74.151.10.in-addr.arpa**

  ```
  cp /etc/bind/db.local /etc/bind/jarkom/74.151.10.in-addr.arpa
  ```

  *Keterangan 74.151.10 adalah 3 byte pertama IP KATSU yang dibalik urutan penulisannya*

![Klampis10](image/10.PNG)

- Edit file **74.151.10.in-addr.arpa** menjadi seperti gambar di bawah ini


![Klampis11](image/11.PNG)

- Kemudian restart bind9 dengan perintah 

  ```
  service bind9 restart
  ```

- Untuk mengecek apakah konfigurasi sudah benar atau belum, lakukan perintah 

  ```
  host -t PTR "IP KATSU"
  ```

![Klampis12](image/12.PNG)



### 1.5 Record CNAME
Record CNAME adalah sebuah record yang membuat alias name dan mengarahkan domain ke alamat/domain yang lain.

Buka file klampis.com pada KLAMPIS dan tambahkan syntax berikut:

![Klampis13](image/13.PNG)

Kemudian restart bind9 dengan perintah **service bind9 restart**

Lalu cek dengan melakukan **host -t CNAME www.klampis.com** atau **ping www.klampis.com** akan mengarah ke host dengan IP KLAMPIS.

![Klampis14](image/14.PNG)


### 1.6 Membuat DNS Slave
DNS Slave adalah DNS cadangan yang akan diakses jika server DNS utama mengalami kegagalan. Lakukan **apt-get update** kemudian install bind9 di PUCANG dengan perintah **apt-get install bind9**

Edit file **/etc/bind/named.conf.local** pada KLAMPIS dan tambahkan syntax berikut:

![Klampis16](image/15.PNG)

Kemudian buka file **/etc/bind/named.conf.local** pada PUCANG dan tambahkan syntax berikut:

![Klampis17](image/16.PNG)

Restart **service bind9 restart**

Apabila terjadi kegagalan pada DNS Server KLAMPIS, maka DNS Server akan dialihkan ke Server PUCANG. Ubah nameserver client yang tersambung dengan KLAMPIS (NGINDEN dan NGAGEL) dengan mengedit file **etc/resolv.conf** menjadi IP PUCANG

![Klampis18](image/17.PNG)

### 1.7 Membuat Subdomain
Subdomain adalah bagian dari sebuah nama domain induk. Subdomain umumnya mengacu ke suatu alamat fisik di sebuah situs contohnya: **klampis.com** merupakan sebuah domain induk. Sedangkan **test.klampis.com** merupakan sebuah subdomain.

Edit file **/etc/bind/klampis/klampis.com** lalu tambahkan subdomain untuk klampis.com yang mengarah ke IP KLAMPIS.

![Klampis19](image/18.PNG)

Restart **service bind9 restart**

Coba ping ke subdomain dengan perintah **ping cloud.klampis.com" atau **host -t A cloud.klampis.com**

![Klampis19](image/19.PNG)


### 1.8 Delegasi Subdomain
Delegasi subdomain adalah pemberian wewenang atas sebuah subdomain kepada DNS baru.

Pada KLAMPIS, edit file **/etc/bind/klampis/klampis.com** dan ubah menjadi seperti di bawah ini sesuai dengan pembagian IP KLAMPIS kelompok masing-masing.

![Klampis20](image/20.PNG)

Kemudian comment **dnssec-validation auto;** dan tambahkan baris berikut pada **/etc/bind/named.conf.options**

![Klampis21](image/21.PNG)

Kemudian edit file **/etc/bind/named.conf.local** menjadi seperti gambar di bawah:

![Klampis22](image/22.PNG)

Setelah itu restart dengan menjalankan **service bind9 restart**

Pada PUCANG, comment **dnssec-validation auto;** dan tambahkan baris berikut pada **/etc/bind/named.conf.options**

![Klampis23](image/23.PNG)

Masuk direktori /etc/bind **cd /etc/bind/** Kemudian edit file **named.conf.local** menjadi seperti gambar di bawah:

![Klampis24](image/24.PNG)

Kemudian buat direktori dengan nama pucang **mkdir pucang** dan copy db.local ke direktori pucang dan edit namanya menjadi pucang.klampis.com **cp db.local pucang/pucang.klampis.com**

![Klampis25](image/25.PNG)

Kemudian pada **/etc/bind/pucang/pucang.klampis.com** ubah dan tambahkan record NS dan A untuk domain **pucang.klampis.com** dan satu lagi record A untuk subdomain www.pucang.klampis.com yang mengarah ke PUCANG (sesuaikan dengan IP masing-masing)

![Klampis25](image/26.PNG)DISCLAIMER

Restart dengan menjalankan **service bind9 restart**

Setelah mendelegasikan zone pucang.klampis.com menuju **PUCANG**, kita dapat mengakses subdomain (daerah.pucang.klampis.com) yang ada pada pucang.klampis.com dengan menggunakan nameserver **KLAMPIS** maupun **PUCANG** dengan cara **ping daerah.pucang.klampis.com** pada client (**NGAGEL** dan **NGINDEN**)

![Klampis26](image/27.PNG)

### 1.9 DNS Forwarder

DNS Forwarder digunakan untuk mengarahkan DNS Server ke IP yang ingin dituju.

Edit file di /etc/bind/named.conf.option
Uncomment pada bagian ini
```
forwarders {
    8.8.8.8;
};
```
Comment pada bagian ini
```
// dnssec-validation auto;
```
Dan tambahkan
```
allow-query{any;};
```

![Klampis30](image/30.PNG)

Harusnya jika nameserver pada /etc/resolv.conf diubah menjadi IP KLAMPIS maka akan diforward ke IP DNS google yaitu 8.8.8.8 dan bisa mendapatkan koneksi.



### 2.1 Keterangan


- #### Penulisan Serial
1. Ditulis dengan format YYYYMMDDXX
```
YYYY adalah tahun
MM adalah bulan
DD adalah tanggal
XX adalah counter
```
Contoh :

![Klampis26](image/28.PNG)

## Latihan
1. Buatlah domain mawho.com dan www.mawho.com (CNAME mawho.com). Apa yang terjadi jika melakukan ping mawho.com dengan ping www.mawho.com? Mengapa hal itu terjadi?
2. Buatlah sebuah subdomain pada domain mawho.com dengan nama abc.mawho.com

## References
* https://computer.howstuffworks.com/dns.htm
* http://knowledgelayer.softlayer.com/faq/what-does-serial-refresh-retry-expire-minimum-and-ttl-mean
* https://en.wikipedia.org/wiki/List_of_DNS_record_types
* https://kb.indowebsite.id/knowledge-base/pengertian-catatan-dns-atau-record-dns/

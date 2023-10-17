# JARKOM-MODUL-2-D18-2023
## Abhinaya Radiansyah Listiyanto  (5025211173)
## Fauzi Rizki Pratama			       (5025211220)

#### 1
> Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian sebagai berikut. Folder topologi dapat diakses pada drive berikut

<img width="1374" alt="image" src="https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114478450/51f438da-c479-4c62-87f8-d2188cabf538">

#### 2

> Buatlah website utama pada node arjuna dengan akses ke arjuna.yyy.com dengan alias www.arjuna.yyy.com dengan yyy merupakan kode kelompok.

````
#!/bin/bash

apt-get update
apt-get install bind9 -y

echo '
zone "arjuna.d18.com" {
        type master;
        file "/etc/bind/jarkom/arjuna.d18.com";
};' > /etc/bind/named.conf.local

mkdir -p /etc/bind/jarkom
cp /etc/bind/db.local /etc/bind/jarkom/arjuna.d18.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     arjuna.d18.com. root.arjuna.d18.com. (
                     2023101001         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      arjuna.d18.com.
@       IN      A       192.200.2.2     ; IP Arjuna
www     IN      CNAME   arjuna.d18.com.
@       IN      AAAA    ::1' > /etc/bind/jarkom/arjuna.d18.com

service bind9 restart

````

#### Penjelasan


1. `apt-get update` dan `apt-get install bind9 -y` adalah perintah untuk mengupdate daftar paket perangkat lunak dan menginstal BIND9. BIND9 adalah server DNS open-source yang digunakan untuk mengelola resolusi nama domain menjadi alamat IP.

2. `echo '...' > /etc/bind/named.conf.local` adalah perintah untuk menambahkan konfigurasi zona ke dalam file `/etc/bind/named.conf.local`. Ini mendefinisikan zona DNS untuk domain "arjuna.d18.com" sebagai zona master dengan menunjuk ke file zona yang ada.

3. `mkdir -p /etc/bind/jarkom` adalah perintah untuk membuat direktori `/etc/bind/jarkom` jika belum ada. Ini adalah tempat di mana file zona DNS untuk domain "arjuna.d18.com" akan disimpan.

4. `cp /etc/bind/db.local /etc/bind/jarkom/arjuna.d18.com` adalah perintah untuk menggandakan file zona DNS bawaan (`/etc/bind/db.local`) ke direktori `/etc/bind/jarkom` dan memberikannya nama `arjuna.d18.com`. File ini akan berisi catatan DNS untuk domain "arjuna.d18.com".

5. `echo '...' > /etc/bind/jarkom/arjuna.d18.com` adalah perintah untuk menambahkan konfigurasi DNS ke dalam file zona DNS "arjuna.d18.com". File ini akan berisi catatan DNS untuk domain "arjuna.d18.com", seperti catatan SOA, NS, A, CNAME, dan AAAA.

6. `service bind9 restart` adalah perintah untuk me-restart layanan BIND9, sehingga konfigurasi baru yang telah ditambahkan akan diterapkan.

Secara keseluruhan, skrip ini digunakan untuk mengkonfigurasi BIND9 agar dapat melayani DNS untuk domain "arjuna.d18.com". File zona DNS akan mengandung catatan DNS yang menentukan bagaimana nama domain "arjuna.d18.com" akan diresolusi menjadi alamat IP. Ini adalah langkah dasar dalam konfigurasi server DNS di sistem Linux.

Hasil pada saat diping di Nacula Client:

<img width="684" alt="image" src="https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114478450/738b85fb-cfee-4e06-909e-cfe83463b3a1">

#### 3
> Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke abimanyu.yyy.com dan alias www.abimanyu.yyy.com.

````
#!/bin/bash

echo '
zone "abimanyu.d18.com" {
        type master;
        file "/etc/bind/jarkom/abimanyu.d18.com";
};' >> /etc/bind/named.conf.local

cp /etc/bind/db.local /etc/bind/jarkom/abimanyu.d18.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.d18.com. root.abimanyu.d18.com. (
                     2023101001         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.d18.com.
@       IN      A       192.200.3.3     ; IP Abimanyu
www     IN      CNAME   abimanyu.d18.com.
@       IN      AAAA    ::1' > /etc/bind/jarkom/abimanyu.d18.com

service bind9 restart

````
#### Penjelasan
Kode yang Anda berikan adalah skrip shell (bash) yang digunakan untuk mengatur layanan DNS (Domain Name System) dengan menggunakan program BIND9 di sistem berbasis Linux. Mari kita bahas langkah-langkahnya:

1. `echo '...' >> /etc/bind/named.conf.local`: Ini adalah perintah untuk menambahkan konfigurasi zona DNS ke dalam file `/etc/bind/named.conf.local`. Konfigurasi ini mendefinisikan zona DNS untuk domain "abimanyu.d18.com" sebagai zona master dan menunjuk ke file zona yang akan digunakan.

2. `cp /etc/bind/db.local /etc/bind/jarkom/abimanyu.d18.com`: Ini adalah perintah untuk menggandakan file zona DNS bawaan (`/etc/bind/db.local`) ke direktori `/etc/bind/jarkom` dan memberikan nama `abimanyu.d18.com`. File ini akan berisi catatan DNS untuk domain "abimanyu.d18.com".

3. Konfigurasi DNS yang ada dalam skrip ini kemudian ditambahkan ke file zona DNS "abimanyu.d18.com" yang baru dibuat di `/etc/bind/jarkom/abimanyu.d18.com`. Konfigurasi DNS tersebut mencakup catatan SOA (Start of Authority), NS (Name Server), A (Alamat IPv4), CNAME (Alias Kanonikal), dan AAAA (Alamat IPv6) yang mendefinisikan bagaimana domain "abimanyu.d18.com" akan diresolusi menjadi alamat IP.

4. `service bind9 restart`: Ini adalah perintah untuk me-restart layanan BIND9, sehingga konfigurasi DNS yang baru telah ditambahkan akan diterapkan. Dengan demikian, server DNS BIND9 akan dapat meresolusi nama domain "abimanyu.d18.com" ke alamat IP yang sesuai sesuai dengan konfigurasi yang telah ditentukan.

Secara keseluruhan, skrip ini digunakan untuk mengkonfigurasi BIND9 agar dapat melayani DNS untuk domain "abimanyu.d18.com". File zona DNS akan berisi catatan DNS yang menentukan bagaimana nama domain ini akan diresolusi menjadi alamat IP. Ini adalah langkah dasar dalam konfigurasi server DNS di sistem Linux.


Hasil pada saat diping di Nacula Client:
<img width="684" alt="image" src="https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114478450/d49a3f03-02b3-43cc-8333-30fdce958a1d">

#### 4 
> Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.yyy.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.

````
#!/bin/bash

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.d18.com. root.abimanyu.d18.com. (
                     2023101001         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.d18.com.
@       IN      A       192.200.3.3      ; IP Abimanyu
www     IN      CNAME   abimanyu.d18.com.
parikesit IN    A       192.200.3.3      ; IP Abimanyu
@       IN      AAAA    ::1
' > /etc/bind/jarkom/abimanyu.d18.com

service bind9 restart
````
Hasil pada saat testing di Nakula Client:
<img width="684" alt="image" src="https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114478450/a5032c0a-bffc-4b35-b6d5-cfdcecae335f">

#### Penjelasan
Kode yang Anda berikan adalah bagian dari konfigurasi zona DNS yang digunakan untuk mengatur resolusi nama domain menjadi alamat IP pada server DNS BIND9 di sistem berbasis Linux. Mari kita bahas konfigurasi ini secara rinci:

1. `$TTL 604800`: Ini adalah Time-to-Live (TTL) untuk catatan DNS di zona ini. TTL mengontrol berapa lama catatan DNS akan di-cache oleh klien DNS sebelum diminta untuk diperbarui. Nilai 604800 detik adalah nilai TTL yang biasanya digunakan untuk zona.

2. `@ IN SOA abimanyu.d18.com. root.abimanyu.d18.com. ( ... )`: Ini adalah catatan Start of Authority (SOA). Ini mengidentifikasi domain (abimanyu.d18.com) dan menyediakan informasi tentang zona DNS, termasuk nomor serial, waktu pembaruan (Refresh), waktu retry (Retry), waktu kadaluwarsa (Expire), dan waktu TTL negatif (Negative Cache TTL).

3. `@ IN NS abimanyu.d18.com.`: Ini adalah catatan Name Server (NS) yang menunjuk pada nama server DNS yang bertanggung jawab untuk zona ini, yaitu "abimanyu.d18.com".

4. `@ IN A 192.200.3.3`: Ini adalah catatan Address (A) yang mengaitkan nama domain "abimanyu.d18.com" dengan alamat IPv4 "192.200.3.3".

5. `www IN CNAME abimanyu.d18.com.`: Ini adalah catatan Canonical Name (CNAME) yang mengonversi nama "www" ke "abimanyu.d18.com". Ini adalah alias, sehingga "www.abimanyu.d18.com" akan meresolusi ke alamat yang sama dengan "abimanyu.d18.com".

6. `parikesit IN A 192.200.3.3`: Ini adalah catatan Address (A) lain yang mengaitkan nama domain "parikesit" dengan alamat IPv4 "192.200.3.3".

7. `@ IN AAAA ::1`: Ini adalah catatan Address (AAAA) yang menetapkan alamat IPv6 "::1" untuk nama domain "abimanyu.d18.com".

Kemudian, konfigurasi zona DNS ini disimpan dalam file `/etc/bind/jarkom/abimanyu.d18.com` yang akan digunakan oleh server DNS BIND9.

Terakhir, perintah `service bind9 restart` digunakan untuk me-restart layanan BIND9 sehingga konfigurasi DNS yang baru telah ditambahkan akan diterapkan. Dengan ini, server DNS BIND9 akan dapat meresolusi nama domain sesuai dengan konfigurasi yang telah ditentukan di dalam zona DNS "abimanyu.d18.com".

#### 5
> Buat juga reverse domain untuk domain utama. (Abimanyu saja yang direverse)

````
#!/bin/bash

echo '
zone "3.200.192.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/3.200.192.in-addr.arpa";
};' >> /etc/bind/named.conf.local

cp /etc/bind/db.local /etc/bind/jarkom/3.200.192.in-addr.arpa

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.d18.com. root.abimanyu.d18.com. (
                     2023101001         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
3.200.192.in-addr.arpa. IN      NS      abimanyu.d18.com.
3                       IN      PTR     abimanyu.d18.com.       ; Byte ke-4 IP Abimanyu' > /etc/bind/jarkom/3.200.192.in-addr.arpa

service bind9 restart

Nakula
#!/bin/bash

echo 'nameserver 192.200.1.4' > /etc/resolv.conf
apt-get update
apt-get install dnsutils

echo 'nameserver 192.200.1.4' > /etc/resolv.conf
host -t PTR 192.200.3.3

````
#### Penjelasan

Kode yang Anda berikan terdiri dari dua skrip shell yang digunakan untuk mengonfigurasi layanan DNS pada server (dalam hal ini menggunakan BIND9) dan menguji resolusi nama domain.

**Skrip Pertama: Mengonfigurasi Server DNS (BIND9)**

```bash
echo '
zone "3.200.192.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/3.200.192.in-addr.arpa";
};' >> /etc/bind/named.conf.local
```

- Skrip ini menambahkan konfigurasi zona DNS terbalik (Reverse DNS) ke file `/etc/bind/named.conf.local`. Konfigurasi ini mendefinisikan zona DNS untuk alamat IP 192.200.3.x yang berkaitan dengan nama domain "abimanyu.d18.com".
- `type master` menunjukkan bahwa server ini adalah zona master untuk zona DNS tersebut.
- File zona DNS akan disimpan di `/etc/bind/jarkom/3.200.192.in-addr.arpa`.

```bash
cp /etc/bind/db.local /etc/bind/jarkom/3.200.192.in-addr.arpa
```

- Ini menggandakan file zona DNS bawaan (`/etc/bind/db.local`) ke direktori `/etc/bind/jarkom` dan memberinya nama `3.200.192.in-addr.arpa`.
- File ini akan digunakan untuk menyimpan catatan DNS terbalik yang mengaitkan alamat IP dengan nama domain.

```bash
echo '
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.d18.com. root.abimanyu.d18.com. (
                     2023101001         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
3.200.192.in-addr.arpa. IN      NS      abimanyu.d18.com.
3                       IN      PTR     abimanyu.d18.com.       ; Byte ke-4 IP Abimanyu' > /etc/bind/jarkom/3.200.192.in-addr.arpa
```

- Ini adalah konfigurasi zona DNS terbalik untuk alamat IP 192.200.3.x. Ini mencakup catatan SOA, NS (Name Server), dan catatan PTR (Pointer) yang mengaitkan alamat IP dengan nama domain.
- File ini kemudian akan digunakan oleh server DNS BIND9 untuk resolusi terbalik (resolusi dari alamat IP ke nama domain).

```bash
service bind9 restart
```

- Ini adalah perintah untuk me-restart layanan BIND9 sehingga konfigurasi DNS yang baru ditambahkan akan diterapkan.

**Skrip Kedua: Pengaturan Resolver dan Pengujian**

```bash
echo 'nameserver 192.200.1.4' > /etc/resolv.conf
```

- Skrip ini mengatur file `/etc/resolv.conf` dengan menambahkan alamat IP server DNS (192.200.1.4) yang akan digunakan sebagai resolver untuk permintaan DNS pada sistem.

```bash
apt-get update
apt-get install dnsutils
```

- Skrip ini melakukan pembaruan paket dan menginstal utilitas DNS pada sistem.

```bash
echo 'nameserver 192.200.1.4' > /etc/resolv.conf
```

- Ini adalah perintah lain yang mengatur file `/etc/resolv.conf` dengan alamat IP server DNS.

```bash
host -t PTR 192.200.3.3
```

- Ini adalah perintah untuk menguji resolusi terbalik (reverse DNS) untuk alamat IP 192.200.3.3. Hasilnya akan menampilkan nama domain yang terkait dengan alamat IP tersebut. 

Hasil dari testing dan bash di Nakula client:
<img width="684" alt="image" src="https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114478450/9dd69ab9-84c2-4cdf-9af2-dd4483697874">



# 6. Membuat DNS slave di Werkudara
1. Membuat script DNS Master di node Yudhistira dengan type master dan transfer file ke IP Werkudara
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/804d9532-2956-48a2-ae32-573d19212dcf)

2. Membuat scriptnya dulu di node Werkudara, dengan memasukkan zone dengan type slave di dalam etc/bind/named.conf.local dan jangan lupa buat direktorinya
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/fb47f4b3-6c7e-4fa8-95e1-fbc09116a3a3)

3. Masuk ke node Nakula untuk testing, masukan dulu nameserver IP Yudhistira (DNS Master) dan IP Werkudara (DNS Slave) didalam etc/resolv.conf
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/000de5a0-b001-4520-9a7b-c51a385afb1d)

4. Pengetesan kita matikan service bind9 dinode Yudhistira
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/029a4370-b6a3-4d35-a368-f1ab84c7cf61)

5. Lakukan Ping di node Nakula
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/56c1e09e-9e77-4b71-8572-2c4a7f29136f)

# 7. Buat domain khusus untuk baratayuda
1. Membuat domain master dulu didalam node Yudhistira dengan nama baratayuda
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/99073a83-76c5-453b-a6a9-babb09cace30)

2. Edit berkas didalam folder baratayuda dan tambahkan CNAME www, dan jangan lupa untuk direstart
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/498e0d66-831a-458b-a7b7-15fbe70f5621)

3. Membuat domain slave didalam Werkudara dan setting IPnya ke IP Yudhistira dan jangan lupa untuk di restart
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/a1de6e63-a001-4a7d-8911-330f367e1dee)

4. Testing di node Nakula kembali
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/a8b68e79-89a9-47e2-b25c-55f041ae4dd5)

# 8. Membuat subdomain rjp didalam baratayuda
1. Edit berkas baratayuda dan tambahkan baris terakhir dengan nama rjp dan diminta menuju ke node abimanyu oleh karena itu masukan IP abimanyu
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/90a04786-5ad8-4960-b523-4b33514c3bb9)

2. Untuk testing kembali ke node Nakula dan ketikan host jika berhasil akan menampilkan kalimat ini
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/82f2e354-9c5d-4b0d-aee1-ec709580523f)

# 9. Membuat Load Balancer Nginx di dalam node Arjuna
1. Membuat domain utama dulu di node Arjuna seperti membuat dns master
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/4c424d04-68a7-4cb0-ba56-f613e4f9d5fe)

2. Edit isi berkas arjuna site dan PTR IP
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/bcf023da-5533-4f4d-a2c9-8bc4f56afbbf)
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/cc0cad9c-9e99-4c12-876b-dc87f153fa72)

3. Membuat nginx worker di 3 node, dan membuat file baru (Prabakusuma, Abimanyu, Wisanggeni)
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/07f4ec2d-8e89-4f96-94e2-e5e1ddd1ccd6)

4. Kemudian buat symlinknya dan jangan lupa untuk direstart
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/9825c52f-6cae-4996-adc8-4e57550bc0da)

5. Membuat Load Balancer di bagian node Arjuna
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/51ec5391-9676-4667-ad2d-47d1157151f8)

6. Dan buat symlink
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/2366d893-5ed5-4855-8025-a8075ff530e5)

7. Testing di node Sadewa
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/b0cb0662-63f1-410e-bbe3-1e0c986a6788)

# 10. Membuat Round Robin dan Mengganti Port
1. Pada pembuatan Round Robin sudah saya gunakan di nomor sebelumnya
2. Step ini sampai akhir akan sama untuk node node lainnya
3. copy terlebih dahulu default.confnya dan edit isi berkasnya denga port yang diinginkan
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/85dbe2dc-2436-4a57-8540-78fd5d9cd60d)

4. Kemudian edit juga berkas port yang berada di folder apache2
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/337e37e1-0f72-447d-a306-9c4b0876b895)

5. dan jangan lupa jika belum ada folder /var/www/…. Maka dibuat terlebih dahulu dan restart nodenya
6. Testing di node Sadewa dengan memasukkan lynx http://IPNode:Port contoh http://192.200.3.2:8001
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/1f5539ac-5f29-469f-b56f-a1dfea3570a8)

# 11. Apache web server pada abimanyu.d18.com
1. membuat directory terlebih dahulu /var/www/abimanyu.d18.com
2. kemudian edit berkasnya 
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/6f56e720-307f-4aa7-bfb6-1c484101158a)

3. aktifkan apache2nya dan restart
4. testing bisa langsung melalui node abimanyu
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/d887ea26-fc4e-4339-b6eb-890ec5b7e2ee)


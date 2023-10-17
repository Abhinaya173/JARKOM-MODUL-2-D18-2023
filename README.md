# JARKOM-MODUL-2-D18-2023
## Abhinaya Radiansyah Listiyanto  (5025211173)
## Fauzi Rizki Pratama			       (5025211220)

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

# 10. Membuad Round Robin dan Mengganti Port
1. Pada pembuatan Round Robin sudah saya gunakan di nomor sebelumnya
2. Step ini sampai akhir akan sama untuk node node lainnya
3. copy terlebih dahulu default.confnya dan edit isi berkasnya denga port yang diinginkan
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/85dbe2dc-2436-4a57-8540-78fd5d9cd60d)

4. Kemudian edit juga berkas port yang berada di folder apache2
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/337e37e1-0f72-447d-a306-9c4b0876b895)

5. dan jangan lupa jika belum ada folder /var/www/…. Maka dibuat terlebih dahulu dan restart nodenya
6. Testing di node Sadewa dengan memasukkan lynx http://IPNode:Port contoh http://192.200.3.2:8001
   ![image](https://github.com/Abhinaya173/JARKOM-MODUL-2-D18-2023/assets/114990549/1f5539ac-5f29-469f-b56f-a1dfea3570a8)

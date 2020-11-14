# Jarkom_Modul2_Lapres_T15

Nama Anggota: 
  - Widyantari Febiyanti 05311840000030
  - Nabella Desyawulansari 05311840000039

## Membuat Topologi Jaringan
1. Membuat ```topologi.sh``` sesuai ketentuan
![no1](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/topologi.png)
2. Mengatur settings **_sysctl_** dengan perintah ```nano /etc/sysctl.conf```. Kemudian hilangkan tanda **(#)** pada bagian ```net.ipv4.ip_forward=1```. 
Gunakan perintah ```sysctl -p``` untuk mengaktifkan perubahan.

 ![no2](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/systcl.png)

3. Mengatur IP untuk setiap UML yang ada dengan perintah ```nano /etc/network/interfaces```

**Surabaya:** 

![no3](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/surabaya%20topo.png)

**Malang:**

![no4](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/malang%20topo.png)

**Sidoarjo:**

![no5](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/sidoarjo%20topo.png)

**Probolinggo:**

![no6](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/probolinggo%20topo.png)

**Mojokerto:**

![no7](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/mojokerto%20topo.png)

**Gresik:**

![no8](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/gresik%20topo.png)

4. Restart network dengan perintah ```service networking restart``` disetiap UML. 
5. Cek dengan perintang ```ipconfig```
6. Lalu jalankan perintah ```iptables –t nat –A POSTROUTING –o eth0 –j MASQUERADE –s 192.168.0.0/16``` pada router **SURABAYA** agar internet terhubung kejaringan luar. 
7. Export ```proxy.sh``` untuk setiap UML.

![no8](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/proxy.png)

8. Update package list dengan perintah ```apt-get update```
9. Install bind9 dengan perintah ```apt-get install bind9 -y```

## Soal 1
Membuat domain ```semerut15.pw```

## Jawaban
1. Konfigurasikan zone pada UML **MALANG** dengan membuka perintah ```nano /etc/bind/named.conf.local```

![no1](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/no%201%20zone.png)

2. Buat folder dengan perintah ```mkdir /etc/bind/jarkom```
3. Meng-copy file db.local dengan perintah ```cp /etc/bind/db.local /etc/bind/jarkom/semerut15.pw```
4. Buka ```nano /etc/bind/jarkom/semerut15.pw``` kemudian edit seperti ini. 

![no2](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/no%201.png)

5. Restart bind9 dengan perintah ```service bind9 restart```
6. Lalu atur pada Nameserver pada client **GRESIK** 

![no3](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/setting%20nameserver%20client.png)

7. Tes ```ping semerut15.pw```

![no4](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/no%201%20hasil.png)

## Soal 2
Membuat domain alias ```www.semerut15.pw```

## Jawaban
1. Tambahkan **CNAME** pada file ```/etc/bind/jarkom/semerut15.pw``` 

![no1](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/no%202.png)

2. Restart bind9 dengan perintah ```service bind9 restart```
3. Tes ```ping www.semerut15.pw``` pada **GRESIK**

![no2](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/no%202%20hasil.png)

## Soal 3
Pembuatan subdomain ```http://penanjakan.semerut15.pw```yang diatur pada **MALANG** dan diarahkan ke IP Server **PROBOLINGGO**

## Jawaban
1. Tambahkan **penanjakan** pada file ```/etc/bind/jarkom/semerut15.pw``` 

![no1](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/no%203.png)

2. Restart bind9 dengan perintah ```service bind9 restart```
3. Tes ```ping penanjakan.semerut15.pw``` pada **GRESIK**

![no2](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/no%203%20hasil.jpg)

## Soal 4
Pembuatan reverse domain

## Jawaban
1. Konfigurasikan zone pada UML **MALANG** dengan membuka perintah ```nano /etc/bind/named.conf.local```

![no1](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/no%204.png)

2. Meng-copy **db.local** ke file **77.151.10.in-addr.arpa** dengan perintah ```cp /etc/bind/db.local /etc/bind/jarkom/77.151.10.in-addr.arpa```
3. Edit file **77.151.10.in-addr.arpa**

![no2](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/no%204_.png)

4. Tes pada **GRESIK** dengan perintah ```host -t PTR 10.151.70.172```

![no3](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/no%204%20hasil.png)

## Soal 5
Pembuatan dns slave ke **MOJOKERTO**

## Jawaban
1. Konfigurasikan zone pada UML **MALANG** dengan membuka perintah ```nano /etc/bind/named.conf.local```

![no1](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/no%201%20zone.png)

2. Restart bind9 dengan perintah ```service bind9 restart```
3. Konfigurasikan zone pada UML **MOJOKERTO** dengan membuka perintah ```nano /etc/bind/named.conf.local```

![no2](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/no%205%20mojo.png)

4. Restart bind9 dengan perintah ```service bind9 restart```
5. Lalu atur pada Nameserver pada client **GRESIK**. Tambahkan **(#)** pada Nameserver **MALANG**

![no3](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/setting%20nameserver%20client.png)

6. Tes ```ping semerut15.pw```

![no4](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/no%205%20hasil.jpg)

## Soal 6
Pembuatan subdomain ```gunung.semeruyyy.pw``` yang didelegasikan pada **MOJOKERTO** dan mengarahkan ke IP **PROBOLINGGO**

## Jawaban
1. Edit file ```/etc/bind/jarkom/kanto.a1.com``` di **MALANG**

![no1](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/6%20malang.png)

2. Edit file ```/etc/bind/named.conf.options``` di **MALANG**. Kemudian tambahkan **allow-query{any;};**

![no2](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/6%20malang%20dns%20forwader.png)

3. Edit file ```/etc/bind/named.conf.local``` di **MALANG*

![no3](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/no%201%20zone.png)

4. Restart bind9 dengan perintah ```service bind9 restart```
5. Edit file ```/etc/bind/named.conf.options``` di **MOJOKERTO**

![no4](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/6%20mojo%20dns%20forwader.png)

6. Edit file ```/etc/bind/named.conf.local``` di **MOJOKERTO**

![no5](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/6%20zone%20mojo.png)

7. Buat direktori delegasi dan copy file **db.local** di **MOJOKERTO**
```
mkdir /etc/bind/delegasi
cp /etc/bind/db.local /etc/bind/delegasi/gunung.semerut15.pw.
```

8. Edit file ```gunung.semerut15.pw.```

![no6](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/6%20mojokerto.JPG)

9. Restart bind9 dengan perintah ```service bind9 restart```
10. Tes ```ping gunung.semerut15.pw```

![no7](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/6%207%20hasil.jpg)

## Soal 7
Membuat subdomain ```naik.gunung.semerut15.pw```

## Jawaban
1. Edit file ```gunung.semerut15.pw.```

![no6](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/6%20mojokerto.JPG)

2. Restart bind9 dengan perintah ```service bind9 restart```
3. Tes ```ping naik.gunung.semerut15.pw```

![no7](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/6%207%20hasil.jpg)

## Membuat Topologi Jaringan
1. Membuat seperti dibawah: 

![no1](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/topologi%20webserver.png)

2. Install **apache2** di **PROBOLINGGO** dengan perintah ```apt-get install apache2```
3. Install **php** di **PROBOLINGGO** dengan perintah ```apt-get install php7.0```

## Soal 8
1. cd menuju ```etc/apache2/sites-available``` dan edit file **000-default.conf**

![no1](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/000-default.png)

2. Buat directory website (mkdir /var/www/semerut15.pw)
3. Pindah ke direktori ```/etc/apache2/sites-available``` dan copy file default ke file **semerut15.pw**
4. Edit file **semerut15.pw**

![no2](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/8%20default%20semerut15.pw.png)

5. Restart **apache** dengan perintah ```service apache2 restart```
6. Aktifkan konfigurasi dengan perintah ```a2ensite semerut15.pw```
7. Download file pendukung dengan **wget 10.151.36.202/semeru.pw.zip** di directory ```/var/www/semerut15.pw```
8. Extract file (.zip)
9. Jalankan di web browser ```semerut15.pw```

![no3](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/semerut15.pw.png)

## Soal 9
Mod rewrite agar **semerut15.p/index.php/home** menjadi **semerut15.pw/home**

## Jawaban
1. Pindah ke directory ```/var/www/semerut15.pw``` dan buat file ```.htaccess``` dengan isi:

![no1](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/9%20.htaccess.png)

2. Buka /etc/apache2/sites-available/semerut15.pw lalu tambahkan:

![no2](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/9.png)

3. Aktifkan module rewrite (a2enmod rewrite)
4. Restart **apache2** dengan perintah ```service apache restart```
5. Jalankan di web browser ```semerut15.pw/home```

![no3](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/9%20semerut15.pw.png)

## Soal 10
Dibuat web dengan domain **http://penanjakan.semerut15.pw** untuk menyimpan file dengan DocumentRoot **/var/www/penanjakan.semerut15.pw**

## Jawaban
1. Buat directory website (mkdir **/var/www/penanjakan.semerut15.pw**)
2. Pindah ke direktori /etc/apache2/sites-available dan copy file default ke file **penanjakan.semerut15.pw**
3. Edit file **penanjakan.semerut15.pw**

![no1](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/10.png)

4. Aktifkan konfigurasi dengan ```a2ensite penanjakan.semerut15.pw```
5. Download file pendukung dengan wget 10.151.36.202/penanjakan.semeru.pw.zip di directory /var/www/penanjakan.semerut15.pw
6. Extract file (**.zip**)
7. Restart **apache** dengan perintah ```service apache2 restart```
8. Jalankan ```penanjakan.semerut15.pw```

![no2](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/10%20penanjakan.semerut15.pw.png)

## Soal 11
Pada folder /public diperbolehkan directory listing tetapi folder didalamnya tidak diperbolehkan

## Jawaban
1. cd ke **/var/www/penanjakan.semerut15.pw** lalu **ls**

![no1](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/11%20ls.png)

2. Untuk setiap sub-folder didalam **folder public** dibuat **file .htaccess** dengan isi:

![no2](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/11%20.htaccess.png)

3. Restart apache dengan perintah ```service apache2 restart```
4. Jalankan dengan perintah ```penanjakan.semerut15.pw/public/css/```

![no3](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/11%20jalan.png)

## Soal 12
Disediakan file **404.html** untuk mengganti error default 404 dari apache

## Dijawab
1. Edit file **/etc/apache2/sites-available/penanjakan.semerut15.pw**

![no1](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/12%20eror.png)

2. Restart apache dengan perintah ```service apache2 restart```
3. Jalankan dengan ```penanjakan.semerut15.pw/haha```

![no2](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/12%20hasil.png)

## Soal 13
Untuk mengakses file assets javascript awalnya harus menggunakan url http://penanjakan.semerut15.pw/public/javascripts. Karena terlalu panjang maka dibuatkan konfigurasi virtual host agar ketika mengakses file assets menjadi http://penanjakan.semerut15.pw/js

## Jawaban

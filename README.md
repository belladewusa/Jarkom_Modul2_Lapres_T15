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
cp /etc/bind/db.local /etc/bind/delegasi/naik.gunung.semerut15.pw.
```

8. Edit file ```naik.gunung.semerut15.pw.```

![no6](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/6%20mojokerto.JPG)

9. Restart bind9 dengan perintah ```service bind9 restart```
10. Tes ```ping naik.gunung.semerut15.pw```

![no7](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/6%207%20hasil.jpg)

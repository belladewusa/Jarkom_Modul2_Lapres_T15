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
6. Lalu jalankan perintah ```iptables –t nat –A POSTROUTING –o eth0 –j MASQUERADE –s 192.168.0.0/16``` pada router SURABAYA agar internet terhubung kejaringan luar. 
7. Export ```proxy.sh``` untuk setiap UML.

![no8](https://github.com/belladewusa/Jarkom_Modul2_Lapres_T15/blob/main/gambar/proxy.png)

8. Update package list dengan perintah ```apt-get update```
9. Install bind9 dengan perintah ```apt-get install bind9 -y```

## Soal 1


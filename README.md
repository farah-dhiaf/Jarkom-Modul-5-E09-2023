# Jarkom-Modul-5-E09-2023

|Nama Anggota |NRP |
|---|---|
|Thoriq Fatihassalam | 5025201254 |
|Farah Dhia Fadhila | 5025211030 |

## Topologi 
<img alt="topologi" width="600" src="https://github.com/farah-dhiaf/Jarkom-Modul-5-E09-2023/assets/91003215/ce32b509-a720-4e1f-9077-a4475b742009"></br>
Keterangan:	</br>
- Richter adalah DNS Server
- Revolte adalah DHCP Server
- Sein dan Stark adalah Web Server
- Jumlah Host pada SchwerMountain adalah 64
- Jumlah Host pada LaubHills adalah 255
- Jumlah Host pada TurkRegion adalah 1022
- Jumlah Host pada GrobeForest adalah 512

## Subnet VLSM
<img alt="subnet" width="600" src="https://github.com/farah-dhiaf/Jarkom-Modul-5-E09-2023/assets/91003215/7fa41d7c-6901-4cf5-a978-a798a43ac806"></br>

## VLSM Tree
<img width="600" alt="tree" src="https://github.com/farah-dhiaf/Jarkom-Modul-5-E09-2023/assets/91003215/13acca5d-a062-4830-9fe5-5eae65e4c271"></br>

Dari tree tersebut, didapatkan pembagian IP sebagai berikut </br>
<img width="600" alt="pembagianIP" src="https://github.com/farah-dhiaf/Jarkom-Modul-5-E09-2023/assets/91003215/b2ecfd16-e76b-435b-a709-6c28626a17ba">

## Konfigurasi Node
### Aura
```
auto eth0
iface eth0 inet dhcp
hwaddress ether a2:ea:72:43:a0:3c

auto eth1
iface eth1 inet static
	address 10.41.1.109
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.41.1.105
	netmask 255.255.255.252

```
### Heiter
```
auto eth0
iface eth0 inet static
	address 10.41.1.106
	netmask 255.255.255.252
	gateway 10.41.1.105

auto eth1
iface eth1 inet static
	address 10.41.8.1
	netmask 255.255.248.0

auto eth2
iface eth2 inet static
	address 10.41.4.1
	netmask 255.255.252.0

```
### Frieren
```
auto eth0
iface eth0 inet static
	address 10.41.1.110
	netmask 255.255.255.252
	gateway 10.41.1.109

auto eth1
iface eth1 inet static
	address 10.41.1.113
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.41.1.117
	netmask 255.255.255.252

```
### Himmel
```
auto eth0
iface eth0 inet static
	address 10.41.1.118
	netmask 255.255.255.252
	gateway 10.41.1.117

auto eth1
iface eth1 inet static
	address 10.41.2.1
	netmask 255.255.254.0

auto eth2
iface eth2 inet static
	address 10.41.1.129
	netmask 255.255.255.128

```
### Fern
```
auto eth0
iface eth0 inet static
	address 10.41.1.131
	netmask 255.255.255.128
	gateway 10.41.1.129

auto eth1
iface eth1 inet static
	address 10.41.1.121
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.41.1.125
	netmask 255.255.255.252
```
### Sein
```
auto eth0
iface eth0 inet static
	address 10.41.4.2
	netmask 255.255.252.0
	gateway 10.41.4.1
```
### Stark
```
auto eth0
iface eth0 inet static
	address 10.41.1.114
	netmask 255.255.255.252
	gateway 10.41.1.113
```
### Richter
```
auto eth0
iface eth0 inet static
	address 10.41.1.122
	netmask 255.255.255.252
	gateway 10.41.1.121
```
### Revolte
```
auto eth0
iface eth0 inet static
	address 10.41.1.126
	netmask 255.255.255.252
	gateway 10.41.1.125
```
### Client 
```
auto eth0
iface eth0 inet dhcp
```
## Routing
### Aura
```
route add -net 10.41.8.0 netmask 255.255.248.0 gw 10.41.1.106
route add -net 10.41.4.0 netmask 255.255.252.0 gw 10.41.1.106
route add -net 10.41.1.112 netmask 255.255.255.252 gw 10.41.1.110
route add -net 10.41.1.116 netmask 255.255.255.252 gw 10.41.1.110
route add -net 10.41.2.0 netmask 255.255.254.0 gw 10.41.1.110
route add -net 10.41.1.128 netmask 255.255.255.128 gw 10.41.1.110
route add -net 10.41.1.120 netmask 255.255.255.252 gw 10.41.1.110
route add -net 10.41.1.124 netmask 255.255.255.252 gw 10.41.1.110
```
### Frieren
```
route add -net 10.41.2.0 netmask 255.255.254.0 gw 10.41.1.118
route add -net 10.41.1.128 netmask 255.255.255.128 gw 10.41.1.118
route add -net 10.41.1.120 netmask 255.255.255.252 gw 10.41.1.118
route add -net 10.41.1.124 netmask 255.255.255.252 gw 10.41.1.118
```
### Himmel
```
route add -net 10.41.1.120 netmask 255.255.255.252 gw 10.41.1.131
route add -net 10.41.1.124 netmask 255.255.255.252 gw 10.41.1.131
```
## Persiapan
Dikarenakan IP Client dibagikan dengan DHCP, oleh karena itu perlu men-setting DHCP. Sebelum itu, untuk menginstall packages yang dibutuhkan, perlu adanya sambungan ke jaringan luar internet. </br>

Setting `IPTABLES` di Aura.
```
iptables -t nat -A POSTROUTING -s 10.41.0.0/20 -o eth0 -j SNAT --to-source 192.168.122.116
```
Lalu masukkan `nameserver 192.168.122.1` pada `/etc/resolv.conf` di setiap node.</br>
<img width="600" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-5-E09-2023/assets/91003215/e91c034a-5d95-43df-a813-963ae54dbdcf"></br>

Setting Richter menjadi DNS server. </br>
```
apt-get update && apt-get install bind9 -y && apt-get install netcat

echo '
options {
        directory "/var/cache/bind";
        forwarders {
                192.168.122.1;
        };
        allow-query{any;};

        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
};' > /etc/bind/named.conf.options

service bind9 restart
```

Setting Revolte menjadi DHCP server.
```
apt-get update && apt-get install isc-dhcp-server -y && apt-get install netcat

echo '
INTERFACES="eth0" 
' > /etc/default/isc-dhcp-server

echo '
ddns-update-style none;
option domain-name "example.org";
option domain-name-servers ns1.example.org, ns2.example.org;
default-lease-time 600;
max-lease-time 7200;
log-facility local7;

#turkregion 
subnet 10.41.8.0 netmask 255.255.248.0 {
    range 10.41.8.2 10.41.15.254;
    option routers 10.41.8.1;
    option broadcast-address 10.41.15.255;
    option domain-name-servers 10.41.1.122;
    default-lease-time 600;
    max-lease-time 7200;
}

#grobeforest
subnet 10.41.4.0 netmask 255.255.252.0 {
    range 10.41.4.2 10.41.7.254;
    option routers 10.41.4.1;
    option broadcast-address 10.41.7.255;
    option domain-name-servers 10.41.1.122;
    default-lease-time 600;
    max-lease-time 7200;
}

#laubhills
subnet 10.41.2.0 netmask 255.255.254.0 {
    range 10.41.2.2 10.41.3.254;
    option routers 10.41.2.1;
    option broadcast-address 10.41.3.255;
    option domain-name-servers 10.41.1.122;
    default-lease-time 600;
    max-lease-time 7200;
}

#schwermountains
subnet 10.41.1.128 netmask 255.255.255.128 {
    range 10.41.1.130 10.41.1.254;
    option routers 10.41.1.129;
    option broadcast-address 10.41.1.255;
    option domain-name-servers 10.41.1.122;
    default-lease-time 600;
    max-lease-time 7200;
}

subnet 10.41.1.104 netmask 255.255.255.252 {}
subnet 10.41.1.108 netmask 255.255.255.252 {}
subnet 10.41.1.112 netmask 255.255.255.252 {}
subnet 10.41.1.116 netmask 255.255.255.252 {}
subnet 10.41.1.120 netmask 255.255.255.252 {}
subnet 10.41.1.124 netmask 255.255.255.252 {}

' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

Setting Heiter, Frieren, dan Himmel menjadi DHCP relay.
```
apt update && apt install isc-dhcp-relay -y && apt-get install netcat

echo '
SERVERS="10.41.1.126"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""
' > /etc/default/isc-dhcp-relay

service isc-dhcp-relay restart
```
Jangan lupa untuk uncomment `net.ipv4.ip_forward=1` pada `/etc/sysctl.conf`</br>

Setting Sein dan Stark menjadi web server.
```
apt-get update && apt-get install apache2 -y && apt-get install netcat -y

cp /var/www/html/index.html
echo '
Listen 80
Listen 443

<IfModule ssl_module>
        Listen 443
</IfModule>

<IfModule mod_gnutls.c>
        Listen 443
</IfModule>' > /etc/apache2/ports.conf

service apache2 start

echo "
$HOSTNAME
" > /var/www/html/index.html
```
Setelah itu semua node perlu menginstall netcat untuk keperluan testing dengan command `apt-get install netcat -y`</br>

Berikut adalah IP client yang telah diberikan DHCP.</br>
<img width="600" alt="turkregion" src="https://github.com/farah-dhiaf/Jarkom-Modul-5-E09-2023/assets/91003215/b2a21ec3-1202-4fc1-8700-b7290352045a"></br>
<img width="600" alt="grobeforest" src="https://github.com/farah-dhiaf/Jarkom-Modul-5-E09-2023/assets/91003215/97cbf281-c596-4ffa-8d61-a2b857e5ac2f"></br>
<img width="600" alt="laubhills" src="https://github.com/farah-dhiaf/Jarkom-Modul-5-E09-2023/assets/91003215/f0420a33-66cd-4634-9fd5-ed0f2416e763"></br>
<img width="600" alt="schwermountain" src="https://github.com/farah-dhiaf/Jarkom-Modul-5-E09-2023/assets/91003215/4b2c8bb8-9788-4853-8a49-459f27ff0cc7"></br>


## Soal 1
>Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.

### Jawaban
Pada node Aura diperlukan setting IPTABLES untuk mengakses keluar tanpa menggunakan MASQUERADE, di sini saya menggunakan `SNAT` sebagai gantinya.
```
iptables -t nat -A POSTROUTING -s 10.41.0.0/20 -o eth0 -j SNAT --to-source 192.168.122.116
```
Dengan to-source mengarah ke IP Aura.

### Output
Melakukan testing dengan ping google.com.</br>
<img width="600" alt="image" src="https://github.com/farah-dhiaf/Jarkom-Modul-5-E09-2023/assets/91003215/e91c034a-5d95-43df-a813-963ae54dbdcf"></br>

## Soal 2
>Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.
### Jawaban
Karena tidak ada keterangan setting IPTABLES di node mana, saya memilih node Revolte untuk setting IPTABLES. Syntax untuk drop semua input dari TCP dan UDP, tetapi tidak untuk TCP dengan port 8080.
```
iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
iptables -A INPUT -p tcp -j DROP
iptables -A INPUT -p udp -j DROP
```
### Output
Melakukan testing dengan netcat dengan command `nc -l -p [PORT]` di receiver dan `nc [IP Receiver] [PORT]` di sender. Dalam kasus ini receiver adalah Revolte dan sender adalah LaubHills. </br>

Berikut port 8080 yang diizinkan, maka kedua node tersebut bisa saling komunikasi.</br>
<img width="600" alt="Screenshot 2023-12-16 050721" src="https://github.com/farah-dhiaf/Jarkom-Modul-5-E09-2023/assets/91003215/ed2160c6-b719-4195-a919-622502752d8b">

Berikut port 80 yang tidak diizinkan, receiver tidak menerima pesan dari sender.</br>
<img width="600" alt="Screenshot 2023-12-16 051022" src="https://github.com/farah-dhiaf/Jarkom-Modul-5-E09-2023/assets/91003215/ab2041d5-4310-4aae-8767-22d2684abeca">

## Soal 3
>Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.
### Jawaban
Setting IPTABLES pada DHCP server dan DNS server sebagai berikut. ICMP merupakan protokol yang digunakan untuk ping dan connlimit di atur menjadi 3, jadi client yang ingin ping ke DHCP server maupun DNS server akan dibatasi maksimal 3.
```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
iptables -I INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
```
### Output
Melakukan testing ping ke DHCP server yaitu Revolte dari empat client. Client keempat yaitu GrobeForest tidak bisa ping karena sudah melewati limit 3 device.</br>
<img width="600" alt="Screenshot 2023-12-16 055450" src="https://github.com/farah-dhiaf/Jarkom-Modul-5-E09-2023/assets/91003215/9872e2a5-8792-4013-b012-99df906624fb"></br>
<img width="600" alt="Screenshot 2023-12-16 055457" src="https://github.com/farah-dhiaf/Jarkom-Modul-5-E09-2023/assets/91003215/0562c120-69d8-406c-8543-756baf0435b0"></br>
<img width="600" alt="Screenshot 2023-12-16 055504" src="https://github.com/farah-dhiaf/Jarkom-Modul-5-E09-2023/assets/91003215/e74e134b-7404-4a50-b49f-9c8cdef853a5"></br>
<img width="600" alt="Screenshot 2023-12-16 055511" src="https://github.com/farah-dhiaf/Jarkom-Modul-5-E09-2023/assets/91003215/6ab6f349-7d68-4a01-8c7e-b6ab16d4971c">

## Soal 4
>Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.
### Jawaban
Setting IPTABLES pada node web server untuk membatasi koneksi SSH hanya dapat dilakukan oleh GrobeForest. Port 22 adalah port yang digunakan oleh koneksi SSH dan dikarenakan IP GrobeForest adalah dinamis diberikan oleh DHCP, sebagai gantinya saya menggunakan range IP dari GrobeForest. Selain itu akan didrop.
```
iptables -A INPUT -p tcp --dport 22 -m iprange --src-range 10.41.4.2-10.41.7.254 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP
```
### Output
## Soal 5
>Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.
### Jawaban
Setting IPTABLES pada node web server untuk membatasi input. Input pada hari Sabtu dan Minggu, serta input pada hari Senin-Jumat pada 00.00-08.00 dan 16.00-23.59 semuanya akan didrop.
```
iptables -A INPUT -m time --weekdays Sat,Sun -j DROP
iptables -A INPUT -m time --weekdays Mon,Tue,Wed,Thu,Fri --timestart 00:00 --timestop 08:00 -j DROP
iptables -A INPUT -m time --weekdays Mon,Tue,Wed,Thu,Fri --timestart 16:00 --timestop 23:59 -j DROP
```
### Output
## Soal 6
>Lalu, karena ternyata terdapat beberapa waktu di mana network administrator dari WebServer tidak bisa stand by, sehingga perlu ditambahkan rule bahwa akses pada hari Senin - Kamis pada jam 12.00 - 13.00 dilarang (istirahat maksi cuy) dan akses di hari Jumat pada jam 11.00 - 13.00 juga dilarang (maklum, Jumatan rek).
### Jawaban
Menambahkan setting IPTABLES pada node web server untuk membatasi input. Input pada hari Senin-Jumat pada 12.00-13.00 dan pada hari Jumat 11.00-13.00 semuanya akan didrop.
```
iptables -A INPUT -m time --weekdays Mon,Tue,Wed,Thu --timestart 12:00 --timestop 13:00 -j DROP
iptables -A INPUT -m time --weekdays Fri --timestart 11:00 --timestop 13:00 -j DROP
```
### Output
## Soal 7
>Karena terdapat 2 WebServer, kalian diminta agar setiap client yang mengakses Sein dengan Port 80 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan dan request dari client yang mengakses Stark dengan port 443 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan.
### Jawaban
Karena tidak ada keterangan setting IPTABLES di node mana, saya memilih node Frieren untuk setting IPTABLES. Untuk setting queue ini diperlukan tambahan konfifurasi dengan menggunakan PREROUTING. Saya mengatur akses yang menuju destinasi port 80 yang mana akses 2 paket pertama didahulukan untuk menuju ke Sein, lalu kemudian 2 paket ke Stark, dan selanjutnya bergantian. Begitu juga untuk port 443 yang akses 2 paket pertama didahulukan menuju Stark, kemudian 2 paket ke Sein, dan selanjutnya bergantian.
```
## untuk sein
iptables -A PREROUTING -t nat -p tcp --dport 80 -d 10.41.1.114 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 10.41.4.2:80
## untuk stark
iptables -A PREROUTING -t nat -p tcp --dport 443 -d 10.41.4.2 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 10.41.1.114:443
```
### Output
## Soal 8
>Karena berbeda koalisi politik, maka subnet dengan masyarakat yang berada pada Revolte dilarang keras mengakses WebServer hingga masa pencoblosan pemilu kepala suku 2024 berakhir. Masa pemilu (hingga pemungutan dan penghitungan suara selesai) kepala suku bersamaan dengan masa pemilu Presiden dan Wakil Presiden Indonesia 2024.
### Jawaban
Setting IPTABLES di node web server untuk filtering terhadap paket yang masuk dimulai pada hari di mana saya melakukan setting hingga berakhirnya masa pemilu 2024. Paket-paket tersebut akan didrop hingga berakhirnya masa pemilu 2024.
```
iptables -A INPUT -p tcp --dport 80 -s 10.41.1.124/30 -m time --datestart 2023-12-16 --datestop 2024-03-20 -j DROP
```
### Output
## Soal 9
>Sadar akan adanya potensial saling serang antar kubu politik, maka WebServer harus dapat secara otomatis memblokir alamat IP yang melakukan scanning port dalam jumlah banyak (maksimal 20 scan port) di dalam selang waktu 10 menit. 
(clue: test dengan nmap)
### Jawaban
Pada kasus ini diperlukan chain bernama PORTSCAN karena akan melakukan scanning port dari sebuah alamat IP. Chain ini akan memfilter input yang menerima scan port sebanyak 20 scan port atau lebih selama 10 menit (600 detik) dan akan didrop. Chain ini juga akan memfilter paket yang lewat (forward).
```
iptables -N PORTSCAN
iptables -A INPUT -m recent --name PORTSCAN --update --seconds 600 --hitcount 20 -j DROP
iptables -A FORWARD -m recent --name PORTSCAN --update --seconds 600 --hitcount 20 -j DROP
iptables -A INPUT -m recent --name PORTSCAN --set -j ACCEPT
iptables -A FORWARD -m recent --name PORTSCAN --set -j ACCEPT
```
### Output
Melakukan testing dengan command `nmap -p 1-100 10.41.4.2` yang mana akan melakukan scan terhadap port 1 sampai port 100 untuk Sein. Setelah terdeteksi scan lebih dari 20, maka ping ke alamat IP tersebut akan terblokir atau tidak bisa akses ke alamat IP tersebut (diblokir).</br> 
<img width="600" alt="Screenshot 2023-12-16 083406" src="https://github.com/farah-dhiaf/Jarkom-Modul-5-E09-2023/assets/91003215/758adbe7-55f7-4d94-94a4-f245865c6a45">

## Soal 10
>Karena kepala suku ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level. 
### Jawaban
Setelah men-setting chain IPTABLES, pada soal ini akan melakukan logging terhadap paket-paket dari alamat IP yang didrop. 
```
iptables -N PORTSCAN
iptables -A INPUT -m recent --name PORTSCAN --update --seconds 600 --hitcount 20 -j LOG --log-prefix "IPTables-Dropped: " --log-level 6
iptables -A INPUT -m recent --name PORTSCAN --update --seconds 600 --hitcount 20 -j DROP
iptables -A FORWARD -m recent --name PORTSCAN --update --seconds 600 --hitcount 20 -j LOG --log-prefix "IPTables-Dropped: " --log-level 6
iptables -A FORWARD -m recent --name PORTSCAN --update --seconds 600 --hitcount 20 -j DROP
iptables -A INPUT -m recent --name PORTSCAN --set -j ACCEPT
iptables -A FORWARD -m recent --name PORTSCAN --set -j ACCEPT
service rsyslog restart
```
### Output
Melakukan testing dengan `IPTABLES -L` untuk melihat logging.



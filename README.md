# Jarkom-Modul-5-B03-2022

## Anggota Kelompok:

| Nama                           | NRP        |
| ------------------------------ | ---------- |
| Maheswara Danendra Satriananda | 5025201060 |
| James Silaban                  | 5025201169 |
| Anak Agung Yatestha Parwata    | 5025201234 |

### A. Tugas pertama kalian yaitu membuat topologi jaringan sesuai dengan rancangan yang diberikan Loid

![image](https://user-images.githubusercontent.com/78299006/206942129-560ee3f4-6d3d-4186-99b3-c15ccb15a051.png)

### B. Untuk menjaga perdamaian dunia, Loid ingin meminta kalian untuk membuat topologi tersebut menggunakan teknik CIDR atau VLSM setelah melakukan subnetting.

Pada praktikum ini, teknik yang digunakan adalah VLSM. Sebelum melakukan pembagian IP ke setiap node pada topologi, Pertama-tama, dilakukan pembagian subnet pada topologi, sehingga akan didapatkan 8 subnet

![image](https://user-images.githubusercontent.com/78299006/206942356-cca01508-7613-44cd-92fa-568ca782e269.png)

Kemudian dilakukan pencarian Netmask induk yang dapat menampung total IP yang dibutuhkan

| Subnet | Jumlah IP | Netmask |
| --- | --- | --- |
| A1  | 3 | /29 |
| A2 | 2 | /30 |
| A3 | 63 | /25 |
| A4 | 2 | /30 |
| A5 | 701 | /23 |
| A6 | 256 | /23 |
| A7 | 201 | /24 |
| A8 | 3 | /29 |
| **Total** | **1231** | **/21** |

Kemudian, setelah didapatkan Netmask induknya, lalu lakukan pembagian IP sesuai dengan netmask yang dibutuhkan

![image](https://user-images.githubusercontent.com/78299006/206942951-e8916dd3-76e0-45dd-b3b1-b224e736a7eb.png)

Untuk memudahkan pengerjakan, NID, Netmask, serta Broadcast ID setiap subnet dituliskan ke dalam bentuk tabel

![image](https://user-images.githubusercontent.com/78299006/206943193-8df3fd06-8802-406e-9c07-5cc54962f460.png)

Setelah itu, lakukan pengisian IP pada setiap node yang ada pada GNS3 sesuai dengan pembagian IP yang didapatkan. Pembagian IP setiap node dapat dilihat pada berikut ini:

Strix
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.174.0.1
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 192.174.0.5
	netmask 255.255.255.252
```

Westalis
```
auto eth0
iface eth0 inet static
	address 192.174.0.2
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 192.174.0.9
	netmask 255.255.255.248

auto eth2
iface eth2 inet static
	address 192.174.0.129
	netmask 255.255.255.128

auto eth3
iface eth3 inet static
	address 192.174.2.1
	netmask 255.255.254.0
```

Eden
```
auto eth0
iface eth0 inet static
	address 192.174.0.10
	netmask 255.255.255.248
	gateway 192.174.0.9
```

WISE
```
auto eth0
iface eth0 inet static
	address 192.174.0.11
	netmask 255.255.255.248
	gateway 192.174.0.9
```

Forger
```

auto eth0
iface eth0 inet static
        address 192.174.0.130
        netmask 255.255.255.128
        gateway 192.174.0.129
```

Desmond
```
auto eth0
iface eth0 inet static
        address 192.174.2.2
        netmask 255.255.254.0
       gateway 192.174.2.1
```

Ostania
```
auto eth0
iface eth0 inet static
	address 192.174.0.6
	netmask 255.255.255.252

auto eth1
iface eth1 inet static
	address 192.174.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.174.4.1
	netmask 255.255.254.0

auto eth3
iface eth3 inet static
	address 192.174.0.17
	netmask 255.255.255.248
```

Blackbell
```
auto eth0
iface eth0 inet static
        address 192.174.4.2
        netmask 255.255.254.0
        gateway 192.174.4.1
```

Briar
```
auto eth0
iface eth0 inet static
        address 192.174.1.2
        netmask 255.255.255.0
        gateway 192.174.1.1
```

Garden
```
auto eth0
iface eth0 inet static
	address 192.174.0.18
	netmask 255.255.255.248
	gateway 192.174.0.17
```

SSS
```
auto eth0
iface eth0 inet static
	address 192.174.0.19
	netmask 255.255.255.248
	gateway 192.174.0.17
```

### C. Anya, putri pertama Loid, juga berpesan kepada anda agar melakukan Routing agar setiap perangkat pada jaringan tersebut dapat terhubung.

Agar setiap perangkat pada jaringan tersebut dapat terhubung, dilakukan routing pada setiap router

Strix
```
### Bawah
route add -net 192.174.0.8 netmask 255.255.255.248 gw 192.174.0.2
#NID A1 (Switch1)

route add -net 192.174.0.128 netmask 255.255.255.128 gw 192.174.0.2
#NID A3 (Forger)

route add -net 192.174.2.0 netmask 255.255.254.0 gw 192.174.0.2
#NID A5 (Desmond)



### Ostania
route add -net 192.174.4.0 netmask 255.255.254.0 gw 192.174.0.6
#NID A6 (Blackbell)

route add -net 192.174.1.0 netmask 255.255.255.0 gw 192.174.0.6
#NID A7 (Briar)

route add -net 192.174.0.16 netmask 255.255.255.248 gw 192.174.0.6
#NID A8 (Switch2)
```

Westalis

```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.174.0.1
```

Ostania

```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.174.0.5
```

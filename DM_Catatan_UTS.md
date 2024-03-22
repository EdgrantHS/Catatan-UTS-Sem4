# **Desain Manajemen Jaringan**

Link kelas: `https://lms.netacad.com/course/view.php?id=2210235`

# Week 1

## Review

### RIP (konvergensi lama)

- berdasarkan hop count (tidak peduli bandwidth)

## OSPF (Link State - saling menukar informasion)

### 5 tipe paket

- Hello (establish neighbor)
  - header
  - packet body
- Database Description (sending link state database)
- Link State Request (request for more information)
- Link State Update (response to request)
- Link State Acknowledgement

### paket yang ditukar membuat OSPF Database

- Adjacency database - Neighbor Table `show ip ospf neighbor`
- Link State Database (LSDB) - Topology Table (ALL other router in network) `show ip ospf database`
- Forwarding Database - Routing Table `show ip route`

### Algoritma Dijkstra (Shortest Path First)

### Proses operasi

- Step by step
  - bangun neighbor adjacency
  - tukar pesan link-state advertisement (LSA)
  - bangun database link-state
  - jalankan algorithm Dijkstra
  - cari jalur terpendek
- States
  - Down
  - Init: mengirim hello
  - 2-way: menerima hello
  - Exstart: menentukan DR dan BDR
  - Exchange: tukar database
  - Loading
  - Full

### Area OSPF

- Single Area OSPF
  - semua router dalam satu area (best practice areo 0)
- Multi Area OSPF
  - menggunakan banyak area
  - banyak pengelompokan router
  - semua area terhubung dengan area 0

### OSPVv3 (IPv6)

### Router Id

- 32 bit
- 32 bit IP address
- 32 bit loopback address
- 32 bit manually configured
- 32 bit highest active IP address

### wildcard-mask

- inversenya subnet mask
- contoh: /30 = 255.255.255.252 (wildcard-mask = 255-252 = 3)

### Setup single area

```cisco
conf t
network 10.10.1.1 0.0.0.0 area 0
  network network-address wildcard-mask area area-id
// Cara lain
int fa0/0
ip ospf 10 area 0
// default static route
ip route 0.0.0.0 0.0.0.0 loopback0
router ospf 10
default-information originate //bingung gw
```

### Pasive interface

- interface yang tidak mengirimkan hello
- port ke end device

### Cost

- default cost = 1
- cost = 100Mbps / bandwidth

# Week 3

## Review ospf

- area 0 = backbone
- abr (area border router) = router yang terhubung dengan area 0 dan area lain
- multiarea = area 0 + area lain, seluruh area terhubung dengan area 0

## EIGRP

- Cisco Proprietary
- Dual (Diffusing Update Algorithm)
- parsial update

## EIGRP Protocol-Dependent Module (PDM)

- Neighbor Table
  - next hop router intervace
- Topology Table
  - best path (successor)
  - Alternate path (feasible successor)
- Routing Table

## RTP (Reliable Transport Protocol)

- PDM di aplication layer, isinya neighbor, topology, dan routing table
- RTP di transport layer, mengirimkan pesan

## Hello Packet

- hello: 5 detik
- multicast di v4 dan v6

## Autonomous System

- kalau dalam 1 organisasi yang sama, bisa as yang sama
- as itu 1 organisasi yang ngatur

```cisco
router eigrp autonomous-system
```

## Command

```cisco
router eigrp 1
router eigrp autonomous-system
eigrp router-id ipv4-address
network [ip addr]
passive-interface [interface-type] [interface-number]
show ip protocols
```

# Week 4 (cyber security)

## Security Terms

- Assets:
- Vulnerability:
- threat:
- exploit:
- mitigation:
- risks:

## Threat actor

- white hat
- black hat
- grey hat

## Security tools

- password cracker
- wireless hacking
- network scanning tools, nmap
- packet crafting
- packet sniffer, wireshark
- rootkit detector
- foreinsic tools

## Attack types

- eavedropping
- data modif
- ip spoofing
- password based attack
- DOS
  - syn flood attack
  - ARP Poisoning
  - DNS attack
  - DHCP Attack
- social enginerring attack
- buffer overflow

## Malware

### Virus

- replikasi dipakai dengan user action, biasa menempel pada program laink

### Trojan horse

- aplikasi palsu

### Worm

- self replicating tanpa user action dan pakai network utk cari host lain

## Security

- VPN
- ASA Firewall (Adaptive Security Appliance)
- IDS/IDP (instrusion detection system/prevention)
- Cryptography (data confidentiality, data integrity, authentication)
  - symmetric key
  - asymmetric key
    - Diffie-Hellman

# week 5 (acl nat)

## purpose

- kontrol akses
- sequensial ceknya jadi penting urutannya
- implementasi di router
- security dengan filter network

## packet filtering

- filter berdasarkan layer 3 dan 4
- source and destination address
- source and destination port

## tipe

- standard (hanya filter layer 3)
  - source address
  - number 1-99, 1300-1999
  - **taro di deket di tujuan**
- extended (melihat layer 3 dan 4)
  - source and destination address
  - source and destination port
  - protocol
  - port
  - number 100-199, 2000-2699
  - **taro di deket di sumber**

## konfigurasi

```cisco
ip access-list extended ftp-filter
  permit tcp 192.168.1.0 0.0.0.255 any eq ftp
  permit tcp 192.168.1.0 0.0.0.255 any eq ftp-data
```

- belum diimplementasi, inbound dan outbound belum diatur
- implementasi di interface

### inbound

- setup di interface saat masuk router
- lebih efisien karena paket sudah di drop sebelum masuk router

### outbound

- setup di interface keluar dari router

### wildcard mask

- keyword
  - host: wildcard mask 0.0.0.0
  - any: wildcard mask 255.255.255.255

### aturan implementasi

setiap interface hanya boleh:  

- 1 acl inbound ipv4
- 1 acl outbound ipv4
- 1 acl inbound ipv6
- 1 acl outbound ipv6

# Week 6 (Virtual Interface)

- Nomor IP dijadikan interface virtual

## VPN Uses in real

- saat ingin membuat WAN lewat internet, perlu VPN
- VPN bisa diimplementasi di router

## Benefits

- cost effective
- secure
- scalable
- compatible

## Security concern

- Hanya nomor IP yang berubah

## Beda VPN dan NAT

- NAT mengubah nomor ip
- VPN nonmor ip jadi layer 1, jadi interface

## Tipe

- Site to site VPN
  - Ada vpn gateway (router) di setiap networkk
- Remote Access
  - dulu namanya client to site

## SSL VPN

SSL vs IPsec VPN:

- SSL (memastikan koneksi utk orang yang benar, limited encription): lebih mudah, tidak perlu install software
- IPsec (Enkripsi, limited connection identification): lebih secure, lebih kompleks

## Protocol

- GRE (Generic Routing Encapsulation)
  - Paling sering digunakan di kelas
  - encapsulate layer 3
  - bisa lewat internet
  - tidak secure

### Konfigurasi
  
```cisco
interface tunnel0
  ip address [ip] [subnet]
  tunnel source [interface] !seluruh nomor ip pada interface ini akan dijadikan nomor ip tunnel
  tunnel destination [ip] 
  tunnel protection ipsec profile [profile-name] (optional - jika ingin secure) 
```

### Kekurangan GRE

- jika menggunakan virtual switch, tidak bisa lewat
- solution, DMVPN (Dynamic Multipoint VPN)

## MPLS (Multi Protocol Label Switching)

## IPsec (Internet Protocol Security)

- confidenciality
- integrity
- authentication: IKE (Internet Key Exchange)
- Diffie-Hellman: key exchange (format identitas)
  - group 1,2,5: Depricatedd
  - group 14: 2048 bit
  - group 24: 2048 bit
  - group 15: 3072 bit
  - group 16: 4096 bit
  - group 19: 256 bit
  - group 20: 384 bit
  - group 21: 521 bit

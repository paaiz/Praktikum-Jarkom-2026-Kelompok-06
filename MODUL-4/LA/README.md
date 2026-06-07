# Modul 4 - Firewall & NAT

## Anggota Kelompok

| Nama                                | NRP        |
| ----------------------------------- | ---------- |
| Roos Habib Faiz Dzaki               | 5024241079 |
| Reidita Eirene Anastasia Katampuge  | 5024241001 |
| Nayaka Shafarrel Razaan Nalaprassya | 5024241057 |

---

# Topologi Jaringan

![Topologi](TUGAS_MODUL/TOPOLOGI.png)

---

# Tabel IP Address

| Perangkat    | Interface | IP Address       | Gateway      |
| ------------ | --------- | ---------------- | ------------ |
| MikroTik ISP | ether1    | DHCP Client      | DHCP         |
| MikroTik ISP | ether2    | 10.10.10.1/30    | -            |
| MikroTik ISP | ether3    | 172.16.100.1/24  | -            |
| FortiGate    | port1     | 10.10.10.2/30    | 10.10.10.1   |
| FortiGate    | port2     | 10.20.20.1/30    | -            |
| FortiGate    | port3     | 192.168.20.1/24  | -            |
| Cisco Router | G0/0      | 10.20.20.2/30    | -            |
| Cisco Router | G0/1      | 192.168.10.1/24  | -            |
| Client LAN   | eth0      | 192.168.10.10/24 | 192.168.10.1 |
| Client WAN   | eth0      | 172.16.100.10/24 | 172.16.100.1 |
| Ubuntu DMZ   | eth0      | 192.168.20.10/24 | 192.168.20.1 |

---

# Konfigurasi MikroTik ISP

## Konfigurasi

- DHCP Client pada ether1
- IP Address:
  - ether2 : 10.10.10.1/30
  - ether3 : 172.16.100.1/24
- NAT Masquerade ke internet
- Route menuju LAN dan DMZ melalui FortiGate

## Dokumentasi

![MikroTik](TUGAS_MODUL/KONFIG_MIKROTIK.png)

---

# Konfigurasi FortiGate

## Konfigurasi

- port1 : WAN
- port2 : LAN
- port3 : DMZ
- Static Route ke LAN
- Default Route ke MikroTik
- Firewall Policy
- VIP Port Forwarding

## Dokumentasi

![FortiGate1](TUGAS_MODUL/KONFIG_FORTIGATE.png)

![FortiGate2](TUGAS_MODUL/KONFIG_FORTIGATE2.png)

![FortiGate3](TUGAS_MODUL/KONFIG_FORTIGATE3.png)

![FortiGate4](TUGAS_MODUL/KONFIG_FORTIGATE4.png)

---

# Konfigurasi Cisco Router

![Cisco](TUGAS_MODUL/KONFIG_CISCO_ROUTER.png)

---

# Konfigurasi Ubuntu Server DMZ

![DMZ](TUGAS_MODUL/KONFIG_DMZ_LINUX.png)

---

# Konfigurasi Client LAN

![LAN](TUGAS_MODUL/KONFIG_LAN_CLIENT.png)

---

# Konfigurasi Client WAN

![WAN](TUGAS_MODUL/KONFIG_WAN_CLIENT.png)

---

# Hasil Pengujian

## Pengujian Client LAN

### Ping ke Cisco Router, FortiGate, dan DMZ

![LAN Test](TUGAS_MODUL/TEST_PING_LAN.png)

### Analisis

Client LAN berhasil berkomunikasi dengan Cisco Router, FortiGate, dan Server DMZ. Hal ini menunjukkan bahwa routing antara jaringan LAN dan DMZ telah berjalan dengan baik.

---

## Pengujian Client WAN

### Ping ke MikroTik dan FortiGate

![WAN Test](TUGAS_MODUL/TEST_PING_WAN.png)

### Analisis

Client WAN berhasil mencapai MikroTik dan FortiGate sehingga konektivitas jaringan luar menuju firewall telah berjalan dengan baik.

---

## Pengujian Firewall

![Firewall Test](TUGAS_MODUL/TEST_WAN_FIREWALL.png)

### Analisis

Client WAN tidak dapat mengakses jaringan LAN maupun IP asli server DMZ. Hal ini menunjukkan bahwa kebijakan firewall pada FortiGate berhasil membatasi akses dari jaringan luar.

---

## Pengujian DMZ ke LAN

![DMZ to LAN](TUGAS_MODUL/TEST_PING_DMZ_TO_LAN.png)

### Analisis

Server DMZ masih dapat berkomunikasi dengan jaringan LAN sesuai dengan aturan routing yang telah dikonfigurasi.

---

## Pengujian Akses Web dari LAN

![Web LAN](TUGAS_MODUL/ACCESS_WEB_LAN.png)

### Analisis

Client LAN berhasil mengakses web server Nginx menggunakan alamat IP DMZ secara langsung.

---

## Pengujian Akses Web dari WAN

![Web WAN](TUGAS_MODUL/ACCESS_WEB_WAN.png)

### Analisis

Client WAN berhasil mengakses web server menggunakan alamat publik FortiGate melalui mekanisme Virtual IP (VIP) dan Destination NAT.

---

# Kesimpulan

Pada praktikum ini berhasil dilakukan implementasi Firewall dan NAT menggunakan FortiGate sebagai perangkat keamanan utama. FortiGate berfungsi sebagai pemisah antara jaringan WAN, LAN, dan DMZ. Routing statis berhasil menghubungkan seluruh segmen jaringan, sedangkan NAT memungkinkan akses dari jaringan internal menuju internet.

Implementasi Virtual IP (VIP) dan Destination NAT memungkinkan web server pada jaringan DMZ diakses dari jaringan WAN tanpa membuka akses langsung ke alamat IP asli server. Hasil pengujian menunjukkan bahwa kebijakan firewall berjalan sesuai kebutuhan, yaitu mengizinkan akses yang diperlukan serta memblokir akses yang tidak diperbolehkan. Dengan demikian, tujuan praktikum mengenai implementasi Firewall, NAT, dan DMZ berhasil tercapai.

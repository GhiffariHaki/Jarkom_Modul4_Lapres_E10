# Jarkom_Modul4_Lapres_E10
- Ardy Wahyu Setiawan           05111840000050
- Mochamad Haikal Ghiffari      05111840000095
## VLSM
1.	Menentukan subnet – subnet yang ada.

![image](https://user-images.githubusercontent.com/57068224/102013802-f2001080-3d84-11eb-9daf-eb1590f9394a.png)

2.	Menghitung jumlah IP dan submask yang dibutuhkan pada setiap subnet, lalu dihitung jumlah seluruh IP yang dibutuhkan beserta length yang dibutuhkan.

![image](https://user-images.githubusercontent.com/57068224/102013864-5622d480-3d85-11eb-8170-13cb735318fe.png)

3.	Membentuk tree VLSM.

![image](https://user-images.githubusercontent.com/57068224/102013875-66d34a80-3d85-11eb-9c1e-1639b9c5be77.png)

4.	Menentukan NID, netmask, dan Broadcast ID setiap subnet.

![image](https://user-images.githubusercontent.com/57068224/102013876-68047780-3d85-11eb-8fd9-e2fbcbe7d741.png)

5.	Setting VLSM

![image](https://user-images.githubusercontent.com/57068224/102013900-866a7300-3d85-11eb-803f-2827ad92b20c.png)

6.	Pada Router mengatur interface yang mengarah ke subnet – subnet yang berada di dekatnya, IPv4 diisi dengan NID + 1

![image](https://user-images.githubusercontent.com/57068224/102013924-a26e1480-3d85-11eb-9145-e5c6c5fccb02.png)
![image](https://user-images.githubusercontent.com/57068224/102013926-a39f4180-3d85-11eb-9f46-e4de8e64f9b4.png)

7.	Pada setiap client mengatur IP Configuration yang diisi minimal dengan NID + 2 dan default gateaway dengan NID + 1.

![image](https://user-images.githubusercontent.com/57068224/102013938-be71b600-3d85-11eb-8d26-0832074ca23b.png)

8.	Melakukan Routing pada setiap router. Setiap router harus diatur defaultnya kecuali router Surabaya.

![image](https://user-images.githubusercontent.com/57068224/102013940-c16ca680-3d85-11eb-84ef-0f382a341ca9.png)

Untuk Routing mengikuti table berikut.

![image](https://user-images.githubusercontent.com/57068224/102013951-d34e4980-3d85-11eb-8413-df9ea8ad011c.png)

9.	Testing dengan ping.

![image](https://user-images.githubusercontent.com/57068224/102013970-fbd64380-3d85-11eb-9b1b-8d121e835415.png)

## CIDR
1. Buat Subnet-Subnetnya.

![image](https://user-images.githubusercontent.com/57068224/102014379-32ad5900-3d88-11eb-9a5a-5cbb26a7d881.png)
![image](https://user-images.githubusercontent.com/57068224/102014403-5a042600-3d88-11eb-938a-84a0695cb0f0.png)
![image](https://user-images.githubusercontent.com/57068224/102014424-6e482300-3d88-11eb-8226-63f216373960.png)
![image](https://user-images.githubusercontent.com/57068224/102014444-8b7cf180-3d88-11eb-9219-82fbdd1a3f95.png)
![image](https://user-images.githubusercontent.com/57068224/102014527-02b28580-3d89-11eb-9a21-4fa420577c21.png)
![image](https://user-images.githubusercontent.com/57068224/102014544-178f1900-3d89-11eb-822f-6e166b7f57b9.png)
![image](https://user-images.githubusercontent.com/57068224/102014601-6046d200-3d89-11eb-80f1-739306126535.png)
![image](https://user-images.githubusercontent.com/57068224/102014632-8bc9bc80-3d89-11eb-92fa-f1a478a21733.png)

2.  Membentuk tree CIDR.

![image](https://user-images.githubusercontent.com/57068224/102014707-f24eda80-3d89-11eb-8ab9-e5761d291811.png)

3.  Modifikasi topologi.sh
```
# Switch

uml_switch -unix switch1 > /dev/null < /dev/null & 
uml_switch -unix switch2 > /dev/null < /dev/null & 
uml_switch -unix switch3 > /dev/null < /dev/null & 
uml_switch -unix switch7 > /dev/null < /dev/null & 
uml_switch -unix switch11 > /dev/null < /dev/null & 
uml_switch -unix switch13 > /dev/null < /dev/null & 
uml_switch -unix switch15 > /dev/null < /dev/null & 
uml_switch -unix switch16 > /dev/null < /dev/null & 
uml_switch -unix switch17 > /dev/null < /dev/null & 
uml_switch -unix switch18 > /dev/null < /dev/null & 
uml_switch -unix switch19 > /dev/null < /dev/null & 
uml_switch -unix switch21 > /dev/null < /dev/null & 
uml_switch -unix switch20 > /dev/null < /dev/null & 
uml_switch -unix switch22 > /dev/null < /dev/null & 
uml_switch -unix switch25 > /dev/null < /dev/null & 


# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.76.25 eth1=daemon,,,switch1 eth2=daemon,,,switch2 eth3=daemon,,,switch7 eth4=daemon,,,switch13 mem=64M &
xterm -T PASURUAN -e linux ubd0=PASURUAN,jarkom umid=PASURUAN eth0=daemon,,,switch2 eth1=daemon,,,switch3 eth2=daemon,,,switch19 mem=64M &
xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch3 eth1=daemon,,,switch15 eth2=daemon,,,switch16 mem=64M &
xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch7 eth1=daemon,,,switch11 eth2=daemon,,,switch21 eth3=daemon,,,switch22 mem=64M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch22 eth1=daemon,,,switch25 mem=64M &
xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch11 eth1=daemon,,,switch17 eth2=daemon,,,switch18 mem=64M &
xterm -T BLITAR -e linux ubd0=BLITAR,jarkom umid=BLITAR eth0=daemon,,,switch17 eth1=daemon,,,switch20 mem=64M &


# Server

xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch18 mem=64M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch13 mem=64M &

# Klien 1
xterm -T SAMPANG -e linux ubd0=SAMPANG,jarkom umid=SAMPANG eth0=daemon,,,switch1 mem=64M &
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch19 mem=64M &
xterm -T BANYUWANGI -e linux ubd0=BANYUWANGI,jarkom umid=BANYUWANGI eth0=daemon,,,switch16 mem=64M &
xterm -T JEMBER -e linux ubd0=JEMBER,jarkom umid=JEMBER eth0=daemon,,,switch16 mem=64M &
xterm -T BONDOWOSO -e linux ubd0=BONDOWOSO,jarkom umid=BONDOWOSO eth0=daemon,,,switch15 mem=64M &
xterm -T JOMBANG -e linux ubd0=JOMBANG,jarkom umid=JOMBANG eth0=daemon,,,switch22 mem=64M &
xterm -T BOJONEGORO -e linux ubd0=BOJONEGORO,jarkom umid=BOJONEGORO eth0=daemon,,,switch25 mem=64M &
xterm -T NGANJUK -e linux ubd0=NGANJUK,jarkom umid=NGANJUK eth0=daemon,,,switch21 mem=64M &
xterm -T LUMAJANG -e linux ubd0=LUMAJANG,jarkom umid=LUMAJANG eth0=daemon,,,switch17 mem=64M &
xterm -T TULUNGAGUNG -e linux ubd0=TULUNGAGUNG,jarkom umid=TULUNGAGUNG eth0=daemon,,,switch20 mem=64M &
```

4.  Modifikasi nano /etc/network/interfaces tiap uml
    
    **Surabaya**
    
    ```
    auto lo
    iface lo inet loopback
    
    #cloud
    auto eth0
    iface eth0 inet static
    address 10.151.70.46
    netmask 255.255.255.252
    gateway 10.151.70.45

    #sampang
    auto eth1
    iface eth1 inet static
    address 192.168.64.1
    netmask 255.255.252.0

    #pasuruan
    auto eth2
    iface eth2 inet static
    address 192.168.192.1
    netmask 255.255.255.252

    #batu
    auto eth3
    iface eth3 inet static
    address 192.168.32.1
    netmask 255.255.255.252

    #mojokerto
    auto eth4
    iface eth4 inet static
    address 10.151.71.89
    netmask 255.255.255.252
    ```

    **Pasuruan**
    ```
    auto lo
    iface lo inet loopback

    #surabaya
    auto eth0
    iface eth0 inet static
    address 192.168.192.2
    netmask 255.255.255.252
    gateway 192.168.192.1

    #probolinggo
    auto eth1
    iface eth1 inet static
    address 192.168.144.1
    netmask 255.255.255.252

    #sidoarjo
    auto eth2
    iface eth2 inet static
    address 192.168.160.1
    netmask 255.255.252.0
    ```
    
    **Probolinggo**
    ```
    auto lo
    iface lo inet loopback

    #pasuruan
    auto eth0
    iface eth0 inet static
    address 192.168.144.2
    netmask 255.255.255.252
    gateway 192.168.144.1

    #bondowoso
    auto eth1
    iface eth1 inet static
    address 192.168.136.1
    netmask 255.255.255.128

    #jember&banyuwangi
    auto eth2
    iface eth2 inet static
    address 192.168.128.1
    netmask 255.255.248.0
    ```
    
    **Bondowoso**
    ```
    auto lo
    iface lo inet loopback

    #probolinggo
    auto eth0
    iface eth0 inet static
    address 192.168.136.2
    netmask 255.255.255.128
    gateway 192.168.136.1
    ```

    **Jember**
    ```
    auto lo
    iface lo inet loopback

    #probolinggo
    auto eth0
    iface eth0 inet static
    address 192.168.128.2
    netmask 255.255.248.0
    gateway 192.168.128.1
    ```

    **Banyuwangi**
    ```
    auto lo
    iface lo inet loopback

    #probolinggo
    auto eth0
    iface eth0 inet static
    address 192.168.128.3
    netmask 255.255.248.0
    gateway 192.168.128.1
    ```

    **Sidoarjo**
    ```
    auto lo
    iface lo inet loopback

    #pasuruan
    auto eth0
    iface eth0 inet static
    address 192.168.160.2
    netmask 255.255.252.0
    gateway 192.168.160.1
    ```

    **Sampang**
    ```
    auto lo
    iface lo inet loopback

    #surabaya
    auto eth0
    iface eth0 inet static
    address 192.168.64.2
    netmask 255.255.252.0
    gateway 192.168.64.1
    ```

    **Batu**
    ```
    auto lo
    iface lo inet loopback

    #surabaya
    auto eth0
    iface eth0 inet static
    address 192.168.32.2
    netmask 255.255.255.252
    gateway 192.168.32.1

    #kediri
    auto eth1
    iface eth1 inet static
    address 192.168.8.1
    netmask 255.255.255.252

    #nganjuk
    auto eth2
    iface eth2 inet static
    address 192.168.20.1
    netmask 255.255.252.0

    #jombang
    auto eth3
    iface eth3 inet static
    address 192.168.18.1
    netmask 255.255.254.0
    ```

    **Nganjuk**
    ```
    auto lo
    iface lo inet loopback

    #batu
    auto eth0
    iface eth0 inet static
    address 192.168.20.2
    netmask 255.255.252.0
    gateway 192.168.20.1
    ```

    **Jombang**
    ```
    auto lo
    iface lo inet loopback

    #batu
    auto eth0
    iface eth0 inet static
    address 192.168.18.2
    netmask 255.255.254.0
    gateway 192.168.18.1
    ```

    **Madiun**
    ```
    auto lo
    iface lo inet loopback

    #bojonegoro
    auto eth0
    iface eth0 inet static
    address 192.168.16.1
    netmask 255.255.255.240

    #batu
    auto eth1
    iface eth1 inet static
    address 192.168.18.3
    netmask 255.255.254.0
    gateway 192.168.18.1
    ```

    **Kediri**
    ```
    auto lo
    iface lo inet loopback

    #batu
    auto eth0
    iface eth0 inet static
    address 192.168.8.2
    netmask 255.255.255.252
    gateway 192.168.8.1

    #lumajang
    auto eth1
    iface eth1 inet static
    address 192.168.4.1
    netmask 255.255.255.0

    #malang
    auto eth2
    iface eth2 inet static
    address 10.151.71.93
    netmask 255.255.255.252
    ```

    **Lumajang**
    ```
    auto lo
    iface lo inet loopback

    #kediri
    auto eth0
    iface eth0 inet static
    address 192.168.4.2
    netmask 255.255.255.0
    gateway 192.168.4.1
    ```

    **Blitar**
    ```
    auto lo
    iface lo inet loopback

    #tulungagung
    auto eth0
    iface eth0 inet static
    address 192.168.0.1
    netmask 255.255.252.0

    #kediri
    auto eth1
    iface eth1 inet static
    address 192.168.4.3
    netmask 255.255.255.0
    gateway 192.168.4.1
    ```

    **Tulungagung**
    ```
    auto lo
    iface lo inet loopback

    #blitar
    auto eth0
    iface eth0 inet static
    address 192.168.0.2
    netmask 255.255.252.0
    gateway 192.168.0.1
    ```

    **Bojonegoro**
    ```
    auto lo
    iface lo inet loopback

    #madiun
    auto eth0
    iface eth0 inet static
    address 192.168.16.2
    netmask 255.255.255.240
    gateway 192.168.16.1
    ```

    **Mojokerto**
    ```
    #surabaya
    auto eth0
    iface eth0 inet static
    address 10.151.71.90
    netmask 255.255.255.252
    gateway 10.151.71.89
    ```

    **Malang**
    ```
    #kediri
    auto eth0
    iface eth0 inet static
    address 10.151.71.94
    netmask 255.255.255.252
    gateway 10.151.71.93
    ```
5.  Tambah routing

**Surabaya**
```
#Pasuruan D1/18
route add -net 192.168.128.0 netmask 255.255.192.0 gw 192.168.192.2
#Batu D2/19
route add -net 192.168.0.0 netmask 255.255.224.0 gw 192.168.32.2
#Malang
route add -net 10.151.71.92 netmask 255.255.255.252 gw 192.168.32.2
```
**Pasuruan**
```
#Probilinggo
route add -net 192.168.128.0 netmask 255.255.240.0 gw 192.168.144.2
```
**Batu**
```
#Kediri
route add -net 192.168.0.0 netmask 255.255.248.0 gw 192.168.8.2
#Malang>>Kediri
route add -net 10.151.71.92 netmask 255.255.255.252 gw 192.168.8.2
#Madiun
route add -net 192.168.16.0 netmask 255.255.252.0 gw 192.168.18.3
```
**Kediri**
```
#Blitar
route add -net 192.168.0.0 netmask 255.255.248.0 gw 192.168.4.
```

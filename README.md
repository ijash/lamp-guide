# Penerapan MySQL Database Server Pada Raspberry Pi

## Pendahuluan

Mengapa menggunakan Raspberry sebagai server daripada menggunakan penyedia layanan khusus web hosting?  
 Pertama, dari sudut pandang ekonomi, Bahwa layanan web hosting tidak gratis dan harus membayar setiap bulan/tahun. Berbeda dengan Raspberry yang hanya perlu koneksi. Selain itu, dengan memilih Raspberry, Pengguna memiliki kemungkinan untuk memodifikasi sesuai kebutuhan sesuai dengan keinginan pengguna (contoh: ukuran disk, hosting Database, dll.), hal tersebut biasanya tidak dapat dilakukan pada web hosting khusus, yang sering dijual bersama domain dengan kapasitas konfigurasi rendah.  
 Namun, untuk mendukung fleksibilitas lebih, Praktikum makalah ini menggunakan Raspberry Pi 3 Model B, dengan kapasitas 1GB RAM, dibandingkan dengan model Raspberry Pi lainnya yang memiliki spesifikasi lebih rendah.

  Pertanyaan yang sekarang muncul adalah, bagaimana cara membuat server web di Raspeberry Pi?


## Persiapan Hardware
*masukan foto2 dan spek*

Berikut ini adalah alat-alat yang perlu dipersiapkan:  
* Raspberry Pi 3 Model
* Micro SD Card (Min. 8Gb)
* Kabel LAN untuk ke router (bisa menggunakan WLAN, tapi tidak disarankan)
* Keyboard USB
* Monitor
* VGA to HDMI Converter (jika Monitor menggunakan VGA)
* Power Supply Raspberry Pi, DC 5V 2.5A
* Micro SD Card Reader
* Laptop atau PC
* Koneksi Internet



## Instalasi OS
*masukan terapan install di sd card*

Sebelum dinyalakan, Raspberry Pi wajib menggunakan OS yang mendukung prosesor jenis ARM. Salah satunya adalah Raspbian, yaitu berupa OS GNU/Linux turunan dari Debian. Untuk membuat server, pilih **Raspbian Stretch Lite** yang disediakan di [situs resmi Raspberry Pi](https://www.raspberrypi.org/downloads/raspbian/).  
Setelah download, file berupa kompresi zip, dan harus diekstrak dari kompresi tersebut hingga berupa satu file *virtual CD* berekstensi "*.iso*".

Lalu, sambungkan SD Card dengan komputer untuk menginstall Raspbian kedalam SD Card. Setelah SD Card terdeteksi, gunakan USB Image writer atau software sejenisnya untuk memindahkan isi dari *virtual CD* Raspbian yang sudah didownload sebelumnya". Untuk pengguna Windows atau Linux bisa menggunakan [Etcher](https://etcher.io/) sebagai alat pemindah *virtual CD* ke SD card. Namun, di OS linux biasanya sudah disediakan *tools* sejenis(*USB Image Writer pada Linux Mint*). Lanjutkan dengan menjalankan pemindahan *virtual CD* kedalam SD Card dan OS Raspbian siap digunakan dengan memindahkan SD Card ke Raspberry Pi.

## Booting dan login
Setelah menginstall OS pada kartu SD Card, dan setelah memulai Raspberry Pi untuk pertama kalinya, Tampilan dimulai dengan CLI (*Command Line Interface*).
Login dengan ID dan Password bawaan dari raspberry yaitu:  
user name `pi`  
password `raspberry`  
Sehingga pengguna bisa masuk ke dalam shell Debian linux pada raspberry pi.

## Pengaturan SSH
Setalah masuk ke dalam shell, pengguna sebaiknya mengatur pengaturan raspberry agar bisa di akses melalui terminal dari komputer lain. Tehnik ini biasa disebut *remote login* atau SSH (*Secure Shell*).  
Untuk mengaktifkannya, SSH server pada Raspberry Pi perlu diaktifkan. Untuk mengaktifkannya, ketikkan perintah dibawah ini:  
`sudo raspi-config`  
sehingga tampilan akan muncul ke tampilan menu **Raspberry Pi Software Configuration Tool **.  
Pada menu pilihan **raspi-config**, masuk ke **Interfacing Options**, lalu pilih **SSH**.


![alt text](images/raspi-config.png "Raspberry Pi Software Configuration Tool")  
![alt text](images/interface-opt.png "Interfacing Option")

lalu pilih `yes` untuk mengaktifkan SSH server pada Raspberry Pi.
![alt text](images/ssh.png "SSH")  

Selain mengaktifkan SSH server, menu ini bisa juga untuk mengubah password bawaan menjadi pasword yang dikehendaki.

## Remote Login menggunakan ssh
Setelah Network dan SSH diatur dengan benar, maka pengguna bisa mengontrol Raspberry Pi dari perangkat atau komputer lain, sehingga tidak perlu memasang monitor dan keyboard pada Raspberry Pi. Cukup menghidupkan dan memasang kabel LAN, dan Raspberry bisa digunakan melalui SSH.</br>
pada OS Windows, pengguna dapat menggunakan SSH dengan software [Putty](https://www.putty.org/) atau software SSH client lainnya. Namun, pada panduan kali ini, penulis menggunakan OS *Linux Mint* sebagai *remote-client* untuk SSH terhadap Raspberry Pi.

## Apache Web server
setelah memegang alih Raspberry Pi dengan SSH, pengguna dapat menggunakan shell untuk keperluan instalasi Apache dengan mengetikkan:
```
sudo apt update
sudo apt upgrade
sudo apt install apache2
```
lalu sebagai tambahan, pengguna bisa mengatur hak akses pada folder `/var/www/html` agar memudahkan pengguna dalam mengatur website nantinya. Maka, ketikan:
```
sudo chown -R pi:www-data /var/www/html/
sudo chmod -R 770 /var/www/html/
```
Setelah instalasi selesai, kita dapat menguji apakah Apache berfungsi dengan benar dengan membuka alamat Raspberry.
Untuk melakukan ini, Anda perlu mencoba mengakses Raspberry dari port `80`. Caranya cukup mudah, yaitu dengan membuka browser web anda, dan masuk ke alamat IP LAN raspberry anda. Anda kemudian harus mendapatkan halaman dengan pesan seperti `It Works!` Dan banyak teks lainnya.

Jika Anda belum memiliki GUI di Raspbian Anda, atau Anda menggunakan SSH untuk terhubung ke Raspberry Anda, Anda dapat menggunakan perintah berikut:
```
wget -O check_apache.html [alamat IP Raspberry]

```
Perintah ini akan menyimpan kode HTML dari halaman dalam file "check_apache.html" di direktori saat ini.
Jadi Anda hanya perlu membaca file tersebut dengan perintah:
```
cat ./check_apache.html
```
Jika Anda melihat `It Works!` di dalam kode  berarti Apache telah bekerja dengan semestinya.

Apache menggunakan direktori `/var/www/html` sebagai root untuk situs Anda. Ini berarti bahwa ketika Anda memanggil Raspberry Anda di port 80 (http), Apache mencari file di `/var/www/html`.
Misalnya, jika Anda memanggil alamat `http://[alamat Raspberry]/contoh`, Apache akan mencari file "contoh" di direktori `/var/www/html`.

Untuk menambahkan file baru, situs, dll., Anda perlu menambahkannya ke direktori ini.

Anda sekarang dapat menggunakan Raspberry Anda untuk membuat situs dalam HTML, CSS, dan JavaScript, secara internal. Namun dalam kasus kali ini, pengguna membutuhkan apache sebagai alat untuk menjalankan PHPmyAdmin yang dimana sebagai alat untuk membantu mengolah Database MySQL.

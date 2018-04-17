# Penerapan MySQL Database Server Pada Raspberry Pi

## Pendahuluan

Mengapa menggunakan Raspberry sebagai server daripada menggunakan penyedia layanan khusus web hosting?  
 Pertama, dari sudut pandang ekonomi, Bahwa layanan web hosting tidak gratis dan harus membayar setiap bulan/tahun. Berbeda dengan Raspberry yang hanya perlu koneksi. Selain itu, dengan memilih Raspberry, Pengguna memiliki kemungkinan untuk memodifikasi sesuai kebutuhan sesuai dengan keinginan pengguna (contoh: ukuran disk, hosting Database, dll.), hal tersebut biasanya tidak dapat dilakukan pada web hosting khusus, yang sering dijual bersama domain dengan kapasitas konfigurasi rendah.  
 Namun, untuk mendukung fleksibilitas lebih, Praktikum makalah ini menggunakan Raspberry Pi 3 Model B, dengan kapasitas 1GB RAM, dibandingkan dengan model Raspberry Pi lainnya yang memiliki spesifikasi lebih rendah.

  Pertanyaan yang sekarang muncul adalah, bagaimana cara membuat server web di Raspeberry Pi?


## PHP

Pertama-tama, Pengguna harus tahu bahwa PHP adalah bahasa pemrograman yang ditafsirkan (_interpreted language_). Dan seperti dalam kasus server, akronim PHP dapat memiliki beberapa arti. Ketika berbicara tentang PHP, berarti berbicara tentang bahasa atau penerjemah(_interpreter_).
Di sini, ketika berbicara tentang menginstal PHP, itu berarti akan menginstal _interpreter_, untuk menggunakan bahasa PHP.

PHP (bahasa) biasanya digunakan untuk membuat situs dinamis, artinya bahwa pengguna mengirimkan informasi ke server yang mengembalikan hasil yang dimodifikasi sesuai dengan informasi yang diberikan. Sebaliknya, situs statis tidak menyesuaikan dengan informasi yang diberikan oleh pengguna.

PHP itu gratis, dan dikelola oleh Yayasan PHP, serta Zend Enterprise, dan berbagai perusahaan lain (perlu dicatat bahwa Zend juga penulis _zend framework_ yang terkenal, banyak digunakan dan diakui dalam dunia "bisnis") .

Ini adalah salah satu bahasa pemrograman yang paling banyak digunakan, dan bahkan yang paling banyak digunakan untuk pemrograman web, dengan sekitar 79% pangsa pasar.

Sekali lagi, semua keterampilan yang dapat diperoleh, pada bahasa, atau pada instalasi dan konfigurasi interpreter, akan selalu berguna. Jadi kami hanya dapat menyarankan Anda untuk belajar PHP, yang benar-benar bahasa yang indah dan terlalu sering diremehkan.


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
wget -O check_apache.html http://127.0.0.1

```
Perintah ini akan menyimpan kode HTML dari halaman dalam file "check_apache.html" di direktori saat ini.
Jadi Anda hanya perlu membaca file tersebut dengan perintah:
```
cat ./check_apache.html
```
Jika Anda melihat `It Works!` di dalam kode  berarti Apache telah bekerja dengan semestinya.

Apache menggunakan direktori `/var/www/html` sebagai root untuk situs. Ini berarti bahwa ketika Anda memanggil Raspberry Anda di port 80 (http), Apache mencari file di `/var/www/html`.
Misalnya anda menggunakan IP `192.168.0.11` sebagai alamat Raspberry, jika pengguna memanggil alamat `http://192.168.0.11/contoh` pada browser, Apache akan mencari file "contoh" di direktori `/var/www/html`.

Untuk menambahkan file baru, situs, dll.,pengguna perlu menambahkannya ke direktori ini.

Pengguna sekarang dapat menggunakan Raspberry untuk membuat situs dalam HTML, CSS, dan JavaScript, secara internal. Namun dalam kasus kali ini, pengguna membutuhkan apache sebagai alat untuk menjalankan PHPmyAdmin yang dimana sebagai alat untuk membantu mengolah Database MySQL.

## Instalasi PHP

Lanjutkan dengan mengetikan:
```
sudo apt install php php-mbstring
```
lalu cek apakah php telah jalan.

Anda akan terlebih dahulu menghapus file `index.html` di direktori `/var/www/html`.
Kemudian buat file "index.php" di direktori ini, dengan baris perintah ini
```
echo "<?php phpinfo ();?>" > /var/www/html/index.php
```

Dari sini, lakukan hal sama dengan pemeriksaan Apache. Pastikan hasil browser mendekati gambar ini:  
![alt text](images/phpinfo.jpg "PHP Info")  

jika tidak memiliki antarmuka (_GUI_), gunakan metode SSH yang sama seperti sebelumnya, dan cari kata-kata `PHP Version`

## Database MySQL untuk server

Setelah mengatur PHP, pengguna perlu menyimpan informasi agar dapat digunakan di situs terkait. Untuk hal ini, databaselah yang paling sering digunakan. Oleh karena itu diperlukanlah DBMS (Database Management System), yaitu MySQL.

MySQL adalah DBMS yang gratis, kuat, dan digunakan secara besar-besaran (sekitar 56% pangsa pasar DBMS gratis). Di sini sekali lagi, MySQL sangat penting untuk pengembangan, apa pun bahasanya, bahwa pengguna harus benar-benar belajar dan menguasainya.

Untuk menerapkannya, pengguna memerlukan `mysql-server` dan `php-mysql` (yang akan berfungsi sebagai penghubung antara php dan mysql). Ketikan perintah:  
```
sudo apt install mysql-server php-mysql
```
lalu pastikan mysql telah jalan.
```
sudo mysql --user=root
```
dan pengguna akan pindah ke konsol `MariaDB`.
Disini, user _root_ bawaan mysql tidak dihapus dan membuat _root_ mysql yang baru dengan hak akses berbeda karena, default _root_ hanya dapat digunakan dengan akun _root_ Linux, sehingga tidak tersedia untuk skrip webserver dan PHP.

Untuk melakukannya, setelah terhubung ke MySQL, jalankan saja perintah (ganti kata sandi dengan kata sandi yang diinginkan):

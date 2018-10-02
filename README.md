# Penerapan MySQL Database Server Pada Raspberry Pi
![logo](images/pi_logo.png "Raspberry Pi")  
## Pendahuluan

Jika melihat dari sudut pandang ekonomi, layanan web hosting tidak gratis dan harus membayar setiap bulan/tahun. Berbeda dengan Raspberry yang hanya perlu koneksi serta daya listrik yang rendah. Selain itu, dengan memilih Raspberry, pengguna memiliki kemungkinan untuk memodifikasi sesuai kebutuhan yang di inginkan (ukuran disk, hosting Database, dll.), hal tersebut biasanya tidak dapat dilakukan pada web hosting umumnya.

 Untuk mendukung fleksibilitas lebih, Praktikum ini menggunakan Raspberry Pi 3 Model B, dengan kapasitas 1GB RAM, dibandingkan dengan model Raspberry Pi lainnya yang memiliki spesifikasi lebih rendah. Dan untuk kumpulan software yang akan di install, biasa disebut _LAMP stack_ yang berarti _Linux Apache MySQL PHP_.
## Latar belakang
Semakin berkembangnya teknologi hingga sekarang, kebutuhan akan daya listrikpun semakin sedikit. Hal tersebut disebabkan oleh semakin teknologi yang semakin efisien. Dalam kasus penerapan server, konsumsi daya listrikpun menjadi salah satu pertimbangan. Saat ini, telah dikembangkan mikroprosesor yang hemat daya yang banyak digunakan di perangkat seluler dengan sebutan  RISC(_reduced instruction set computer_).
Raspberry pi merupakan komputer kecil dan hemat daya dengan prosesor RISC yang menggunakan arsitektur _CPU ARM_. Karena kemampuannya yang sama dengan komputer _Desktop_, Raspberry Pi dapat juga digunakan untuk penerapan server, sehingga daya konsumsi listrik yang sebelumnya bisa mencapai ratusan _watt_ dapat dipotong menjadi kurang dari 15 _watt_. Meninjau semakin banyaknya kebutuhan akan database pada usaha kecil maupun pribadi, Raspberry Pi merupakan pilihan tepat .

## Rumusan Masalah
Adapun rumusan masalah pada kasus ini adalah:
1. Bagaimana _LAMP Stack_ dijalankan pada komputer berasitektur ARM seperti di Raspberry Pi?
2. Bagaimana penerapan database _MySQL_ pada Raspberry Pi?

## Tujuan

Tujuan dalam kasus ini adalah:
1. Membuat server hemat daya berasitektur _ARM_ seperti Raspberry Pi yang bisa digunakan untuk keperluan pribadi maupun usaha kecil.
2. Menerapkan _MySQL_ pada Raspberry Pi.

## Landasan Teori
### Raspberry Pi
Raspberry Pi adalah sebuah SBC (_Single Board Computer_) seukuran kartu kredit menggunakan sistem operasi Raspbian. Raspberry Pi dihubungkan ke monitor komputer atau TV, menggunakan keyboard dan mouse standard. Raspberry Pi menggunakan SD Card untuk proses booting dan penyimpanan data jangka-panjang.
### LAMP Stack
LAMP adalah istilah yang merupakan singkatan dari _Linux, Apache, MySQL dan Perl/PHP/Phyton_. Merupakan sebuah paket perangkat lunak bebas yang digunakan untuk menjalankan sebuah aplikasi secara lengkap.
### Linux
Linux adalah nama yang diberikan kepada sistem operasi komputer bertipe Unix. Linux merupakan salah satu contoh hasil pengembangan perangkat lunak bebas dan sumber terbuka utama. Seperti perangkat lunak bebas dan sumber terbuka lainnya pada umumnya, _Source Code_ Linux dapat dimodifikasi, digunakan dan didistribusikan kembali secara bebas oleh siapa saja.
### Raspbian
Raspbian adalah Sistem Operasi Linux turunan dari distro Debian yang diperuntukan khusus untuk bekerja di sistem dengan perangkat keras Raspberry Pi, yang mana di dalamnya terdapat processor Arm.
### Apache
Server HTTP Apache adalah server web yang dapat dijalankan di banyak sistem operasi (Unix, BSD, Linux, Microsoft Windows dan Novell Netware serta platform lainnya) yang berguna untuk melayani dan memfungsikan situs web. Protokol yang digunakan untuk melayani fasilitas web/www ini menggunakan HTTP.
### MySQL
![mysql](images/mysql_logo.png "MySQL")
_MySQL_ adalah sebuah perangkat lunak sistem manajemen basis data SQL (bahasa Inggris: database management system) atau DBMS yang multialur, multipengguna, dengan sekitar 6 juta instalasi di seluruh dunia. _MySQL_ AB membuat _MySQL_ tersedia sebagai perangkat lunak gratis di bawah lisensi _GNU General Public License_ (GPL), tetapi mereka juga menjual di bawah lisensi komersial untuk kasus-kasus di mana penggunaannya tidak cocok dengan penggunaan GPL.
### PHP
Untuk menginstal server web pada Raspberry, pertama Pengguna harus tahu bahwa PHP adalah bahasa pemrograman yang ditafsirkan (_interpreted language_). Dan seperti dalam kasus server, akronim PHP dapat memiliki beberapa arti. Ketika berbicara tentang PHP, berarti berbicara tentang bahasa atau penerjemah(_interpreter_).Di sini, ketika berbicara tentang menginstal PHP, itu berarti akan menginstal _interpreter_, untuk menggunakan bahasa PHP.

PHP (bahasa) biasanya digunakan untuk membuat situs dinamis, artinya bahwa pengguna mengirimkan informasi ke server, setelah itu server mengembalikan hasil yang dimodifikasi sesuai dengan informasi yang diberikan. Sebaliknya, situs statis tidak menyesuaikan dengan informasi yang diberikan oleh pengguna.

PHP itu gratis, dan dikelola oleh Yayasan PHP, serta Zend Enterprise, dan berbagai perusahaan lain (perlu dicatat bahwa Zend juga penulis _zend framework_ yang terkenal, banyak digunakan dan diakui dalam dunia "bisnis") .

Ini adalah salah satu bahasa pemrograman yang paling banyak digunakan, dan bahkan yang paling banyak digunakan untuk pemrograman web, dengan sekitar 79% pangsa pasar.

Semua keterampilan yang dapat diperoleh, pada bahasa, atau pada instalasi dan konfigurasi interpreter, akan selalu berguna. Maka dari itu pengguna disarankan untuk belajar PHP.

### SSH
SSH adalah akronim dari Secure Shell yang merupakan sebuah protokol jaringan yang memanfaatkan kriptografi untuk melakukan komunikasi data pada perangkat jaringan agar lebih aman. Dalam konsepnya penggunaan SSH ini harus didukung oleh server maupun perangkat atau komputer klien yang melakukan pertukaran data. Keduanya harus memiliki SSH Server dari sisi komputer server dan SSH Klien untuk komputer penerima (klien).
Banyak digunakan pada sistem operasi berbasis Linux dan Unix untuk mengakses akun Shell, SSH dirancang sebagai pengganti Telnet dan shell remote tak aman lainnya, yang mengirim informasi, terutama kata sandi, dalam bentuk teks sederhana yang membuatnya mudah untuk dicegat. Enkripsi yang digunakan oleh SSH menyediakan kerahasiaan dan integritas data melalui jaringan yang tidak aman seperti internet.

## Pembahasan

### Persiapan Hardware
![Raspberry Pi 3 Model B](images/raspberrypi3b.png "Raspberry Pi 3 Model B")

Alat-alat yang diperlukan :  
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

![Raspberry Pi 3 Model B](images/pi3spec.png "Raspberry Pi 3 Model B")

### Instalasi OS
![Raspberry Pi 3 Details](images/sd_card_install.jpg "Raspberry Pi 3 SD card")
Raspberry Pi wajib menggunakan OS yang mendukung prosesor jenis ARM. Contohnya adalah Raspbian, yang merupakan OS GNU/Linux turunan dari Debian. Untuk membuat server, pilih **Raspbian Stretch Lite** yang disediakan di [situs resmi Raspberry Pi](https://www.raspberrypi.org/downloads/raspbian/).  
File yang berupa kompresi zip, harus diekstrak dari kompresi tersebut hingga berupa satu file *virtual CD* berekstensi "*.iso*".

Sambungkan SD Card dengan komputer untuk menginstall Raspbian kedalam SD Card. Setelah SD Card terdeteksi, gunakan USB Image writer atau software sejenisnya untuk memindahkan isi dari *virtual CD* Raspbian yang sudah didownload sebelumnya. Untuk pengguna Windows atau Linux bisa menggunakan [Etcher](https://etcher.io/) sebagai alat pemindah *virtual CD* ke SD card. Namun, di OS linux biasanya sudah disediakan *tools* sejenis(*USB Image Writer pada Linux Mint*). Lanjutkan dengan menjalankan pemindahan *virtual CD* kedalam SD Card dan OS Raspbian dapat digunakan setelah memasukan SD Card ke Raspberry Pi.

### Booting dan login
Pada saat memulai Raspberry Pi untuk pertama kali, Tampilan dimulai dengan CLI (*Command Line Interface*).
Login dengan ID dan Password bawaan dari raspberry.  
User name `pi`  
Password `raspberry`  
Setelah login, pengguna akan masuk ke dalam shell Debian linux pada raspberry pi.

### Pengaturan SSH
Pengguna sebaiknya mengatur pengaturan raspberry agar bisa di akses melalui terminal dari komputer lain. Tehnik ini biasa disebut *remote login* atau SSH (*Secure Shell*).  
Untuk mengaktifkan SSH server pada Raspberry Pi, ketikkan perintah:  
`sudo raspi-config`  
Akan muncul tampilan menu **Raspberry Pi Software Configuration Tool **.  
Pada menu pilihan **raspi-config**, masuk ke **Interfacing Options**, lalu pilih **SSH**.


![alt text](images/raspi-config.png "Raspberry Pi Software Configuration Tool")  
![alt text](images/interface-opt.png "Interfacing Option")

Pilih `yes` untuk mengaktifkan SSH server pada Raspberry Pi.
![alt text](images/ssh.png "SSH")  

Selain mengaktifkan SSH server, menu ini bisa juga untuk mengubah password bawaan menjadi pasword yang dikehendaki.

### Remote Login menggunakan ssh
Setelah Network dan SSH diatur dengan benar, maka pengguna bisa mengontrol Raspberry Pi dari perangkat atau komputer lain, sehingga tidak perlu memasang monitor dan keyboard pada Raspberry Pi. Cukup menghidupkan dan memasang kabel LAN, dan Raspberry bisa digunakan melalui SSH.</br>
pada OS Windows, pengguna dapat menggunakan SSH dengan software [Putty](https://www.putty.org/) atau software SSH client lainnya. Namun, pada panduan kali ini, penulis menggunakan OS *Linux Mint* sebagai *remote-client* untuk SSH terhadap Raspberry Pi.

### Apache Web server
setelah memegang alih Raspberry Pi dengan SSH, pengguna dapat menggunakan shell untuk keperluan instalasi Apache dengan mengetikkan:
```
sudo apt update
sudo apt upgrade
sudo apt install apache2
```
Pengguna bisa mengatur hak akses pada folder `/var/www/html` agar memudahkan pengguna dalam mengatur website nantinya. Untuk mengaturnya, ketikan:
```
sudo chown -R pi:www-data /var/www/html/
sudo chmod -R 770 /var/www/html/
```
Pengguna dapat menguji apakah Apache berfungsi dengan benar dengan membuka alamat Raspberry.
Untuk melakukannya, Pengguna perlu mencoba mengakses Raspberry dari port `80`. Dengan cara membuka web browser, dan masuk ke alamat IP LAN raspberry Pengguna. Akan muncul pesan `It Works!` dan banyak teks lainnya pada halaman web browser pengguna.

Jika belum memiliki GUI di Raspbian, atau jika menggunakan SSH untuk terhubung ke Raspberry, pengguna dapat menggunakan perintah berikut:
```
wget -O check_apache.html http://127.0.0.1

```
Perintah diatas akan menyimpan kode HTML dari halaman dalam file "check_apache.html" di direktori saat ini.
Untuk membacanya ketikan perintah:
```
cat ./check_apache.html
```
Jika muncul `It Works!` di dalam kode  berarti Apache telah bekerja dengan semestinya.

Apache menggunakan direktori `/var/www/html` sebagai _root_ untuk situs. Ini berarti bahwa ketika Anda memanggil Raspberry Anda di port 80 (http), Apache mencari file di `/var/www/html`.
Misalnya pengguna menggunakan IP `192.168.0.11` sebagai alamat Raspberry, jika pengguna memanggil alamat `http://192.168.0.11/contoh` pada browser, Apache akan mencari file "contoh" di direktori `/var/www/html`.

Untuk menambahkan file baru, situs, dll, pengguna hanya perlu menambahkannya ke direktori ini.

Pengguna sekarang dapat menggunakan Raspberry untuk membuat situs dalam HTML, CSS, dan JavaScript secara internal. Namun dalam kasus kali ini, pengguna membutuhkan apache sebagai alat untuk menjalankan PHPmyAdmin yang dimana sebagai alat untuk membantu mengolah Database MySQL.

### Instalasi PHP

Lanjutkan dengan mengetikan:
```
sudo apt install php php-mbstring
```
lalu cek apakah PHP telah jalan.

Pengguna akan terlebih dahulu menghapus file `index.html` di direktori `/var/www/html`.
Kemudian buat file "index.PHP" di direktori ini, dengan mengetikan perintah:
```
echo "<?PHP PHPinfo ();?>" > /var/www/html/index.php
```

Lakukan hal sama dengan pemeriksaan Apache. Pastikan hasil browser mendekati gambar ini:  
![alt text](images/phpinfo.jpg "PHP Info")  

Jika tidak memiliki antarmuka (_GUI_), gunakan metode SSH yang sama seperti sebelumnya, dan cari kata-kata `PHP Version`

### Database MySQL untuk server

Setelah mengatur PHP, pengguna perlu menyimpan informasi agar dapat digunakan di situs terkait. Untuk hal ini, databaselah yang paling sering digunakan. Maka diperlukan DBMS (Database Management System), yaitu MySQL.

Pengguna memerlukan `mysql-server` dan `php-mysql` (yang akan berfungsi sebagai penghubung antara PHP dan mysql). Ketikan perintah:  
```
sudo apt install mysql-server php-mysql
```
Pastikan mysql telah jalan.
```
sudo mysql --user=root
```
Setelah itu pengguna akan pindah ke konsol `MariaDB`.
Disini, user _root_ bawaan mysql tidak dihapus dan membuat _root_ mysql yang baru dengan hak akses berbeda, karena default _root_ hanya dapat digunakan dengan akun _root_ Linux, sehingga tidak tersedia untuk skrip webserver dan PHP.

Untuk melakukannya, setelah terhubung ke MySQL, jalankan perintah (ganti kata sandi dengan kata sandi yang diinginkan):
```
DROP USER 'root'@'localhost';
CREATE USER 'root'@'localhost' IDENTIFIED BY 'password_yang_diinginkan';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost'
```
untuk membuka MySQL ke koneksi publik, buat user _root_ publik, gunakan:
```
CREATE USER 'root'@'%' IDENTIFIED BY 'password_yang_diinginkan';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%'
```
Membuat _root_ ke publik tidak disarankan atas alasan keamanan. Namun boleh digunakan jika untuk keperluan pribadi dan tidak menggunakan data-data yang vital.

Di penggunaan berikutnya, pengguna tidak perlu lagi menggunakan `sudo` untuk mengakses MySQL dengan perintah:
```
mysql --user=root --password=password_yang_telah_dibuat
```

### PHPmyAdmin

PHPmyAdmin adalah fitur opsional namun membantu dalam pengaturan database. Untuk menginstall PHPmyAdmin, ketikan:  
```
sudo apt install PHPmyadmin
```
Program instalasi PHPMyAdmin akan menanyakan beberapa pertanyaan. Tentang bagian `dbconfig-common`, pilih untuk tidak menggunakannya (karena dalam praktek sebelumya telah mengkonfigurasi database). Tentang server untuk mengkonfigurasi PHPMyAdmin, pilih Apache. Dan kata sandi root adalah yang telah diatur sebelumnya untuk MySQL.

Untuk memeriksa apakah PHPMyAdmin berfungsi, akses menggunakan alamat Raspberry, diikuti oleh / PHPmyadmin. Misal, secara lokal akan menjadi `http://127.0.0.1/PHPmyadmin` pada web browser.

## Kesimpulan & Saran
### Keasimpulan

Setelah Raspberry Pi bisa berjalan dengan lancar maka dapat disimpulkan bahwa:
1. Raspberry Pi berhasil menggunakan MySQL sebagai RDBMS
2. Pengguna dapat memotong penggunaan daya dalam pembuatan server kecil dibandingkan dengan komputer _Desktop_.

### Saran
Saran yang dapat diberikan adalah:
1. Gunakan Raspberry Pi sebagai server pribadi ataupun bisnis kecil. ini disebabkan kemampuan Raspberry Pi yang terbatas.
2. Sebaiknya gunakan kabel Ethernet untuk server sebagai alasan kestabilan koneksi

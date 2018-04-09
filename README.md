# Penerapan MySQL Database Server Pada Raspberry Pi

## Pendahuluan

Mengapa menggunakan Raspberry sebagai server daripada menggunakan penyedia layanan khusus web hosting? </br> Pertama, dari sudut pandang ekonomi, Bahwa layanan web hosting tidak gratis dan harus membayar setiap bulan/tahun. Berbeda dengan Raspberry yang hanya perlu koneksi. Selain itu, dengan memilih Raspberry, Pengguna memiliki kemungkinan untuk memodifikasi sesuai kebutuhan sesuai dengan keinginan pengguna (contoh: ukuran disk, hosting Database, dll.), hal tersebut biasanya tidak dapat dilakukan pada web hosting khusus, yang sering dijual bersama domain dengan kapasitas konfigurasi rendah. </br>
Namun, untuk mendukung fleksibilitas lebih, Praktikum makalah ini menggunakan Raspberry Pi 3 Model B, dengan kapasitas 1GB RAM, dibandingkan dengan model Raspberry Pi lainnya yang memiliki spesifikasi lebih rendah.
</br>Pertanyaan yang sekarang muncul adalah, bagaimana cara membuat server web di Raspeberry Pi?


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

Sebelum dinyalakan, Raspberry Pi wajib menggunakan OS yang mendukung prosesor jenis ARM. Salah satunya adalah Raspbian, yaitu berupa OS GNU/Linux turunan dari Debian. Untuk membuat server, pilih **Raspbian Stretch Lite** yang disediakan di [situs resmi Raspberry Pi](https://www.raspberrypi.org/downloads/raspbian/).</br>
Setelah download, file berupa kompresi zip, dan harus diekstrak dari kompresi tersebut hingga berupa satu file *virtual CD* berekstensi "*.iso*".

Lalu, sambungkan SD Card dengan komputer untuk menginstall Raspbian kedalam SD Card. Setelah SD Card terdeteksi, gunakan USB Image writer atau software sejenisnya untuk memindahkan isi dari *virtual CD* Raspbian yang sudah didownload sebelumnya". Untuk pengguna Windows atau Linux bisa menggunakan [Etcher](https://etcher.io/) sebagai alat pemindah *virtual CD* ke SD card. Namun, di OS linux biasanya sudah disediakan *tools* sejenis*(USB Image Writer pada Linux Mint*). Lanjutkan dengan menjalankan pemindahan *virtual CD* kedalam SD Card dan OS Raspbian siap digunakan dengan memindahkan SD Card ke Raspberry Pi.

## Booting dan login
Setelah menginstall OS pada kartu SD Card, dan setelah memulai Raspberry Pi untuk pertama kalinya, Tampilan dimulai dengan CLI (*Command Line Interface*).
Login dengan ID dan Password bawaan dari raspberry yaitu:</br>
user name `pi`</br>password `raspberry`</br>
Sehingga pengguna bisa masuk ke dalam shell Debian linux pada raspberry pi.

## Pengaturan SSH
Setalah masuk ke dalam shell, pengguna sebaiknya mengatur pengaturan raspberry agar bisa di akses melalui terminal dari komputer lain. Tehnik ini biasa disebut *remote login* atau SSH (*Secure Shell*). </br>
Untuk mengaktifkannya, SSH server pada Raspberry Pi perlu diaktifkan. Untuk mengaktifkannya, ketikkan perintah dibawah ini:</br>
`sudo raspi-config`</br>
sehingga tampilan akan muncul ke tampilan menu **Raspberry Pi Software Configuration Tool **.</br>


Pada menu pilihan **raspi-config**, masuk ke **Interfacing Options**, lalu pilih **SSH**.


![alt text](images/raspi-config.png "Raspberry Pi Software Configuration Tool")</br>

![alt text](images/interface-opt.png "Interfacing Option")

lalu pilih `yes` untuk mengaktifkan SSH server pada Raspberry Pi.
![alt text](images/interface-opt.png "SSH")</br>

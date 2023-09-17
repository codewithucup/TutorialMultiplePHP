# TutorialMultiplePHP
TUTORIAL BAGAIMANA CARA INSTALASI DAN MENJALANKAN 2 VERSI PHP 8.2 DAN VERSI DIBAWAHNYA DI XAMPP : https://medium.com/p/a188c6c92b3d

Kebutuhan program yang beragam terkadang mengharuskan seorang pengembang atau programmer untuk menjalankan berbagai versi PHP (Hypertext Preprocessor) dalam satu instalasi XAMPP.

Contohnya, mungkin ada program lama yang memerlukan PHP versi 8.0, tetapi instalasi XAMPP saat ini sudah menggunakan PHP versi 8.2, atau sebaliknya. Selain itu disaat pengembangan memiliki banyak project PHP secara bersamaan dengan Framework Laravel dan Codeigniter yang beda versi mempengaruhi jalan dan tidaknya PHP. Oleh karena itu, diperlukan kemampuan untuk menjalankan XAMPP yang mendukung PHP versi 8.0 dan 8.2 secara bersamaan. Hal ini memungkinkan pengembang untuk menangani berbagai proyek yang memerlukan versi PHP yang berbeda tanpa perlu menginstal ulang XAMPP setiap kali.

CARA INSTALASI 2 VERSI MULTI PHP DI XAMPP
Dalam pembahasan ini, kita akan berasumsi bahwa kita akan menginstal XAMPP dengan PHP versi terbaru, yaitu 8.2, dan menambahkan PHP versi sebelumnya yaitu 8.0 sebagai mesin PHP kedua.

Berikut adalah langkah-langkah yang perlu diikuti untuk menginstal dan menjalankan dua versi PHP atau lebih dalam satu instalasi XAMPP.

Langkah 1:
Pertama-tama, lakukan instalasi XAMPP dengan mengunduhnya dari situs resmi https://www.apachefriends.org/download.html. Pilih versi paket XAMPP yang sesuai dengan kebutuhan Anda (dalam posting kali ini, kita akan menginstal versi terbaru PHP 8.2).

Langkah 2:
Setelah XAMPP terinstal dengan sukses di laptop atau komputer Anda, lanjutkan dengan mengunduh engine PHP dari situs resmi https://windows.php.net/download. Pilih versi PHP 8.0 dan sesuaikan dengan arsitektur sistem Anda, yaitu x64 jika menggunakan Windows 64-bit, atau x86 jika menggunakan Windows 32-bit. Pastikan untuk memilih versi “Thread Safe” yang berformat .zip.

Langkah 3:
Buka folder instalasi XAMPP Anda, misalnya di lokasi drive “C:\xampp”. Selanjutnya, buat folder baru dengan nama “php80”.

Langkah 4:
Ekstrak file engine PHP yang tadi Anda unduh ke dalam folder “php80”.

Langkah 5:
Setelah selesai mengekstrak file engine PHP, cari dan buka file php.ini di lokasi “C:\xampp\php80\php.ini” menggunakan aplikasi text editor yang Anda gunakan. Jika file php.ini tidak ditemukan, Anda bisa menyalin file “php.ini-development” dan kemudian mengganti namanya menjadi “php.ini”.

Selanjutnya, buka file tersebut dan hilangkan tanda ; di awal baris kode yang sesuai dengan langkah-langkah yang Anda perlukan.

;extension_dir = "ext"
menjadi

extension_dir = "ext"

Langkah 6
buka Control Panel XAMPP, pada bagian modul Apache, klik tombol “Config” lalu pilih pada bagian “Apache (httpd-xampp.conf)”.

Sebuah halaman text editor akan muncul berisikan kumpulan config, silahkan anda masukan baris kode berikut di baris paling bawah dari file config, lalu simpan dengan cara shortcut keyboard CTRL + S (untuk notepad).

ScriptAlias /php80 "C:/xampp/php80"
<Directory "C:/xampp/php80">
    AllowOverride None
    Options None
    Require all denied
    <Files "php-cgi.exe">
        Require all granted
    </Files>
</Directory>
Instalasi selesai, jika langkah-langkah di atas sudah anda lakukan dengan tepat, maka aplikasi virtual server XAMPP sudah berhasil terpasang dua versi PHP, yaitu versi PHP bawaan dari XAMPP (8.2) dan versi PHP yang anda tambahkan yaitu versi (8.0).

CARA MENJALANKAN 2 VERSI MULTI PHP DI XAMPP
Setelah melakukan instalasi pada langkah sebelumnya kini anda sudah memiliki 2 versi php dalam program XAMPP yang berjalan bersamaan.

Namun perlu anda ketahui bahwa saat anda menjalankan XAMPP dan mengakses localhost di browser maka secara bawaan / standar menggunakan PHP bawaan dari XAMPP yaitu 8.2, lalu bagaimana cara mengakses localhost dengan versi PHP 8.0 yang tadi ditambahkan?

Sebagai gambaran kita akan menggunakan port (yang berbeda) untuk mengakses versi php lain di localhost, berikut langkah-langkah lengkapnya:

Langkah 1, silahkan anda buka kembali Control Panel XAMPP, pada bagian modul Apache, klik tombol “Config” lalu pilih pada bagian “Apache (httpd-xampp.conf)” seperti langkah sebelumnya, lalu masukan baris kode berikut di baris paling bawah :

Listen 8030
<VirtualHost *:8030>
    UnsetEnv PHPRC
    <FilesMatch "\.php$">
        php_flag engine off
        SetHandler application/x-httpd-php80
        Action application/x-httpd-php80 "/php74/php-cgi.exe"
    </FilesMatch>
</VirtualHost>
Jika diperhatikan, pada baris kode di atas kita menggunakan Port 8030 untuk mengakses localhost dengan menggunakan versi PHP yang kita tambahkan sebelumnya, di sini anda bebas menggunakan Port lain yang tersedia di komputer saat ini, namun pastikan kembali Port yang anda gunakan tidak terpakai dengan port-port lain yang sudah aktif.

Sebagai informasi tambahan port standar localhost apache XAMPP adalah 80, jadi anda dapat menggunakan port selain itu.

Langkah 2, lalu simpan dengan cara shortcut keyboard CTRL + S (untuk notepad). Lalu restart kembali modul Apache dari halaman Control Panel XAMPP kalian.

Langkah 3, anda sudah berhasil menambahkan port khusus untuk mengakses php versi lain.


Untuk mengakses localhost dengan menggunakan PHP bawaan XAMPP (8.2) cukup akses “localhost” di kolom URL browser anda dan untuk mengecek versi php menggunakan http://localhost:8030/dashboard/phpinfo.php


sedangkan untuk mengakses localhost dengan menggunakan versi PHP (8.0) yang anda tambahkan sebelumnya silahkan akses “localhost:8030” di kolom URL browser anda dan untuk mengecek versi php menggunakan http://localhost:8030/dashboard/phpinfo.php

Dengan begitu anda dapat menjalankan program sesuai kebutuhan versi php enginenya, baik menggunakan php versi 8.2 atau 7.4. Panduan dan tutorial dalam post ini hanya sebagai contoh saja, sehingga tidak terbatas pada jumlah versi php yang ingin anda tambahkan, bahkan anda bisa menambahkan versi php lebih dari 2 sesuai kebutuhan tentunya.

Happy and Enjoy Coding! #codewithucup :)

Referensi
https://wandercom.id/read/cara-install-menjalankan-multi-php-xampp/

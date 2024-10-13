Nama : Armanda Fathurrahman
NIM : 09011282126055
Kelas : SK7A Indralaya

Dumping and Cracking SAM Hashes to Extract Plain Text Password

 Security Account Manager (SAM) adalah komponen penting dalam sistem operasi Windows yang berfungsi sebagai database untuk menyimpan informasi keamanan terkait akun pengguna, termasuk kata sandi dan hak akses. SAM menyimpan hash dari kata sandi pengguna, bukan kata sandi sebenarnya, untuk memastikan keamanan data autentikasi. Ketika pengguna mencoba login ke sistem, Windows akan membandingkan hash kata sandi yang dimasukkan dengan hash yang tersimpan di SAM untuk memastikan identitas pengguna. File SAM, yang biasanya terletak di direktori `C:\Windows\System32\Config\SAM`, dilindungi ketat oleh sistem dan tidak bisa diakses atau dimodifikasi secara langsung saat sistem sedang berjalan, karena Windows menguncinya untuk melindungi integritas dan keamanan data pengguna. SAM memainkan peran vital dalam memastikan bahwa hanya pengguna yang berwenang yang bisa mengakses sumber daya di dalam sistem, dan karena sifat pentingnya, file SAM sering menjadi target serangan bagi peretas yang berusaha mendapatkan akses tidak sah ke akun pengguna. Untuk mencegah akses yang tidak sah, Windows menggunakan beberapa lapisan perlindungan, termasuk enkripsi dan pembatasan akses pada file SAM, sehingga peretas tidak bisa dengan mudah memanipulasi atau mencurinya.
 
Dumping dan cracking SAM adalah metode yang sering digunakan oleh penyerang untuk mendapatkan akses tidak sah ke akun pengguna pada sistem Windows. Dumping merujuk pada proses mengekstrak data dari file SAM yang berisi hash kata sandi, yang kemudian digunakan untuk melakukan cracking. Karena file SAM dilindungi oleh sistem saat sedang berjalan, penyerang sering menggunakan alat atau teknik khusus, seperti menjalankan sistem dalam mode offline atau menggunakan perangkat lunak seperti Mimikatz atau pwdump untuk mem-bypass perlindungan tersebut. Setelah hash kata sandi diekstrak, langkah berikutnya adalah melakukan cracking, yaitu mencoba memecahkan hash tersebut untuk mendapatkan kata sandi asli. Salah satu teknik yang umum digunakan untuk cracking adalah *brute-force* atau *dictionary attack*, di mana penyerang mencoba berbagai kombinasi kata sandi atau menggunakan daftar kata sandi yang umum. Meski hash dirancang untuk sulit dipecahkan, jika kata sandi yang digunakan lemah atau tidak aman, proses cracking bisa lebih mudah dan cepat. Oleh karena itu, penggunaan kata sandi yang kuat serta lapisan keamanan tambahan seperti enkripsi file SAM dan penggunaan *salting* pada hash dapat membantu mengurangi risiko dumping dan cracking ini.
Tujuan dari dumping and cracking SAM adalah :
1.	Mengetahui cara mengunakan alat pwdump7 untuk mengekstrak hash kata sandi.
2.	Mengetahui cara mengunakan alat Ophcrack untuk memecahkan kata sandi dan mendapatkan teks biasa.

Langkah-langkah

1.	Kita mencari tahu User ID dengan username menggunakan CMD via mode administrator.
![image](https://github.com/user-attachments/assets/66dd3970-2e89-44af-9ea0-5ce013405c71)

2.	Masukkan kode “wmic useraccount get name,sid” pada CMD yang memiliki fungsi menampilkan daftar semua akun pengguna yang ada di sistem beserta SID-nya masing-masing.
![image](https://github.com/user-attachments/assets/63f2f13f-9977-4184-9faa-8f56bf68daf4)

3.	Download dan extract pwdump dan ophcrack.
![image](https://github.com/user-attachments/assets/81acbdb5-71ea-4377-bac1-ebe115a9236d)

4.	Buka dan salin lokasi file pwdump dan klik enter untuk masuk ke directory pwdumpmaster, kemudian ketik PwDump7.exe untuk mendapatkan dan menampilkan password hashes dan userID.
![image](https://github.com/user-attachments/assets/b766267a-16d9-4ced-94c3-e8875bbe361a)

5.	Pindahkan dan copy semua data hasil dari PwDump7.exe ke hashes.txt menggunakan command PwDump7.exe > c:\hashes.txt
![image](https://github.com/user-attachments/assets/f0d0f61b-ea04-4f31-b072-7269fac06ec6)

Berikut isi dari hashes yang sudah disalin.
![image](https://github.com/user-attachments/assets/844a111c-13a6-401b-a86e-4acb89e22882)

6.	Isi semua username yang kosong sesuai dengan username pengguna pada step 2 kemudian save file hashes.txt
![image](https://github.com/user-attachments/assets/48b96c42-0dcc-4b6c-a1cd-725f633ed60e)

7.	Buka ophcrack, kemudian pilih Load > PWDUMP file dan pilih file hashes.txt sebelumnya.
Berikut tampilan file hashes pada ophcrack.
![image](https://github.com/user-attachments/assets/1a2618b0-a5c4-407c-b7a6-c848595606cc)

8.	Klik Table, dan pada table selection pilih vista free kemudian klik install, kemudian pilih table vista free yang sudah di download sebelumnya. (table vista free bisa di download menggunakan link : https://ophcrack.sourceforge.io/tables.php)
![image](https://github.com/user-attachments/assets/873f570e-ff5b-4908-822d-11e0e5ae1953)
 
9.	Klik crack setelah menginstall tables sebelumnya untuk memecahkan kata sandi yang ada. Tunggu hingga selesai, OPHCrack akan memakan beberapa waktu untuk memecahkan kata sandinya. 
![image](https://github.com/user-attachments/assets/aa0f4dff-1825-4db9-86ca-1be62b8788b5)
 
10.	Setelah selesai maka password akan tampil, Jika hasilnya menunjukkan not found maka kemungkinan besar karena windows 10 terbaru secara default tidak lagi menyimpan password di hash LM karena kurang aman atau bisa juga karena beberapa akun (seperti "Guest" atau "DefaultAccount") mungkin tidak memiliki password atau sedang tidak aktif, sehingga Ophcrack tidak menemukan apa-apa.
![image](https://github.com/user-attachments/assets/ba75ecd7-22fc-4909-9b34-c48eaead48f5)


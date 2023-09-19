# Poster
- TryHackMe Room: https://tryhackme.com/room/poster
- IP Machine: 10.10.230.31

## Task 1 - Flag

- **Pertanyaan:** What is the rdbms installed on the server?
- Lakukan scanning dengan nmap
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

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Poster/assets/p%206.JPG)

- Jalankan modul dengan perintah `run` dan tunggu hingga proses selesai

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
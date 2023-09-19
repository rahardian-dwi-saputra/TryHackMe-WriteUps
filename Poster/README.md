# Poster
- TryHackMe Room: https://tryhackme.com/room/poster
- IP Machine: 10.10.230.31

## Task 1 - Flag

- **Pertanyaan:** What is the rdbms installed on the server?
- Lakukan scanning dengan nmap
```sh
nmap -sC -sV <IP_Machine>
```


- **Jawaban:**
```sh
postgresql
```

- **Pertanyaan:** What port is the rdbms running on?
- Lihat kembali nmap dari pertanyaan sebelumnya

- **Jawaban:**
```sh
5432
```

- **Pertanyaan:** After starting Metasploit, search for an associated auxiliary module that allows us to enumerate user credentials. What is the full path of the modules (starting with auxiliary)?
- Buka `msfconsole` di terminal

- Lalu cari modul untuk postgres
```sh
search postgres
```

- Disini kita menemukan modul PostgreSQL Login Utility


- **Jawaban:**
```sh
auxiliary/scanner/postgres/postgres_login
```

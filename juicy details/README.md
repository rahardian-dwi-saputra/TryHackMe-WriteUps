# Juicy Details
Tryhackme room: https://tryhackme.com/room/juicydetails

## Task 1 Introduction
- Download task file (**logs.zip**)
- Ekstrak file **logs.zip** dengan tool unzip
```sh
unzip logs.zip
```
- Setelah proses ekstrasi berhasil terdapat 3 jenis file yaitu **access.log**, **auth.log**, dan **vsftpd.log**

- **Pertanyaan:** Are you ready?
```sh
I am ready!
```

## Task 2 Reconnaissance
- **Pertanyaan:** What tools did the attacker use? (Order by the occurrence in the log)
- Buka file **access.log** di terminal dengan perintah sebagai berikut
```sh
cat access.log
```
- Di Log bagian atas terdapat log penggunaan tool **nmap**
- Scroll kebawah, di log berikutnya terdapat log penggunaan tool **hydra**
- Scroll kebawah lagi, di log berikutnya lagi terdapat log penggunaan tool **sqlmap**
- Scroll kebawah lagi, di log berikutnya lagi terdapat log penggunaan tool **curl**
- Dibawah log tool **curl** terdapat log penggunaan tool **feroxbuster**
- **Jawaban**
```sh
nmap, hydra, sqlmap, curl, feroxbuster
```

- **Pertanyaan:** What endpoint was vulnerable to a brute-force attack?
- Buka file **access.log** di terminal dengan perintah sebagai berikut
```sh
cat access.log | grep Hydra
```
- **Jawaban**
```sh
/rest/user/login
```

- **Pertanyaan:** What endpoint was vulnerable to SQL injection?
- Buka file **access.log** di terminal dengan perintah sebagai berikut
```sh
cat access.log | grep sqlmap
```

- **Jawaban**
```sh
/rest/products/search
```

- **Pertanyaan:** What parameter was used for the SQL injection?
- **Jawaban**
```sh
q
```

- **Pertanyaan:** What endpoint did the attacker try to use to retrieve files? (Include the /)
```sh
cat vsftpd.log
```
- Terlihat bahwa attacker mengakses FTP untuk mengunduh file
- **Jawaban**
```sh
/ftp
```
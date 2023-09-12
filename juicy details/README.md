# Juicy Details
Tryhackme room: https://tryhackme.com/room/juicydetails

## Task 1 Introduction
- Download task file (**logs.zip**)
- Ekstrak file **logs.zip** dengan tool unzip
```sh
unzip logs.zip
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/juicy%20details/assets/jd%201.JPG)

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

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/juicy%20details/assets/jd%202.JPG)

- Di Log bagian atas terdapat log penggunaan tool **nmap**
- Scroll kebawah, di log berikutnya terdapat log penggunaan tool **hydra**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/juicy%20details/assets/jd%203.JPG)

- Scroll kebawah lagi, di log berikutnya lagi terdapat log penggunaan tool **sqlmap**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/juicy%20details/assets/jd%204.JPG)

- Scroll kebawah lagi, di log berikutnya lagi terdapat log penggunaan tool **curl**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/juicy%20details/assets/jd%205.JPG)

- Dibawah log tool **curl** terdapat log penggunaan tool **feroxbuster**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/juicy%20details/assets/jd%206.JPG)

- **Jawaban**
```sh
nmap, hydra, sqlmap, curl, feroxbuster
```

- **Pertanyaan:** What endpoint was vulnerable to a brute-force attack?
- Buka file **access.log** di terminal dengan perintah sebagai berikut
```sh
cat access.log | grep Hydra
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/juicy%20details/assets/jd%207.JPG)

- **Jawaban**
```sh
/rest/user/login
```

- **Pertanyaan:** What endpoint was vulnerable to SQL injection?
- Buka file **access.log** di terminal dengan perintah sebagai berikut
```sh
cat access.log | grep sqlmap
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/juicy%20details/assets/jd%208.JPG)

- **Jawaban**
```sh
/rest/products/search
```

- **Pertanyaan:** What parameter was used for the SQL injection?

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/juicy%20details/assets/jd%209.JPG)

- **Jawaban**
```sh
q
```

- **Pertanyaan:** What endpoint did the attacker try to use to retrieve files? (Include the /)
```sh
cat vsftpd.log
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/juicy%20details/assets/jd%2010.JPG)

- Terlihat bahwa attacker mengakses FTP untuk mengunduh file
- **Jawaban**
```sh
/ftp
```
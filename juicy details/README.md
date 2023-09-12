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

## Task 3 Stolen data
- **Pertanyaan:** What section of the website did the attacker use to scrape user email addresses?
- Buka kembali file **access.log**
```sh
cat access.log
```
- Setelah attacker membuka halaman product review, dia membuka halaman whoami untuk melihat detail user
- **Jawaban**
```sh
product review
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/juicy%20details/assets/jd%2011.JPG)

- **Pertanyaan:** Was their brute-force attack successful? If so, what is the timestamp of the successful login? (Yay/Nay, 11/Apr/2021:09:xx:xx +0000)
- Gunakan grep untuk memfilter file **access.log**
```sh
cat access.log | grep Hydra | grep 200
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/juicy%20details/assets/jd%2012.JPG)

- Attacker berhasil login pada tanggal 11 April 2021 pukul 09:16
- **Jawaban**
```sh
Yay, 11/Apr/2021:09:16:31 +0000
```

- **Pertanyaan:** What user information was the attacker able to retrieve from the endpoint vulnerable to SQL injection?
- Attacker biasanya mencari username dan password melalui serangan SQL injection sehingga kita bisa memanfaatkan filter username atau password pada file **access.log**
- Disini kita berhasil menggunakan filter password pada file **access.log**
```sh
cat access.log | grep password
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/juicy%20details/assets/jd%2013.JPG)

- **Jawaban**
```sh
email, password
```

- **Pertanyaan:** What files did they try to download from the vulnerable endpoint? (endpoint from the previous task, question #5)
- Buka file **vsftpd.log** lalu scroll kebawah
```sh
cat vsftpd.log
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/juicy%20details/assets/jd%2014.JPG)

- **Jawaban**
```sh
coupons_2013.md.bak,www-data.bak
```

- **Pertanyaan:** What service and account name were used to retrieve files from the previous question? (service, username)
- Di file **vsftpd.log** terlihat bahwa, Attacker mengakses FTP menggunakan username **anonymous**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/juicy%20details/assets/jd%2015.JPG)

- **Jawaban**
```sh
ftp, anonymous
```

- **Pertanyaan:** What service and username were used to gain shell access to the server? (service, username)
- Buka file **auth.log** di terminal dengan perintah sebagai berikut
```sh
cat auth.log
```
- Disini terlihat bahwa attacker berusaha mengakses SSH dengan username **www-data**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/juicy%20details/assets/jd%2016.JPG)

- **Jawaban**
```sh
ssh, www-data
```
# WebOSINT
- TryHackMe Challenge: https://tryhackme.com/room/webosint
- Domain: RepublicOfKoffee.com

## Task 2 Whois Registration

- Buka halaman web https://lookup.icann.org/en lalu ketikkan nama domain dan tekan tombol **Lookup**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%201.JPG)

- **Pertanyaan:** What is the name of the company the domain was registered with?
- Lihat informasi dibagian **Contact Information**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%202.JPG)

- **Jawaban:**
```sh
Namecheap Inc
```

- **Pertanyaan:** What phone number is listed for the registration company? (do not include country code or special characters/spaces)
- Lihat informasi dibagian **Raw Registry RDAP Response**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%203.jpg)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%204.JPG)

- **Jawaban:**
```sh
6613102107
```

- **Pertanyaan:** What is the first nameserver listed for the site?
- Lihat informasi dibagian **Domain Information**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%205.JPG)

- **Jawaban:**
```sh
ns1.brainydns.com
```

- **Pertanyaan:** What is listed for the name of the registrant?
- Lihat informasi dibagian **Registrant**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%206.JPG)

- **Jawaban:**
```sh
redacted for privacy
```

- **Pertanyaan:** What country is listed for the registrant?
- **Jawaban:**
```sh
Panama
```

## Task 3 Ghosts of Websites Past

- Buka halaman web https://archive.org/web/ lalu ketikkan nama domain dan tekan tombol **Browse History**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%207.JPG)

- **Pertanyaan:** What is the first name of the blog's author?
- Pilih timeline tahun 2016

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%208.JPG)

- Pilih tanggal 9 Februari lalu klik di tanggal tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%209.jpg)

- Klik continue ready untuk melihat detail post

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2010.jpg)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2011.JPG)

- **Jawaban:**
```sh
Steve
```

- **Pertanyaan:** What city and country was the author writing from?
- Di postingan sebelumnya tertulis nama kampus **Choson University**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2012.JPG)

- Sekarang kita cari di google dimana letak kampus tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2013.JPG)

- Dari hasil pencarian google kita mendapatkan informasi dimana letak kampus tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2014.JPG)

- **Jawaban:**
```sh
Gwangju, South Korea
```

- **Pertanyaan:** [Research] What is the name (in English) of the temple inside the National Park the author frequently visits?
- Klik link di tab Recent Post

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2015.jpg)

- Disini disebut lokasi meeting yang pernah berlangsung

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2016.JPG)

- Sekarang kita cari lewat google dengan kata kunci `Mudeungsan national park area of Gwangju temple`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2017.JPG)

- Dari hasil pencarian, didapatkan nama temple yang berada di sekitar lokasi tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2018.JPG)

- **Jawaban:**
```sh
Jeungsimsa Temple
```
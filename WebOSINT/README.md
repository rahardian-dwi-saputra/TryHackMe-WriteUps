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

## Task 4 Digging into DNS
- Buka halaman web https://viewdns.info/

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2019.JPG)

- **Pertanyaan:** What was RepublicOfKoffee.com's IP address as of October 2016?
- Pada field **IP History** ketikkan nama domain lalu tekan tombol **GO**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2020.JPG)

- Scroll hingga paling bawah hingga menemukan timeline tahun 2016

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2021.JPG)

- **Jawaban:**
```sh
173.248.188.152
```

- **Pertanyaan:** Based on the other domains hosted on the same IP address, what kind of hosting service can we safely assume our target uses?
- Kembali ke halaman utama https://viewdns.info/ lalu pada field **Reverse IP Lookup** dan tekan tombol **GO**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2022.JPG)

- Diketerangan bagian atas tertulis shared hosting

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2023.JPG)

- **Jawaban:**
```sh
shared
```

- **Pertanyaan:** How many times has the IP address changed in the history of the domain?
- Dari hasil pencarian sebelumnya terdapat 4 waktu yaitu tahun 2020, 2019, 2018 dan 2017

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2024.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2025.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2026.JPG)

- **Jawaban:**
```sh
4
```

## Task 5 Taking Off The Training Wheels
- Domain: heat.net 

- **Pertanyaan:** What is the second nameserver listed for the domain?
- Buka halaman web https://lookup.icann.org/en lalu ketikkan nama domain dan tekan tombol **Lookup**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2027.JPG)

- Lihat informasi pada bagian **Domain Information**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2028.JPG)

- **Jawaban:**
```sh
NS2.HEAT.NET
```

- **Pertanyaan:** What IP address was the domain listed on as of December 2011?
- Buka halaman web https://viewdns.info/ kemudian pada field **IP History** isikan nama
domain dan klik tombol **GO**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2029.JPG)

- Lihat IP pada timeline bulan Desember tahun 2011

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2030.JPG)

- **Jawaban:**
```sh
72.52.192.240
```

- **Pertanyaan:** Based on domains that share the same IP, what kind of hosting service is the domain owner using?
- Kembali ke halaman utama https://viewdns.info/ lalu pada field **Reverse IP Lookup** dan tekan tombol **GO**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2031.JPG)

- Diketerangan bagian atas tertulis shared hosting

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2032.JPG)

- **Jawaban:**
```sh
shared
```

- **Pertanyaan:** On what date did was the site first captured by the internet archive? (MM/DD/YY format)
- Buka halaman web https://archive.org/web/ lalu ketikkan nama domain dan tekan tombol **Browse History**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2033.JPG)

- Disini tertulis terekam internet archive sejak tanggal 1 juni 1997

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2034.JPG)

- **Jawaban:**
```sh
06/01/97
```

- **Pertanyaan:** What is the first sentence of the first body paragraph from the final capture of 2001?
- Dari hasil pencarian sebelumnya, pilih timeline tahun 2001

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2035.JPG)

- Record terakhir adalah tanggal 6 juli 2001, pilih tanggal tersebut dan klik link di tanggal tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2036.jpg)

- Scroll ke bawah dan kita menemukan 1 postingan sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2037.JPG)

- **Jawaban:**
```sh
After years of great online gaming, it’s time to say good-bye.
```

- **Pertanyaan:** Using your search engine skills, what was the name of the company that was responsible for the original version of the site?
- Karena web berisi tentang gaming, kita cari di google dengan kata pencarian `heat.net gaming`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2038.JPG)

- Dari hasil pencarian ditemukan SegaSoft

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2039.JPG)

- **Jawaban:**
```sh
segasoft
```

- **Pertanyaan:** What does the first header on the site on the last capture of 2010 say?
- Dari hasil pencarian sebelumnya, pilih timeline tahun 2010

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2040.JPG)

- Record terakhir adalah tanggal 30 Desember 2010, pilih tanggal tersebut dan klik link di tanggal tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2041.jpg)

- Disini tertulis judul postingan

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2042.JPG)

- **Jawaban:**
```sh
Heat.net – Heating and Cooling
```

## Task 6 Taking A Peek Under The Hood Of A Website
- URL: heat.net/36/need-to-hire-a-commercial-heating-contractor

- **Pertanyaan:** How many internal links are in the text of the article?
- Buka halaman web https://archive.org/web/ lalu ketikkan URL diatas dan tekan tombol **Browse History**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2043.JPG)

- Record terakhir adalah tanggal 12 Mei 2023, pilih tanggal tersebut dan klik link di halaman tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2044.jpg)

- Internal link adalah link yang mengarah ke website yang sama. Disini kita berhasil mendapatkan 5 buah link

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2045.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2046.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2047.JPG)

- **Jawaban:**
```sh
5
```

- **Pertanyaan:** How many external links are in the text of the article?
- External link adalah link yang mengarah ke website yang berbeda. Dari hasil pencarian sebelumnya kita hanya menemukan 1 link

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2048.JPG)

- **Jawaban:**
```sh
1
```

- **Pertanyaan:** Website in the article's only external link ( that isn't an ad)
- Buka external link di tab baru dari pertanyaan sebelumnya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2049.JPG)

- **Jawaban:**
```sh
purchase.org
```

- **Pertanyaan:** Try to find the Google Analytics code linked to the site
- Klik kanan pada halaman lalu pilih View Page Source

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2050.jpg)

- Scroll kebawah, disini kita menemukan source code Google Analytics

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2051.JPG)

- **Jawaban:**
```sh
UA-251372-24
```

- **Pertanyaan:** Is the the Google Analytics code in use on another website? Yay or nay
- Buka halaman web https://www.nerdydata.com/ lalu ketikkan code google analytic diatas dan tekan enter

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2052.jpg)

- Hasilnya tidak ada web manapun yang menggunakan code google analytic tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2053.JPG)

- **Jawaban:**
```sh
Nay
```

- **Pertanyaan:** Does the link to this website have any obvious affiliate codes embedded with it? Yay or Nay
- Tidak ditemukan code affiliasi di page source pada pertanyaan sebelumnya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2054.JPG)

- **Jawaban:**
```sh
Panama
```

## Task 7 Final Exam: Connect the Dots
- **Pertanyaan:** Use the tools in Task 4 to confirm the link between the two sites. Try hard to figure it out without the hint.
- Buka halaman web https://viewdns.info/ kemudian pada field **IP History** ketikkan nama domain lalu tekan tombol **GO**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2055.JPG)

- Disini tercantum ownernya adalah Liquid Web

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2056.JPG)

- Jika kita cari lewat google, tipe perusahaannya adalah LLC

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2057.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/WebOSINT/assets/wo%2058.JPG)

- **Jawaban:**
```sh
Liquid Web, L.L.C
```
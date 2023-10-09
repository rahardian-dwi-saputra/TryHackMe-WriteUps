# OhSINT
- TryHackMe Room: https://tryhackme.com/room/ohsint

## Task 1 OhSINT
- Download Task File Terlebih Dahulu

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/OhSINT/assets/osh%201.JPG)

- **Pertanyaan:** What is this user's avatar of?
- Gunakan exiftool untuk menganalisa gambar. Disini kita mendapatkan nama pemilik gambar
```sh
exiftool WindowsXP.jpg
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/OhSINT/assets/osh%202.JPG)

- Sekarang kita search di Google untuk menemukan siapa pemilik gambar tersebut. Disini ditemukan link twitter yang mengarah ke user tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/OhSINT/assets/osh%203.JPG)

- Setelah dibuka, kita menemukan halaman profil akun twitter sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/OhSINT/assets/osh%204.JPG)

- **Jawaban:**
```sh
cat
```

- **Pertanyaan:** What city is this person in?
- Di halaman profil akun twitter, user telah memposting MAC Address WiFi (BSSID) yang dia gunakan

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/OhSINT/assets/osh%205.JPG)

- Selanjutnya buka halaman web https://wigle.net/ dan lakukan registrasi terlebih dahulu jika anda belum memiliki akunnya
- Selanjutnya pilih **View > Basic Search**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/OhSINT/assets/osh%206.jpg)

- Setelah ketikkan BSSID dan pilih tombol **Query**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/OhSINT/assets/osh%207.JPG)

- Geser peta hingga menemukan titik atau lingkaran berwarna ungu lalu zoom in. Disini kita berhasil menemukan titik tersebut berada di kota London

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/OhSINT/assets/osh%208.jpg)

- **Jawaban:**
```sh
London
```

- **Pertanyaan:** What is the SSID of the WAP he connected to?
- Dari hasil pertanyaan sebelumnya, sekarang kita zoom in lagi hingga pembesaran maksimal untuk menemukan SSID WiFi tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/OhSINT/assets/osh%209.JPG)

- **Jawaban:**
```sh
UnileverWiFi
```

- **Pertanyaan:** What is his personal email address?
- Dari hasil pencarian google lainnya kita juga menemukan link yang mengarah ke repository github

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/OhSINT/assets/osh%2010.JPG)

- Di repository github tersebut kita menemukan akun email dari user tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/OhSINT/assets/osh%2011.JPG)

- **Jawaban:**
```sh
OWoodflint@gmail.com
```

- **Pertanyaan:** What site did you find his email address on?
- Dari pertanyaan sebelumnnya kita berhasil menemukan akun email user tersebut di repository github
- **Jawaban:**
```sh
github
```

- **Pertanyaan:** Where has he gone on holiday?
- Dari hasil pencarian google lainnya kita juga menemukan link yang mengarah ke halaman wordpress

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/OhSINT/assets/osh%2012.JPG)

- Di postingan wordpress tersebut dijelaskan bahwa sekarang dia sedang berada di New York

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/OhSINT/assets/osh%2013.JPG)

- **Jawaban:**
```sh
New York
```

- **Pertanyaan:** What is the person's password?
- Klik kanan pada halaman wordpress lalu pilih **View Page Source**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/OhSINT/assets/osh%2014.JPG)

- Disini kita akan menemukan sebuah password

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/OhSINT/assets/osh%2015.JPG)

- **Jawaban:**
```sh
pennYDr0pper.!
```
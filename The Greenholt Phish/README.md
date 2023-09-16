# The Greenholt Phish
- TryHackMe Challenge: https://tryhackme.com/room/phishingemails5fgjlzxc

## Task 1 Challenge
- Gunakan Split View untuk mengakses machine

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%201.jpg)

- **Pertanyaan:** What date was the email received? (answer format: M/DD/YY)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%202.jpg)

- **Jawaban:**
```sh
6/10/20
```

- **Pertanyaan:** Who is the email from?

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%203.jpg)

- **Jawaban:**
```sh
Mr. James Jackson
```

- **Pertanyaan:** What is his email address?

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%204.jpg)

- **Jawaban:**
```sh
info@mutawamarine.com
```

- **Pertanyaan:** What email address will receive a reply to this email?

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%205.jpg)

- **Jawaban:**
```sh
info.mutawamarine@mail.com
```

- **Pertanyaan:** What is the Originating IP?
- Klik **More** kemudian pilih **View Source**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%206.jpg)

- Scroll kebawah sedikit untuk menemukan jawabannya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%207.JPG)

- **Jawaban:**
```sh
192.119.71.157
```

- **Pertanyaan:** Who is the owner of the Originating IP? (Do not include the "." in your answer.)
- Buka website https://who.is/ kemudian ketikkan IP `192.119.71.157` di field pencarian

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%208.JPG)

- Jika sudah tekan enter, maka akan tampil nama organisasi pemilik IP tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%209.jpg)

- **Jawaban:**
```sh
Hostwinds LLC
```

- **Pertanyaan:** What is the SPF record for the Return-Path domain?
- Sender Policy Framework (SPF) digunakan untuk mengautentikasi pengirim email. Dengan adanya catatan SPF, Penyedia Layanan Internet dapat memverifikasi bahwa server email diberi wewenang untuk mengirim email untuk domain tertentu. Data SPF adalah data TXT DNS yang berisi daftar alamat IP yang diizinkan untuk mengirim email atas nama domain Anda.
- Buka kembali View Source dari pertanyaan sebelumnya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%2010.JPG)

- Buka website https://mxtoolbox.com/spf.aspx kemudian ketik nama domain lalu tekan tombol **SPF Record Lookup**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%2011.jpg)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%2012.JPG)

- **v=spf1** → Ini adalah awal dari catatan SPF
- **include:spf.protection.outlook.com** → Ini menentukan domain mana yang dapat mengirim email
- **-all** → Email tidak resmi akan ditolak

- **Jawaban:**
```sh
spf1 include:spf.protection.outlook.com -all
```
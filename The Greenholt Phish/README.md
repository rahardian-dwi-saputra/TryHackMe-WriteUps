# The Greenholt Phish
- TryHackMe Challenge: https://tryhackme.com/room/phishingemails5fgjlzxc

## Studi Kasus
Seorang Sales Executive di Greenholt PLC menerima email yang tidak terduga dari seorang customer. Dia mengklaim bahwa customer tidak pernah menggunakan salam umum seperti "Selamat siang" dan tidak mengharapkan sejumlah uang ditransfer ke rekeningnya. Email tersebut juga berisi lampiran yang tidak pernah dia minta. Dia meneruskan email tersebut ke bagian SOC (Security Operations Center) untuk penyelidikan lebih lanjut.

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

- **Pertanyaan:** What is the DMARC record for the Return-Path domain?
- Domain-based Message Authentication Reporting and Conformance (DMARC) adalah metode otentikasi pesan email
- Klik tanda panah kemudian pilih **DMARC Lookup**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%2013.jpg)

- Kemudian tekan tombol **DMARC Lookup**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%2014.jpg)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%2015.JPG)

- **v=DMARC1** → Harus menggunakan huruf kapital semua, dan ini bukan opsional.
- **p=quarantine** → Jika pemeriksaan gagal, maka email akan dikirim ke folder spam (Kebijakan DMARC).
- **fo** → Menentukan opsi pelaporan kegagalan/forensik.
- **fo=1** → Buat laporan kegagalan/forensik DMARC jika SPF atau DKIM menghasilkan hasil selain lintasan yang selaras.

- **Jawaban:**
```sh
DMARC1; p=quarantine; fo=1
```

- **Pertanyaan:** What is the name of the attachment?
- Buka kembali email dari task sebelumnya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%2016.jpg)

- **Jawaban:**
```sh
SWT_#09674321____PDF__.CAB
```

- **Pertanyaan:** What is the SHA256 hash of the file attachment?
- Tekan tombol Save untuk menyimpan attachment file ke local

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%2017.png)

- Lalu tekan tombol **Save** untuk menyimpan

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%2018.jpg)

- Buka terminal

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%2019.jpg)

- Gunakan tool `sha256sum` untuk mengecek kode hash file
```sh
sha256sum SWT_#09674321____PDF__.CAB
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%2020.JPG)

- **Jawaban:**
```sh
2e91c533615a9bb8929ac4bb76707b2444597ce063d84a4b33525e25074fff3f
```

- **Pertanyaan:** What is the attachments file size? (Don't forget to add "KB" to your answer, NUM KB)
- Ukuran file yang dimaksud bukan ukuran file yang tertera di local
- Copy hash file dari pertanyaan sebelumnya
- Buka website https://www.virustotal.com/gui/home/search kemudian paste hash file di field pencarian

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%2021.jpg)

- Tekan enter kemudian pindah ke tab **Details**, pada **Basic Properties** terdapat informasi **File size** yang merupakan ukuran file sebenarnya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%2022.JPG)

- **Jawaban:**
```sh
400.26 KB
```

- **Pertanyaan:** What is the actual file extension of the attachment?

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/The%20Greenholt%20Phish/assets/tgh%2023.jpg)

- **Jawaban:**
```sh
rar
```
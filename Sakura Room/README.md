# Sakura Room
- TryHackMe Room: https://tryhackme.com/room/sakura

## Task 2 TIP-OFF
- **Pertanyaan:** What username does the attacker go by?
- Akses gambar yang ditinggalkan attacker di link https://raw.githubusercontent.com/OsintDojo/public/3f178408909bc1aae7ea2f51126984a8813b0901/sakurapwnedletter.svg

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%201.JPG)

- Download gambar tersebut ke local
```sh
wget https://raw.githubusercontent.com/OsintDojo/public/3f178408909bc1aae7ea2f51126984a8813b0901/sakurapwnedletter.svg
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%202.JPG)

- Analisis file gambar tersebut dengan exiftool
```sh
exiftool sakurapwnedletter.svg
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%203.JPG)

- **Jawaban:**
```sh
SakuraSnowAngelAiko
```

## Task 3 RECONNAISSANCE
- Gunakan google untuk melakukan pencarian

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%204.JPG)

- **Pertanyaan:** What is the full email address used by the attacker?
- Disini kita berhasil menemukan akun github pelaku

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%205.JPG)

- Sekarang kita buka coba akun github tersebut. Disini ditemukan repository yang berisi kunci PGP

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%206.JPG)

- Buka repository tersebut, disini terdapat 1 file publickey. Klik file tersebut untuk membuka

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%207.JPG)

- Copy semua key dengan menekan tombol copy

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%208.JPG)

- Buka halaman web https://asecuritysite.com/rsa/pgp1 untuk mengkonversi kunci PGP menjadi ASCII

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%209.JPG)

- Hapus semua isi field PGP Public Key Block kemudian paste PGP key yang sudah dicopy lalu klik tombol Determine

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2010.JPG)

- Setelah proses konversi selesai kita berhasil mendapatkan email attacker

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2011.JPG)

- **Jawaban:**
```sh
SakuraSnowAngel83@protonmail.com
```

- **Pertanyaan:** What is the attacker's full real name?
- Selain mendapatkan akun github attacker, kita juga menemukan link akun twitter yang mengarah ke attacker

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2012.JPG)

- Setelah dibuka muncul halaman profil twitter sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2013.JPG)

- Di halaman profil tersebut terdapat tweet tentang pengenalan diri

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2014.JPG)

- **Jawaban:**
```sh
Aiko Abe
```

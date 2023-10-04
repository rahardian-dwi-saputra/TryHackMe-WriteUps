# Sakura Room
- TryHackMe Room: https://tryhackme.com/room/sakura

## Task 2 TIP-OFF
- **Pertanyaan:** What username does the attacker go by?
- Akses gambar yang ditinggalkan attacker di link https://raw.githubusercontent.com/OsintDojo/public/3f178408909bc1aae7ea2f51126984a8813b0901/sakurapwnedletter.svg

- Download gambar tersebut ke local
```sh
wget https://raw.githubusercontent.com/OsintDojo/public/3f178408909bc1aae7ea2f51126984a8813b0901/sakurapwnedletter.svg
```

- Analisis file gambar tersebut dengan exiftool
```sh
exiftool sakurapwnedletter.svg
```

- **Jawaban:**
```sh
SakuraSnowAngelAiko
```

## Task 3 RECONNAISSANCE
- Gunakan google untuk melakukan pencarian

- **Pertanyaan:** What is the full email address used by the attacker?
- Disini kita berhasil menemukan akun github pelaku


- Sekarang kita buka coba akun github tersebut. Disini ditemukan repository yang berisi kunci PGP

- Buka repository tersebut, disini terdapat 1 file publickey. Klik file tersebut untuk membuka

- Copy semua key dengan menekan tombol copy

- Buka halaman web https://asecuritysite.com/rsa/pgp1 untuk mengkonversi kunci PGP menjadi ASCII

- Hapus semua isi field PGP Public Key Block kemudian paste PGP key yang sudah dicopy lalu klik tombol Determine

- Setelah proses konversi selesai kita berhasil mendapatkan email attacker

- **Jawaban:**
```sh
SakuraSnowAngel83@protonmail.com
```

- **Pertanyaan:** What is the attacker's full real name?
- Selain mendapatkan akun github attacker, kita juga menemukan link akun twitter yang mengarah ke attacker

- Setelah dibuka muncul halaman profil twitter sebagai berikut

- Di halaman profil tersebut terdapat tweet tentang pengenalan diri

- **Jawaban:**
```sh
Aiko Abe
```

# Sakura Room
- TryHackMe Room: https://tryhackme.com/room/sakura

## Task 2 TIP-OFF
- **Plotwish:** OSINT Dojo baru-baru ini menjadi korban serangan cyber. Tampaknya tidak ada kerusakan besar, dan tampaknya tidak ada indikator signifikan lainnya yang menunjukkan adanya kompromi pada sistem kami. Namun selama analisis forensik, admin kami menemukan gambar yang ditinggalkan oleh penjahat dunia maya. Mungkinkah ini berisi beberapa petunjuk yang memungkinkan kita menentukan siapa penyerangnya?

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
- **Plotwish:** Tampaknya penyerang kami melakukan kesalahan fatal dalam keamanan operasionalnya. Mereka tampaknya juga menggunakan kembali nama pengguna mereka di platform media sosial lainnya. Hal ini akan memudahkan kami mengumpulkan informasi tambahan tentang mereka dengan menemukan akun media sosial mereka yang lain.

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

## Task 4 UNVEIL
- **Plotwish:** Tampaknya penjahat dunia maya sadar bahwa kita sedang memburu mereka. Saat kami menyelidiki akun Github mereka, kami mengamati indikator bahwa pemilik akun sudah mulai mengedit dan menghapus informasi untuk menghilangkan jejak mereka. Kemungkinan besar mereka menghapus informasi ini karena berisi data yang dapat menambah penyelidikan kami. Mungkin ada cara untuk mendapatkan kembali informasi asli yang mereka berikan?

- Sekarang kita kembali mengamati akun github attacker https://github.com/sakurasnowangelaiko?tab=repositories disini kita menemukan repository yang yang berhubungan dengan cryptocurrency yaitu ETH (Ethereum)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2015.JPG)

- Jika kita buka repository tersebut hanya berisi 1 buah file

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2016.JPG)

- Setelah kita file tersebut, tidak ditemukan informasi apapun disini. Kemudian file ini sudah diubah oleh pemiliknya. Klik History untuk melihat riwayat perubahan file

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2017.JPG)

- Disini hanya ada 1 kali pengubahan. Klik kode hash untuk melihat kondisi file sebelum diubah

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2018.JPG)

- Disini kita berhasil menemukan alamat dompet mata uang kripto dari attacker

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2019.JPG)

- **Pertanyaan:** What cryptocurrency does the attacker own a cryptocurrency wallet for?
- **Jawaban:**
```sh
Ethereum
```

- **Pertanyaan:** What is the attacker's cryptocurrency wallet address?
- **Jawaban:**
```sh
0xa102397dbeeBeFD8cD2F73A89122fCdB53abB6ef
```

- **Pertanyaan:** What mining pool did the attacker receive payments from on January 23, 2021 UTC?
- Searching di google

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2020.JPG)

- Disini kita menemukan web etherscan yang mengarah ke dompet digital attacker

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2021.JPG)

- Setelah dibuka, kita mendapati akun dompet digital beserta riwayat transaksi di bawahnya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2022.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2023.JPG)

- Disini kita berhasil menemukan riwayat transaksi pada tanggal 23 Januari 2023

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2024.JPG)

- Detail transaksi tersebut adalah sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2025.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2026.JPG)

- **Jawaban:**
```sh
Ethermine
```

- **Pertanyaan:** What other cryptocurrency did the attacker exchange with using their cryptocurrency wallet?
- Di riwayat transaksi lain kita juga menemukan, attacker juga menggunakan mata uang tether USDT

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2027.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2028.JPG)

- **Jawaban:**
```sh
Tether
```
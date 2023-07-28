# Solusi - Crack The Hash
- TryHackMe Challenge: [https://tryhackme.com/room/crackthehash](https://tryhackme.com/room/crackthehash)

## Level 1
Bisakah Anda menyelesaikan tugas level 1 dengan memecahkan hash?

### Task 1
- Hash: 48bb6e862e54f2a795ffc4e541caed4d
- Gunakan tool crack hash online [CrackStation](https://crackstation.net/)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Crack%20the%20hash/assets/ch%201.JPG)

- Jawaban:
```sh
easy
```

### Task 2
- Hash: CBFDAC6008F9CAB4083784CBD1874F76618D2A97
- Gunakan tool crack hash online [CrackStation](https://crackstation.net/)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Crack%20the%20hash/assets/ch%202.JPG)

- Jawaban:
```sh
password123
```

### Task 3
- Hash: 1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032
- Gunakan tool crack hash online [CrackStation](https://crackstation.net/)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Crack%20the%20hash/assets/ch%203.JPG)

- Jawaban:
```sh
letmein
```

### Task 4
- Hash: $2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom
- Gunakan tool analisa hash online [Hash Analyzer](https://www.tunnelsup.com/hash-analyzer/) untuk mengetahui jenis algoritma hash yang digunakan
- Gunakan baris perintah `hashcat --help | grep bcrypt` untuk mengetahui mode yang digunakan pada tool hashcat untuk algoritma bcrypt
- Dari format hash yang diberikan dan hasil analisa diatas, maka nomor mode hashcat yang akan digunakan adalah 3200
- Dari petunjuk soal, diketahui bahwa format jawaban hanya terdiri dari 4 karakter. Jadi kita filter wordlists rockyou.txt yang hanya memiliki panjang 4 karakter saja untuk mempersingkat waktu. Baris perintah yang digunakan: `awk 'length($0) == 4' /usr/share/wordlists/rockyou.txt > rockyou-length4.txt`
- Simpan hash kedalam sebuah file dengan baris perintah `echo 'hash' > nama_file`
- Lakukan crack hash dengan baris perintah `hashcat -m 3200 <file hash> <wordlists>`
- Jawaban:
```sh
bleh
```

### Task 5
- Hash: 279412f945939ba78ce0758d3fd83daa
- Gunakan tool crack hash online [CrackStation](https://crackstation.net/)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Crack%20the%20hash/assets/ch%203.JPG)

- Jawaban:
```sh
Eternity22
```

## Level 2
Tugas ini meningkatkan kesulitan. Semua jawaban akan ada di daftar kata sandi rockyou.txt

### Task 1
- Hash: F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85
- Gunakan tool crack hash online [CrackStation](https://crackstation.net/)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Crack%20the%20hash/assets/ch%203.JPG)

- Jawaban:
```sh
paule
```

### Task 2
- Hash: 1DFECA0C002AE40B8619ECF94819CC1B
- Gunakan tool crack hash online [CrackStation](https://crackstation.net/)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Crack%20the%20hash/assets/ch%203.JPG)

- Jawaban:
```sh
n63umy8lkf4i
```

### Task 3
- Hash: $6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02.
- Salt: aReallyHardSalt
- Gunakan tool hashid untuk mengetahui jenis algoritma hash dan mode hashcat yang akan digunakan. Gunakan baris perintah `hashid -m 'hash'`
- Dari hasil analisa diatas, maka nomor mode hashcat yang akan digunakan adalah 1800
- Dari petunjuk soal, diketahui bahwa format jawaban hanya terdiri dari 6 karakter. Jadi kita filter wordlists rockyou.txt yang hanya memiliki panjang 6 karakter saja untuk mempersingkat waktu. Baris perintah yang digunakan `awk 'length($0) == 6' /usr/share/wordlists/rockyou.txt > rockyou-length6.txt`
- Simpan hash kedalam sebuah file dengan baris perintah `echo 'hash' > nama_file`
- Lakukan crack hash dengan baris perintah `hashcat -m 1800 <file hash> <wordlists>`
- Jawaban:
```sh
waka99
```
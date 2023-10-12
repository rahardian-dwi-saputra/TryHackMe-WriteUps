# c4ptur3-th3-fl4g
- TryHackMe Room: https://tryhackme.com/room/c4ptur3th3fl4g

## Task 1 Translation & Shifting

- **Pertanyaan:** c4n y0u c4p7u23 7h3 f149?
- **Jawaban:**
```sh
can you capture the flag?
```

- **Pertanyaan:** 01101100 01100101 01110100 01110011 00100000 01110100 01110010 01111001 00100000 01110011 01101111 01101101 01100101 00100000 01100010 01101001 01101110 01100001 01110010 01111001 00100000 01101111 01110101 01110100 00100001
- Gunakan tool online https://www.rapidtables.com/convert/number/binary-to-ascii.html

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%201.JPG)

- **Jawaban:**
```sh
lets try some binary out!
```

- **Pertanyaan:** MJQXGZJTGIQGS4ZAON2XAZLSEBRW63LNN5XCA2LOEBBVIRRHOM======
- Decode menggunakan base32
```sh
echo 'MJQXGZJTGIQGS4ZAON2XAZLSEBRW63LNN5XCA2LOEBBVIRRHOM======' | base32 -d
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%202.JPG)

- **Jawaban:**
```sh
base32 is super common in CTF's
```

- **Pertanyaan:** RWFjaCBCYXNlNjQgZGlnaXQgcmVwcmVzZW50cyBleGFjdGx5IDYgYml0cyBvZiBkYXRhLg==
- Decode menggunakan base64
```sh
echo 'RWFjaCBCYXNlNjQgZGlnaXQgcmVwcmVzZW50cyBleGFjdGx5IDYgYml0cyBvZiBkYXRhLg==' | base64 -d
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%203.JPG)

- **Jawaban:**
```sh
Each Base64 digit represents exactly 6 bits of data.
```

- **Pertanyaan:** 68 65 78 61 64 65 63 69 6d 61 6c 20 6f 72 20 62 61 73 65 31 36 3f
- Gunakan tool online https://www.rapidtables.com/convert/number/hex-to-ascii.html

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%204.JPG)

- **Jawaban:**
```sh
hexadecimal or base16?
```

- **Pertanyaan:** Ebgngr zr 13 cynprf!
- Format teks ini sepertinya adalah ROT13. ROT13 adalah bentuk Caesar cipher yang diputar sebanyak 13 kali
- Gunakan tool CyberChef https://gchq.github.io/CyberChef/ lalu kita cari ROT13 di field pencarian kemudian tarik ke field recipe

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%205.jpg)

- Masukkan input maka akan diperoleh hasil sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%206.JPG)

- **Jawaban:**
```sh
Rotate me 13 places!
```

- **Pertanyaan:** `*@F DA:? >6 C:89E C@F?5 323J C:89E C@F?5 Wcf E:>6DX`
- Format teks ini sepertinya adalah ROT47. ROT47 adalah bentuk Caesar cipher yang diputar sebanyak 47 kali
- Gunakan tool CyberChef https://gchq.github.io/CyberChef/ lalu kita cari ROT47 di field pencarian kemudian tarik ke field recipe

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%207.jpg)

- Masukkan input maka akan diperoleh hasil sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%208.JPG)

- **Jawaban:**
```sh
You spin me right round baby right round (47 times)
```

- **Pertanyaan:**
```sh
- . .-.. . -.-. --- -- -- ..- -. .. -.-. .- - .. --- -.
. -. -.-. --- -.. .. -. --.
```
- Ini adalah kode morse. Kode morse merupakan kombinasi sinyal yang dibuat dari impuls pendek dan panjang (titik dan garis). Ini dirancang untuk telekomunikasi.
- Gunakan tool CyberChef https://gchq.github.io/CyberChef/ lalu kita cari morse di field pencarian kemudian tarik ke field recipe

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%209.jpg)

- Masukkan input maka akan diperoleh hasil sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2010.JPG)

- **Jawaban:**
```sh
telecommunication encoding
```

- **Pertanyaan:** 85 110 112 97 99 107 32 116 104 105 115 32 66 67 68
- Ini adalah contoh text Binary-Coded Decimal (BCD). Kita tinggal mengkonversi BCD menjadi text biasa (plain text)
- Gunakan tool CyberChef https://gchq.github.io/CyberChef/ lalu kita cari decimal di field pencarian kemudian tarik ke field recipe

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2011.jpg)

- Masukkan input maka akan diperoleh hasil sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2012.JPG)

- **Jawaban:**
```sh
Unpack this BCD
```
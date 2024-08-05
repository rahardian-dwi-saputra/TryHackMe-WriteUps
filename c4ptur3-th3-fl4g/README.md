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

- **Pertanyaan:** 
```sh
LS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0KLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLS0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLi0tLS0KLS0tLS0gLi0tLS0gLi0tLS0gLS0tLS0gLS0tLS0gLi0tLS0gLS0tLS0gLi0tLS0=
```
- Decode menggunakan base64 terlebih dahulu. Maka diperoleh output berupa kode morse

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2013.JPG)

- Tambahkan decode kode morse. Maka disini diperoleh kode biner

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2014.JPG)

- Tambahkan decode kode biner. Maka disini diperoleh teks berformat ROT47

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2015.JPG)

- Tambahkan decode ROT47. Maka disini diperoleh kode BCD

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2016.JPG)

- Tambahkan decode BCD. Maka kita berhasil memperoleh plain text

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2017.JPG)

- **Jawaban:**
```sh
Let's make this a bit trickier...
```

## Task 2 Spectrograms
- Spektogram adalah representasi visual dari spektrum frekuensi sinyal yang bervariasi terhadap waktu. Ketika diterapkan pada sinyal audio, spektogram kadang-kadang disebut sonograf, voiceprints, atau voicegrams. Jika data direpresentasikan dalam plot 3D, data tersebut dapat disebut air terjun.
- Download task file
- Download tool Audacity disini https://www.audacityteam.org/download/linux/ lalu berikan akses execute
```sh
chmod +x audacity-linux-3.3.3-x64.AppImage
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2018.JPG)

- Jalankan tool Audacity
```sh
./audacity-linux-3.3.3-x64.AppImage
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2019.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2020.JPG)

- Drag task file ke tool Audacity

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2021.JPG)

- Klik tanda panah lalu pilih Spectogram, maka akan keluar secret text dibalik file audio tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2022.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2023.JPG)

- **Pertanyaan:** Download the file
- **Jawaban:**
```sh
super secret message
```

## Task 3 Steganography
- Steganografi adalah praktik menyembunyikan file, pesan, gambar, atau video di dalam file, pesan, gambar, atau video lain.
- Download task file
- Gunakan tool steghide untuk mengekstrak steganografi. Saat dimintai password langsung tekan enter
```sh
steghide extract -sf stegosteg.jpg
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2024.JPG)

- Setelah itu kita buka isi file hasil ekstraksi steganografi
```sh
cat steganopayload2248.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2025.JPG)

- **Pertanyaan:** Decode the image to reveal the answer.
- **Jawaban:**
```sh
SpaghettiSteg
```

## Task 4 Security through obscurity
- Download task file
- Gunakan tool `binwalk` untuk menganalisa apakah terdapat file tersembunyi dibalik gambar tersebut. Dari hasil analisa dibalik gambar terdapat 3 buah file tersembunyi
```sh
binwalk meme.jpg 
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2026.JPG)

- Tambahkan opsi `-e` untuk mengekstrak semua file yang tersembunyi
```sh
binwalk meme.jpg -e
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2027.JPG)

- Dari hasil ekstraksi kita menemukan file **hackerchat.png**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2028.JPG)

- Sekarang kita gunakan tool `strings` untuk menganalisa text dibalik gambar tersebut
```sh
strings meme.jpg
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2029.JPG)

- Dibaris terakhir kita menemukan pesan tersembunyi dibalik task file tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/c4ptur3-th3-fl4g/assets/ctf%2030.JPG)

- **Pertanyaan:** Download and get 'inside' the file. What is the first filename & extension?
- **Jawaban:**
```sh
hackerchat.png
```
- **Pertanyaan:** Get inside the archive and inspect the file carefully. Find the hidden text.
- **Jawaban:**
```sh
AHH_YOU_FOUND_ME!
```
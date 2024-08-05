# 0x41haz
- TryHackMe Challenge: https://tryhackme.com/room/0x41haz

## Task 1 Find the password!
- Download Task File terlebih dahulu

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/0x41haz/assets/haz%201.JPG)

- Cek jenis file dengan tool `file` dan disini terdapat keterangan `MSB *unknown arch 0x3e00*`
```sh
file 0x41haz.0x41haz
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/0x41haz/assets/haz%202.JPG)

- Berdasarkan referensi https://pentester.blog/?p=247 kita harus mengubah byte ke 6 menjadi 01 (bilangan hexa)
- Buka file dengan tool hexeditor
```sh
hexeditor 0x41haz.0x41haz
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/0x41haz/assets/haz%203.JPG)

- Ubah byte ke 6 dari **02** menjadi **01** seperti ini

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/0x41haz/assets/haz%204.JPG)

- Kemudian tekan **Ctrl+X** untuk menyimpan dan keluar lalu tekan **enter**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/0x41haz/assets/haz%205.JPG)

- Jika kita cek jenis file kembali maka akan terbaca ELF 64-bit

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/0x41haz/assets/haz%206.JPG)

- Sekarang kita analisa code assembly dengan tool `redare2` dan masuk ke function main
```sh
r2 0x41haz.0x41haz
aaa
s main
pdf
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/0x41haz/assets/haz%207.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/0x41haz/assets/haz%208.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/0x41haz/assets/haz%209.JPG)

- Disini ditemukan rangkaian string yang mungkin ini adalah passwordnya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/0x41haz/assets/haz%2010.JPG)

- Buka terminal baru dan tambahkan permission execute ke file tersebut
```sh
chmod +x 0x41haz.0x41haz
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/0x41haz/assets/haz%2011.JPG)

- Eksekusi file tersebut lalu sekarang kita coba masukkan rangkaian password dan ternyata berhasil. Maka ini adalah passwordnya
```sh
./0x41haz.0x41haz
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/0x41haz/assets/haz%2012.JPG)

- **Pertanyaan:** What is the password? (format: THM{password})

- **Jawaban:**
```sh
THM{2@@25$gfsT&@L}
```
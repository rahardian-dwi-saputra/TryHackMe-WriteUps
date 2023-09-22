# 0x41haz
- TryHackMe Challenge: https://tryhackme.com/room/0x41haz

## Task 1 Find the password!
- Download Task File terlebih dahulu

- Cek jenis file dengan tool `file` dan disini terdapat keterangan `MSB *unknown arch 0x3e00*`
```sh
file 0x41haz.0x41haz
```

- Berdasarkan referensi https://pentester.blog/?p=247 kita harus mengubah byte ke 6 menjadi 01 (bilangan hexa)
- Buka file dengan tool hexeditor
```sh
hexeditor 0x41haz.0x41haz
```

- Ubah byte ke 6 dari **02** menjadi **01** seperti ini


- Kemudian tekan **Ctrl+X** untuk menyimpan dan keluar lalu tekan **enter**

- Jika kita cek jenis file kembali maka akan terbaca ELF 64-bit

- Sekarang kita analisa code assembly dengan tool `redare2`
```sh
r2 0x41haz.0x41haz
```

- Disini ditemukan rangkaian string yang mungkin ini adalah passwordnya

- Buka terminal baru dan tambahkan permission execute ke file tersebut
```sh
chmod +x 0x41haz.0x41haz
```

- Eksekusi file tersebut lalu sekarang kita coba masukkan rangkaian password dan ternyata berhasil. Maka ini adalah passwordnya
```sh
./0x41haz.0x41haz
```


- **Pertanyaan:** What is the password? (format: THM{password})

- **Jawaban:**
```sh
THM{2@@25$gfsT&@L}
```
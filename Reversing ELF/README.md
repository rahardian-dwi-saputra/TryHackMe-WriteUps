# Reversing ELF
- TryHackMe Room: https://tryhackme.com/room/reverselfiles

## Task 1 Crackme1
- Download Task File
- Berikan akses excute pada file tersebut
```sh
chmod +x index.crackme1
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%201.JPG)

- Jalankan program tersebut
```sh
./index.crackme1
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%202.JPG)

- **Pertanyaan:** What is the flag?
- **Jawaban:**
```sh
flag{not_that_kind_of_elf}
```

## Task 2 Crackme2
- Download Task File
- Berikan full akses pada file tersebut
```sh
chmod 777 index.crackme2
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%203.JPG)

- Print semua string yang ada di dalam file tersebut. Disini kita berhasil menemukan sebuah password
```sh
strings index.crackme2
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%204.JPG)

- Eksekusi file tersebut dengan memasukkan password yang sudah ditemukan
```sh
./index.crackme2 super_secret_password
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%205.JPG)

- **Pertanyaan:** What is the super secret password ?
- **Jawaban:**
```sh
super_secret_password
```
- **Pertanyaan:** What is the flag?
- **Jawaban:**
```sh
flag{if_i_submit_this_flag_then_i_will_get_points}
```

## Task 3 Crackme3
- Download Task File
- Berikan full akses pada file tersebut
```sh
chmod 777 index.crackme3
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%206.JPG)

- Print semua string yang ada di dalam file tersebut. Disini kita berhasil menemukan sebuah password yang masih dalam keadaan ter encode
```sh
strings index.crackme3
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%207.JPG)

- Decode password tersebut
```sh
echo 'ZjByX3kwdXJfNWVjMG5kX2xlNTVvbl91bmJhc2U2NF80bGxfN2gzXzdoMW5nNQ==' | base64 -d
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%208.JPG)

- Eksekusi file tersebut dengan memasukkan password yang sudah di decode
```sh
./index.crackme3 f0r_y0ur_5ec0nd_le55on_unbase64_4ll_7h3_7h1ng5
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%209.JPG)

- **Pertanyaan:** What is the flag?
- **Jawaban:**
```sh
f0r_y0ur_5ec0nd_le55on_unbase64_4ll_7h3_7h1ng5
```

## Task 4 Crackme4
- Download Task File
- Berikan full akses pada file tersebut
```sh
chmod 777 index.crackme4
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2010.JPG)

- Eksekusi file tersebut. Setelah dieksekusi disini terdapat petunjuk bahwa file tersebut menggunakan **strcmp**
```sh
./index.crackme4
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2011.JPG)

- Debug program menggunakan tool **ltrace** dan masukkan sembarang password, misalnya kita input password 123456. Disini kita dapat melihat isi string di fungsi strcmp
```sh
ltrace ./index.crackme4 <password>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2012.JPG)

- **Pertanyaan:** What is the password ?
- **Jawaban:**
```sh
my_m0r3_secur3_pwd
```

## Task 5 Crackme5
- Download Task File
- Berikan full akses pada file tersebut
```sh
chmod 777 index.crackme5
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2013.JPG)

- Jika kita jalankan file tersebut, kita akan dimintai input. Disini kita inputkan sembarang string, misalnya 'test'

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2014.JPG)

- Debug program menggunakan tool **ltrace**
```sh
ltrace ./index.crackme5
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2015.JPG)

- Lalu inputkan sembarang string, misalnya test. Maka akan tampil function strncmp yang berisi sebuah password

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2016.JPG)

- **Pertanyaan:** What is the input ?
- **Jawaban:**
```sh
OfdlDSA|3tXb32~X3tX@sX`4tXtz
```
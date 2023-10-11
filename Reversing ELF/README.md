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

## Task 6 Crackme6
- Download Task File
- Berikan full akses pada file tersebut
```sh
chmod 777 index.crackme6
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2017.JPG)

- Debug dengan tool redare2
```sh
r2 -d ./index.crackme6
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2018.JPG)

- Analisa
```sh
aaa
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2019.JPG)

- Menampilkan list function. Disini ditemukan fungsi main
```sh
afl
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2020.JPG)

- Menampilkan isi fungsi main. Disini ditemukan fungsi **sym.compare_pwd**
```sh
pdf @main
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2021.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2022.JPG)

- Masuk ke fungsi **sym.compare_pwd**, disini ditemukan fungsi **sym.my_secure_test**
```sh
pdf @sym.compare_pwd
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2023.JPG)

- Masuk ke fungsi **sym.my_secure_test**. Disini terdapat beberapa proses pencocokan karakter
```sh
pdf @sym.my_secure_test
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2024.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2025.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2026.JPG)

- Kalau dikumpulkan satu per satu akan ketemu pola sebagai berikut
```sh
0x00400597 cmp al, 0x31
0x004005bf cmp al, 0x33
0x004005e7 cmp al, 0x33
0x0040060f cmp al, 0x37
0x00400637 cmp al, 0x5f 
0x0040065f cmp al, 0x70
0x00400684 cmp al, 0x77
0x004006a9 cmp al, 0x64
```
- Sekarang kita gabungkan semua bilangan hexa diatas lalu kita convert ke ASCII di website https://www.rapidtables.com/convert/number/hex-to-ascii.html
```sh
313333375f707764
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2027.JPG)

- **Pertanyaan:** What is the password ?
- **Jawaban:**
```sh
1337_pwd
```

## Task 7 Crackme7
- Download Task File
- Berikan full akses pada file tersebut
```sh
chmod 777 index.crackme7
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2028.JPG)

- Debug dengan tool redare2
```sh
r2 -d ./index.crackme7
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2029.JPG)

- Masuk ke fungsi main
```sh
aaa
afl
pdf @main
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2030.JPG)

- Scroll kebawah, disini kita menemukan proses pencocokan karakter

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2031.JPG)

- Sekarang kita convert bilangan hexa tersebut ke bilangan desimal di website https://www.rapidtables.com/convert/number/hex-to-decimal.html

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2032.JPG)

- Eksekusi file tersebut
```sh
./index.crackme7
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2033.JPG)

- Lalu inputkan bilangan `31337` untuk mendapatkan flag

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2034.JPG)

- **Pertanyaan:** What is the flag ?
- **Jawaban:**
```sh
flag{much_reversing_very_ida_wow}
```

## Task 8 Crackme8
- Download Task File
- Berikan full akses pada file tersebut
```sh
chmod 777 index.crackme8
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2035.JPG)

- Debug dengan tool redare2
```sh
r2 -d ./index.crackme8
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2036.JPG)

- Masuk ke fungsi main
```sh
aaa
afl
pdf @main
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2037.JPG)

- Di fungsi main kita menemukan pecocokan karakter dengan bilangan hexa **0xcafef00d** dan sebelumnya ada pemanggilan fungsi **atoi** untuk mengubah string menjadi bilangan integer

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2038.JPG)

- Konversi bilangan hexa **0xcafef00d** menjadi bilangan desimal di website https://www.rapidtables.com/convert/number/hex-to-decimal.html 

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2039.JPG)

- Jalankan file dengan memasukkan bilangan desimal hasil konversi untuk mendapatkan flag
```sh
./index.crackme8 -889262067
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Reversing%20ELF/assets/rev%2040.JPG)

- **Pertanyaan:** What is the flag ?
- **Jawaban:**
```sh
flag{at_least_this_cafe_wont_leak_your_credit_card_numbers}
```
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
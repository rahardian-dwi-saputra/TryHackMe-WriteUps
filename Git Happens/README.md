# Git Happens
Tryhackme challenge: https://tryhackme.com/room/githappens
IP Machine: 10.10.19.3

## Task 1 Capture the Flag
- Scanning port menggunakan nmap
```sh
nmap -sC -sV -A <IP_Machine> 
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Git%20Happens/assets/gh%201.JPG)

- Port yang terbuka hanya port 80 (Web Server). Sekarang kita coba akses halaman web melalui browser dengan url `http://<IP_Machine>`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Git%20Happens/assets/gh%202.JPG)

- Sekarang kita coba mencari halaman yang tersembunyi dengan menggunakan tool gobuster
```sh
gobuster dir -u http://<IP_Machine> -w /usr/share/wordlists/dirb/common.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Git%20Happens/assets/gh%203.JPG)

- Ditemukan halaman **/.git**, sekarang kita coba akses halaman tersebut di browser dengan url `http://<IP_Machine>/.git`. Ternyata halaman tersebut berisi hasil clonning repository git

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Git%20Happens/assets/gh%204.JPG)

- Kita bisa memanfaatkan GitTools untuk menyalin repository tersebut ke local. Untuk melakukan instalasi cukup jalankan perintah berikut ini
```sh
git clone https://github.com/internetwache/GitTools.git
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Git%20Happens/assets/gh%205.JPG)

- Navigasi ke folder **GitTools/Dumper** tempat program **gitdumper.sh** tersimpan

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Git%20Happens/assets/gh%206.JPG)

- Clonning repository ke local dengan **gitdumper.sh** dan tunggu prosesnya hingga selesai
```sh
./gitdumper.sh http://10.10.19.3/.git/ <path_local>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Git%20Happens/assets/gh%207.JPG)

- Navigasi ke folder hasil clonning kemudian cek status terakhir repository dengan git
```sh
git status
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Git%20Happens/assets/gh%208.JPG)

- Sekarang kita lihat log perubahannya dengan git
```sh
git log
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Git%20Happens/assets/gh%209.JPG)

- Tekan enter untuk menampilkan log berikutnya. Di log selanjutnya terdapat commit kapan halaman login dibuat. Halaman login dibuat pada tanggal 23 Juli 2020. Copy kode hash pada bagian commit untuk menampilkan detail log nya 

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Git%20Happens/assets/gh%2010.JPG)

- Tampilkan detail lognya dengan git
```sh
git show 395e087334d613d5e423cdf8f7be27196a360459
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Git%20Happens/assets/gh%2011.JPG)

- Tekan enter untuk menampilkan log selanjutnya. Pada bagian paling bawah ditemukan username dan password

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Git%20Happens/assets/gh%2012.JPG)

- **Pertanyaan:** Find the Super Secret Password
- **Jawaban:**
```sh
Th1s_1s_4_L0ng_4nd_S3cur3_P4ssw0rd!
```


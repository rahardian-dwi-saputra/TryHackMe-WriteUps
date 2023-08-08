# CTF - h4acked
- TryHackMe Challenge: https://tryhackme.com/room/h4cked
- IP Machine: 10.10.128.226

## Task 1 Oh no! We've been hacked!
- Buka file **capture.pcapng** menggunakan tool Wireshark
- **Pertanyaan:** The attacker is trying to log into a specific service. What service is this?
- Sorting packet berdasarkan protocol, disini kita melihat bahwa attacker berusaha mengakses masuk ke FTP Server

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%201.JPG)

```sh
FTP
```
- **Pertanyaan:** There is a very popular tool by Van Hauser which can be used to brute force a series of services. What is the name of this tool?
- Lakukan pencarian menggunakan google, disini didapat informasi bahwa tool tersebut adalah **thc-hydra** atau lebih dikenal dengan **hydra**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%202.JPG)

- Di kali linux juga sudah terinstall tool hydra secara default. Jika bisa menggunakan perintah `hydra -h` untuk melihat deskripsi dari tool ini  
```sh
hydra
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%203.JPG)

- **Pertanyaan:** The attacker is trying to log on with a specific username. What is the username?
- Kita bisa menerapkan filter **ftp.request** di Wireshark dan disini dapat kita amati bahwa attacker berusaha masuk ke FTP Server dengan Username **jenny**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/h4cked/assets/hk%204.JPG)

```sh
jenny
```
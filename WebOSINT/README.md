# WebOSINT
- TryHackMe Challenge: https://tryhackme.com/room/webosint
- Domain: RepublicOfKoffee.com

## Task 2 Whois Registration

- Buka halaman web https://lookup.icann.org/en lalu ketikkan nama domain dan tekan tombol **Lookup**

- **Pertanyaan:** What is the name of the company the domain was registered with?
- Lihat informasi dibagian **Contact Information**
- **Jawaban:**
```sh
Namecheap Inc
```

- **Pertanyaan:** What phone number is listed for the registration company? (do not include country code or special characters/spaces)
- Lihat informasi dibagian **Raw Registry RDAP Response**
- **Jawaban:**
```sh
6613102107
```

- **Pertanyaan:** What is the first nameserver listed for the site?
- Lihat informasi dibagian **Domain Information**
- **Jawaban:**
```sh
ns1.brainydns.com
```

- **Pertanyaan:** What is listed for the name of the registrant?
- Lihat informasi dibagian **Registrant**
- **Jawaban:**
```sh
redacted for privacy
```

- **Pertanyaan:** What country is listed for the registrant?
- **Jawaban:**
```sh
Panama
```
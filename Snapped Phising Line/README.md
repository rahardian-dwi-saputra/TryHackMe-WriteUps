# The Greenholt Phish
- TryHackMe Challenge: https://tryhackme.com/room/snappedphishingline

## Studi Kasus
Sebagai personil departemen IT SwiftSpend Financial, salah satu tanggung jawab Anda adalah mendukung sesama karyawan dalam masalah teknis mereka. Meskipun semuanya tampak biasa dan biasa saja, hal ini berangsur-angsur berubah ketika beberapa karyawan dari berbagai departemen mulai melaporkan email tidak biasa yang mereka terima. Sayangnya, beberapa sudah mengirimkan kredensial mereka dan tidak bisa login lagi. Anda sekarang melanjutkan untuk menyelidiki apa yang terjadi dengan:

- Menganalisis sampel email yang diberikan oleh kolega Anda
- Menganalisis URL phishing dengan browser Firefox
- Mengambil kit phishing yang digunakan oleh musuh
- Menggunakan peralatan terkait CTI untuk mengumpulkan lebih banyak informasi tentang musuh
- Menganalisis perangkat phishing untuk mengumpulkan lebih banyak informasi tentang musuh

## Task 1 Challenge Scenario
- Gunakan Split View untuk mengakses machine

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%201.jpg)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%202.JPG)

- **Pertanyaan:** Who is the individual who received an email attachment containing a PDF?
- Buka sample email di folder **phis-emails**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%203.jpg)

- Double klik file untuk membuka. Anda bisa mencoba membuka satu-persatu untuk menemukan file email yang mengandung lampiran file berekstensi PDF

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%204.jpg)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%205.jpg)

- **Jawaban:**
```sh
William McClean
```

- **Pertanyaan:** What email address was used by the adversary to send the phishing emails?

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%206.jpg)

- **Jawaban:**
```sh
Accounts.Payable@groupmarketingonline.icu
```

- **Pertanyaan:** What is the redirection URL to the phishing page for the individual Zoe Duncan? (defanged format)
- Buka file email Zoe Duncan

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%207.jpg)

- Tekan tombol **Save** untuk mendownload lampiran file

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%208.jpg)

- Simpan lampiran file di **Desktop > phis-emails** lalu tekan tombol save

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%209.jpg)

- Buka terminal

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2010.jpg)

- Buka lampiran file yang tersimpan dengan perintah `cat <nama_file>`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2011.JPG)

- Copy URL redirect yang ada di file tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2012.JPG)

- Buka tool [Cyber Chef](https://gchq.github.io/CyberChef/) kemudian search 'defang'

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2013.jpg)

- Paste URL tadi di field Input untuk mengkonversi ke format defang 

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2014.JPG)

- **Jawaban:**
```sh
hxxp[://]kennaroads[.]buzz/data/Update365/office365/40e7baa2f826a57fcf04e5202526f8bd/?email=zoe[.]duncan@swiftspend[.]finance&error
```

- **Pertanyaan:** What is the URL to the .zip archive of the phishing kit? (defanged format)
- Buka url `http://kennaroads.buzz/data` dengan Firefox

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2015.JPG)

- Klik kanan pada file **Update365.zip** kemudian pilih Copy Link

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2016.jpg)

- Kemudian paste url tersebut tool [Cyber Chef](https://gchq.github.io/CyberChef/) dari pertanyaan sebelumnya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2017.JPG)

- **Jawaban:**
```sh
hxxp[://]kennaroads[.]buzz/data/Update365[.]zip
```

- **Pertanyaan:** What is the SHA256 hash of the phishing kit archive?
- Double klik file **Update365.zip** untuk mendownload

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2018.JPG)

- Buka terminal lalu arahkan ke directory **Downloads** dan cek menggunakan tool sha256sum
```sh
sha256sum <nama_file>
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2019.JPG)

- **Jawaban:**
```sh
ba3c15267393419eb08c7b2652b8b6b39b406ef300ae8a18fee4d16b19ac9686
```

- **Pertanyaan:** When was the phishing kit archive first submitted? (format: YYYY-MM-DD HH:MM:SS UTC)
- Copy hash dari pertanyaan sebelumnya
- Buka website Virus Total: https://www.virustotal.com/gui/home/search lalu paste hash di field pencarian dan tekan enter

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2020.jpg)

- Setelah pindah ke tab **Details**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2021.JPG)

- Pada bagian history terdapat informasi kapan file ini disubmit pertama kali

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2022.JPG)

- **Jawaban:**
```sh
2020-04-08 21:55:50 UTC
```

- **Pertanyaan:** When was the phishing domain that was used to host the phishing kit archive first registered? (format: YYYY-MM-DD)
- Buka website [ThreatBook CTI](https://threatbook.io/) dan ketikkan domain di field pencarian lalu tekan tombol search

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2023.jpg)

- Setelah hasil pencarian muncul pindah ke tab Whois

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2024.jpg)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2025.JPG)

- **Jawaban:**
```sh
2020-06-25
```

- **Pertanyaan:** What was the email address of the user who submitted their password twice?
- Buka halaman http://kennaroads.buzz/data/Update365/ klik file **log.txt** untuk membuka

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2026.jpg)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2027.JPG)

- **Jawaban:**
```sh
michael.ascot@swiftspend.finance
```

- **Pertanyaan:** What was the email address used by the adversary to collect compromised credentials?
- Di pertanyaan sebelumnya kita sudah mendownload file **Update365.zip** jadi sekarang kita tinggal mengekstraknya saja
- Buka terminal dan ekstrak file **Update365.zip**
```sh
cd Downloads
unzip Update365.zip
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2028.JPG)

- Setelah itu kita cari semua file yang mengandung email dengan tool grep
```sh
grep -rEi "[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}" Update365
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2029.JPG)

- Disini kita menemukan file **submit.php** yang berada file folder **Update365/office365/Validation**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2030.JPG)

- Sekarang kita coba buka file tersebut di File Explorer

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2031.png)

- Klik kanan file tersebut kemudian pilih Open With Text Editor

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2032.jpg)

- Setelah ditelusuri ternyata email tersebut akan menerima pesan yang berisi email dan password dari hasil phising

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2033.JPG)

- **Jawaban:**
```sh
m3npat@yandex.com
```

- **Pertanyaan:** The adversary used other email addresses in the obtained phishing kit. What is the email address that ends in "@gmail.com"?
- Jawaban sudah ada dipertanyaan sebelumnya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2034.JPG)

- **Jawaban:**
```sh
jamestanner2299@gmail.com
```

- **Pertanyaan:** What is the hidden flag?
- Buka halaman http://kennaroads.buzz/data/Update365/office365/flag.txt di Firefox kemudian copy secret tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2035.JPG)

- Buka tool [Cyber Chef](https://gchq.github.io/CyberChef/) kemudian drag opsi **From Base64** dan drop kolom Recipe

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2036.jpg)

- Kemudian encode secret tersebut. Setelah itu copy hasil encode secret tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2037.JPG)

- Hapus Recipe kemudian ketik **reverse** di field pencarian dan drag lalu drop di field Recipe

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2038.jpg)

- Reverse hasil encode sebelumnya untuk mendapatkan flag

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Snapped%20Phising%20Line/assets/spl%2039.JPG)

- **Jawaban:**
```sh
THM{pL4y_w1Th_tH3_URL}
```
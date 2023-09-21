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



- **Pertanyaan:** Who is the individual who received an email attachment containing a PDF?
- Buka sample email di folder **phis-emails**



- Double klik file untuk membuka. Anda bisa mencoba membuka satu-persatu untuk menemukan file email yang mengandung lampiran file berekstensi PDF

- **Jawaban:**
```sh
William McClean
```

- **Pertanyaan:** What email address was used by the adversary to send the phishing emails?



- **Jawaban:**
```sh
Accounts.Payable@groupmarketingonline.icu
```

- **Pertanyaan:** What is the redirection URL to the phishing page for the individual Zoe Duncan? (defanged format)
- Buka file email Zoe Duncan

- Tekan tombol **Save** untuk mendownload lampiran file

- Simpan lampiran file di **Desktop > phis-emails** lalu tekan tombol save

- Buka terminal

- Buka lampiran file yang tersimpan dengan perintah `cat <nama_file>`

- Copy URL redirect yang ada di file tersebut

- Buka tool [Cyber Chef](https://gchq.github.io/CyberChef/) kemudian search 'defang'

- Paste URL tadi di field Input untuk mengkonversi ke format defang 

- **Jawaban:**
```sh
hxxp[://]kennaroads[.]buzz/data/Update365/office365/40e7baa2f826a57fcf04e5202526f8bd/?email=zoe[.]duncan@swiftspend[.]finance&error
```

- **Pertanyaan:** What is the URL to the .zip archive of the phishing kit? (defanged format)
- Buka url `http://kennaroads.buzz/data` dengan Firefox

- Klik kanan pada file **Update365.zip** kemudian pilih Copy Link


- Kemudian paste url tersebut tool [Cyber Chef](https://gchq.github.io/CyberChef/) dari pertanyaan sebelumnya

- **Jawaban:**
```sh
hxxp[://]kennaroads[.]buzz/data/Update365[.]zip
```

- **Pertanyaan:** What is the SHA256 hash of the phishing kit archive?
- Double klik file **Update365.zip** untuk mendownload

- Buka terminal lalu arahkan ke directory **Downloads** dan cek menggunakan tool sha256sum
```sh
sha256sum <nama_file>
```

- **Jawaban:**
```sh
ba3c15267393419eb08c7b2652b8b6b39b406ef300ae8a18fee4d16b19ac9686
```

- **Pertanyaan:** When was the phishing kit archive first submitted? (format: YYYY-MM-DD HH:MM:SS UTC)
- Copy hash dari pertanyaan sebelumnya
- Buka website Virus Total: https://www.virustotal.com/gui/home/search lalu paste hash di field pencarian dan tekan enter

- Setelah pindah ke tab **Details**

- Pada bagian history terdapat informasi kapan file ini disubmit pertama kali

- **Jawaban:**
```sh
2020-04-08 21:55:50 UTC
```

- **Pertanyaan:** When was the phishing domain that was used to host the phishing kit archive first registered? (format: YYYY-MM-DD)

- **Jawaban:**
```sh
x
```

- **Pertanyaan:** What was the email address of the user who submitted their password twice?

- **Jawaban:**
```sh
x
```

- **Pertanyaan:** What was the email address used by the adversary to collect compromised credentials?

- **Jawaban:**
```sh
x
```

- **Pertanyaan:** The adversary used other email addresses in the obtained phishing kit. What is the email address that ends in "@gmail.com"?

- **Jawaban:**
```sh
x
```

- **Pertanyaan:** What is the hidden flag?

- **Jawaban:**
```sh
x
```

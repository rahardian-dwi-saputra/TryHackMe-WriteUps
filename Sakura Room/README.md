# Sakura Room
- TryHackMe Room: https://tryhackme.com/room/sakura

## Task 2 TIP-OFF
- **Plotwish:** OSINT Dojo baru-baru ini menjadi korban serangan cyber. Tampaknya tidak ada kerusakan besar, dan tampaknya tidak ada indikator signifikan lainnya yang menunjukkan adanya kompromi pada sistem kami. Namun selama analisis forensik, admin kami menemukan gambar yang ditinggalkan oleh penjahat dunia maya. Mungkinkah ini berisi beberapa petunjuk yang memungkinkan kita menentukan siapa penyerangnya?

- **Pertanyaan:** What username does the attacker go by?
- Akses gambar yang ditinggalkan attacker di link https://raw.githubusercontent.com/OsintDojo/public/3f178408909bc1aae7ea2f51126984a8813b0901/sakurapwnedletter.svg

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%201.JPG)

- Download gambar tersebut ke local
```sh
wget https://raw.githubusercontent.com/OsintDojo/public/3f178408909bc1aae7ea2f51126984a8813b0901/sakurapwnedletter.svg
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%202.JPG)

- Analisis file gambar tersebut dengan exiftool
```sh
exiftool sakurapwnedletter.svg
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%203.JPG)

- **Jawaban:**
```sh
SakuraSnowAngelAiko
```

## Task 3 RECONNAISSANCE
- **Plotwish:** Tampaknya penyerang kami melakukan kesalahan fatal dalam keamanan operasionalnya. Mereka tampaknya juga menggunakan kembali nama pengguna mereka di platform media sosial lainnya. Hal ini akan memudahkan kami mengumpulkan informasi tambahan tentang mereka dengan menemukan akun media sosial mereka yang lain.

- Gunakan google untuk melakukan pencarian

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%204.JPG)

- **Pertanyaan:** What is the full email address used by the attacker?
- Disini kita berhasil menemukan akun github pelaku

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%205.JPG)

- Sekarang kita buka coba akun github tersebut. Disini ditemukan repository yang berisi kunci PGP

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%206.JPG)

- Buka repository tersebut, disini terdapat 1 file publickey. Klik file tersebut untuk membuka

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%207.JPG)

- Copy semua key dengan menekan tombol copy

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%208.JPG)

- Buka halaman web https://asecuritysite.com/rsa/pgp1 untuk mengkonversi kunci PGP menjadi ASCII

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%209.JPG)

- Hapus semua isi field PGP Public Key Block kemudian paste PGP key yang sudah dicopy lalu klik tombol Determine

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2010.JPG)

- Setelah proses konversi selesai kita berhasil mendapatkan email attacker

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2011.JPG)

- **Jawaban:**
```sh
SakuraSnowAngel83@protonmail.com
```

- **Pertanyaan:** What is the attacker's full real name?
- Selain mendapatkan akun github attacker, kita juga menemukan link akun twitter yang mengarah ke attacker

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2012.JPG)

- Setelah dibuka muncul halaman profil twitter sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2013.JPG)

- Di halaman profil tersebut terdapat tweet tentang pengenalan diri

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2014.JPG)

- **Jawaban:**
```sh
Aiko Abe
```

## Task 4 UNVEIL
- **Plotwish:** Tampaknya penjahat dunia maya sadar bahwa kita sedang memburu mereka. Saat kami menyelidiki akun Github mereka, kami mengamati indikator bahwa pemilik akun sudah mulai mengedit dan menghapus informasi untuk menghilangkan jejak mereka. Kemungkinan besar mereka menghapus informasi ini karena berisi data yang dapat menambah penyelidikan kami. Mungkin ada cara untuk mendapatkan kembali informasi asli yang mereka berikan?

- Sekarang kita kembali mengamati akun github attacker https://github.com/sakurasnowangelaiko?tab=repositories disini kita menemukan repository yang yang berhubungan dengan cryptocurrency yaitu ETH (Ethereum)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2015.JPG)

- Jika kita buka repository tersebut hanya berisi 1 buah file

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2016.JPG)

- Setelah kita file tersebut, tidak ditemukan informasi apapun disini. Kemudian file ini sudah diubah oleh pemiliknya. Klik History untuk melihat riwayat perubahan file

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2017.JPG)

- Disini hanya ada 1 kali pengubahan. Klik kode hash untuk melihat kondisi file sebelum diubah

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2018.JPG)

- Disini kita berhasil menemukan alamat dompet mata uang kripto dari attacker

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2019.JPG)

- **Pertanyaan:** What cryptocurrency does the attacker own a cryptocurrency wallet for?
- **Jawaban:**
```sh
Ethereum
```

- **Pertanyaan:** What is the attacker's cryptocurrency wallet address?
- **Jawaban:**
```sh
0xa102397dbeeBeFD8cD2F73A89122fCdB53abB6ef
```

- **Pertanyaan:** What mining pool did the attacker receive payments from on January 23, 2021 UTC?
- Searching di google

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2020.JPG)

- Disini kita menemukan web etherscan yang mengarah ke dompet digital attacker

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2021.JPG)

- Setelah dibuka, kita mendapati akun dompet digital beserta riwayat transaksi di bawahnya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2022.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2023.JPG)

- Disini kita berhasil menemukan riwayat transaksi pada tanggal 23 Januari 2021

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2024.JPG)

- Detail transaksi tersebut adalah sebagai berikut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2025.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2026.JPG)

- **Jawaban:**
```sh
Ethermine
```

- **Pertanyaan:** What other cryptocurrency did the attacker exchange with using their cryptocurrency wallet?
- Di riwayat transaksi lain kita juga menemukan, attacker juga menggunakan mata uang tether USDT

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2027.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2028.JPG)

- **Jawaban:**
```sh
Tether
```

## Task 5 TAUNT
- **Plotwish:** Seperti yang kami duga, penjahat dunia maya menyadari sepenuhnya bahwa kami mengumpulkan informasi tentang mereka setelah serangan mereka. Mereka bahkan dengan berani mengirimkan pesan ke OSINT Dojo di Twitter dan mengejek upaya kami. Akun Twitter yang mereka gunakan tampaknya menggunakan nama pengguna yang berbeda dari yang kami lacak sebelumnya, mungkin ada beberapa informasi tambahan yang dapat kami temukan untuk mendapatkan gambaran kemana tujuan mereka selanjutnya?

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2030.png)

- **Pertanyaan:** What is the attacker's current Twitter handle?
- Di Task 3 kita berhasil menemukan akun twitter attacker. Yang kebetulan foto profilnya sama dengan tangkapan layar diatas

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2013.JPG)

- **Jawaban:**
```sh
SakuraLoverAiko
```

- **Pertanyaan:** What is the URL for the location where the attacker saved their WiFi  SSIDs and passwords?
- Buka kembali halaman profil twitter attacker yang berhasil ditemukan di https://twitter.com/SakuraLoverAiko
- Di halaman profil tersebut, attacker pernah memposting tweet tentang informasi di Dark Web. Tweet tersebut berisi md5sum untuk mengakses konten di Dark Web

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2029.JPG)

- Di petunjuk soal juga diperoleh tangkapan layar dari Dark Web di link https://raw.githubusercontent.com/OsintDojo/public/main/deeppaste.png

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2031.png)

- Dari 2 petunjuk diatas kita dapat menemukan URL dimana attacker menyimpan SSID dan password WiFi
- **Jawaban:**
```sh
http://deepv2w7p33xa4pwxzwi2ps4j62gfxpyp44ezjbmpttxz3owlsp4ljid.onion/show.php?md5=b2b37b3c106eb3f86e2340a3050968e2
```

- **Pertanyaan:** What is the BSSID for the attacker's Home WiFi?
- Buka halaman web https://wigle.net/ dan lakukan registerasi terlebih dahulu jika anda belum memiliki akunnya
- Pilih View > Basic Search

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2032.jpg)

- Ketikkan kata pencarian `dk1f-g` di bagian field SSD kemudian tekan tombol Query. Untuk menemukan hasil pencarian anda harus menggeser peta secara manual ke negara Jepang

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2033.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2034.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2035.JPG)

- Disini kita berhasil menemukan BSSID dari WiFi yang digunakan oleh attacker

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2036.JPG)

- **Jawaban:**
```sh
84:AF:EC:34:FC:F8
```

## Task 6 HOMEBOUND
- **Plotwish:** Berdasarkan tweet mereka, nampaknya penjahat dunia maya kita memang pulang ke rumah seperti yang mereka klaim. Akun Twitter mereka tampaknya memiliki banyak foto yang memungkinkan kami mengetahui rute pulang mereka. Jika kita mengikuti jejak rumah yang mereka tinggalkan, kita seharusnya bisa melacak pergerakan mereka dari satu lokasi ke lokasi berikutnya hingga ke tujuan akhirnya. Setelah kami dapat mengidentifikasi perhentian terakhir mereka, kami dapat mengidentifikasi ke organisasi penegak hukum mana kami harus meneruskan temuan kami.

- **Pertanyaan:** What airport is closest to the location the attacker shared a photo from prior to getting on their flight?
- Attacker telah memposting sebuah foto sebelum dia pulang

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2037.JPG)

- Download foto yang dibagikan di postingan tersebut. Kemudian buka website https://yandex.com/images dan klik icon camera untuk upload gambar

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2038.JPG)

- Kemudian seleksi pada bagian ini. Lalu tekan tombol done

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2039.JPG)

- Dari hasil penelusuran yang muncul, ternyata itu adalah menara Monumen Washington

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2040.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2041.JPG)

- Sekarang kita tahu bahwa foto tersebut diambil di bandara yang dekat dengan Monumen Washington. Sekarang kita bisa cari tahu bandara apa yang dekat dengan monumen tersebut lewat google

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2042.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2043.JPG)

- **Jawaban:**
```sh
DCA
```

- **Pertanyaan:** What airport did the attacker have their last layover in?
- Attacker juga telah memposting dimana ia terakhir kali singgah

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2044.JPG)

- Download foto yang dibagikan di postingan tersebut. Sekarang kita gunakan pencarian gambar lewat google. Tekan icon camera pada field pencarian

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2045.JPG)

- Kemudian upload gambar yang sudah di download tadi

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2046.JPG)

- Disini muncul beberapa hasil pencarian. Kita bisa memilih satu per satu untuk menemukan informasi. Misalnya kita memilih informasi dari halaman web singleflyer yang muncul di pencarian

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2047.JPG)

- Di web ini tertulis code bandaranya adalah HND

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2048.JPG)

- **Jawaban:**
```sh
HND
```

- **Pertanyaan:** What lake can be seen in the map shared by the attacker as they were on their final flight home?
- Attacker juga telah memposting sebuah peta yang dekat dengan rumahnya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2049.JPG)

- Jika kita cocokkan dengan google maps. Peta ini mirip dengan peta Jepang, dimana disisi kiri terdapat sebuah pulau kemudian terdapat sebuah danau di tengahnya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2050.JPG)

- Kita tinggal zoom peta tersebut untuk mengetahui nama danau

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Sakura%20Room/assets/sr%2051.JPG)

- **Jawaban:**
```sh
lake Inawashiro
```

- **Pertanyaan:** What city does the attacker likely consider "home"?
- Di task 5 pertanyaan terakhir, kita berhasil memvisualisasikan dimana lokasi SSID WiFi yang attacker gunakan dan juga dari hasil investigasi diatas menunjukkan bahwa attacker telah pulang ke rumahnya di Jepang. Jadi bisa disimpulkan bahwa lokasi SSID WiFi itu sendiri kemungkinan adalah rumahnya attacker 
- **Jawaban:**
```sh
hirosaki
```
# Investigating Windows
Tryhackme room: https://tryhackme.com/room/investigatingwindows

## Studi Kasus
Mesin windows telah diretas, tugas Anda adalah menyelidiki mesin windows ini dan menemukan petunjuk tentang apa yang mungkin dilakukan oleh peretas.

## Task 1 Investigating Windows
- Gunakan tool remmina untuk menghubungkan Kali Linux ke Windows
- Gunakan perintah dibawah ini untuk menginstall aplikasi remmina di Kali Linux
```sh
sudo apt-get update
sudo apt-get install remmina remmina-plugin-rdp remmina-plugin-secret
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%200.JPG)

- Buka aplikasi remmina lalu ketikkan IP machine dan tekan enter

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%201.JPG)

- Isi username dan password sesuai petunjuk di soal kemudian tekan **OK**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%202.JPG)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%203.JPG)

- **Pertanyaan:** Whats the version and year of the windows machine?
- Klik Start dan buka Command Prompt (cmd)

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%204.png)

- Kemudian ketikkan perintah ini
```sh
systeminfo
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%205.JPG)

- **Jawaban**
```sh
Windows Server 2016
```

- **Pertanyaan:** Which user logged in last?
- Klik Start kemudian pilih Event Viewer

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%206.png)

- Lalu pilih **Windows Logs > Security** kemudian cari task dengan kategori Logon

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%207.JPG)

- Double klik task tersebut untuk menampilkan detailnya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%208.JPG)

- **Jawaban**
```sh
Administrator
```

- **Pertanyaan:** When did John log onto the system last?
- Buka Command Prompt (cmd) dan ketik perintah dibawah ini
```sh
net user John
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%209.png)

- **Jawaban**
```sh
03/02/2019 5:48:32 PM
```

- **Pertanyaan:** What IP does the system connect to when it first starts?
- Klik Start lalu Search 'regedit'

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2010.JPG)

- Pergi ke path **HKEY_LOCAL_MACHINE > SOFTWARE > Microsoft > Windows > CurrentVersion > Run**. Pada **UpdateSvc** terdapat alamat IP yang terhubung dengan sistem

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2011.JPG)

- **Jawaban**
```sh
10.34.2.3
```

- **Pertanyaan:** What two accounts had administrative privileges (other than the Administrator user)?
- Klik Start dan pilih Windows PowerShell

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2012.jpg)

- Lalu ketikkan perintah berikut
```sh
Get-LocalGroupMember -Group "Administrators"
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2013.JPG)

- **Jawaban**
```sh
Jenny,Guest
```

- **Pertanyaan:** Whats the name of the scheduled task that is malicous.
- Klik Start dan search 'Task Scheduler'

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2014.JPG)

- Kemudian pilih Task Scheduler Library dan disana terdapat task **Clean file system** yang berjalan setiap hari

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2015.JPG)

- **Jawaban**
```sh
Clean file system
```

- **Pertanyaan:** What file was the task trying to run daily?
- Double klik task **Clean file system** untuk menampilkan detailnya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2016.JPG)

- Kemudian pindah ke **Actions**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2017.jpg)

- **Jawaban**
```sh
nc.ps1
```

- **Pertanyaan:** What port did this file listen locally for?

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2018.jpg)

- **Jawaban**
```sh
1348
```

- **Pertanyaan:** When did Jenny last logon?
- Buka Command Prompt (cmd) dan ketik perintah dibawah ini
```sh
net user Jenny
```

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2019.jpg)

- **Jawaban**
```sh
Never
```

- **Pertanyaan:** At what date did the compromise take place?
- Buka File Explorer dan buka Local Disk (C:) kemudian perhatikan **Data modified** di masing-masing folder. Tanggal yang muncul terbanyak adalah jawabannya

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2020.JPG)

- **Jawaban**
```sh
03/02/2019
```

- **Pertanyaan:** During the compromise, at what time did Windows first assign special privileges to a new logon?
- Klik Start kemudian pilih Event Viewer

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%206.png)

- Kemudian klik Create Custom View

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2021.jpg)

- Kemudian pada Field Logged pilih Custom range ...

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2022.JPG)

- Kemudian pada field From dan To pilih Events On

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2023.JPG)

- Dari pertanyaan sebelumnya kita tahu bahwa serangan terjadi di tanggal 2 Maret 2019, jadi kita bisa memasukkan tanggal tersebut. Kemudian dari pertanyaan terakhir kita tahu pukul berapa berapa serangan itu terjadi, jadi kita bisa menggunakan perkiraan waktu pukul 4:00 PM hingga 4:30 PM lalu tekan OK

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2024.JPG)

- Pada Event Logs pilih **Windows Logs > Security**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2025.JPG)

- Jika sudah tekan OK

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2026.JPG)

- Kemudian muncul pop up untuk memberi nama view, tekan OK

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2027.JPG)

- Cari task dengan kategori **Security Group Management**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2028.JPG)

- **Jawaban**
```sh
03/02/2019 4:04:47 PM
```

- **Pertanyaan:** What tool was used to get Windows passwords?
- Buka File Explorer lalu buka **Local Disk (C:) > TMP**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2029.JPG)

- Buka file **mim-out**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2030.JPG)

- **Jawaban**
```sh
mimikatz
```

- **Pertanyaan:** What was the attackers external control and command servers IP?
- Buka File Explorer dan pergi ke path **C:\ > Windows > System32 > drivers > etc**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2031.JPG)

- Double klik file **hosts** kemudian pilih Notepad dan tekan OK

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2032.JPG)

- Di file ini, kita bisa menemukan domain google.com yang seharusnya tidak perlu ditambahkan karena host bisa mengaksesnya langsung lewat internet. Bisa jadi ini cara attacker menyamarkan server mereka lewat

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2033.JPG)

- Kemudian kita coba lakukan ping ke google.com di Command Prompt. Ternyata langsung diarahkan ke IP yang terdapat di file hosts

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2034.JPG)

- **Jawaban**
```sh
76.32.97.132
```

- **Pertanyaan:** What was the extension name of the shell uploaded via the servers website?
- Buka File Explorer dan buka **Local Disk (C:)**. Disini terdapat satu folder yang mencurigakan yaitu **inetpub** yang biasanya tidak terdapat di directory C:

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2035.JPG)

- Setelah dibuka terdapat satu folder yaitu **wwwroot**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2036.JPG)

- Didalam folder **wwwroot** terdapat beberapa file berekstensi .jsp

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2037.JPG)

- **Jawaban**
```sh
.jsp
```

- **Pertanyaan:** What was the last port the attacker opened?
- Klik Start dan Search 'firewall'

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2038.JPG)

- Pilih **Inbound Rules** kemudian tekan tanda panah pada **Filter by Group**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2039.JPG)

- Kemudian pilih **Rules Without a Group** yang berada di baris paling bawah

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2040.JPG)

- Kemudian double klik **Allow outside connections for development**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2041.JPG)

- Maka akan muncul pop up seperti gambar dibawah ini

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2042.JPG)

- Setelah itu pindah ke tab **Protocols and Ports**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2043.JPG)

- **Jawaban**
```sh
1337
```

- **Pertanyaan:** Check for DNS poisoning, what site was targeted?
- Di file **hosts** dari pertanyaan sebelumnya sudah cukup jelas

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Investigating%20Windows/assets/iw%2044.jpg)

- **Jawaban**
```sh
google.com
```
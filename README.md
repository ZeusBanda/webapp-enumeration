# WebApp Enumeration Commands
List of commands to run when performing webapp enumeration.

## Perform Vhost Enumeration
```zsh
ffuf -ic -w /usr/share/secLists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://<Target:PORT>/ -H 'HOST: FUZZ.<target.domain>'
```
or 
```zsh
cat /usr/share/seclists/Discovery/DNS/namelist.txt | while read vhost;do echo "\n********\nFUZZING: ${vhost}\n********";curl -s -I http://<IP> -H "HOST: ${vhost}.<target.domain>" | grep "Content-Length: ";done
```

## Directory Fuzzing
```zsh
ffuf -ic -w /usr/share/secLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://<SIP:PORT>/FUZZ
```

## Web apge Fuzzing
Fine the extension the server uses
```zsh
ffuf -ic -w /usr/share/secLists/Discovery/Web-Content/web-extensions.txt:FUZZ -u http://<IP:PORT>/<Directory>/indexFUZZ

```
Make note of what returns a 200 response code.

Page Fuzzing
```zsh
ffuf -ic -w /usr/share/secLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://<IP:PORT>/<Directory>/FUZZ.<ext> -v
```

Recursive Fuzzing
```zsh
ffuf -ic -w /usr/share/secLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://<IP:PORT>/<Directory>/FUZZ -recursion -recursion-depth 1 -e <ext> -v
```

## Subdomain Enumeration
ffuf -ic -w /usr/share/secLists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://FUZZ.<target.domain>/

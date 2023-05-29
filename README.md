# WebApp Enumeration Commands
List of commands to run when performing webapp enumeration.

## Perform Vhost Enumeration
```zsh
ffuf -ic -w /usr/share/seclists/Discovery/DNS/namelist.txt -u http://<IP> -H "HOST: FUZZ.<target.domain>"
```
or 
```zsh
cat /usr/share/seclists/Discovery/DNS/namelist.txt | while read vhost;do echo "\n********\nFUZZING: ${vhost}\n********";curl -s -I http://<IP> -H "HOST: ${vhost}.<target.domain>" | grep "Content-Length: ";done
```



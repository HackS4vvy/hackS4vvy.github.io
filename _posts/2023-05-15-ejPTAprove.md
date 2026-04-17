---
title:  "Aprobar el eJPT a la primera"
categories: 
  - Archivo
header:
  teaser: /assets/images/ejpt.png
tags:
  - eJPT
toc: true
toc_label: "Tabla de contenido"
---
El presente artículo es tomado del repositorio de [Johny Chafla](https://hacknotes.github.io) y contiene una guía del procedimiento a llevar acabo para aprobar con éxito el examen de la certificación [eJPT](https://elearnsecurity.com/product/ejpt-certification/).

## Barrido de ping

Una vez te conectes por **VPN** al laboratorio, lo primero que deberías hacer es un reconocimiento al sistema, encontrando activos, para lo cual los siguientes comandos te serian de ayuda:

```bash
nmap -sn 10.10.10.0/24
fping -a -g 10.10.10.0/24 2>/dev/null
```
## Escaneo exhaustivo

Ya en este punto, después de tener tu lista de host activos, lo siguiente que deberías hacer es un escaneo más exhaustivo, es decir listar los puertos abiertos con los que cuentan los host, así mismo como los servicios y versiones que están corriendo en ellos. No olvides ir guardando todos tus escaneos y datos relevantes encontrados.

```bash
nmap -p- --open -n -v -T5 10.10.14.16 -oN puertos
sudo nmap -sS --min-rate 200 -p- --open -n -v -Pn 10.10.14.16 -oN puertos
nmap -sV -sC -p21,22,80 10.10.14.16 -oN serviciosVersiones
nmap --script=vuln -p22,21,80,445 -v 10.10.14.16 -oN vulnScan
nmap --script=smb-vuln* -p445 -v 10.10.14.16 -oN smbScan
```
En esta etapa también debes ir realizando un reconocimiento a todos los servicios y puertos listados con los comandos anteriores, algunas cosas que deberías probar dependiendo el puerto y/o servicio seria:

### **Servicios Web**

```bash
nmap --script=http-enum -p80 10.10.14.16 -oN webScan
wfuzz -c --hc=404 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u https://10.10.14.15/FUZZ
wfuzz -c --hc=404 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u https://10.10.14.15/FUZZ.php
```

- **XSS**

```bash
<script>alert(xss)</script>
<h1>H1</h1>
```

- **SQLMap**

```bash
sqlmap -u "http://10.10.14.12/file.php?id=1" -p id
sqlmap -u "http://10.10.14.12/file.php?id=1" -p id --dbs
sqlmap -u "http://10.10.14.12/file.php?id=1" -p id -D dbname --tables
sqlmap -u "http://10.10.14.12/file.php?id=1" -p id -D dbname -T table_name --dump
```

### **Enumeración de SMB**

```bash
smbclient -L 10.10.14.12 -N
smbmap -H 10.10.14.12 -u 'null'
nmap --script=smb-vuln* -p445 10.10.14.15 -oN smbScan
smbmap -H 10.10.14.15 -R backups -u 'null'
smbclient //10.10.14.15/backups
```
### **Enumeración de FTP**

```bash
nmap --script=ftp-anon -p21 10.10.14.12
ftp 10.10.14.12
cd ..
```
## Explotación

En esta fase es en la cual debes aprovechar de los resultados anteriores obtenidos, con esos resultados podrás buscar posibles exploits o maneras de aprovecharte de ellos, como por ejemplo:

### FTP - Fuerza Bruta

```bash
hydra -l admin -P passlist.txt ftp://192.168.0.1
hydra -L userlist.txt -P passlist.txt ftp://192.168.0.1
```
**Pista:** 
Después de encontrar lo que te solicitan podrías necesitar **unshadow** y **john**
{: .notice--danger}

### Reverse Shell

Si te basas en los resultados anteriores y te ayudas de **Google** o **searchsploit** necesitarás:

- **nc**
```bash
nc -nlvp 443
```
- **metasploit**
```bash 
msfconsole
```
### Enumeración de windows

Una vez hayas comprometido el activo, deberás enumerar lo, los siguientes comandos te serán de gran ayuda:
```bash
dir /b/s "\*.conf*"
dir /b/s "\*.txt*"
dir /b/s "\*secret*"
route print
netstat -r
fsutil fsinfo drives
wmic logicaldisk get Caption,Description,providername
```

## Post Explotación

Ahora, una vez hayas realizado todo lo anterior, deberías preocuparte por descubrir nuevos activos y repetir los pasos anteriores si fuese necesario.

### Wireshark
```bash
ip.addr==192.168.12
ip.src == 192.168.2.11
ip.dst == 192.168.2.15
```
### IP Route
```bash
ip route add 10.10.10.0/24 via 10.10.11.1 dev tap0
```
## Recomendaciones
- **No** olvides revisar el material que te entregan antes del examen.
- Si deseas ver solo los comandos necesarios o alternativos para el examen, revisa mi [eJPT - Cheatsheet](https://github.com/hacknotes/eJPT-Cheatsheet)

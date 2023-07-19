---
title: ¿Que es el fuzzing❓
published: true
---

Para empezar hay que entender que dentro de una página web no todos los directorios son públicos y suele haber directorios que son paneles de incio de sesión para modificar o administrar la web, aunque generalmente no podríamos saber donde está el directorio privado, gracias a alguna técnica como el **'fuzzing'** podemos llegar a encontrarlos si tienen nombre comunes.

## ¿Como funciona?

El **'fuzzing'** consiste en que una herramienta pruebe un listado de palabras que suelen ser directorios privados y vaya probando si alguno es un directorio oculto dentro de la página web en la que se está buscando, para esto se suelen utilizar herramientas como:

* Wfuzz
* Gobuster
* Dirsearch

Estas son las más comunes pero exsisten muchas otras.

## Prueba de herramientas

Para demostrar de lo que estas herramientas son capaces he creado una página web y he puesto creado un directorio escondido con el nombre **'administrator'**. El diccionario que voy a usar es el [directory-list-2.3-medium.txt](https://gitlab.com/kalilinux/packages/dirbuster/blob/kali/master/directory-list-2.3-medium.txt).

* Wfuzz

```bash
#Comando

wfuzz -c --hc=404 -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt http://localhost/FUZZ.html


#Respuesta
********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://localhost/FUZZ.html
Total requests: 220546

=====================================================================
ID           Response   Lines    Word       Chars       Payload                                                                                               
=====================================================================

000000001:   200        89 L     174 W      1821 Ch     "index"                                                                                               
000005675:   200        11 L     13 W       143 Ch      "administrator"

```

* Gobuster

```bash

#Comando
gobuster dir -w /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt -u http://localhost/ -x html

#Respuesta
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://localhost/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Extensions:              html
[+] Timeout:                 10s
===============================================================
2022/08/16 12:11:07 Starting gobuster in directory enumeration mode
===============================================================
/administrator.html   (Status: 200) [Size: 143]
/index.html           (Status: 200) [Size: 1848]

```

* Dirsearch

```bash

#Comando
dirsearch -u http://localhost:80


#Respuesta
  _|. _ _  _  _  _ _|_    v0.4.2
 (_||| _) (/_(_|| (_| )

Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 30 | Wordlist size: 10903

Output File: /usr/lib/python3/dist-packages/dirsearch/reports/localhost:80/_22-08-16_16-46-24.txt

Target: http://localhost:80/

[16:46:24] Starting: 
[16:46:30] 200 -  143B  - /administrator.html
[16:46:35] 200 -    2KB - /index.html

```

## ¿Como evito el **'fuzzing'**?

Para evitarlo puedes hacer que baneen a los usuarios que envían muchas peticiones y así no hacer que puedan correr su ataque correctamente.

## Conclusión

En conclusión tenemos unas herramientas muy potentes, pero no por ello silenciosas de hecho son demasiado ruidosas porque al servidor le llegan todos los intentos del diccionario en forma de petición que son unos 2 millones más o menos, y que como ya he explicado si la web está bien gestionada lo más normal es que te echen de la misma o baneen tu ip.

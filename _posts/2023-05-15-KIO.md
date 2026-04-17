---
title:  "Resolución Kio"
categories:
  - Archivo
tags:
  - KIO
toc: true
toc_label: "Tabla de contenido"
---


El presente artículo es para dar algunos tips principales sobre pentesting poniendo de ejemplo la primer máquina de la certificación [PMJ](https://www.hacker-mentor.com/blog/que-es-pentester-mentor-junior)

## Reconocimiento de Red

El ataque desde el inicio se planea con un buen **escaneo**, un buen escaneo y una buena identificación de una vulnerabilidad te ahorrará horas de complicación. 

Lo primero es saber nuestra dirección ip con el comando ifconfig

![Panel principal](/assets/images/1.png)

Después se utiliza el comando sudo arp-scan -l

El reconocimiento ARP (Address Resolution Protocol) es un proceso utilizado por los dispositivos de red para asociar direcciones IP (Protocolo de Internet) con direcciones MAC (Control de Acceso al Medio) en una red local.

Cuando un dispositivo en una red local desea enviar un paquete a otro dispositivo, necesita conocer la dirección MAC del destino para enviar el paquete a través de la red. El proceso de reconocimiento ARP se utiliza para determinar la dirección MAC del dispositivo de destino.

El reconocimiento ARP funciona mediante la emisión de una solicitud de ARP a través de la red local para solicitar la dirección MAC correspondiente a una dirección IP determinada. Si el dispositivo de destino está en la misma red local, responderá a la solicitud de ARP con su dirección MAC. Si el dispositivo de destino no está en la misma red local, la solicitud de ARP se enviará al router predeterminado de la red, que luego intentará determinar la dirección MAC del dispositivo en otra red.

![Panel principal](/assets/images/2.png)

**Suplantación de MAC**

Nota: Cuando se realice un análisis siempre es recomendable cambiar la dirección MAC porque hay elementos de seguridad que se pegan y no sólo bloquean la ip del equipo, sino también la MAC. (se cambia antes de conectarse o prender la máquina)

Esto también permite saltar los NAC (Network Access Control)

![Panel principal](/assets/images/4.png)

La herramienta por excelencia o navaja suiza para escaneos es nmap

Usaremos el comando sudo nmap -sN + dirección de red.

El argumento "-sN" en Nmap se refiere a la técnica de escaneo de puertos "TCP Null Scan", o reconocimiento por ping. Esta técnica de escaneo envía paquetes TCP sin establecer ninguno de los bits de control TCP, como el bit SYN, FIN o RST. Sirve para determinar si un puerto está abierto, cerrado o filtrado. 

Si el puerto de destino está abierto, no se enviará una respuesta ya que el servidor no sabrá cómo interpretar el paquete. En cambio, si el puerto está cerrado, el servidor enviará una respuesta RST para indicar que el puerto está cerrado.

El escaneo TCP Null Scan es una técnica de escaneo sigilosa, ya que no establece ninguna conexión TCP y no deja registros en los registros de la red. Sin embargo, algunos firewalls pueden detectar y bloquear el escaneo TCP Null Scan. Esta técnica es útil para identificar los puertos que están abiertos y disponibles para posibles ataques.

![Panel principal](/assets/images/5.png)

![Panel principal](/assets/images/6.png)

Aquí muestra la dirección ip de la máquina kio y de mi máquina virtual kali.


Para no mandar ping al host se utiliza el comando sudo nmap -Pn + direccion de red.

Esta manera manda a reconocer puerto por puerto. El comando "nmap -Pn" utiliza la opción "-Pn" para saltar la detección de hosts para determinar los dispositivos activos en una red. Esta técnica se utiliza para escanear redes donde los hosts pueden estar ocultos o no responder a las solicitudes de ping. Si se establece esta opción, Nmap asume que todos los hosts especificados están activos y escanea todos los puertos especificados en cada uno de ellos.

![Panel principal](/assets/images/7.png)

También se utiliza el comando sudo nmap -Pn -p- + dirección de red.

El comando `nmap -Pn` se utiliza para indicarle a Nmap que no realice una detección de hosts (ping) antes de comenzar a escanear los puertos. En otras palabras, desactiva la comprobación de la conectividad de los hosts objetivo.

La opción "-p-" indica a Nmap que escanee todos los puertos posibles en los hosts especificados. Esta opción escaneará todos los puertos del 1 al 65535 en cada host especificado en el rango de direcciones IP.

En resumen, el comando "nmap -Pn -p-" se utiliza para realizar un escaneo completo de todos los puertos de un rango de direcciones IP, sin realizar una detección previa de los hosts activos. Este tipo de escaneo puede ser útil para identificar rápidamente todos los servicios disponibles en una red o para realizar un análisis exhaustivo de seguridad en una red específica. Sin embargo, es importante tener en cuenta que este tipo de escaneo puede ser intensivo en términos de recursos y tiempo, por lo que es recomendable tener cuidado al usarlo en redes grandes o con restricciones de ancho de banda.

![Panel principal](/assets/images/8.png)

![Panel principal](/assets/images/9.png)

Si se comienza a recibir que está abierto desde el puerto 1 hasta el 65000 hay que parar el escaneo porque se puede estar frente a un elemento de seguridad, este puede ser un IPS o un IDS y hay que tener precaución.

Se puede añadir la bandera -vvv (vervose) al comando para visualizar que es lo que está pasando y escaneando. El comando completo sería:

```bash
sudo nmap -Pn -p-  -vvv + dirección de red.
```

También se pueden escanear puertos en específico:

```bash
sudo nmap -Pn -p80 -T5 -vvv + dirección de red.
```

Este comando escanea el puerto 80 a una velocidad de 5 que es rápida y con verbose para visualizar lo que se está escaneando.

![Panel principal](/assets/images/10.png)

Otro comando para ver la versión del puerto que se analiza el cual es la bandera -sV :

```bash
sudo nmap -sV -vvvv -p80,22,111,139,443,1024 -T4  + direccion
```

![Panel principal](/assets/images/11.png)

![Panel principal](/assets/images/12.png)

De aquí en adelante de acuerdo a las versiones de los puertos se puede explotar o buscar exploits en google.

Si se utiliza el mismo comando pero con -oA kio se puede guardar la salida en la carpeta kio

![Panel principal](/assets/images/13.png)

A simple vista no se ve nada, pero  para el análisis se crearon archivos con comandos de grep o "grepeables" encima de un archivo para poder buscar.

![Panel principal](/assets/images/14.png)

Una vez creados estos archivos. Con el comando **xsltproc kio.xml -o kio.html** se visualizará el análisis de manera detallada a través de firefox.

![Panel principal](/assets/images/15.png)

![Panel principal](/assets/images/16.png)

Esto puede servir bastante para un informe que se requiera. Transforma de un xml a un tema de html.


Este mismo comando hace una comparación de fingerprinting o huellas que tiene el servidor para saber de que sistema operativo es el servidor con la bandera -O

El comando "nmap -O" es utilizado para realizar la detección del sistema operativo (OS, por sus siglas en inglés) de un host o dispositivo en una red. El comando envía una serie de paquetes de prueba al dispositivo y analiza las respuestas para determinar el sistema operativo que está siendo utilizado.

El objetivo principal de la detección del sistema operativo es obtener información sobre los sistemas que se encuentran en la red, lo que puede ser útil para realizar tareas de administración y mantenimiento de la red. Además, puede ser útil para identificar vulnerabilidades específicas de un sistema operativo y tomar medidas para proteger la red.

![Panel principal](/assets/images/17.png)

![Panel principal](/assets/images/18.png)

Otra manera de identificar el sistema operativo sin nmap  es a través del comando  ping + la direccion de red.

![Panel principal](/assets/images/19.png)

Cuando el TTL (Time-to-Live) se muestra como 255 en una respuesta a un ping, significa que el host de destino está en la misma red local que el host que envió el ping.

El valor TTL se establece en 255 en el paquete ICMP (Internet Control Message Protocol) que se utiliza para el ping, y cada vez que el paquete atraviesa un router, el valor del TTL se reduce en 1. Si el valor del TTL llega a 0, el paquete se descarta y no se entrega.

En una red local, los paquetes no necesitan atravesar un router para llegar a su destino, por lo que el valor del TTL no se reduce en ningún momento y se mantiene en su valor original de 255. Esto es porque los paquetes en la misma red local no necesitan ser enrutados y, por lo tanto, no necesitan pasar por ningún router.

Poner comando nmap --help para ver todos los comandos y acciones que se pueden realizar.

```bash
nikto -h http://192.168.188.131
```
![Panel principal](/assets/images/20.png)

El comando "nikto" es una herramienta de seguridad de red de código abierto que se utiliza para escanear servidores web en busca de vulnerabilidades y posibles amenazas de seguridad. Es capaz de detectar una amplia variedad de vulnerabilidades, como inyecciones de SQL, archivos expuestos, vulnerabilidades en aplicaciones, entre otros.

La herramienta "nikto" realiza una serie de pruebas de seguridad en el servidor web, como la enumeración de archivos y directorios, la búsqueda de vulnerabilidades conocidas en aplicaciones web, la revisión de la configuración del servidor web y la comprobación de la seguridad del servidor SSL.

Es una herramienta útil para los profesionales de la seguridad cibernética, los administradores de sistemas y los investigadores de seguridad, ya que puede ayudarles a identificar y corregir las vulnerabilidades en los servidores web y evitar posibles ataques.

Después de utilizar el comando nikto se va a desplegar información acerca del servidor.
Si copias y pegas la parte seleccionada /usage/ y lo abres el navegador poniendo la dirección de red se visualizará lo siguiente.

![Panel principal](/assets/images/21.png)

![Panel principal](/assets/images/22.png)

"Fuzzing" (también conocido como "prueba de penetración basada en mutaciones") es una técnica de prueba de seguridad de software que implica enviar datos aleatorios o semi-aleatorios a una aplicación para ver cómo maneja esos datos y si es vulnerable a errores o vulnerabilidades. El objetivo del fuzzing es encontrar vulnerabilidades en una aplicación que puedan ser explotadas por un atacante para tomar el control de la aplicación o del sistema en el que se ejecuta.

El proceso de fuzzing implica generar datos de entrada aleatorios o semi-aleatorios y enviarlos a la aplicación, observando cómo la aplicación responde a cada entrada. La entrada puede ser datos como cadenas de caracteres, números, archivos, protocolos de red, entre otros. El objetivo es identificar fallas de seguridad en la aplicación, como errores de programación, excepciones no controladas, fugas de memoria, entre otros.

El fuzzing puede ser una técnica muy efectiva para identificar vulnerabilidades en aplicaciones y es una herramienta comúnmente utilizada por los profesionales de la seguridad cibernética y los investigadores de seguridad para evaluar la seguridad de las aplicaciones. Es importante destacar que el fuzzing debe ser realizado de forma ética y legal, y el objetivo debe ser mejorar la seguridad del software en lugar de causar daño a la aplicación o al sistema en el que se ejecuta.

![Panel principal](/assets/images/23.png)

Msfconsole es la consola principal de la herramienta Metasploit Framework, un framework de pruebas de penetración de código abierto que se utiliza para desarrollar y ejecutar exploits contra sistemas informáticos para evaluar su seguridad.

Msfconsole es una interfaz de línea de comandos que permite a los usuarios interactuar con la base de datos de Metasploit, configurar y lanzar módulos de explotación, y administrar sesiones remotas en sistemas comprometidos. La consola es una herramienta potente que proporciona a los usuarios un amplio conjunto de funciones, desde la exploración de vulnerabilidades hasta la creación de exploits personalizados.

Al utilizar Metasploit Framework y msfconsole, los profesionales de seguridad y los investigadores de vulnerabilidades pueden probar la seguridad de sus propios sistemas, identificar debilidades en los sistemas de terceros, y ayudar a asegurar los sistemas que protegen. También se puede utilizar para probar la efectividad de las defensas de seguridad en lugar de para atacar sistemas no autorizados.

```bash
nikto -h http://192.168.188.131
```
Metasploit ayudará a identificar parámetros después de haber usado el comando nikto y así escoger que exploit elegir de acuerdo a la enumeración que se presenta.

![Panel principal](/assets/images/24.png)

1.-Se empieza poniendo search seguido de lo que necesitamos ver, en este caso TRACE.
2.-Después se utiliza la palabra use seguido del número a elegir., en este caso sería: use 2

![Panel principal](/assets/images/25.png)

![Panel principal](/assets/images/26.png)

El comando "show options" es un comando utilizado en la consola de Metasploit Framework que muestra una lista de opciones configurables para un módulo específico.

Los módulos en Metasploit Framework son piezas de código que se utilizan para explotar o realizar pruebas de penetración en sistemas informáticos específicos. Cada módulo tiene opciones configurables que pueden personalizarse para adaptarse a las necesidades de una tarea específica.

Cuando se ejecuta un módulo en la consola de Metasploit Framework, el comando "show options" proporciona una lista de las opciones configurables para ese módulo, como la dirección IP del objetivo, el puerto, el nombre de usuario y la contraseña. Los usuarios pueden utilizar este comando para ver qué opciones están disponibles para un módulo específico y personalizar las opciones necesarias para adaptarse a su situación específica.

Una vez que se han personalizado las opciones del módulo, el usuario puede ejecutar el comando "exploit" para iniciar la ejecución del módulo en el objetivo. En resumen, el comando "show options" es una herramienta útil para explorar y personalizar los módulos en Metasploit Framework antes de utilizarlos para llevar a cabo pruebas de penetración en sistemas informáticos.

![Panel principal](/assets/images/27.png)

Después se debe usar el comando set RHOSTS + dirección de red. Después volver a escribir el comando show options para visualizar los cambios en el RHOSTS como se observa en la imágen anterior.

Después de eso se escribe el comando exploit o run, en su defecto.

![Panel principal](/assets/images/28.png)

Aqui muestra que la dirección ip y el puerto 80 son vulnerables al Cross-site Tracing 

Si una dirección de red con el puerto 80 es vulnerable al XST, significa que un atacante puede utilizar esta técnica de ataque para robar información confidencial de los usuarios que acceden al servidor web a través de esa dirección. Por lo tanto, es importante que los administradores de sistemas y los desarrolladores web implementen medidas de seguridad adecuadas para proteger sus sitios web contra este tipo de vulnerabilidad.

En particular, el XST se aprovecha de la funcionalidad de seguimiento de solicitudes de los navegadores (llamada "trace") para interceptar información de cookies y tokens de autenticación que se transmiten a través de una conexión HTTP. El puerto 80 es el puerto predeterminado utilizado por los servidores web para atender las solicitudes HTTP.

El módulo auxiliar realiza un escaneo y funciona para reconocimiento, indicando que el exploit va a funcionar.

En Metasploit, un "módulo auxiliar" es una herramienta que se utiliza para realizar una variedad de tareas de seguridad, que van desde la exploración y el análisis de vulnerabilidades hasta la recopilación de información y la ejecución de ataques específicos. Los módulos auxiliares se utilizan a menudo como complementos a los módulos de explotación y post-explotación en una campaña de penetración.

Algunos ejemplos de módulos auxiliares incluyen:

-   Escaneo de puertos: Este tipo de módulo puede utilizarse para descubrir los servicios que se están ejecutando en una red determinada, identificar los puertos abiertos y evaluar la exposición de una red a los ataques.
 
-   Fuzzing: Estos módulos se utilizan para enviar entradas aleatorias o malformadas a una aplicación o servicio web para descubrir vulnerabilidades en el mismo.
 
-   Recopilación de información: Estos módulos pueden utilizarse para recopilar información sobre un objetivo específico, como la versión del sistema operativo, los puertos abiertos, la configuración de red, entre otros.
 
-   Ataques específicos: Los módulos auxiliares también pueden utilizarse para realizar ataques específicos, como la inyección de SQL, la explotación de vulnerabilidades de día cero, la suplantación de identidad (phishing), entre otros.

```bash
+Apache/1.3.20 appears to be outdated (current is at least Apache/2.4.54). Apache 2.2.34 is the EOL for the 2.x branch.
+OpenSSL/0.9.6b appears to be outdated (current is at least 3.0.7). OpenSSL 1.1.1s is current for the 1.x branch and will be supported until Nov 11 2023.
```

![Panel principal](/assets/images/29.png)

El comando "dirb" es una herramienta de enumeración web que se utiliza para realizar un escaneo de directorios y archivos en un servidor web determinado. Este comando se utiliza con la dirección de red de un sitio web para descubrir qué archivos y directorios están disponibles públicamente en el servidor web. Se puede utilizar el comando dib seguido de la direccion ip o poniendo el dominio del sitio web que se desea escanear.

El comando dirb examinará los archivos y directorios en el sitio web y producirá una lista de los recursos que se pueden encontrar. Esta lista puede ser muy útil para los analistas de seguridad para identificar vulnerabilidades de seguridad en el sitio web, como la exposición de archivos confidenciales, directorios con permisos de escritura, entre otros.

Es importante tener en cuenta que, aunque el comando dirb puede ser útil para los profesionales de la seguridad, también puede ser utilizado maliciosamente para realizar ataques cibernéticos.

Otra herramienta que funciona bien en este caso es:
dirbuster

Se abrirá una ventana como esta:

![Panel principal](/assets/images/30.png)

En browse se pueden agregar los diccionarios. Los diccionarios se encuentran en el directorio usr/share/wordlists/

![Panel principal](/assets/images/31.png)

Se puede agregar a file extension que busque archivos php, zip,rar y después hay que dar start. Iniciará el escaneo y tardará aproximadamente unos 30 min o más, pero esta es la manera gráfica de realizar el escaneo.

![Panel principal](/assets/images/32.png)

El reporte se guarda en algún directorio de elección en kali linux 

Otra herramienta de Fuzzing es wfuzz.

wfuzz realiza una serie de solicitudes HTTP personalizadas y automatizadas al sitio web objetivo, y utiliza una lista de palabras o diccionario para intentar descubrir archivos ocultos, directorios y parámetros no válidos.

En otras palabras, wfuzz es una herramienta de fuerza bruta que puede ser utilizada por los profesionales de seguridad para descubrir posibles vulnerabilidades en la aplicación web, tales como inyección SQL, vulnerabilidades de cross-site scripting, archivos y directorios sensibles expuestos, etc.

```bash
wfuzz -c --hc=404 -t 200 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt http://192.***.***.***/FUZZ
```
![Panel principal](/assets/images/33.png)

Estos son algunos de los parámetros que pueden ser utilizados con la herramienta "wfuzz" en la línea de comando. A continuación, se explica el significado de cada uno de ellos:

-   "-c": Este parámetro se utiliza para establecer el número de conexiones que se van a realizar simultáneamente durante la prueba. Por ejemplo, si se establece "-c 10", entonces se realizarán hasta 10 conexiones simultáneas al objetivo durante la prueba.

-   "--hc=404": Este parámetro se utiliza para indicar cuál es el código de estado HTTP que se considerará como respuesta válida por parte del objetivo. En este caso, se ha establecido que sólo se considerará una respuesta válida si el código de estado es 404 (página no encontrada). Esto puede ser útil para ignorar las respuestas 200 (OK) o 302 (Redirección) que no son relevantes para el objetivo de la prueba.

-   "-t 200": Este parámetro se utiliza para establecer un tiempo límite para cada solicitud realizada durante la prueba. En este caso, se ha establecido un límite de tiempo de 200 segundos. Esto significa que si una solicitud tarda más de 200 segundos en obtener una respuesta, wfuzz la ignorará y pasará a la siguiente solicitud.

-   "-w": Este parámetro se utiliza para indicar la ubicación del diccionario de palabras que se utilizará durante la prueba. En este caso, "-w" se utiliza para especificar la ubicación del archivo de palabras que se utilizará para realizar la prueba. El archivo de palabras puede ser un archivo de texto simple que contiene una lista de palabras o frases que se probarán durante la prueba.

El comando wfuzz arrojó este resultado

![Panel principal](/assets/images/34.png)

Otra herramienta es whatweb

"WhatWeb" es una herramienta de análisis de huellas digitales de sitios web que se utiliza para identificar las tecnologías utilizadas en un sitio web y obtener información sobre la configuración y la estructura del sitio. La herramienta utiliza técnicas de análisis automatizado y heurísticas para determinar qué tecnologías se están utilizando en un sitio web, incluyendo el sistema de gestión de contenido (CMS), el servidor web, el lenguaje de programación, el sistema operativo y otros detalles técnicos.

"WhatWeb" funciona mediante la emisión de solicitudes HTTP y el análisis de las respuestas del servidor. La herramienta utiliza una base de datos de huellas digitales y patrones para identificar los detalles técnicos del sitio web y puede ser muy útil para los profesionales de seguridad que buscan identificar vulnerabilidades y riesgos potenciales en un sitio web. Además, la herramienta también puede ser utilizada por los investigadores y los profesionales de marketing para recopilar información sobre la competencia y las tendencias del mercado en el ámbito digital.

Da una premisa de lo que podría estar pasando dentro del servidor, que servidor web está montado, el tipo de versión y tipo de servidor. Sirve patra hacer un reconocimiento.

Otra herramienta a utilizar es con el siguiente comando:

```bash
ffuf -u http://192.***.***.***/FUZZ -w /usr/share/dirbuster/directory-list-2.3-medium.txt -e .txt
```
![Panel principal](/assets/images/35.png)

NESSUS

Nessus es una herramienta de escaneo de vulnerabilidades y gestión de vulnerabilidades de red que se utiliza para identificar y evaluar vulnerabilidades en sistemas informáticos y redes. Fue desarrollado por Tenable, una empresa de ciberseguridad, y es una de las herramientas de seguridad de red más populares y ampliamente utilizadas en la industria.

Nessus utiliza una amplia variedad de técnicas de escaneo, incluyendo escaneos de puertos, escaneos de vulnerabilidades, pruebas de intrusión y evaluaciones de cumplimiento de políticas para identificar posibles vulnerabilidades en los sistemas y redes de destino. La herramienta puede realizar escaneos de vulnerabilidades en sistemas operativos, aplicaciones web, bases de datos, servidores de correo electrónico, dispositivos de red, sistemas SCADA/ICS y otros componentes de infraestructura de red.

Nessus también cuenta con una amplia gama de funciones de gestión de vulnerabilidades, que permiten a los usuarios rastrear y priorizar las vulnerabilidades encontradas, así como proporcionar recomendaciones y orientación sobre cómo mitigar los riesgos identificados. La herramienta también puede integrarse con otros sistemas de gestión de seguridad de la información, como SIEM y GRC, para una mejor visibilidad y gestión de la seguridad.

![Panel principal](/assets/images/36.png)

![Panel principal](/assets/images/37.png)

Reconocimiento SMB

SMB (Server Message Block) es un protocolo de red utilizado para compartir archivos, impresoras y otros recursos entre computadoras en una red. El reconocimiento SMB se refiere a la técnica utilizada por los atacantes para identificar los sistemas que tienen el servicio SMB activo y configurado de forma incorrecta, lo que puede permitir el acceso no autorizado a los recursos compartidos en el sistema.

El reconocimiento SMB se puede realizar mediante varias herramientas, como Nmap, Metasploit y otras herramientas de exploración de redes y vulnerabilidades. Estas herramientas envían solicitudes al puerto TCP 445, que es el puerto utilizado por el servicio SMB, para obtener información sobre los sistemas que están escuchando en este puerto.

Una vez que un atacante ha identificado un sistema con el servicio SMB activo y configurado de forma incorrecta, puede intentar explotar las vulnerabilidades conocidas en el protocolo SMB para obtener acceso no autorizado al sistema y los recursos compartidos. Las vulnerabilidades en SMB han sido utilizadas en varios ataques notables, como el ransomware WannaCry y NotPetya.

Es importante asegurarse de que los sistemas en una red tengan el servicio SMB configurado de manera segura y se apliquen los parches de seguridad para las vulnerabilidades conocidas en SMB para evitar ataques de reconocimiento SMB y otros ataques que exploten vulnerabilidades en SMB.

![Panel principal](/assets/images/38.png)

![Panel principal](/assets/images/39.png)

Los resultados del script de host sugieren que el escaneo ha identificado un sistema llamado "KIOPTRIX" y ha intentado negociar el protocolo SMB2, pero la negociación ha fallado.

El resultado `_nbstat` indica que se ha utilizado el comando `nbtstat` para obtener información de NetBIOS del sistema escaneado. La respuesta indica que el nombre de NetBIOS del sistema es "KIOPTRIX", pero no se ha podido identificar el usuario de NetBIOS ni la dirección MAC.

El resultado `_smb2-time` indica que el script ha intentado negociar la conexión con el sistema utilizando el protocolo SMB2, pero ha fallado. El protocolo SMB2 es una versión más reciente del protocolo SMB que se utiliza en sistemas operativos modernos, como Windows Vista, Windows 7 y versiones posteriores. El resultado puede significar que el sistema no es compatible con SMB2 o que la negociación ha fallado por otros motivos, como la falta de permisos o la configuración incorrecta de SMB.

Es importante tener en cuenta que los resultados del script de host pueden proporcionar información útil, pero no deben considerarse como una evaluación completa de la seguridad del sistema escaneado. Se deben realizar pruebas adicionales y se deben tomar medidas adecuadas para proteger el sistema y la red en general.

Abriremos metasploit con el comando msfconsole y se pondrá search smb

![Panel principal](/assets/images/40.png)

![Panel principal](/assets/images/41.png)

Se utilizará el número 105

![Panel principal](/assets/images/42.png)

Identifica que la versión del protocolo SMB en un servidor SMB en la red es 2.2.1a

El comando **set RHOSTS (dirección IP)** se utiliza en la herramienta de prueba de penetración Metasploit Framework para establecer la dirección IP del host remoto objetivo que se va a escanear o atacar.

El término **RHOSTS** significa "Remote Hosts", que se traduce como "Hosts Remotos" en español, y es una variable utilizada por Metasploit para especificar una o varias direcciones IP de destino que se van a escanear o atacar.

La opción **set** se utiliza para establecer o cambiar el valor de una variable en el contexto actual de Metasploit. Al utilizar `set RHOSTS <dirección IP>`, se establece la dirección IP del host remoto como el valor de la variable RHOSTS.

Una vez que se ha establecido la dirección IP del host remoto objetivo, Metasploit Framework puede utilizar los módulos correspondientes para realizar diversas pruebas de vulnerabilidades y ataques en el host remoto, como escaneo de puertos, escaneo de vulnerabilidades, ejecución remota de código, entre otros.

![Panel principal](/assets/images/43.png)

SearchSploit es una herramienta que se utiliza para buscar exploits y vulnerabilidades conocidas en sistemas y aplicaciones específicas.

Samba es una implementación de software libre del protocolo de archivos compartidos de Microsoft Windows. La versión 2.2.1a de Samba es una versión antigua y ya no se utiliza ampliamente.

Por lo tanto, al buscar "searchsploit samba 2.2.1a", es probable que se muestren los exploits conocidos para esa versión específica de Samba. Es importante tener en cuenta que, como se trata de una versión antigua, es posible que las vulnerabilidades hayan sido parcheadas en versiones más recientes de Samba.

![Panel principal](/assets/images/44.png)

Se vuelve a abrir metasploit en la terminal y se pone search trans2open 

Search Trans2Open es un módulo de Metasploit que busca una vulnerabilidad conocida en el protocolo Trans2 de Samba. El protocolo Trans2 se utiliza en Samba para proporcionar diversas funciones, como la enumeración de archivos y directorios compartidos.

Este módulo de Metasploit utiliza una técnica de desbordamiento de búfer para explotar una vulnerabilidad en el protocolo Trans2. Si la vulnerabilidad es explotada con éxito, un atacante remoto puede ejecutar código malicioso en el sistema objetivo con los permisos del usuario que ejecuta el servicio Samba.

Es importante tener en cuenta que este módulo solo funciona contra sistemas que tengan una versión vulnerable de Samba y que no hayan sido parcheados.

En este caso se puede escoger el módulo 1 y 3. Usaremos el 1.

![Panel principal](/assets/images/45.png)

Debido a que el payload que utilizamos para realizar el exploit no funcionó se tiene que buscar otro, por lo que se utiliza el comando show payloads el cual arrojará una lista.

![Panel principal](/assets/images/46.png)

Se escribe set payload linux/x86/shell_  y se presiona el tabulador para que muestre las opciones que se pueden utilizar a partir de lo ya escrito.

El payload a utilizar será el número 33. Después se escribe show options para ver las opciones disponibles y configurar el módulo

![Panel principal](/assets/images/47.png)

En este caso no se tiene que configurar nada ya que el host y los puertos en los que se intenta hacer explotar la vulnerabilidad ya están configurados. (por lo regular solo se pone el RHOSTS) la dirección ip del sistema a vulnerar.

![Panel principal](/assets/images/48.png)

Después solo se escribe run o exploit para correr el programa. Y como se aprecia en la imágen ya se logró la explotación haciendose root del sistema Kioptrix.

Se utiliza bash -i para iniciar una sesión interactiva y se coloca el comando:
find / -name  bandera*.txt 2>/dev/null

![Panel principal](/assets/images/49.png)

Utilizando el comando cat se abren los archivos .txt donde están las banderas.

![Panel principal](/assets/images/50.png)

Otra forma de realizar la explotación es a traves del comando searchsploit mod_ssl

![Panel principal](/assets/images/51.png)

En este caso se utilizará la última versión del exploit

![Panel principal](/assets/images/52.png)

![Panel principal](/assets/images/53.png)

La copia tiene que estar donde están los demás exploits.

![Panel principal](/assets/images/54.png)

El comando a utilizar es: gcc -o OpenFuck 47080.c -lcrypto

![Panel principal](/assets/images/55.png)

![Panel principal](/assets/images/56.png)

![Panel principal](/assets/images/57.png)

![Panel principal](/assets/images/58.png)



![Panel principal](/assets/images/59.png)

![Panel principal](/assets/images/60.png)


![Panel principal](/assets/images/61.png)

![Panel principal](/assets/images/62.png)

![Panel principal](/assets/images/63.png)


![Panel principal](/assets/images/64.png)

![Panel principal](/assets/images/65.png)

![Panel principal](/assets/images/66.png)

![Panel principal](/assets/images/67.png)


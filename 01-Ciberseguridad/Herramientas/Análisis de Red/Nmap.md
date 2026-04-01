---
tags:
  - herramientas/analisis-red
  - redes
---
## Lista de Opciones

A continuación se encuentra un listado con las opciones más habituales, aunque no se encuentran las opciones menos conocidas. La última versión de este listado se puede encontrar en [https://nmap.org/data/nmap.usage.txt](https://nmap.org/data/nmap.usage.txt).

USO: `nmap [Tipo(s) de Análisis/Sondeo] [Opciones] {especificación de objetivos}` 

Se divide en 10 secciones principales:

* [[Nmap#Especificación de Objetivo|Especificación del Objetivo]]
* [[Nmap#Descubrimiento de Hosts|Descubrimiento de Hosts]]
* [[Nmap#Técnicas de Análisis|Técnicas de Análisis]]
* [[Nmap#Especificación de Puertos y Orden de Análisis|Especificación de Puertos y Orden de Análisis]]
* [[Nmap#Detección de Servicio/Versión|Detección de Servicio/Versión]]
* [[Nmap#Detección de Sistema Operativo|Detección de Sistema Operativo]]
* [[Nmap#Temporizado y Rendimiento|Temporizado y Rendimiento]]
* [[Nmap#Evasión y Falsificación de Cortafuegos/IDS|Evasión y Falsificación de Cortafuegos/IDS]]
* [[Nmap#Salida|Salida]]
* [[Nmap#Misceláneo|Misceláneo]]

### Especificación de Objetivo

Se pueden indicar nombres de sistema, direcciones IP, redes, etc.
[[Nmap#Especificación del Objetivo|Más detalles aquí.]]

| **FLAG**                              | **EFECTO**                                   |
| ------------------------------------- | -------------------------------------------- |
| -iL <archivo_entrada>                 | Lee una lista de sistemas/redes del archivo. |
| -iR <número de sistemas>              | Selecciona objetivos al azar.                |
| --exclude <sist1[,sist2][,sist3],...> | Excluye ciertos sistemas o redes.            |
| --excludefile <fichero_exclusión>     | Excluye los sistemas indicados en el fichero |

### Descubrimiento de Hosts

| **FLAG**                          | **EFECTO**                                                                |
| --------------------------------- | ------------------------------------------------------------------------- |
| -sL                               | Sondeo de lista - Simplemente lista los objetivos a analizar              |
| -sP                               | Sondeo Ping     - Sólo determina si el objetivo está vivo                 |
| -P0                               | Asume que todos los objetivos están vivos.                                |
| -PS/PA/PU [listadepuertos]        | Análisis TCP SYN, ACK o UDP de los puertos indicados                      |
| -PE/PP/PM                         | Solicita un análisis ICMP del tipo echo, marca de fecha y máscara de red. |
| -n/-R                             | No hacer resolución DNS / Siempre resolver [por omisión: a veces].        |
| --dns-servers <serv1[,serv2],...> | Especificar servidores DNS específicos.                                   |
| --system-dns                      | Utilizar la resolución del sistema operativo.                             |

### Técnicas de Análisis

| **FLAG**                           | **EFECTO**                                    |
| ---------------------------------- | --------------------------------------------- |
| -sS/sT/sA/sW/sM                    | Análisis TCP SYN/Connect()/ACK/Window/Maimon. |
| -sN/sF/sX                          | Análisis TCP Null, FIN, y Xmas.               |
| --scanflags <indicador>            | Personalizar los indicadores TCP a utilizar.  |
| -sI <sistema zombi[:puerto_sonda]> | Análisis pasivo («Idle», N. del T.).          |
| -sO                                | Análisis de protocolo IP                      |
| -b <servidor ftp rebote>           | Análisis por rebote FTP.                      |

### Especificación de Puertos y Orden de Análisis

| **FLAG**              | **EFECTO**                                                                                    |
| --------------------- | --------------------------------------------------------------------------------------------- |
| -p <rango de puertos> | Sólo sondear los puertos indicados. Ej: -p22; -p1-65535; -p U:53,111,137,T:21-25,80,139,8080. |
| -F                    | Rápido - Analizar sólo los puertos listados en el archivo nmap-services.                      |
| -r                    | Analizar los puertos secuencialmente, no al azar.                                             |

### Detección de Servicio/Versión

| **FLAG**                    | **EFECTO**                                                              |
| --------------------------- | ----------------------------------------------------------------------- |
| -sV                         | Sondear puertos abiertos, para obtener información de servicio/versión. |
| --version-intensity <nivel> | Fijar de 0 (ligero) a 9 (probar todas las sondas).                      |
| --version-light             | Limitar a las sondas más probables (intensidad 2).                      |
| --version-all               | Utilizar todas las sondas (intensidad 9).                               |
| --version-trace             | Presentar actividad detallada del análisis (para depurar).              |

### Detección de Sistema Operativo

| **FLAG**       | **EFECTO**                                           |
| -------------- | ---------------------------------------------------- |
| -O             | Activar la detección de sistema operativo (SO).      |
| --osscan-limit | Limitar la detección de SO a objetivos prometedores. |
| --osscan-guess | Adivinar el SO de la forma más agresiva.             |

### Temporizado y Rendimiento

| **FLAG**                                                      | **EFECTO**                                                                       |
| ------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| -T[0-5]                                                       | Seleccionar plantilla de temporizado (los números altos son más rápidos).        |
| --min-hostgroup/max-hostgroup <tamaño>                        | Paralelizar los sondeos.                                                         |
| --min-parallelism/max-parallelism <numsondas>                 | Paralelización de sondeos,                                                       |
| --min-rtt-timeout/max-rtt-timeout/initial-rtt-timeout <msegs> | Indica el tiempo de ida y vuelta de la sonda.                                    |
| --max-retries <reintentos>                                    | Limita el número máximo de retransmisiones de las sondas de análisis de puertos. |
| --host-timeout <msegs>                                        | Abandonar un objetivo pasado este tiempo.                                        |
| --scan-delay/--max-scan-delay <msegs>                         | Ajusta el retraso entre sondas.                                                  |

### Evasión y Falsificación de Cortafuegos/IDS

| **FLAG**                                                 | **EFECTO**                                                         |
| -------------------------------------------------------- | ------------------------------------------------------------------ |
| -f; --mtu <valor>                                        | fragmentar paquetes (opc. con el MTU indicado).                    |
| -D <señuelo1,señuelo2[,ME],...>                          | Disimular el análisis con señuelos. N. del T.: «ME» es «YO» mismo. |
| -S <Dirección_IP>                                        | Falsificar la dirección IP origen.                                 |
| -e <interfaz.>                                           | Utilizar la interfaz indicada.                                     |
| -g/--source-port <numpuerto.>                            | Utilizar el número de puerto dado.                                 |
| --data-length <num.>                                     | Agregar datos al azar a los paquetes enviados.                     |
| --ttl <val.>                                             | Fijar el valor del campo time-to-live (TTL) de IP.                 |
| --spoof-mac <dirección mac/prefijo/nombre de fabricante> | Falsificar la dirección MAC.                                       |
| --badsum                                                 | Enviar paquetes con una suma de comprobación TCP/UDP falsa.        |

### Salida

| **FLAG**                | **EFECTO**                                                                                                                                                    |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| -oN/-oX/-oS/-oG <file.> | Guardar el sondeo en formato normal, XML, s\|<rIpt kIddi3 (n3n3b4n4n4), y Grepeable (para usar con grep(1), N. del T.), respectivamente, al archivo indicado. |
| -oA <nombre_base>       | Guardar en los tres formatos principales al mismo tiempo.                                                                                                     |
| -v                      | Aumentar el nivel de mensajes detallados (-vv para aumentar el efecto).                                                                                       |
| -d[nivel]               | Fijar o incrementar el nivel de depuración (Tiene sentido hasta 9).                                                                                           |
| --packet-trace          | Mostrar todos los paquetes enviados y recibidos.                                                                                                              |
| --iflist                | Mostrar interfaces y rutas (para depurar).                                                                                                                    |
| --append-output         | Agregar, en vez de sobreescribir, a los archivos indicados con -o.                                                                                            |
| --resume <archivo.>     | Retomar un análisis abortado/detenido.                                                                                                                        |
| --stylesheet <ruta/URL> | Convertir la salida XML a HTML según la hoja de estilo XSL indicada                                                                                           |
| --webxml                | Referenciar a la hoja de estilo de Insecure.Org para tener un XML más portable.                                                                               |
| --no-stylesheet         | No asociar la salida XML con ninguna hoja de estilos XSL.                                                                                                     |

### Misceláneo

| **FLAG**               | **EFECTO**                                                         |
| ---------------------- | ------------------------------------------------------------------ |
| -6                     | Habilitar análisis IPv6.                                           |
| -A                     | Habilita la detección de SO y de versión.                          |
| --datadir <nombreDir.> | Indicar la ubicación de los archivos de datos Nmap personalizados. |
| --send-eth/--send-ip   | Enviar paquetes utilizando tramas Ethernet o paquetes IP "crudos". |
| --privileged           | Asumir que el usuario tiene todos los privilegios.                 |
| -V                     | Muestra el número de versión.                                      |
| -h                     | Muestra esta página resumen de la ayuda.                           |

## ¿Qué es?

Nmap es un escáner de redes de open-source publicado por primera vez en 1997. Desde entonces, una multitud de aspectos y opciones han sido añadidas. Es un escáner de red poderoso y flexible que puede ser adaptado para varios escenarios y configuraciones.

Se usa para exploración de red y auditoría de seguridad. Se diseñó para analizar rápidamente grandes redes, aunque funciona muy bien contra equipos individuales. 

En este apunte se verá:

* Descubrimiento de hosts activos.
* Encontrar servicios corriendo en hosts activos.
* Distinguir los diferentes tipos de escaneos de puertos.
* Detectar las versiones de los servicios funcionando.
* Controlar el timing.
* Formatear el output.

## Salidas de Nmap

La salida de Nmap es un listado de objetivos analizados, con información adicional para cada uno dependiendo de las opciones utilizadas. La informació primordial es la "tabla de puertos interesantes". Dicha tabla lista el número de puerto y protocolo, el nombre más común del servicio, y su estado.

El estado puede ser open (abierto), filtered (filtrado), closed (cerrado), o unfiltered (no filtrado). 

* Abierto significa que la aplicación en la máquina de destino se encuentra esperando conexiones o paquetes en ese puerto.
* Filtrado indica que un cortafuegos, filtro, u otro obstáculo de la red está bloqueando el acceso a ese puerto, por lo que Nmap no puede saber si se encuentra abierto o cerrado.
* Los puertos cerrados no tienen ninguna aplicación escuchando en los mismos, aunque podrían abrirse en cualquier momento.
* Los clasificados como no filtrados, son aquellos que responden a los sondeos de Nmap, pero para los que Nmap no puede determinar si se encuentran abiertos o cerrados.

Nmap informa de las combinaciones de estado open|filtered y closed|filtered cuando no puede determinar en cuál de los dos estados está un puerto.

La tabla de puertos también puede incluir detalles de la versión de la aplicación cuando se ha solicitado detección de versiones. Nmap ofrece información de los protocolos IP soportados, en vez de puertos abiertos, cuando se solicita un análisis de protocolo IP con la opción (-sO).

Además de la tabla de puertos interesantes, Nmap puede dar información adicional sobre los objetivos, incluyendo el nombre de DNS según la resolución inversa de la IP, un listado de sistemas operativos posibles, los tipos de dispositivo y direcciones MAC.

## Especificación del Objetivo

Todo lo que se escriba en la línea de parámetros de Nmap que no sea una opción se considera una especificación del sistema objetivo. Ej: la indicación de sólo una IP, o nombre de sistema, para que sea analizado.

Puede darse la situación de que uno desee analizar una red completa de equipos adyacentes. Nmap soporta el direccionamiento estilo CIDR para estos casos. Por ejemplo: 192.168.10.0/24 o 205.217.153.62/16. La máscara más pequeña permitida es /1 y la más grande es /32.

La notación CIDR es breve pero no siempre es suficientemente flexible. Por ejemplo, puede querer sondear la red 19.168.0.0/16 pero omitir cualquier IP que termine por .0 o por .255 ya que son habitualmente direcciones de difusión. Es posible hacer esto con Nmap mediante el direccionamiento por octetos.

En lugar de especificar una dirección IP normal, puede especificar una lista separada por comas de números o rangos para cada octeto. Por ejemplo, si utiliza 192.168.0-255.1-254 se omitirán todas las direcciones del rango que terminen en .0 o .255. Los rangos no tienen que estar limitados a los últimos octetos. Por ejemplo, si especifica 0-255.0-255.13.37, realizará un sondeo en todo internet con las direcciones IP que terminen en 13.37. Este tipo de muestreo amplio puede ser útil para encuestas en Internet y con fines de investigación.

Sólo puede especificar direcciones IPv6 si utiliza su nombre IPv6 totalmente cualificado o su nombre de sistema. No se soporta el uso de CIDR o rangos de octetos para IPv6 porque raramente son útiles.

Con Nmap puede especificar múltiples sistemas en la línea de órdenes y no tienen que ser del mismo tipo. Por ejemplo, la orden `nmap scanme.nmap.org 192.168.0.0/16 10.0.0,1,3-7.0-255` hace lo que uno esperaría.

Aunque habitualmente se especifican los objetivos en la línea de órdenes puede utilizar las siguientes opciones para controlar la selección de objetivos:

`-iL <archivo_entrada>`

* Toma la especificación de objetivos del archivo *<archivo_entrada>*

## Descubrimiento de Hosts: Quién está Online

Nmap usa varias maneras para especificar sus objetivos:

* Rango de IPs usando `-`, si quieres escanear todas las direcciones IP desde 192.168.0.1 hasta 192.168.0.10, puedes escribir `192.168.0.1-10`.
* Subnet de IPs usando `/`, si quieres escanear una subnet, puedes escribir `192.168.0.1/24`, y esto sería equivalente a 192.168.0.0-255.
* Hostname: tambien podemos especificar el objetivo por el hostname, por ejemplo, `example.thm`.

Supongamos que queremos descubrir los hosts online de una red. Nmap ofrece la opción `-sn`, que sería un escaneo por ping. Sin embargo, este no es limitado como ping.

### Escaneando una Red "Local"

En este contexto, usamos el término "Local" para referirnos a la red a la que estamos directamente conectados, como Ethernet o una red Wifi. En esta primera demostración, escanearemos la red Wifi en la que estamos conectados. 

```bash
sudo nmap -sn 192.168.66.0/24
```

Como se está escaneando la red local, podremos ver las direcciones MAC de los dispositivos. En consecuencia, podemos determinar los proveedores de tarjetas de red, lo cual es información beneficiosa ya que puede ayudarnos a adivinar el tipo de dispositivo de destino.

Al escanear una red conectada directamente, Nmap comienza enviando solicitudes ARP. Cuando un dispositivo responde a la solicitud ARP, Nmap lo etiqueta con "Host is up".

### Escaneando una red "Remota"

"Remota" significa que al menos un router separa nuestro sistema de la red objetivo. Como resultado, todo nuestro tráfico hacia los sistemas objetivos deben pasar a través de uno o más routers. A diferencia del escaneo en red local, no podemos enviar ARP requests al objetivo.

Nmap ofrece una lista de escaneo con la opción `-sL`. Este scan solo lista los objetivos a escanear sin escanearlos. Por ejemplo, `nmap -sL 192.168.0.1/24` listará los 256 objetivos que van a ser escaneados. Esta opción ayuda a confirmar los objetivos antes de ejecutar el scan real.

Como se mencionó en un inicio, `-sn` apunta a descubrir hosts activos sin intentar descubrir los servicios que están ejecutando. Este scan puede ser útil si solo quieres descubrir los dispositivos de una red sin causar demasiado ruido. Sin embargo, esto no nos dirá los servicios que están corriendo.

## Escaneo de [[Puertos]]: Quién está escuchando

Anteriormente usamos -sn para descubrir hosts activos. Ahora vamos a descubrir los servicios de red que están escuchando en estos hosts activos. Por servicio de red, nos referimos a cualquier proceso que está escuchando a conexiones entrantes en un puerto TCP o UDP. Los servicios de red comunes incluyen servidores web, que usualmente escuchan puertos 80 y 443 en TCP, y servidores DNS, que usualmente escuchan en UDP (y TCP) en el puerto 53.

Por diseño, TCP tiene 65,535 puertos, y lo mismo aplica para UDP. 

### Escaneando [[Puertos]] TCP

La manera más simple y básica de saber si hay un puerto TCP abuerto es intentando hacer un `telnet` al puerto.

En teoría, puedes intentar completar un TCP three-way handshake con cada puerto del objetivo; sin embargo, solo los puertos TCP abiertos responderían apropiadamente y permitirían que se establezca una conexión TCP. Este procedimiento no es muy diferente al escaneo de puertos de Nmap.

#### Connect Scan

El Connect Scan puede ser disparado usando `-sT`. Intenta completar el TCP three-way handshake con cada puerto TCP del objetivo. Si el puerto TCP resulta estar abierto y Nmap logra conectarse, Nmap derribará la conexión establecida.

#### SYN Scan (Stealth)

A diferencia del Connect Scan, el cual trata de conectarse con el puerto TCP del objetivo, el escaneo SYN solo ejecuta el primer paso: manda un paquete TCP SYN. 

En consecuencia, el TCP three-way handshake nunca se completa. La ventaja es que esto se espera que deje menos logs debido a que la conexión nunca se establece, y por eso, se considera un escaneo relativamente sigiloso. Podemos seleccionar el escaneo SYN con la flag `-sS`.

### Escaneando [[Puertos]] UDP

A pesar de que muchos servicios usan TCP para la comunicación, muchos usan UDP. Algunos ejemplos incluyen DNS, DHCP, NTP (Network Time Protocol), SNMP (Simple Network Management Protocol), y VoIP (Voice over IP). UDP no requiere establecer una conexión y desactivarla después. Además, es muy adecuado para comunicaciones en tiempo real, como trasmisiones en vivo. Todas estas son razones para considerar escanear y descubrir servicios que escuchan en puertos UDP.

Nmap ofrece la opción `-sU` para escanear servicios UDP.

#### Limitación de los puertos objetivo

Nmap escanea los 1000 puertos más comunes de forma predeterminada. Sin embargo, es posible que esto no sea lo que se está buscando. Por lo tanto, Nmap ofrece algunas opciones más.

* `-F` es para el modo rápido, que escanea los 100 puertos más comunes en lugar de los 1000 predeterminados.
* `-p[range]` le permite especificar una variedad de puertos a escanear. Por ejemplo, `-p10-1024` escanea desde el puerto 10 al puerto 1024, mientras `-p-25` escaneará todos los puertos entre 1 y 25. Hay que tener en cuenta que `-p-` es lo mismo que decir `-p1-65535` y es la mejor opción si se quiere ser lo más minucioso posible.

## Detección de Versiones

### Detección de Sistema Operativo

Podemos habilitar la detección de Sistemas Operativos con la opción `-O`. Como el nombre indica, la opción de detección de Sistemas Operativos hace que Nmap confíe en varios indicadores para hacer una suposición fundamentada sobre el sistema operativo del destino. 

Sin embargo, hay que destacar que no existe un detector de SO perfectamente preciso.

### Detección de servicios y versiones

Después de descubrir varios puertos abiertos es probable que se quiera saber qué servicios están escuchando en ellos. `-sV` permite la detección de versiones. Esto es muy conveniente para recopilar más información sobre su objetivo con menos pulsaciones de teclas.

`-A` es una opción que permite la detección del sistema operativo, el escaneo de versiones y traceroute, ademas de otras cosas, en una sola opción, por lo que es conveniente usarla para evitar dar tantas pulsaciones.
### Forzar el escaneo

Cuando ejecutamos nuestro escaneo de puertos, como al usar `-sS`, existe la posibilidad de que el host de destino no responda durante la fase de descubrimiento del host (por ejemplo que no responda a solicitudes ICMP). En consecuencia, Nmap marcará este host como inactivo y no iniciará un escaneo de puerto en su contra.

Podemos pedirle a Nmap que trate a todos los hosts como en línea y que escanee cada host, incluidos aquellos que no respondieron durante la fase de descubrimiento del host. Esta elección se puede activar agregando la opción `-Pn`.

## Timing

Nmap proporciona varias opciones para controlar la velocidad y el tiempo de escaneo.

Hacer un escaneo con la velocidad normal podría activar IDS u otras soluciones de seguridad. Nmap provee de 6 plantillas de timing, con nombres bastante distintivos:

* paranoid (0)
* sneaky (1)
* polite (2)
* normal (3)
* aggressive (4)
* insane (5)

Donde 0 es el más lento y 5 es el más rápido

Para elegir alguno de ellos, podemos agregar `-T0`, `-T 0` o `-T paranoid`.

El número de sondas paralelas se puede controlar con `--min-parallelism <numprobes>` y `--max-parallelism <numprobes>`. Estas opciones pueden ser usadas para establecer el mínimo y el máximo de número de sondas puerto TCP y UDP simultáneas para un grupo de hosts.

Por defecto nmap controla el numero de sondas paralelas de forma automática.

Otra opción útil es `--min-rate <number>`y `--max-rate <number>`. Como el nombre indica, estas controlan la velocidad mínima y máxima con la que nmap envía paquetes. El ratio se provee como *número de paquetes por segundo*.

`--host-timeout <time>` es una opción que nos permite especificar el tiempo máximo que queremos esperar, y es especialmente útil para hosts lentos o hosts con conexiones de internet lentas.

## Output

### Verbosity and Debugging

Para imprimir más detalles en un escaneo podemos usar la opción `-v`, se puede incrementar el nivel de detalles añadiendo otra "v", como `-vv` o `-vvvv`. También podemos especificar el nivel de detalle directamente, por ejemplo `-v2` y `-v4`. Se puede incrementar el nivel de detalles presionando "v" después de que el scan haya empezado.

Si los detalles no son suficientes, podemos usar `-d` para un output a nivel de debugging. Al igual que con el verbosity, podemos agrandar el nivel de detalle añadiendo más "d" o con números, el nivel máximo es `-d9`.

### Saving Scan Report

Nmap nos da varios formatos. Los tres formatos más útiles son el normal (human-friendly), XML output y grepable output, en referencia al comando `grep`. Se puede seleccionar el formate de reporte de scan de esta forma:

* `-oN <filename>` - Normal output
* `-oX <filename>` - XML output
* `-oG <filename>` - grepable output (useful for grep and awk).
* `-oA <filename>` - Output in all major formats

Es decir, que con `-oA <filename>`, el reporte se guarda en tres archivos: nmap, xml y gnmap.

[^1]: 

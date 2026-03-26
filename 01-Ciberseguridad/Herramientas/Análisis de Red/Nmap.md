---
tags:
  - herramientas/analisis-red
  - redes
---
## ¿Qué es?

Nmap es un escáner de redes de open-source publicado por primera vez en 1997. Desde entonces, una multitud de aspectos y opciones han sido añadidas. Es un escáner de red poderoso y flexible que puede ser adaptado para varios escenarios y configuraciones.

En este apunte se verá:

* Descubrimiento de hosts activos.
* Encontrar servicios corriendo en hosts activos.
* Distinguir los diferentes tipos de escaneos de puertos.
* Detectar las versiones de los servicios funcionando.
* Controlar el timing.
* Formatear el output.

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

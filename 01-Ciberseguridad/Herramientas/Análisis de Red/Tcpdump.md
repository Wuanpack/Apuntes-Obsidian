---
tags:
  - herramientas/analisis-red
  - redes
---
## ¿Qué es?

Tcpdump es una utilidad de línea de comandos (CLI) que permite capturar y analizar el tráfico de red que pasa por el sistema. A menudo se utiliza para ayudar a solucionar problemas de red, así como herramienta de seguridad.

Es una herramienta potente y versátil que incluye muchas opciones y filtros, `tcpdump` y su libreria `libpcap` están escritas en C y C++, y fue lanzada para sistemas Unix entre 1980s y 1990s, se puede utilizar en una variedad de casos. Debido a su naturaleza CLI, es ideal para ejecutarse en servidores o dispositivos remotos. También se puede iniciar en segundo plano con un trabajo programado utilizando herramientas como `cron`.

## Instalación en Linux

Para comprobar que tcpdump esté instalado en el sistema:

```bash
which tcpdump
/usr/sbin/tcpdump
```

Si tcpdump no está instalado, se puede instalar usando el administrador de paquetes `dnf`:

```bash
sudo dnf install tcpdump
```

Tcpdump requiere `libpcap`, una biblioteca para la captura de paquetes de red. Si no está instalado, se agrega automáticamente como dependencia.

## Captura de paquetes con tcpdump

Para capturar paquetes, tcpdump requiere permisos elevados, por lo que los siguientes comandos tienen el prefijo `sudo`.

### Para ver qué interfaces están disponibles para capturar:

```bash
sudo tcpdump --list-interfaces
sudo tcpdump -D
```

*-D es la abreviación de --list-interfaces*

También es posible ver las interfaces disponibles con el siguiente comando:

```bash
ip a s
```
o
```bash
ip address show
```

### Para capturar paquetes de cualquier interfaz:

```bash
sudo tcpdump --interface any
```

`any` se puede reemplazar con algún nombre de interfaz que haya salido con `sudo tcpdump -D`.

Usando este comando, tcpdump capturará paquetes hasta que reciba una señal de interrupción. Se puede interrumpir la captura con `ctrl + c`, o añadiendo la opción `-c COUNT` (para contar):

```bash
sudo tcpdump --interface any -c 5
```

Esto es útil en diferentes escenarios. Por ejemplo, si se quiere solucionar un problema de conectividad y capturar algunos paquetes iniciales es suficiente. Esto es aún más útil cuando aplicamos filtros para capturar paquetes específicos.

Por defecto, tcpdump resuelve las [[Direcciones IP]] y los [[Puertos]] en nombres, pero cuando se intentan solucionar problemas de red, suele ser más fácil utilizar las [[Direcciones IP]] y los números de [[Puertos]]. Para deshabilitar la resolución de nombres se utiliza `-n`, y para la resolución de puertos `-nn`

```bash
sudo tcpdump -i any -c5 -nn
```

Lo anterior, a su vez, evita que tcpdump emita búsquedas de DNS, lo que ayuda a reducir el tráfico de red al solucionar problemas de red.

### Para guardar paquetes capturados

Usamos `-w FILE`. La extensión más común es `.pcap`. Los paquetes guardados pueden ser inspeccionados usando otros programas, como [[Wireshark]]. Si elegimos la opcion `-w` no se van a ver el scroll de los paquetes.

### Para leer los paquetes capturados de un paquete 

Usamos `-r FILE`. Esto es especialmente útil para aprender sobre el comportamiento del protocolo.

### Para imprimir más detalles

Usamos `-v`, `-vv` o `-vvv`. Cada uno produce una salida más detallada. Según la página del manual de Tcpdump, la adición de `-v` imprimirá el "time to live, identification, total length and options in an IP packet".

## Filtrando Expresiones

### Filtrar por Host

Se puede limitar los paquetes capturados a un host usando `host IP` o `host HOSTNAME`. Por ejemplo:

```bash
sudo tcpdump host example.com -w http.pcap
```

En el comando anterior, limitamos el host a `example.com` y guardamos la lectura de paquetes con `-w http.pcap`.

Si queremos limitar la búsqueda desde una dirección IP o un hostname, podemos usar `src host IP` o `src host HOSTNAME`. De igual forma, podemos limitar la captura de paquetes que van hacia un destino en específico con `dst host IP` o `dst host HOSTNAME`.

### Filtrar por [[Puertos]]

De igual modo que con `host`, podemos limitar los paquetes capturados con `port PORT_NUMBER`. Y si queremos limitar los paquetes con un puerto de origen específico usamos `src port PORT_NUMBER`, para limitar los que van hacia un puerto se usa `dst port PORT_NUMBER`.

### Filtrar por Protocolo

Otro método para filtrar es por un protocolo en específico, por ejemplo `ip`, `ip6`, `udp`, `tcp`, y `icmp`.

En el ejemplo siguiente se van a limitar los paquetes para capturar los que contengan ICMP:
```bash
sudo tcpdump -i ens5 icmp -n
```

## Operadores Lógicos

Hay tres operadores lógicos que pueden ser de ayuda:

* `and`, captura paquetes donde ambas condiciones sean `true`. Por ejemplo, `tcpdump host 1.1.1.1 and tcp` captura tráfico `tcp` con `host 1.1.1.1`
* `or`, captura paquetes donde cualquiera de las dos condiciones sean `true`. Por ejemplo, `tcpdump udp or icmp` captura tráfico `UDP` o `ICMP`.
* `not`, captura paquetes cuando la condicion es `not true`. Por ejemplo, `tcpdump not tcp` captura todos los paquetes excepto los segmentos `TCP`, en cambio, se espera recibir paquetes `UDP`, `ICMP` y `ARP` entre los resultados.

## Filtrado Avanzado

Se recomienda consultar la pagina del manual `pcap-filter` con el comando `man pcap-filter`. Para este caso, nos centraremos en una opción avanzada que permite filtrar paquetes según los indicadores TCP. Comprender estos indicadores facilitará la creación de este conocimiento y el dominio de técnicas de filtrado más avanzadas.
### Filtrar por tamaño

* `greater LENGTH`, filtra paquetes que sean iguales o mayores que el largo especificado.
* `less LENGTH`, filtra paquetes que tengan menos o la misma cantidad especificada.

### Operaciones binarias

Una operación binaria funciona con bits, es decir, con ceros y unos. Una operación toma uno o dos bits y devuelve un bit.

* & (and) toma dos bits y devuelve 0 a menos de que ambas entradas sean 1.
* | (or) toma dos bits y devuelve uno a menos de que ambas entradas sean 0.
* ! (not) toma un bit y lo invierte; una entrada de 1 da 0 y una entrada de 0 da 1.

### Bytes de encabezado

El propósito en esta sección es poder filtrar paquetes en función del contenido de un byte de encabezado. Considere los siguientes protocolos: ARP, Ethernet, ICMP, IP, TCP y UDP. Éstos son sólo algunos protocolos de red.

Al utilizar pcap-filter, Tcpdump le permite hacer referencia al contenido de cualquier byte de encabezado utilizando la siguiente sintaxis `proto[expr:size]`, donde:

* `proto` se refiere al protocolo.
* `expr` indica el desplazamiento de bytes, donde `0` se refiere al primer byte.
* `size` indica el número de bytes que nos interesan, que pueden ser uno, dos o cuatro. Es opcional y es 1 por defecto.

Para comprender esto, consideremos los dos ejemplos de la página del manual de pcap-filter:

* `ether[0] & 1 !=0` toma el primer byte del encabezado Ethernet y el número decimal 1 (es decir, `0000 0001` en binario) y aplica el `&` (operación binaria `and`). Devuelve verdadero si el resultado no es igual a 0 (es decir, `0000 0000`). El propósito de este filtro es mostrar paquetes enviados a una dirección de multidifusión. Una dirección Ethernet de multidifusión es una dirección particular que identifica un grupo de dispositivos destinados a recibir los mismos datos.
* `ip[0] & 0xf != 5` toma el primer byte del encabezado IP y lo compara con el número hexadecimal F (es decir, `0000 0001` en binario). Devuelve verdadero si el resultado no es igual al decimal 5 (es decir, `0000 0101` en binario), El propósito de este filtro es capturar todos los paquetes IP con opciones.

Estos ejemplos parecen complejos. Pero para este punto no es necesariamente comprender completamente los ejemplos anteriores. Por ahora, nos centraremos en filtrar paquetes TCP en función de indicadores TCP establecidos.

Podemos usar `tcp[tcpflags]` para referirnos al campo de las flags TCP. Las siguientes flags están disponibles para ser comparadas:

* `tcp-syn`, Synchronize.
* `tcp-ack`, Acknowledge.
* `tcp-fin`, Finish.
* `tcp-rst`, Reset.
* `tcp-push`, Push.

Basado en lo anterior, podemos escribir:

* `tcpdump "tcp[tcpflags] == tcp-syn"`, para capturar paquetes TCP con sólo el indicador SYN (Synchronize) configurado, mientras que todos los demás no están configurados.
* `tcpdump "tcp[tcpflags] & tcp-syn != 0"`, para capturar los paquetes TCP con al menos el conjunto de indicadores SYN
* `tcpdump "tcp[tcpflags] & (tcp-syn|tcp-ack) != 0"`, para capturar paquetes TCP con al menos SYN o que tengan establecidos los indicadores ACK.

## Visualización de Paquetes

Tcp es un programa enriquecido con muchas opciones para personalizar cómo se imprimen y muestran los paquetes. Ahora vamos a cubrir las cinco opciones siguientes:

* `-q`, salida rápida, imprimir información breve del paquete.
* `-e`, imprimir el encabezado a nivel de enlace (MAC).
* `-A`, mostrar datos de paquetes en ASCII.
* `-xx`, mostrar datos de paquetes en formato hexadecimal.
* `-X`, mostrar encabezados de paquetes y datos en hexadecimal y ASCII

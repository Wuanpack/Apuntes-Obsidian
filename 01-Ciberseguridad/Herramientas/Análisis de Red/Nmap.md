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

[[Nmap#Descubrimiento de Sistemas|Más detalles aquí.]]

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

`-iL <archivo_entrada>` (Entrada de una lista)

* Toma la especificación de objetivos del archivo `<archivo_entrada>`. Habitualmente es un tanto molesto especificar una lista de sistemas muy grande en la línea de órdenes, pero es algo que también uno quiere hacer. Para sondear un número elevado de objetivos sólo tiene que generar la lista en un archivo y entregárselo a Nmap con la opción `-il`. 
* Las entradas de este archivo pueden estar en cualquiera de los formatos aceptados por Nmap en la línea de órdenes (direcciones IP, nombres de sistema, CIDR, IPv6 o rangos de octeto). 
* Cada elemento debe estar separado por uno o más espacios, tabuladores, o por líneas.
* Si quiere leer el archivo de la entrada estándar puede especificar un guión (-) como nombre de archivo.

`-iR <cant. sistemas` (Elegir objetivos al azar)

* Cuando se quieren realizar encuestas que cubran toda Internet uno puede querer elegir objetivos al azar. La opción `<cant. sistemas>` indica a Nmap cuántas direcciones  IP debe generar aleatoriamente. Se filtran de forma automática las direcciones no deseables, incluyendo las direcciones privadas, de multicast o direccionamiento no asignado.
* Si se utiliza el valor 0, Nmap realizará un análisis que no acabará nunca. Hay que tener en cuenta que a algunos administradores de red puede no gustarle que les analices sus redes, y pueden quejarse. Si realmente está aburrido, puede intentar la orden `nmap -sS -PS80 -iR 0 -p 80` para encontrar servidores web al azar para navegar.

`--exclude <equipo1[,equipo2][,equipo3],...` (Excluir equipo o redes)

* Indica con una lista separada por comas los objetivos que deben excluirse del análisis. Se excluirán aunque se encuentren dentro de un rango especificado en la línea de órdenes.
* La lista que se indica utiliza la sintaxis normal de Nmap, por lo que puede incluir nombres de equipos, rangos de red CIDR, rangos de octeto, etc.
* Esto puede ser útil cuando la red a analizar tiene objetivos que no se deben tocar, como puedan ser servidores de misión crítica, que pueden reaccionar adversamente a un análisis de puertos, o si la red incluye subredes administradas por otras personas.

`--excludefile <archivo>` (Excluir desde una Lista).

* Al igual que `--exclude`, esta función permite excluir objetivos, pero en lugar de utilizar la línea de órdenes toma el listado de un `<archivo>`, que utiliza la misma sintaxis que la opción `-iL`.

## Descubrimiento de Sistemas

Uno de los primeros pasos en cualquier misión de reconocimiento de red es el de reducir un conjunto de rangos de direcciones IP en una lista de equipos activos o interesantes. Analizar cada puerto de cada una de las direcciones IP es lento, y usualmente innecesario.

Evidentemente depende del propósito del análisis. Los administradores de red pueden interesarse sólo en equipos que estén ejecutando un cierto servicio, mientras que los auditores de seguridad pueden interesarse en todos y cada uno de los dispositivos que tengan una dirección IP.

Un administrador puede obtener un listado de equipos en su red interna mediante un ping IMCP, mientras que un consultor en seguridad realizando nu ataque externo puede llegar a un conjunto de docenas de sondas en su intento de saltarse las restricciones de los cortafuegos.

Siendo tan diversas las necesidades de descubrimiento de sistemas, Nmap ofrece una variedad de opciones para personalizar las técnicas utilizadas. Al descubrimiento de sistemas (Host Discovery) se lo suele llamar sondeo ping, pero va más allá de la simple solicitud ICMP echo-request de los paquetes asociados al querido y nunca bien ponderado ping.

Los usuarios pueden evitar el paso de ping utilizando un sondeo de lista (`-sL`), o deshabilitando el ping (`-P0`), o enviando combinaciones arbitrarias de sondas TCP SYN/ACK, UDP e ICMP a múltiples puertos de la red remota. El propósito de estas sondas es el de solicitar respuestas que demuestren que una dirección IP se encuentra activa (está siendo utilizada por un equipo o dispositivo de red). En varias redes solo un pequeño porcentaje de direcciones IP se encuentran activos en cierto momento. 

Esto es aprticularmente común en las redes basadas en direccionamiento privado RFC1918, como la 10.0.0.0/8. Dicha red tiene más de 16 millones de direcciones IP, pero se ha visto siendo utilizada por empresas con menos de 1000 máquinas. El descubrimiento de sistemas puede encontrar dichas máquinas en un rango tan grande como el indicado.

Si no se proveen opciones de descubrimiento de sistemas. Nmap envía un paquete TCP ACK al puerto 80 y un ICMP Echo Request a cada máquina objetivo. Una excepción a este comportamiento es cuando se utiliza un análisis ARP, para los objetivos que se encuentren en la red Ethernet local. Para los usuarios de shell UNIX que no posean privilegios, un paquete SYN es enviado en vez del ACK, utilizando la llamada al sistema `connect()`. Estos valores por omisión son el equivalente a las opciones `-PA` y `-PE`. Este descubrimiento de sistemas es generalmente suficiente cuando se analizan redes locales, pero para auditorías de seguridad se recomienda utilizar un conjunto más completo de sondas de descubrimiento.

Las opciones `-P*` (que permiten seleccionar los tipos de ping) pueden combinarse. Puede aumentar sus probabilidades de penetrar cortafuegos estrictos enviando muchos tipos de sondas utilizando diferentes puertos o banderas TCP y códigos ICMP. Recuerde que el ARP discovery (`-PR`) se realiza por omisión contra objetivos de la red Ethernet local incluso si se especifica otra de las opciones `-P*`, porque es generalmente más rápido y efectivo.

`-sL` (Sondeo de lista)

* El sondeo de lista es un tipo de descubrimiento de sistemas que tan solo lista cada equipo de la/s red/es especificada/s, sin enviar paquetes de ningún tipo a los objetivos. Por omisión, Nmap va a realizar una resolución inversa DNS en los equipos, para obtener sus nombres.
* Adicionalmente, al final, Nmap reporta el número total de direcciones IP. El sondeo de lista es una buena forma de asegurarse de que tenemos las direcciones IP correctas de nuestros objetivos. Si se encontraran nombres de dominios que no reconoces, vale la pena investigar un poco más, para evitar realizar un análisis de red de la empresa equivocada.

`-sP` (Sondeo ping)

* Esta opción le indica a Nmap que únicamente realice descubrimiento de sistemas mediante un sondeo ping, y que luego emita un listado de los equipos que respondieron al mismo. No se realizan más sondeos, como un análisis de puertos o detección de sistema operativo.
* A diferencia del sondeo de lista, el análisis de ping es intrusivo, ya que envía paquetes a los objetivos, pero es usualmente utilizado con el mismo propósito. Permite un reconocimiento liviano de la red objetivo sin llamar mucho la atención. El saber cuántos equipos se encuentran activos es de mayor valor para los atacantes que el listado de cada una de las IP y nombres proporcionado por el sondeo de lista.
* De la misma forma, los administradores de sistemas suelen encontrar valiosa esta opción. Puede ser fácilmente utilizada para contabilizar las máquinas disponibles en una red, o monitorizar servidores. A esto se le llama barrido ping, y es más fiable que hacer ping a la dirección de broadcast, ya que algunos equipos no resopnden a este tipo de consultas.
* Esta opción envía una solicitud de eco ICMP y TCP al puerto 80 por omisión. Cuando un usuario sin privilegios ejecuta Nmap se envía un paquete SYN (utilizado en la llamada `connect()`) al puerto 80 del objetivo. Cuando un usuario privilegiado intenta analizar objetivos en la red Ethernet local se utilizan solicitudes ARP (`-PR`) a no ser que se especifique la opción `--send-ip`.
* También puede combinarse con cualquiera de las opciones de sondas de descubrimiento (las opciones `-P*`, excepto `-P0`) para disponer de mayor flexibilidad. Si se utiliza cualquiera de las opciones de sondas de descubrimiento y número de puerto, se ignoran las sondas por omisión (ACK y solicitud de eco ICMP). Se recomienda utilizar estas técnicas si hay un cortafuegos con un filtrado estricto entre el sistema que ejecuta Nmap y la red objetivo. Sino se hace así pueden llegar a pasarse por alto ciertos equipos, ya que le cortafuegos anularía las sondas o las respuestas a las mismas.

`P0` (No realizar ping)

* Con esta opción, Nmap no realiza la etapa de descubrimiento. Bajo circunstancias normales, Nmap utiliza dicha etapa para determinar qué máquinas se encuentran activas para hacer un análisis más agresivo. Por omisión, Nmap sólo realiza ese tipo de sondeos, como análisis de puertos, detección de versión o del sistema operativo contra los equipos que están "vivos". 
* Nmap utilizará funciones de análisis solicitadas contra todas las direcciones IP especificadas. Por lo tanto, si se especificauna red del tamaño de una clase B cuyo espacio de direccionamiento es de 16 bits, en la línea de órdenes, se analizará cada una de las 65.536 direcciones IP. 
* El segundo carácter de esta opción es un "0", no una "O".
* Al igual que con el sondeo de lista, se evita el descubrimiento apropiado de sistemas, pero, en vez de detenerse y emitir un listado de objetivos, Nmap continúa y realiza las funciones solicitadas como si cada IP objetivo se encontrara activa.

`PS` (Lista de puertos) (Ping TCP SYN)

* Esta opción envía un paquete TCP vacío con la bandera SYN puesta. El puerto destino por omisión es 80 (se puede configurar el tiempo de compilación cambiando el valor de DEFAULT_TCP_PROBE_PORT en nmap.h), pero se puede añadir un puerto alternativo como parámetro. También se puede especificar una lista de puertos separados por comas (ej: -PS22,23,25,80,223,1050). Si hace esto se enviarán sondas en paralelo a cada uno de los puertos.
* La bandera SYN indica al sistema remoto que quiere establecer una conexión. Normalmente, si el puerto destino está cerrado se recibirá un paquete RST (de "reset"). Si el puerto está abierto entonces el objetivo responderá con el segundo paso del saludo del three-way handshake TCP con un paquete TCP SYN/ACK. El sistema donde se ejecuta Nmap romperá la conexión que se está estableciendo enviando un paquete RST en lugar de enviar el paquete ACK que completaría el saludo TCP. Nmap no envía este paquete, sino que lo envía el núcleo del sistema donde se ejecuta Nmap respondiendo al paquete SYN/ACK que no esperaba.
* A Nmap no le importa si el puerto está abierto o cerrado. Si, tal y como se acaba de describir, llega una respuesta RST o SYN/ACK entonces Nmap sabrá que el sistema está disponible y responde.
* En sistemas Unix, generalmente sólo el usuario privilegiado root puede enviar paquetes TCP crudos. Los usuarios no privilegiados tienen una forma de evitar esa restricción utilizando la llamada al sistema "connect()" contra el puerto destino. Esto hace que se envíe el paquete SYN al sistema, para establecer la conexión. Si la llamada "connect()" devuelve un resultado de éxito rápidamente o un fallo ECONNREFUSED entonces se puede deducir que la pila TCP que tiene bajo ésta ha recibido un SYN/ACK o un RST y que puede marcar el sistema como disponible. El sistema se puede marcar como no disponible si el intento de conexión se mantiene parado hasta que vence un temporizador. Esta es también la forma en la que se gestiona esto en conexiones IPv6 ya que Nmap aún no puede crear paquetes IPv6 crudos.

`-PA [lista de puertos] (Ping TCP ACK)`

* El ping TCP ACK es muy parecido al ping SYN que se acaba de tratar. La diferencia es que en este caso se envía un paquete con la bandera ACK en lugar de la SYN. Este paquete indica que se han recibido datos en una conexión TCP establecida, pero se envían sabiendo que la conexión no existe. En este caso los sistemas deberían responder con un paquete RST, lo que sirve para determinar que están vivos.
* Esta opción utiliza el mismo puerto por omisión que la sonda SYN (puerto 80) y también puede tomar una lista de puertos destino en el mismo formato. Si un usuario sin privilegios intenta hacer esto, o se especifica un objetivo IPv6, se utiliza el procedimiento descrito anteriormente. Aunque en este caso el procedimiento no es perfecto porque la llamada «connect()» enviará un paquete SYN en lugar de un ACK.
* Se ofrecen tanto mecanismos de sondeo con ping SYN y ACK para maximizar las posibilidades de atravesar cortafuegos. Muchos administradores configuran los enrutadores y algunos cortafuegos sencillos para que se bloqueen los paquetes SYN salvo para aquellos destinados a los servicios públicos, como pudieran ser el servidor web o el servidor de correo de la organización. Esto evita que se realicen otras conexiones entrantes al mismo tiempo que permite a los usuarios realizar conexiones salientes a Internet. Este acercamiento de filtrado sin estados toma poco recursos de los cortafuegos/enrutadores y está ampliamente soportado por filtros hardware y software.
* El programa de corgafuegos Netfilter/iptables de Linux ofrece la opción `--syn` para implementar este acercamiento sin estados. Cuando se han implementado reglas de filtrado como éstas es posible que se bloqueen las sondas ping SYN (`-PS`) cuando éstas envíen a un puerto cerrado. Sin embargo, en estos casos, las sondas ACK podrían saltarse las reglas y llegar a su destino.
* Otros tipos de cortafuegos comunes utilizan reglas con estados que descartan paquetes  no esperados. Esta funcionalidad se encontraba antes fundamentalmente en los cortafuegos de gama alta pero se ha hecho cada vez más común. El sistema Netfiler/iptables de Linux soporta esta posibilidad a través de la opción `--state`, que hace categorías de paquetes en base a su estado de conexión. En estos sistemas es más probable que funcione una sonda SYN, dado que los paquetes ACK no esperados se reconocen como falsos y se descartan. Una solución a este dilema es enviar sondas SYN y ACK especificando tanto la opción `-PS` como `-PA`.

`-PU [lista de puertos] (Ping UDP)`

* El ping UDP es otra opción para descubrir sistemas. Esta opción envía un paquete UDP vacío (salvo que se especifique `--data-length`) a los puertos indicados. La lista de puertos se debe dar en el mismo formato que se ha indicado anteriormente para las opciones `-PS` y `-PA`. 
* Si no se especifica ningún puerto se utiliza el puerto 31338 por omisión. Se puede configurar este puerto por omisión en el momento de compillar cambiando DEFAULT_UDP_PROBE_PORT en nmap. Se utiliza un puerto alto y poco común por omisión porque no es deseable enviar este sondeo a otro tipo de puertos.
* La sonda UDP debería generar un paquete ICMP de puerto no alcanzable si da contra un puerto cerrado en el sistema objetivo. Si llega éste entonces Nmap puede identificar ese sistema como vivo y alcanzable. Otros errores ICMP, como el de sistema o red inalcanzables o TTL excedido indican un sistema que está muerto o que no es alcanzable.
* Si no llega ninguna respuesta también se entiende que el sistema no está disponible. Si se alcanza un puerto abierto la mayoría de los servicios simplemente descartarán el paquete vacío y no devolverán ninguna respuesta. Esta es la razón por la que se utiliza el puerto por omisión 31338 ya que es poco probable que esté utilizándose. Algunos servicios, como chargen, responderán con un paquete UDP vacío lo que ayuda a Nmap a determinar que el sistema está disponible.
* La ventaja principal de este tipo de sondeos es que atraviesan cortafuegos y filtros que sólo analizan TCP. 

`-PE; -PP; -PM (Tipos de ping ICMP)`

* Nmap puede enviar los paquetes estándar que envía el programa íng además de los tipos de descubrimiento de equipos con TCP y UDP. Nmap envía paquetes ICMP tipo 7 («echo request») a las direcciones IP objetivos y espera recibir un tipo 0 («Echo Reply») de los sistemas que estén disponibles. Lamentablemente para los exploradores de redes, muchos sistemas y cortafuegos ahora bloquean esos paquetes en lugar de responder como requiere el estándar RFC 1122. 
* Por ésta razón los sondeos que sólo utilizan protocolo ICMP no son muy fiables para analizar sistemas desconocidos de Internet. Aunque pueda ser una forma eficiente y práctica de hacerlo para administradores que tengan que monitorizar una red interna. Utilice la opción `-PE` para activar este comportamiento de solicitud de eco.
* Nmap no hace sólo esto, aunque la solicitud eco es la consulta estándar del ping ICMP. el estpandar ICMP (RFC 792) también especifica solicitudes de huellas de tiempo, de información y de máscara de red, que corresponden con los códigos 13, 15, 17 respectivamente.
* Aunque el objetivo de estas solicitudes es obtener la máscara de red o fecha actual de un sistema también pueden utilizarse para descubrir sistemas. Un sistema que responde es porque está vivo y disponible. Nmap no implementa los paquetes de solicitud de información en sí, ya que no están muy soportados.
* El estándar 1122 insiste en que "un equipo NO DEBE implementar estos mensajes". Las consultas de tiempo (código ICMP 14) o de máscara de red (código 18) entonces es que el sistema está disponible. Estas dos consultas pueden ser útiles cuando los administradores bloquean los paquetes de consulta eco explícitamente pero se olvidan de que se pueden utilizar otras consultas ICMP con el mismo fin.

`-PR (Ping ARP)`

* Una de las formas de uso más comunes de Nmap es el sondeo de una red de área local Ethernet. En la mayoría de las redes locales hay muchas direcciones IP sin usar en un momento determinado. Esto es así especialmente en las que utilizan rangos de direcciones privadas definidas en el RFC1918. 
* Cuando Nmap intenta enviar un paquete IP crudo, como pudiera ser una solicitud de eco ICMP, el sistema operativo debe determinar primero la dirección (ARP) correspondiente a la IP objetivo para poder dirigirse a ella en la trama Ethernet. Esto es habitualmente un proceso lento y problemático, dado que los sistemas operativos no se escribieron pensando en que tendrían que hacer millones de consultas ARP contra sistemas no disponibles en un corto periodo de tiempo.
* El sondeo ARP hace que sea Nmap y su algoritmo optimizado el que se encargue de las solicitudes ARP. Si recibe una respuesta, no se tiene ni que preocupar de los paquetes basados en IP dado que ya sabe que el sistema está vivo. 
* Esto hace que el sondeo ARP sea mucho más rápido y fiable que los sondeos basados en IP. Por ello se utiliza por omisión cuando se analizan sistemas Ethernet si Nmap detecta que están en la red local. Nmap utiliza ARP para objetivos en la misma red local aún cuando se utilicen distintos tipos de ping (como `-PE` o `-PS`). Si no quiere hacer un sondeo ARP tiene que especificar la opción `--send-ip`.

`-n (No realizar resolución de nombres)`

* Le indica a Nmap que nunca debe realizar resolución DNS inversa de las direcciones IP activas que encuentre. Ya que DNS es generalmente lento, esto acelera un poco las cosas.

`-R (Realizar resolución de nombres con todos los objetivos)`

* Le indica a Nmap que deberá realizar siempre la resolución DNS inversa de las direcciones IP objetivo. Normalmente se realiza esto sólo si se descubre que el objetivo se encuentra vivo.

`--system-dns (Utilizar resolución DNS del sistema)`

* Por omisión, Nmap resuelve direcciones IP por si mismo enviando las consultas directamente a los servidores de nombres configurados en el sistema, y luego espera las respuestas. Varias solicitudes (generalmente docenas) son realizadas en paralelo para mejorar el rendimiento.
* Especifica esta opción si desea que sí se utiliza la resolución del sistema (una IP por vez utilizando la llamada getnameinfo()). Este método es más lento y raramente útil, a no se que hubiera un error en el código DNS de Nmap. Éste es el método por omisión para los sondeos IPv6.

`--dns-servers <servidor1[,servidor2],...> (Servidores a utilizar para las consultas DNS)`

* Nmap generalmente determina los servidores DNS en su archivo resolv.conf (UNIX) o del registro (Win32). Puede utilizar esta opción para especificar sus propios servidores. Esta opción no se utiliza si utiliza la opción `--system-dns` o está realizando un sondeo IPv6. La resolución a través de más de un servidor de DNS es generalmente más rápida que la consulta a uno solo.
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


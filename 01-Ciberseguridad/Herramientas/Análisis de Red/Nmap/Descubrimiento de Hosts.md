---
tags:
  - herramientas/analisis-red/nmap
---

Nmap ofrece una variedad de opciones para personalizar las técnicas utilizadas. Al descubrimiento de sistemas (Host Discovery) se lo suele llamar sondeo ping, pero va más allá de la simple solicitud ICMP echo-request de los paquetes asociados al querido y nunca bien ponderado ping.

Los usuarios pueden evitar el paso de ping utilizando un sondeo de lista (`-sL`), o deshabilitando el ping (`-P0`), o enviando combinaciones arbitrarias de sondas TCP SYN/ACK, UDP e ICMP a múltiples puertos de la red remota. El propósito de estas sondas es el de solicitar respuestas que demuestren que una dirección IP se encuentra activa (está siendo utilizada por un equipo o dispositivo de red). En varias redes solo un pequeño porcentaje de direcciones IP se encuentran activos en cierto momento. 

Esto es particularmente común en las redes basadas en direccionamiento privado RFC1918, como la 10.0.0.0/8. Dicha red tiene más de 16 millones de direcciones IP, pero se ha visto siendo utilizada por empresas con menos de 1000 máquinas. El descubrimiento de sistemas puede encontrar dichas máquinas en un rango tan grande como el indicado.

Si no se proveen opciones de descubrimiento de sistemas. Nmap envía un paquete TCP ACK al puerto 80 y un ICMP Echo Request a cada máquina objetivo. Excepto cuando se usa el análisis ARP, para los objetivos que se encuentren en la red Ethernet local. Para los usuarios de shell UNIX que no posean privilegios, un paquete SYN es enviado en vez del ACK, utilizando la llamada al sistema `connect()`. Estos valores por omisión son el equivalente a las opciones `-PA` y `-PE`. Este descubrimiento de sistemas es generalmente suficiente cuando se analizan redes locales, pero para auditorías de seguridad se recomienda utilizar un conjunto más completo de sondas de descubrimiento.

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

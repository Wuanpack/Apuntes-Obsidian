---
tags:
  - herramientas/analisis-red/nmap
---
La mayoría de los distintos tipos de sondeo disponibles sólo los puede llevar a cabo un usuario privilegiado. Esto es debido a que envían y reciben paquetes en crudo, lo que hace necesario tener acceso como administrador (root) en la mayoría de los sistemas UNIX. 

En los entornos Windows es recomendable utilizar una cuenta de administrador, aunque Nmap algunas veces funciona para usuarios no privilegiados en aquellas plataformas donde se haya instalado WinPcap. 

La necesidad de privilegios como usuario administrador era una limitación importante cuando se empezó a distribuir Nmap en 1997, ya que muchos usuarios sólo tenian acceso a cuentas compartidas en sistemas como usuarios normales. Ahora, las cosas son distintas. Los ordenadores son más baratos, hay más personas que tienen acceso permanente a Internet, y los sistemas UNIX (incluyendo Linux y MAC OS X) son más comunes.

También se dispone de una versión para Windows de Nmap, lo que permite que se ejecute en más escritorios. Por todas estas razones, cada vez es menos necesario ejecutar Nmap utilizando cuentas de sistemas compartidas. Esto es bueno, porque las opciones que requieren de más privilegios hacen que Nmap sea más potente y flexible.

Aunque Nmap intenta generar resultados precisos, hay que tener en cuenta que estos resultados se basan en los paquetes que devuelve el sistema objetivo (o los firewalls que están delante de éstos). Estos sistemas pueden no ser fiables y enviar respuestas cuyo objetivo sea confundir a Nmap.

Son aún más comunes los sistemas que no cumplen con los estándares RFC, que no responden como deberían a las sondas de Nmap.

Son especialmente susceptibles a este problema los sondeos FIN, Null y Xmas. Hay algunos problemas específicos a algunos tipos de sondeos que se discuten en las entradas dedicadas a sondeos concretos.

Esta sección documenta las aproximadamente doce técnicas de sondeo de puertos que soporta Nmap. Sólo puede utilizarse un método en un momento concreto, salvo por el sondeo UDP (`-sU`) que puede combinarse con cualquiera de los sondeos TCP. Para que sea fácil de recordar, las opciones de los sondeos de puertos son del estilo `-s<C>`, donde `<C>` es una letra caracerística del nombre del sondeo, habitualmente la primera.

La única excepción a esta regla es la opción obsoleta del sondeo FTP rebotado (`-b`). Nmap hace un sondeo SYN por omisión, aunque lo cambia a un sondeo Connect() si el usuario no tiene los suficientes privilegios para enviar paquetes en crudo (requiere acceso de administrador en UNIX) o si se especificaron objetivos IPv6. De los sondeos que se listan en esta sección los usuarios sin privilegios sólo pueden ejecutar los sondeos Connect() o de rebote FTP.

`-sS (sondeo TCP SYN)`

El sondeo SYN es el utilizado por omisión y el más popular por buenas razones. Puede realizarse rápidamente, sondeando miles de puertos por segundo en una red rápida en la que no existan firewalls.

El sondeo SYN es relativamente sigiloso y poco molesto, ya que no llega a completar las conexiones TCP. También funciona contra cualquier pila TCP en lugar de depender de la idiosincrasia específica de una plataforma concreta, al contrario de lo que pasa con los sondeos de Nmap Fin/Null/Xmas, Maimon o pasivo. También muestra un aclara y fiable diferenciación entre los estados abierto, cerrado y filtrado.

A esta técnica se la conoce habitualmente como sondeo medio abierto, porque no se llega a abrir una conexión TCP completa. Se envía un paquete SYN, como si se fuera a abrir una conexión real y después se espera una respuesta. Si se recibe un paquete SYN/ACK esto indica que el puerto está en escucha (abierto), mientras que si se recibe un RST (reset) indica que no hay nada escuchando en el puerto. Si no se recibe ninguna respuesta después de realizar algunas retransmisiones entonces el puerto se marca como filtrado. También se marca como peurto filtrado si se recibe un error de tipo ICMP no alcanzable (tipo 3, códigos 1, 2, 3, 9, 10 o 13).

`-sT (sondeo TCP connect ()`

El sondeo TCP Connect () es el sondeo TCP por omisión cuando no se puede usar el sondeo SYN. Esto sucede, por ejemplo, cuando el usuario no tiene privilegios para enviar paquetes en crudo o cuando se están sondeando redes IPv6.

Nmap le pide al sistema operativo subyacente que establezcan una conexión con el sistema objetivo en el puerto indicado utilizando la llamada del sistema `connect ()`, a diferencia de otros tipos de sonde, que escriben los paquetes a bajo nivel. 

Ésta es la misma llamada del sistema de alto nivel que la mayoría de las aplicaciones de red, como los navegadores web o los clientes P2P, utilizan para establecer una conexión. Esta llamada es parte del interfaz de programación conocido como la API de conectores de Berkeley. También, en lugar de leer las respuestas directamente de la línea, Nmap utiliza esta API para obtener la información de estado de cada intento de conexión.

Generalmente es mejor utilizar un sondeo SYN, si este está disponible. Nmap tiene menos control sobre la llamada de alto nivel `Connect()` que cuando se utiliza paquetes en crudo, lo que hace que sea menos eficiente. La llamada al sistema completa las conexiones para abrir los puertos objetivo, en lugar de realizar el reseteo de la conexión medio abierta como hace el sondeo SYN.

Esto significa que se tarda menos tiempo y son necesarios más paquetes para obtener la información, pero también significa que los sistemas objetivos van a registrar probablemente la conexión. Un IDS decente detectará cualquiera de los dos, pero la mayoría de los equipos no tienen este tipos de sistemas de alarma.

Sin embargo, muchos servicios de los sistemas UNIX habituales añadirán una nota en el syslog, y algunas veces con un mensaje de error extraño, dado que Nmap realiza la conexión y luego la cierra sin enviar ningún dato. Los servicios realmente patéticos morirán cuando ésto pasa, aunque no es habitual. Un administrador que vea muchos intentos de conexión en sus registros que provengan de un único sistema debería saber que ha sido sondeado con este método.

 `-sU (sondeos UDP)`

Aunque la mayoría de los servicios más habituales en Internet utilizan el protocolo TCP, los servicios UDO también son muy comunes. Tres de los más comunes son los servicios DNS, SNMP y DHCP (puertos registrados 53, 161/162 y 67/68 respectivamente). Dado que el sondeo UDP es generalmente más lento y más difícil que TCP, algunos auditores de seguridad ignoran estos puertos. Esto es un error, porque es muy frecuente encontrarse servicios UDP vulnerables y los atacantes no ignoran estos protocolos. Afortunadamente, Nmap puede utilizarse para hacer un inventario de puertos UDP.

El sondeo UDP puede combinarse con un tipo de sondeo TCP como el sondeo SYN (`-sS`) para comprobar ambos protocolos al mismo tiempo.

Los sondeos UDP funcionan mediante el envío (sin datos) de una cabecera UDP para cada puerto objetivo. Si se obtiene un error ICMP que indica que el puerto no es alcanzable (tipo 3, código 3) entonces se marca el puerto como cerrado. Si se recibe cualquier error ICMP no alcanzable (tipo 3, códigos 1, 2, 9, 10, o 13) se marca el puerto como filtrado. En algunas ocasiones se recibirá una respuesta al paquete UDP, lo que prueba que el puerto está abierto. Si no se ha recibido ninguna respuesta después de algunas retransmisiones entonces se clasifica el puerto como abierto|filtrado. Esto significa que el puerto podría estar abiero o que hay un filtro de paquetes bloqueando la comunicación. Puede utilizarse el sondeo de versión (`-sV`) para diferenciar de verdad los puertos abiertos de los filtrados.

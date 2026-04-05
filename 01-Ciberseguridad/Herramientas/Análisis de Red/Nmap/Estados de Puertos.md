---
tags:
  - herramientas/analisis-red/nmap
---
Nmap comenzó como un analizador de puertos eficiente, aunque ha aumentado su funcionalidad a través de los años, aquella sigue siendo su función primaria. La sencilla orden `nmap <objetivo>`. Aunque muchos analizadores de puertos han agrupado tradicionalmente los puertos de dos estados: abierto o cerrado, Nmap es mucho más descriptivo. Se dividen a los puertos en seis estados distitos:

* abierto
* cerrado
* filtrado
* no filtrado
* abierto|filtrado
* cerrado|filtrado

Los seis estados de un puerto, según Nmap

## Abierto

Una aplicación acepta conexiones TCP o paquetes UDP en este puerto. El encontrar esta clase de puertos es generalmente el objetivo primerio de realizar un sondeo de puertos. Las personas orientadas a la seguridad saben que cada puerto abierto es un vector de ataque. 

Los atacantes y las personas que realizan pruebas de intrusión intentan aprovechar puertos abiertos, por lo que los administradores intentan cerrarlos, o protegerlos con cortafuegos, pero sin que los usuarios legítimos pierdan acceso al servicio. 

Los puertos abiertos también son interesantes en sondeos que no están relacionados con la seguridad porque indican qué servicios están disponibles para ser utilizados en una red.

## Cerrado

Un puerto cerrado es accesible: recibe y responde a las sondas de Nmap, pero no tiene una aplicación escuchando en él. Pueden ser útiles para determinar si un equipo está activo en cierta dirección IP (mediante [[Descubrimiento de Hosts]], o sondeo ping), y es parte del proceso de detección de sistema operativo.

Como los puertos cerrados son alcanzables, o sea, no se encuentran filtrados, puede merecer la pena analizarlos pasado un tiempo, en caso de que alguno se abra. Los administradores pueden querer considerar bloquear estos puertos con un firewall. Si se bloquean aparecerían filtrados, como se discute a continuación.

## Filtrado

Nmap no puede determinar si el puerto se encuentra abierto porque un filtrado de paquetes previene que sus sondas alcancen el puerto. El filtrado puede provenir de un dispositivo de firewall dedicado, de las reglas de un enrutador, o por un firewall instalado en el propio equipo. 

Estos puertos suelen frustrar a los atacantes, porque proporcionan muy poca información. A veces responden con mensajes de error ICMP del tipo 3, código 13 (destino inalcanzable: comunicación prohibida por administradores), pero los filtros que sencillamente descartan las sondas sin responder son mucho más comunes. Esto fuerza a Nmap a reintentar varias veces, considerando que la sonda pueda haberse descartado por congestión en la red en vez de haberse filtrado. Esto ralentiza drásticamente los sondeos.

## No Filtrado

Este estado indica que el puerto es accesible, pero que Nmap no puede determinar si se encuentra abierto o cerrado. Solamente el sondeo ACK, utilizado para determinar las reglas de un cortafuegos, clasifica los puertos según este estado.

El analizar puertos no filtrados con otros tipos de análisis, como el sondeo Window, SYN o FIN, pueden ayudar a determinar si el puerto se encuentra abierto.

## Abierto | Filtrado

Nmap marca a los puertos en este estado cuando no puede determinar si el puerto se encuentra abierto o filtrado. Esto ocurre para tipos de análisis donde no responden los puertos abiertos. 

La ausencia de respuesta también puede significar que un filtro de paquetes ha descartado la sonda, o que se elimina cualquier respuesta asociada. De esta forma, Nmap no puede saber con certeza si el puerto se encuentra abierto o filtrado. Los sondeos UDP, protocolo IP, FIN, Null y Xmas clasifican a los puertos de esta manera.

## Cerrado | Filtrado

Este estado se utiliza cuando Nmap no puede determinar si un puerto se encuentra cerrado o filtrado, y puede aparecer sólo un sondeo IPID pasivo.
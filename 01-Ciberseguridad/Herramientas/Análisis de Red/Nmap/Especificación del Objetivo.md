---
tags:
  - herramientas/analisis-red/nmap
---
Todo lo que se escriba en la línea de parámetros de Nmap que no sea una opción se considera una especificación del sistema objetivo. Ej: la indicación de sólo una IP, o nombre de sistema, para que sea analizado.

Nmap soporta el direccionamiento estilo CIDR (192.168.10.0/24 o 205.217.153.63/16). La máscara más pequeña permitida es /1 y la más grande es /32.

CIDR es breve pero no siempre suficientemente flexible. Para ello se puede usar el direccionamiento por octetos. Para ello se puede especificar una lista separada por comas de números o rangos para cada octeto. Ej: 0-255.0-255.13.37, el cual realiza un sondeo en todo internet con las IPs que terminen en 13.37. Este tipo de muestreo amplio puede ser útil para encuestas de Internet y con fines de investigacion

Sólo puede especificar direcciones IPv6 si utiliza su nombre IPv6 totalmente cualificado o su nombre de sistema. No se soporta el uso de CIDR o rangos de octetos para IPv6 porque raramente son útiles.

Con Nmap puede especificar múltiples sistemas en la línea de órdenes y no tienen que ser del mismo tipo. Ej: `nmap scanme.nmap.org 192.168.0.0/16 10.0.0,1,3-7.0-255`.

Aunque habitualmente se especifican los objetivos en la línea de órdenes puede utilizar las siguientes opciones para controlar la selección de objetivos:

`-iL <archivo_entrada>` (Entrada de una lista)

* Toma la especificación de objetivos del archivo `<archivo_entrada>`.
* Las entradas de este archivo pueden estar en cualquiera de los formatos aceptados por Nmap en la línea de órdenes (direcciones IP, nombres de sistema, CIDR, IPv6 o rangos de octeto). 
* Cada elemento debe estar separado por uno o más espacios, tabuladores, o por líneas.
* Si quiere leer el archivo de la entrada estándar puede especificar un guión (-) como nombre de archivo.

`-iR <cant. sistemas>` (Elegir objetivos al azar)

* Cuando se quieren realizar encuestas que cubran toda Internet uno puede querer elegir objetivos al azar. La opción `<cant. sistemas>` indica a Nmap cuántas direcciones IP debe generar aleatoriamente. Se filtran de forma automática las direcciones no deseables, incluyendo las direcciones privadas, de multicast o direccionamiento no asignado.
* Si se utiliza el valor 0, Nmap realizará un análisis que no acabará nunca.

`--exclude <equipo1[,equipo2][,equipo3],...` (Excluir equipo o redes)

* Indica con una lista separada por comas los objetivos que deben excluirse del análisis. Se excluirán aunque se encuentren dentro de un rango especificado en la línea de órdenes.
* La lista que se indica utiliza la sintaxis normal de Nmap, por lo que puede incluir nombres de equipos, rangos de red CIDR, rangos de octeto, etc.
* Útil cuando la red a analizar tiene objetivos que no se deben tocar.

`--excludefile <archivo>` (Excluir desde una Lista).

* Al igual que `--exclude`, esta función permite excluir objetivos, pero en lugar de utilizar la línea de órdenes toma el listado de un `<archivo>`, que utiliza la misma sintaxis que la opción `-iL`.
---
tags:
  - blue-team/IDS-IPS
---

Si un atacante logra bypassear un firewall por una conexión que se ve legítima y luego realiza cualquier actividad maliciosa dentro de la red, debería haber algo para detectarlo en un tiempo apropiado. Para este propósito tenemos una solución llamada Intrusion Detection System (IDS).

## Tipos de IDS

Los IDS pueden estar categorizados de formas distintas dependiendo de ciertos factores. La categorización principal de un IDS depende de su despliegue y sus modos de detección.

### Deployment Modes

Los IDS pueden ser desplegados de las siguientes maneras:

* Host Intrusion Detection System (HIDS): Soluciones IDS basadas en host que son instaladas individualmente en los hosts y son responsables solamente de detectar amenazas de seguridad potenciales asociadas con un host particular. Proporcionan visibilidad de las actividades de los hosts. Sin embargo, los HIDS pueden ser complicados de manejar en redes grandes ya que son resource-intensive y requieren control en cada host.
* Network Intrusion Detection System (NIDS): Estas soluciones IDS son cruciales en la detección de actividades potencialmente maliciosas dentro de la red completa, independientemente de cualquier anfitrión específico. Monitorean el tráfico de red de todos los hosts involucrados para detectar actividades sospechosas. Proporciona una vista centralizada de todas las detecciones dentro de toda la red.

### Detection Modes

* Signatura-Based IDS: Muchos ataques ocurren todos los días. Cada ataque tiene su patrón único, el cual es conocido como firma. Estas firmas son preservadas por el IDS en sus bases de datos para detectar cualquier ataque que ocurra en el futuro por su firma. Mientras más fuerte sea la base de datos de firmas del IDS, más eficientemente va a detectar amenazas conocidas. Sin embargo, los IDS basados en firmas son incapaces de detectar ataques zero-day. Los ataques zero-day no tienen firmas previas (patrones) y no están guardadas dentro de las bases de datos de los IDS.
* Anomaly-Based IDS: Este tipo de IDS primero aprende del comportamiento normal (baseline) de la red o sistema y realiza detecciones si hay cualquier desviación del comportamiento normal. Los IDS basados en anomalías también detectan ataques zero-day porque no recaen en la disponibilidad de firmas para detección. Sin embargo, este tipo de IDS puede generar muchos falsos positivos porque la naturaleza de la mayoría de programas coincide con los maliciosos. Podemos reducir estos falsos positivos modificando finamente el IDS.
* Hybrid IDS: Un IDS híbrido compita los métodos de detección con los IDS basados en firmas y los IDS basados en anomalías para aumentar la fuerza por cada acercamiento.

## Ejemplo de IDS: Snort

Snort es uno de los IDS open-source más ampliamente usados desarrollado en 1998. Usa detecciones basadas en anomalías y firmas para identificar amenazas conocidas. Estos también están definidos en los archivos de reglas de la herramienta Snort. Muchos archivos de reglas built-in viene pre instalados en los paquetes de esta herramienta.

Estas reglas built-in contienen una variedad de patrones de ataque conocidos. Pueden detectar mucho tráfico malicioso por ti. Sin embargo, puedes detectar tipos específicos de tráfico de red no cubierto por los archivos de reglas predeterminadas. 

### Modos de Snort


| Modo                | Descripción                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Packet Sniffer Mode | Este modo lee y muestra paquetes de red sin realizar ningún análisis en ellos. No se relaciona directamente con capacidades IDS, pero puede ser de ayuda en el monitoreo de red y troubleshooting. En algunos casos, los administradores de red podrían necesitar leer el flujo de tráfico sin realizar ninguna detección para diagnosticar problemas específicos. Este modo permite mostrar el tráfico de red en la consola o incluso generarlo en un archivo.                                                                                                                     |
| Packet Logging Mode | Snort realiza detección en el tráfico de la red en tiempo real y muestra las detecciones como alertas en la consola para que los administradores de seguridad toman acciones. Sin embargo, en algunos casos, el tráfico de red necesita ser registrado para un análisis posterior. Permite registrar el tráfico de red como un archivo PCAP (standard packet capture format). Esto incluye todo el tráfico de red y cualquier detección de estos. Los investigadores forense pueden usar los archivos de registro Snort para realizar análisis de causas raíces de ataques previos. |
| Network IDS mode    | Es el modo primario que monitorea el tráfico de red en tiempo real y aplica sus archivos de reglas para identificar cualquier coincidencia con patrones de ataques conocidos guardados como firmas. Si hay una coincidencia genera una alerta. Este modo proporciona las principales funcionalidades de una solución IDS.                                                                                                                                                                                                                                                           |

Snort tiene algunos archivos de reglas built-in, un archivo de configuración, y otros archivos. Estos se almacenan en el directorio `/etc/snort`. El archivo clave para Snort es su archivo de configuración `snort.conf`, donde puedes especificar cuales reglas acivar, qué rango de red monitorear, y permitir otras configuraciones. Estos archivos de reglas están almacenados en la carpeta `rules`.

### Formato de Reglas

Hay una manera específica de escribir reglas. Ejemplo:

![[Pasted image 20260421022347.png]]


* Action: Este especifica cual acción tomar cuando la regla se dispara. En este caso, tenemos la acción "alert" cuando el tráfico coincide con esta regla.
* Protocol: Se refiere al protocolo que coincide con esta regla. En este caso, usamos el protocolo "ICMP" cuando hacemos ping a un host.
* Source IP: Este determina el IP que origina el tráfico. Como queremos detectar el tráfico de cualquier fuente IP, quedó establecido como "any".
* Source Port: Este determina el puerto desde el que se origina el tráfico. Como queremos detectar el tráfico desde cualquier puerto, quedó establecido como "any".
* Destination IP: Esto especifica la dirección IP de destino a la que llega el tráfico coincidente; genera una alerta. En este caso usamos "$HOME_NET". Esta es una variable, y nosotros definimos su valor como el rango de red completo en el archivo de configuración de Snort.
* Destination Port: Especifica el puerto que el tráfico podría alcanzar. Como queremos detectar cualquier tráfico entrante por cualquier puerto, quedó establecido en "any".
* Rule Metadata: Todas las reglas tienen algo de metadata. Este es definido al final de la regla en paréntesis. Los siguientes son sus componentes:
	* Mensaje (msg): Esto describe el mensaje que se muestra cuando se activa la regla del sujeto. El mensaje debería indicar el tipo de actividad detectada. En este caso, usamos "Ping Detected".
	* Signature ID (sid): Cada regla tiene un identificador único que se diferencia de otros. Este indicador se llama signature ID (sid). En este caso, establecimos el sid a "10001".
	* Rule Revision (rev): Esto establece el número de revisión de la regla. Cada vez que la regla es modificada, su número de revisión es incrementado, el cual ayuda en el seguimiento de cambios de cualquier regla.

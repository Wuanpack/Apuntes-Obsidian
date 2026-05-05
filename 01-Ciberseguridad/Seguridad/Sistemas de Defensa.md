---
tags:
  - seguridad
---
## Índice
```table-of-contents
```
## Seguridad de Endpoint

Puede aplicarse a cualquier dispositivo final que contenga un sistema operativo compatible, como es el caso de las estaciones de trabajo que no necesariamente son ocupadas como un punto de trabajo para herramientas productivas que utilizan suites de ofimática o para videollamadas.

Para este caso, también existen equipos que son utilizados en tiendas de retail o supermercados como puntos de venta, comúnmenta llamados POS. También es posible ver herramientas de seguridad en dispositivos móviles, ya sea tablets o smartphones.

## Antivirus

Es un software utilizado para proteger endpoints de amenazas previamente conocidas, los fabricantes crean bases de datos con listas negras de archivos, las cuales son llamadas firmas.

Estas firmas son utilizadas para permitir o denegar el inicio de un ejecutable, el cual puede corromper el sistema, tanto dañando la integridad de los archivos como al realizar acciones involuntarias de carácter malicioso.

Actualmente, el antivirus es conocido como Endpoint Protection Platform (EPP).

## Endpoint Detection and Response ([[Endpoint Detection and Response (EDR)]])

Los [[Endpoint Detection and Response (EDR)]] nacen ante la necesidad de poder cubrir de mejor forma la superficie de ataque de un [[Malware]]. Para un antivirus, al ser un sistema de firmas, si la amenaza cambia ligeramente de forma, esta ya no es la amenaza inicial; si la amenaza modificada no se encuentra en las firmas y no hemos actualizado estas, la emnaza probablemente se ejecutará con éxito; mientras que con una solución de [[Endpoint Detection and Response (EDR)]], esta podría ser reconocida, tanto por comportamiento, o por su [[Hash|hash]], llamado Indicador de Compromiso (IoC).

Adicionalmente, los [[Endpoint Detection and Response (EDR)]] detienen ataques también a base de Inteligencia Artificial, aprendiendo sobre una amenaza, ejecutando también en un entorno aislado para determinar a qué tipo de amenaza corresponde. Finalmente, este sistema permite realizar investigaciones en profundidad sobre los ataques que han sido contenidos.

## HIPS

Es un sistema de protección de intrusos basado en host, conocido en inglés como Host Based Intrusion Prevention System. Es un sistema de protección de amenazas de red, pero instalado directamente en el endpoint, el que tienen algunas misiones como el bloqueo de comportamientos en evetos de red.

## Firewall de Aplicación

Es un software que es capaz de generar bloqueos a la red, a las aplicaciones instaladas en el endpoint. Este software puede bloquear tanto conexiones de salkida como de entrada directamente en el host. Algunos ejemplos son Windows Firewall, Comodo Firewall o Zone Alarm.

## Seguridad en la Red

La seguridad debe centrarse en todas las partes que conforman la red, también en los endpoints como en el perímetro antes de la red local, previniendo el ingreso de amenazas externas.

La forma más frecuente de atacar un endpoint o una estación de trabajo, es a través de la red, toda la información viaja por esta vía antes de llegar a cualquier dispositivo, ya sea por cable o de manera inalámbrica.

Existen diversos sistemas que nos permiten proteger la red, sin embargo, no todos estos sistemas son necesariamente de bloqueo o respuesta, también existen los sitemas que recopilan información y entregan alertas para que los analistas de ciberseguridad puedan tomar los resguardos necesarios ante las amenazas detectadas.

Conceptos relacionados:

* [[Firewall]]
* [[Router|Router (ACL)]]
* [[NAC]]
* [[Switch]]
* [[Intrusion Detection System (IDS)]]
* [[Intrusion Prevention System (IPS)]]

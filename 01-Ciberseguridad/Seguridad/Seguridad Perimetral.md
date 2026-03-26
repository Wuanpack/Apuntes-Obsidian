---
tags:
  - seguridad
---

## ¿Qué es?

La seguridad perimetral es la encargada de proteger nuestra red local de ataques provenientes de internet, aunque no siempre es el caso, ya que podemos proteger cualquier red desde otra. Para este fin es que definimos nuestra [[LAN]] como un verdadero perímetro de seguridad, a fin de evitar que ingresen conexiones no deseadas. 

## Black Hole

El Blackholing es una técnica habitualmente utilizada para mitigar ataques de [[DoS|Denegación de Servicio]] hacia nuestra red, puede ejecutarse desde el mismo firewall, o desde el [[Router]] utilizado como puerta de enlace de nuestro [[Firewall]].

## Filtro de Contenido

El [[Firewall#DNS Firewall|DNS Firewall]], al utilizar la técnica de Sinkholding, puede enviar una petición de un sitio cualquiera a una [[IP]] distinta a la real.

El filtro de contenido, comúnmente, se conoce debido a que a través de [[Proxy|servidores proxy]] podemos realizar el bloqueo de diversos sitios web.

Originalmente, los [[Proxy|servidores proxy]] nacen para acelerar el acceso a internet, guardando copias de los sitios visitados en un caché local en el servidor, evitando que las visitas posteriores dentro de nuestra red tuvieran que ir a buscar a internet nuevamente la página solicitada.

Debemos recordar que hace no muchos años, no todos los sitios web utilizar el protocolo [[HTTPS]], sino que solo utilizaban el protocolo [[HTTP]] a secas, sin cifrar, lo cual permitía que el [[Proxy]] interceptara el tráfico sin cifrar para generar una copia en caché de disco de este.

## Contenidos Relacionados

* [[Firewall]]
* [[Proxy]]
* [[Firewall#DNS Firewall|DNS Firewall]]

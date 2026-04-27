---
tags:
  - cloud
---
## Índice
```table-of-contents
```
## ¿Qué es la computación en nube?

De acuerdo con el [[NIST Cybersecurity Framefork (CSF)|National Institute of Standards and Technology (NIST)]], este define la computación en la nube como un modelo que permite un acceso conveniente a la red bajo demanda, a un conjunto compartido de recursos informáticos configurables tales como: redes, servidores, almacenamiento, aplicaciones y otros servicios que se pueden aprovisionar y liberar rápidamente con un mínimo esfuerzo en gestión o interacción con el proveedor de servicios.

## Características Fundamentales de la Computación en Nube

De acuerdo con [[NIST Cybersecurity Framefork (CSF)]], una nube debe tener las siguientes cinco características:

* Rápida elasticidad: la elasticidad se define como la capacidad de aumentar o reducir los recursos según sea necesario. Para los consumidores, la nube parece infinita y pueden adquirir tanta o tan poca potencia informática como necesitan.
* Servicio medido: los aspectos del servicio de la nube son controlados y monitoreados por el proveedor de nube. Esto es crucial para la facturación, el control de acceso, la optimización de recursos, la planificación de capacidad entre otras tareas.
* Autoservicio bajo demanda: Los aspectos de autoservicio y bajo demanda de la computación en la nube significan que un consumidor puede utilizar los servicios según sea necesario sin ninguna interacción humana con el proveedor.
* Acceso ubicuo a la red: significa que las capacidades del proveedor de la nube están disponibles a través de la red y se pueden acceder a ellas a través de mecanismos estándar tanto para clientes pesados como ligeros.
* Agrupación de recursos: la agrupación de recursos permite a un proveedor de la nube antender a sus consumidores a través de un modelo multiinquilino. Los recursos físicos y virtuales se asignan y reasignan según la demanda. Existe cierta independencia de ubicación en el sentido de que los clientes generalmente no tienen control ni conocimiento sobre la ubicación exacta de los recursos, sin embargo, pueden especificar una ubicación geográfica tal como: país, estado o centro de datos.

## Nube Pública

Ofrece sus servicios a una gama completa de clientes. La naturaleza pública de este modelo es similar a Internet, es decir, los usuarios y servicios pueden estar en cualquier lugar de la World Wide Web. El entorno informático se comparte con varios inquilinos, en un modelo gratuito o de pago por uso.

Un ejemplo es Amazon Web Services (AWS), que ofrece Elastic Compute Cloud (EC2) a cualquier persona con una tarjeta de cŕedito. Normalmente, los precios de alquiler de servidores se cobran por hora.

## Nube Privada

Restringe a sus usuarios a un subconjunto seleccionado, generalmente a una organización específica dentro de una empresa determinada. La Nube Privada es similar a una intranet, es decir, sus servicios se brindan internamente a través de la red interna de una organización.

Un ejemplo es una empresa que ofrece servicios basados en la nube detrás de [[Firewall|firewalls]] corporativos a sus empleados ubicados en diferentes sitios. Los departamentos internos contribuyen o pagan para construir dicha nube, normalmente mantenida por los servicios de TI corporativos.

## Nube Híbrida

Los proveedores de Nube Híbrida ofrecen sus servicios a un rango estrechamente definido de usuarios privados, que, de ser necesario, pueden expandirse para residir en una infraestructura de nube púbica. Alternativamente, un proveedor de servicios públicos puede gestionar de forma remota parte de la infraestructura de una organización privada y utilizar la nube para realizar copias de seguridad.

Un ejemplo es una empresa con un centro de datos interno, que además utiliza la nube pública para determinadas tareas que no son misión crítica o durante períodos de demanda excesiva. El servicio central de TI determina la política sobre cuándo utilizar recursos internos frente a externos, generalmente en función de los patrones de uso o de la confidencialidad de los datos que se comparten y la urgencia de tareas.

## Community Cloud

La infraestructura de la nube es compartida por varias organizaciones para apoyar una comunidad específica. Un ejemplo es un gran complejo de viviendas con servicios comunitarios basados en la nube exclusivos para sus residentes. Todos los residentes, de manera similar a las instalaciones de respaldo de generación de energía o agua es una comunidad cerrada, usan y comparten el costo de dichos servicios.

## Virtual Private Cloud (VPC)

Esto simula una experiencia de nube privada pero ubicada dentro de un clúster de infraestructura de nube pública, como una organización de mantenimiento de la salud que ofrece servicios privados a sus miembros, pero aloja sus datos y aplicaciones en servidores segregados dentro de AWS. Debido a la naturaleza de los datos y las tareas que se manejan, un clúster ce VPC puede estar físicamente aislado en términos de almacenamiento, redes, etc., lo que significa que a los usuarios de VPC se les cobra un costo fijo y luego una cantidad variable según sus patrones de uso.

## [[Virt-Manager|Virtualización]] como tecnología habilitadora de la nube

La [[Virt-Manager|Virtualización]] es una tecnología habilitante de la nube, ya que permite a los proveedores de la nube brindar servicios a los usuarios con su hardware físico existente. Por otra parte, permite a los usuarios de la nube adquirir solo los recursos que necesitan cuando los necesitan y escalar estos recursos de manera rentable en la proporción que crecen sus cargas de trabajo.

## Disponibilidad y Confiabilidad

En el contexto de la nube, un acuerdo de nivel de servicio (SLA) es un acuerdo entre un proveedor de servicios en la nube y un cliente que garantiza que se mantenga un nivel mínimo de servicio. Las métricas más utilizadas se encuentran asociadas a la confiabilidad, disponibilidad y capacidad de respuesta de los sistemas y aplicaciones.

### Disponibilidad

La alta disponibilidad en la computación de la nube corresponde a la capacidad de un sistema o aplicación de permanecer accesible y operativo durante un largo período de tiempo. Es una característica clave de los servicios de la nube, ya que garantiza que puedan manejar diferentes niveles de carga y recuperarse rápidamente de cualquier falla.

En un sistema de alta disponibilidad, las aplicaciones críticas suelen estar distribuidas en varios servidores, centros de datos o incluso regiones geográficas. Así, en el caso que un componente falle, la carga de trabajo se traslada automáticamente a otro componente para evitar interrupciones en el servicio. Por consiguiente, la alta disponibilidad es clave para garantizar que las empresas puedan continuar sus operaciones sin problemas, sin tiempos de inactividad ni interrupciones de servicio.

### Confiabilidad

La confiabilidad en la computación en la nube está relacionada con la calidad de la tecnología en la nube. En este sentido, si los componentes de un servicio en la nube realizan sus funciones y fallan raramente, se dice que el servicio es confiable.

En términos formales, la confiabilidad se define como la capacidad de un sistema o componente para realizar sus funciones requeridas en condiciones indicadas durante un período de tiempo especificado.

Varios factores contribuyen a la confiabilidad de los servicios de computación en la nube, entre ellos destacan:

* Tolerancia a fallas: se refiere a la capacidad de un sistema de continuar funcionando incluso cuando parte de él falla.
* Redundancia: se refiere a la duplicación de componentes o funciones críticas de un sistema que permiten aumentar su confiabilidad.
* Recuperación ante eventos catastróficos: alude al conjunto de políticas, herramientas y procedimientos necesarios para reestablecer el normal funcionamiento de un sistema luego de un evento catastrófico.
## Modelos de Servicio

### Software as a Service (SaaS)

Permite al consumidor utilizar las aplicaciones del proveedor que se ejecutan en una infraestructura de Nube. El usuario no necesita preocuparse por el sistema operativo, los tipos de CPU, la memoria o el almacenamiento necesario para estas aplicaciones.

Además, los desarrolladores de software pueden implementar nuevas versiones y parches sin preocuparse por los instaladores u otros modelos de distribución, cobrando a los usuarios mediante suscripción, de forma muy similar a los servicios de televisión por cable. Un ejemplo de este modelo es el uso de Microsoft Office 365, Zoom, Dropbox, entre otros.

### Platform as a Service (PaaS)

Permite al consumidor implementar en la infraestructura de la nube aplicaciones creadas o adquiridas utilizando lenguajes de programación, bibliotecas, servicios y herramientas compatibles con el proveedor. Este es un nivel inferior al SaaS, pero el usuario no necesita preocuparse por el hardware subyacente, como la memoria, el almacenamiento o las capacidades de la CPU. Un ejemplo de este modelo es Google Workspace y Microsoft Azure App Service.

### Infraestrucure as a Service (IaaS)

Permite al consumidor aprovisionar procesamiento de CPU, almacenamiento, redes y otros recursos informáticos en los niveles de abstracción más bajos, con la capacidad de implementar y ejecutar software, que puede incluir sistemas operativos y aplicaciones. Un ejemplo de este modelo es Amazon Web Services (AWS) y Google Cloud Platform (GCP), en particular, el uso de computación en demanda con servicios como AWS EC2 o Google Compute Engine.


## Habilitadores de competitividad entre proveedores

1. Latencia de la red: Los clientes exigen un gran ancho de banda para superar los problemas de latencia, pero en una cadena de flujo de datos, la demora está determinada por el eslabón más débil. Por lo tanto, los proveedores de servicios suelen utilizar el almacenamiento en caché local cerca de la ubicación del cliente.
2. Migración y aprovisionamiento detallados: Son necesarios para evitar copiar gigabytes de datos cuando es necesario desactivar un servidor físico por mantenimiento planificado o no planificado, por ejemplo, para cambiar su memoria o ventiladores. En este caso, se toman instantáneas periódicas de una [[Virt-Manager|máquina virtual]] para ayudar con una migración rápida, pero es necesario asegurarse de que estas instantáneas de memoria estén protegidas para evitar comprometer la información de un usuario en la nube.
3. Standards and open-source solutions for Cloud SW infraestructure: Se necesita soporte, ya que actualmente la mayoría de proveedores de nube de nivel comercial utlizan sus representaciones de datos internas. En caso de que un proveedor se declare en quiebra o el cliente desee migrar sus datos a otro proveedor, es importante que la información se almacene de manera que pueda ser leída por otros con las claves de seguridad necesarias.
4. Sincronización de datos Offline vs. Online: Ya que internet o el servicio eléctrico rara vez están garantizados las 24 horas del día, los 7 días de la semana en los mercados emergentes. Por lo tanto, los usuarios quieren utilizar dispositivos que vayan más allá de los navegadores de Internet que se ejecutan en clientes ligeros, que pueden almacenar copias locales de aplicaciones y datos que pueden ejecutarse usando un suministro de energía ininterrumpido y, al restablecerse el servicio público, pueden sincronizarse con la base de datos de los proveedores de la nube.
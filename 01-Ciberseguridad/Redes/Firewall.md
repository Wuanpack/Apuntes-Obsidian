---
tags:
  - redes
  - seguridad
---

## ¿Qué es?

Un firewall es un dispositivo de seguridad de red que separa una red interna confiable de una red externa considerada no confiable, como Internet. Regula el tráfico de red entrante y saliente basándose en reglas de seguridad preestablecidas.

Son fundamentales para proteger las redes del acceso no autorizado, actividades dañinas y amenazas potenciales, y pueden existir como hardware, software, [[Introducción Cloud#Software as a Service (SaaS)|software como servicio (SaaS)]], [[Introducción Cloud#Nube Pública|nube pública]] o [[Introducción Cloud#Nube Privada|nube privada]].

Los firewalls examinan los paquetes de red e implementan políticas de seguridad, impidiendo efectivamente que usuarios no autorizados o datos potencialmente dañinos se infiltren o salgan de una red. En particular, los firewalls sirven como guardianes, examinando cada paquete de red y decidiendo si lo permiten o lo bloquean según reglas preestablecidas.

Además de estas funciones principales, los firewalls de pŕoxima generación (NGFW) actuales tienen una variedad de características para reforzar la seguridad de la red. Estos incluyen inspección profunda de paquetes, visibilidad y control de aplicaciones, detección y prevención de intrusiones, defensa contra [[Malware]], filtrado de URL y más.

---

## Tipos de Firewalls

### Packet Filtering Firewall

Estos firewalls examinan cada paquete de datos que pasa a través de ellos y luego los filtran en función de parámetros como [[Direcciones IP|direcciones IP]] de origen y destino, números de [[Puertos|puerto]] y tipos de protocolo. Si bien estos firewalls son relativamente simples y rentables, no pueden examinar el contenido de los paquetes, lo que los 
hace menos efectivos contra ataques sofisticados

### [[Proxy]] Firewall

Es un tipo temprano de dispositivo de firewall que sirve como puerta de enlace de una red a otra para una aplicación específica. Los servidores proxy pueden proporcionar funcionalidad adicional, como almacenamiento en caché de contenido y seguridad, al evitar conexiones directas desde fuera de la red. Sin embargo, esto también puede afectar las capacidades de rendimiento y las aplicaciones que pueden soportar.

### Stateful Inspection Firewall

Ahora considerado un firewall tradicional, este tipo de firewall permite o bloquea el tráfico según el estado, el [[Puertos|puerto]] y el protocolo. Monitorea toda la actividad desde la apertura de una conexión hasta su cierra. las decisiones de filtrado se toman en función tanto de las reglas definidas por el administrador como del contexto, que se refiere al uso de información de conexiones anteriores y paquetes que pertenecen a la misma conexión

### Web Application Firewall (WAF)

Los firewalls de aplicaciones web actúan como intermediarios para redes internas y externas, manejando todas las solicitudes de comunicación en nombre de la red interna. Ofrecen un alto nivel de seguridad, ya que pueden inspeccionar el contenido de los paquetes y filtrar datos maliciosos o no autorizados. Sin embargo, su dependencia de servidores [[Proxy]] puede producir latencia y afectar el rendimiento de la red.

### Unified Threat Management (UTM) Firewall

Un dispositivo UTM normalmente combina, de forma débilmente acoplada, las funciones de un firewall de inspección con estado con prevención de intrusiones y antivirus. También puede incluir servicios adicionales y, a menudo, gestión de la nube. Los UTM se centran en la simplicidad y la facilidad de uso.

### Next-Generation Firewall (NGFW)

Un firewall de próxima generación (NGFW) es un dispositivo de seguridad de red que proporciona capacidades más allá de un firewall tradicional con estado. Si bien un firewall tradicional generalmente proporciona una inspección con estado del tráfico de red entrante y saliente, un firewall de próxima generación incluye funciones adicionales como conocimiento y control de aplicaciones, sistema de prevención de intrusiones (IPS), filtrado de URL basado en geolocalización y reputación, e inteligencia de amenazas. Un NGFW puede facilitar la administración y reducir la complejidad con políticas unificadas que protejan todo el continuo de ataques.

#### Cortafuegos impulsado por IA

Utilizan inteligencia artificial y machine learning para mejorar la protección contra amenazas y la seguridad de la red. Mientras que los firewalls tradicionales utilizan reglas predeterminadas para bloquear y detectar amenazas, los firewalls impulsados por IA funcionan en tiempo real para analizar el tráfico dinámico de la red, identificar patrones y ayudar a las organizaciones a automatizar la gestión del ciclo de vida de su política de firewall.

### Virtual Firewall

Normalmente se implemente como un dispositivo virtual. Se puede alojar localmente en un entorno de nube privada basado en VMware ESXi, Microsoft Hyper-V, KVM, OpenStack y Nutanix. También se puede implementar un firewall virtual en una infraestructura de nube pública, como Amazon Web Services (AWS), Microsoft Azure, Google Cloud Platform (GCP), Oracle Cloud Infraestructure (OCI). Con un firewall virtual, puede proteger sus aplicaciones y datos en entornos multicloud con controles de políticas unificados, administración centralizada y defensa avanzada contra amenazas.

### Cloud-Native Firewall

Los firewalls nativos de la nube modernizan la forma de proteger las aplicaciones y la infraestructura de carga de trabajo a escala. Con funciones de escalamiento automatizado, los firewalls nativos de la nube permiten que los equipos de operaciones de red y operaciones de seguridad funcionen a velocidades ágiles. Un firewall nativo de la nube admite seguridad ágil y elástica, capacidad multiinquilino y equilibrio de carga inteligente.
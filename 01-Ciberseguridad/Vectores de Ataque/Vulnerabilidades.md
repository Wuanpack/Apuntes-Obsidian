
Una vulnerabilidad es una debilidad en los programas software o en el hardware que un atacante puede aprovechar para comprometer el dispositivo digital. 

## Vulnerability Scanning

El escaneo de vulnerabilidades es la inspección de sistemas digitales para encontrar debilidades. Las organizaciones pueden cargar información crítica en su infraestructura digital. Deben escanear regularmente sus sistemas y redes por vulnerabilidades.

Los escaneos de vulnerabilidades pueden ser categorizados en varios tipos; sin embargo, la categorización mayor de estos scans se explica a continuación

### Authenticated vs Unauthenticated Scans

Los escaneos autenticados requieren las credenciales del host y algunos detalles más que los escaneos no autenticados. Estos tupos de escaneos son de ayuda para descubrir la superficie de ataque dentro del host. Sin embargo, los escaneos no autenticados son conducidos sin proporcionar credenciales del host sujeto. Estos escaneos puede ayudar a identificar la superficie de ataque desde afuera del host.


| Authenticated Scans                                                                                                      | Unauthenticated Scans                                                                                                 |
| ------------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------- |
| Las credenciales del host sujeto deben ser proporcionadas al escaner de vulnerabilidades.                                | El escáner de vulnerabilidades no requiere las credenciales del host; solo necesita la dirección IP.                  |
| Identifica las vulnerabilidades que pueden ser explotadas por atacantes que tienen acceso al host.                       | Identifica las vulnerabilidades que pueden ser explotadas por un atacante externo que no tiene acceso al host sujeto. |
| Proporciona una visibilidad profunda dentro del sistema objetivo al escanear su configuración y aplicaciones instaladas. | Su configuración requiere menos recursos y es sencilla.                                                               |
| Por ejemplo, escanear una base de datos interna al proporcionar sus credenciales al escáner de vulnerabilidades          | Por ejemplo, analizar un sitio web público en busca de vulnerabilidades que cualquier usuario pueda explotar.         |

### Internal vs External Scans

Los escaneos internos se conducen desde dentro de la red, mientras que los externos desde afuera.


| Internal Scans                                                                                                  | External Scans                                                                     |
| --------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Conducidos desde dentro de la red.                                                                              | Conducido desde fuera de la red.                                                   |
| Se enfoca en las vulnerabilidades que pueden ser explotadas dentro de la red.                                   | Se enfoca en las vulnerabilidades que pueden ser explotadas desde fuera de la red. |
| Identifica vulnerabilidades que podrían ser expuestos a los atacantes una vez puedan ingresar dentro de la red. | Identifica las vulnerabilidades expuestas desde fuera de la red.                   |

## Herramientas para el Escaneo de Vulnerabilidades

### Nessus

Nessus fue desarrollado como un proyecto open-source en 1998. Después fue adquirido por Tenable en 2005 y se convirtió en el propietario del software. Tiene una extensa opciones de escaneos de vulnerabilidades y es ampliamente usado en grandes empresas. Está disponible en versiones de pago y gratuitas. La versión gratuita ofrece un número limitado de características de escaneo, su versión comercial ofrece características de escaneo avanzadas, escaneos ilimitados, y soporte profesional. 

### Qualys

Qualys se desarrolló en 1999 como una solución de gestión de vulnerabilidades por suscripción. Además del escaneo continuo de vulnerabilidades, ofrece comprobaciones de cumplimiento y gestión de activos. Alerta automáticamente sobre las vulnerabilidades detectadas durante la monitorización continua. La principal ventaja de Qualys es que es una plataforma en la nube, lo que significa que no hay costes ni esfuerzos adicionales para mantenerla en funcionamiento en nuestro hardware físico ni para gestionarla.

### Nexpose

Nexpose fue desarrollada por Rapid7 en 2005, Nexpose es una solución de gestión de vulnerabilidades por suscripción que descubre continuamente nuevos activos en la red y realiza análisis de vulnerabilidades. Proporciona puntuaciones de riesgo de vulnerabilidad según el valor del activo y el impacto de la vulnerabilidad. Además, ofrece comprobaciones de cumplimiento con diversos estándares. Nexpose ofrece modos de implementación tanto locales como híbridos (en la nube y locales).

### OpenVAS (Open Vulnerability Assessment System)

OpenVAS es una solución de análisis de vulnerabilidades de código abierto desarrollada por Greenbone Security. Ofrece funciones básicas con análisis de vulnerabilidades conocidas a través de su base de datos. Si bien es menos completa que las herramientas comerciales, ofrece una experiencia similar a la de un escáner de vulnerabilidades completo. Resulta útil para pequeñas organizaciones y sistemas individuales. En la siguiente sección, exploraremos esta herramienta con mayor detalle mediante un análisis de vulnerabilidades.

## CVE

CVE significa Common Vulnerabilities and Exposures. Considere CVE como un número único para cada una de sus consultas y quejas. Si hay alguna actualización sobre un problema, puede darle seguimiento fácilmente utilizando el número CVE único. Siguiendo el ejemplo del servicio de asistencia técnica, este número CVE es un número único asignado a las vulnerabilidades. Fue desarrollado por la Corporación MITRE. Cada vez que se descubre una nueva vulnerabilidad en una aplicación de software, se le asigna un número CVE único como referencia y se publica en línea en una base de datos CVE. Esta publicación tiene como objetivo que las personas conozcan estas vulnerabilidades para que puedan aplicar medidas de protección para remediarlas. Puede encontrar los detalles de cualquier vulnerabilidad descubierta previamente en la base de datos CVE.

## CVSS

CVSS significa Common VulnerabilityScoring System. Si volvemos al ejemplo del servicio de asistencia técnica, siempre será necesario priorizar las quejas. La forma más eficiente de priorizarlas es según su nivel de gravedad. ¿Qué pasaría si todas las quejas se registraran con una puntuación de 0 a 10, donde una puntuación más alta indica una queja más grave? Esto resolvería el problema de priorizar las quejas críticas. Esto se conoce como puntuación CVSS. En el mundo de la informática, al igual que cada vulnerabilidad tiene un número CVE que la identifica de forma única, cada una tiene una puntuación CVSS que indica su gravedad. La puntuación CVSS se calcula considerando múltiples factores, como su impacto, la facilidad de explotación, etc. La gravedad según las puntuaciones CVSS se puede ver en la tabla a continuación:


| CVSS Score Range | Severity Levels |
| ---------------- | --------------- |
| 0.0 - 3.9        | Low             |
| 4.0 - 6.9        | Medium          |
| 7.0 - 8.9        | High            |
| 9.0 - 10         | Critical        |

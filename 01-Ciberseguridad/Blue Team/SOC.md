## ¿Qué es?

Un Security Operations Center (SOC) es una instalación dedicada operada por un equipo de seguridad especializado. Este equipo apunta al monitoreo continuo de la red de una organización y recursos para identificar actividad sospechosa para prevenir daños. Este equipo trabaja las 24 horas del día, los 7 días de la semana.

## Propósito y Componentes

El foco principal del equipo SOC es mantener la Detección y la Respuesta intactos. El equipo SOC tiene algunos recursos disponibles en forma de soluciones de seguridad que los ayudan a lograr esto. Estas soluciones integran la red de la compañía entera y todos los sistemas para monitorearlos desde una locación centralizada.

### Detection

* Detectar Vulnerabilidades: Una vulnerabilidad es una debilidad que un atacante puede explotar para sacar cosas más allá de su nivel de permisos. Una vulnerabilidad puede ser descubierta en cualquier software de dispositivo, como servidores o computadores. Por ejemplo, el SOC puede descubrir un conjunto de computadores con MS Windows que necesitan ser parcheados contra una vulnerabilidad específica publicada. Estrictamente hablando, las vulnerabilidades no son necesariamente responsabilidad del SOC; sin embargo, las vulnerabilidades no resueltas afectan el nivel de seguridad de la compañía entera.
* Detect Unauthorized Activity: Considera el caso donde el atacante descubre un nombre de usuario y contraseña de uno de los empleados y los usó para iniciar sesión en el sistema de la compañía. Es crucial detectar este tipo de actividad no autorizada rápido antes de que cause cualquier daño. Muchas pistas, como locación geográfica, pueden ayudarnos a detectar esto.
* Detect Policy Violations: Una política de seguridad es un conjunto de reglas y procedimientos creados para ayudar a proteger la compañía contra amenazas de seguridad y garantizar el cumplimiento. Lo que es considerado una violación podría variar de compañía en compañía.
* Detect Intrusions: Las intrusiones se refieren al acceso no autorizado a los sistemas y redes. Un escenario podría ser un atacante explotando exitosamente nuestra aplicación web. 

### Response

* Support with the Incident Response: Una vez el incidente es detectado, ciertos pasos son tomados para responderlo. Esta respuesta incluye minimizar su impacto y realizar el análisis de la causa raíz de este incidente. El equipo SOC también ayuda al equipo de respuesta ante incidentes a realizar estos pasos.

Hay tres pilares de un SOC. Con estos pilares, un equipo SOC se hace maduro y eficiente a la hora de detectar y responder diferentes incidentes. Estos pilares son Personas, Proceso y Tecnología.

## People

Mas allá de la evolución en la automatización de la mayoría de las tareas de seguridad, las Personas en un SOC siempre serán importantes. Una solución de seguridad puede generar numerosos red flags en un entorno SOC, lo que puede causer mucho ruido.

![[Pasted image 20260419212234.png]]


* SOC Analyst (Level 1): Cualquier cosa detectada por una solución de seguridad pasaría a través de este analista primero. Estos son los primeros en responder cualquier detección. Los analistas de nivel 1 del SOC realizan una clasificación básica de alertas para determinar si una detección específica es perjudicial. También informan de estas detecciones a través de los canales adecuados.
* SOC Analyst (Level 2): Si bien el Nivel 1 realiza el análisis de primer nivel, algunas detecciones pueden requerir una investigación más profunda. Los analistas de Nivel 2 les ayudan a profundizar en las investigaciones y a correlacionar los datos de múltiples fuentes para realizar un análisis adecuado.
* SOC Analyst (Level 3): Los analistas de nivel 3 son profesionales experimentados que buscan proactivamente indicadores de amenazas y brindan apoyo en las actividades de respuesta a incidentes. Las detecciones de gravedad crítica reportadas por los analistas de nivel 1 y 2 suelen corresponder a incidentes de seguridad que requieren respuestas detalladas, incluyendo contención, erradicación y recuperación. Aquí es donde la experiencia de los analistas de nivel 3 resulta fundamental.
* Security Engineer: Todos los analistas trabajan en soluciones de seguridad. Estas soluciones necesitan desplegarse y configurarse. Los Ingenieros de Seguridad depliegan y configuran estas soluciones de seguridad para asegurar una operación suave.
* Detection Engineer: Las reglas de seguridad son la lógica construida detrás de soluciones de seguridad para detectar actividades dañinas. Los analistas de nivel 2 y 3 a menudo crean estas reglas, mientras que el equipo SOC a veces también puede utilizar el rol de Detection Engineer independientemente para su responsabilidad.
* SOC Manager: El SOC Manager maneja los procesos que el equipo SOC sigue y provee apoyo. El SOC Manager también mantiene contacto con el CISO de la organización (Chief Information Security Officer) para proporcionarle actualizaciones sobre la postura de seguridad actual y los esfuerzos del equipo SOC.

Los roles en el equipo SOC pueden aumentar o disminuir dependiendo del tamaño y la criticidad de las organizaciones.

## Proceso

### Alert Triage

El alert triage es la base del equipo SOC. La primera respuesta a cualquier alerta es realizar el triage. El triage se enfoca en analizar una alerta específica. Esto determina la severidad de la alerta y nos permite priorizarla. Esta alerta trata de contestar las cinco Ws:


| 5 Ws   | Answers                                                                                                                                                                                                                                      |
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| What?  | Un archivo malicioso fue detectado en uno de los hosts dentro de la red de la organización.                                                                                                                                                  |
| When?  | El archivo fue detectado a las 13:20 el 5 de junio de 2024.                                                                                                                                                                                  |
| Where? | El archivo fue detectado en el directorio del host: "GEORGE PC".                                                                                                                                                                             |
| Who?   | Este archivo fue detectado por el usuario George.                                                                                                                                                                                            |
| Why?   | Después de la investigación, se encontró que el archivo fue descargado desde una página web vendedora de software pirateado. La investigación con el usuario reveló que ellos descargaron el archivo ya que querían usar el software gratis. |

### Reporting

Las alertas dañinas detectadas deben ser escaladas a analistas de nivel superior para una respuesta y resolución oportunas. Estas alertas se escalan como tickets y se asignan a las personas pertinentes. El informe debe abordar las 5 Ws junto con un análisis exhaustivo, y se deben utilizar capturas de pantalla como evidencia de la actividad.

### Incident Response and Forensics

En ocasiones, las detecciones reportadas apuntan a actividades altamente maliciosas que son críticas. En estos escenarios, los equipos de alto nivel inician una respuesta al incidente. Esta actividad forense tiene como objetivo determinar la causa raíz del incidente mediante el análisis de los artefactos de un sistema o red.

## Tecnología

Teniendo la Gente correcta y los Procesos en su lugar nunca sería suficiente sin soluciones de seguridad para detección y respuesta. 

Una red de organización consiste de muchos dispositivos y aplicaciones. Como equipo de seguridad, individualmente detectar y responder a amenazas en cada dispositivo o aplicación podría requerir un esfuerzo o recursos significantes. Las soluciones de seguridad centralizan toda la información de los dispositivos o aplicaciones presente en una red y automatizan las capacidades de detección y respuesta.

* SIEM: Security Information and Event Management (SIEM) es una herramienta popular usada en casi todos los entornos SOC. Esta herramienta colecicona registros desde varios dispositivos de red, referidos como log sources. Las reglas de detección son configuradas en la solución SIEM, la cual contiene lógica para identificar actividad sospechosa. La solución SIEM nos proporciona las detecciones tras correlacionarlas con múltiples fuentes de registro y nos alerta en caso de coincidencia con alguna de las reglas. Las soluciones SIEM modernas van más allá de este análisis de detección basado en reglas, proporcionándonos análisis del comportamiento del usuario y capacidad de inteligencia sobre amenazas. Los algoritmos de aprendizaje automático respaldan esto para mejorar las capacidades de detección. NOTA: La solución SIEM solo nos proporciona capacidades de Detección en un entorno SOC.
* EDR: Endpoint Detection and Response (EDR) proporciona al equipo SOC con visibilidad histórica y en tiempo real de las actividades de los dispositivos. Opera en el nivel de endopoint y pueden realizar respuestas automatizadas. EDR cuenta con amplias capacidades de detección de puntos finales, lo que le permite investigarlos en detalle y responder con unos pocos clics.
* Firewall: Un firewall funciona puramente para seguridad de red y actúa como una barrera entre las redes internas y externas (como internet). Monitorea tráfico de red entrante y saliente y filtra el tráfico no autorizado. El firewall también tiene reglas de detección desplegadas, las cuales nos ayudan a identificar y bloquear el tráfico sospechoso antes de que alcance la red interna.

Muchas otras soluciones de seguridad juegan roles únicos en un entorno SOC, como los antivirus, EPP, IDS/IPS, XDR, SOAR, y más. 
---
tags:
  - blue-team
  - blue-team/roles
---
## Índice
```table-of-contents
```
## Security Operations Center (SOC)

Un Security Operations Center es un equipo de profesionales de ciberseguridad que monitorean la red y sus sistemas para detectar eventos de ciberseguridad maliciosos. Algunas de las áreas de interés principales para un SOC son:

* Vulnerabilidades: Cuando una vulnerabilidad de sistema es detectada, es esencial arreglarlo instalando la actualización o parche apropiados. Cuando no hay una solución disponible, las medidas necesarias deberían ser tomadas para prevenir que un atacante lo explote. Aunque la remediación de vulnerabilidades es vital para un SOC, no necesariamente se les asigna.
* Policy Violations: Una política de seguridad es un conjunto de reglas requeridas para proteger la red y sus sistemas. Por ejemplo, puede ser una violación de políticas si un usuario sube datos confidenciales de la compañía a un servicio de almacenamiento online.
* Actividad no Autorizada: Considera el caso donde los datos de inicio de sesión de un usuario son robados, y el atacante los usa para iniciar sesión dentro de la red. Un SOC debe detectar y bloquear tales eventos ASAP antes de que se haga un daño mayor.
* Network Intrusions: No importa que tan buena es tu seguridad, siempre hay una probabilidad de intrusión. Una intrusión puede ocurrir cuando un usuario hace click en un link malicioso o cuando un atacante explota un servidor público. De cualquier modo, cuando una intrusión ocurre, debemos detectarla ASAP para prevenir mayores daños.

Las Operaciones de Seguridad cubren varias tareas para asegurar protección; una de ellas es Threath Intelligence

### Threath Intelligence

En este contexto, Inteligencia se refiere a la información que se obtiene sobre enemigos actuales o potenciales. Una amenaza es cualquier acción que pueda perturbar o afectar negativamente a un sistema. La inteligencia de amenazas recolecta información para ayudar a la compañía a prepararse mejor frente adversarios potenciales.

La inteligencia necesita datos. Los datos tienen que ser colectados, procesados y analizados. Los datos son colectados desde fuentes locales como network logs y fuentes públicas como foros. El procesamiento de datos los organiza en un formato adecuado para el análisis. La fase de análisis busca encontrar más información sobre los atacantes y sus motivaciones.

Aprender sobre los adversarios permite conocer sus tácticas, técnicas y procedimientos. 

## Digital Forensics and Incident Response (DFIR)

### Digital Forensics 

Forensics es la aplicación de la ciencia para investigar crímenes y establecer hechos. Con el uso y el esparcimiento de sistemas digitales, como computadores o teléfonos inteligentes, una nueva, nació una nueva rama de la ciencia forense para investigar delitos relacionados: la informática forense, que más tarde evolucionó hacia la informática forense digital.

En seguridad defensiva, el foco de las digital forensics cambia para analizar evidencia de un ataque y sus perpretadores y otras áreas como robo de propiedad intelectual, ciber espionaje, y posesión de contenido no autorizado. Consecuentemente, digital forensics cubren diferentes áreas, como:

* File system: Analizar una digital forensics image (low-level copy) de un almacenamiento de sistema revela mucha información, como programas instalados, archivos creados, archivos parcialmente sobreescritos, y archivos eliminados.
* System memory: Si el atacante ejecuta su programa maliciosos en memoria sin guardarlo en el disco, tomar una forensic image (low-level copy) de la memoria de un sistema es la mejor manera de analizar su contenido y aprender sobre el ataque.
* System logs: Cada cliente y computador de servidor mantiene diferentes archivos log sobre que está ocurriendo. Los log files proveen mucha información sobre qué pasó en un sistema. Incluso si el atacante intenta limpiar su rastro, algunos rastros se mantienen.
* Network logs: Los registros de los paquetes de red que han atravesado una red ayudarían a responder más preguntas sobre si se está produciendo un ataque y qué implica.

### Incident Response

Un incidente usualmente se refiere a filtraciones de datos o ciber ataques; sin embargo, en algunos casos, puede ser algo menos crítico, como una mala configuración, un intento de intrusión, o una violación de políticas.

Las cuatro mayores fases de los procesos de respuesta de incidentes son:

1. Preparación: Esto requiere un equipo entrenado y listo para manejar incidentes. Idealmente, varias medidas son puestas en lugar para prevenir incidentes de que sucedan en primer lugar.
2. Detección y Análisis: El equipo tiene los recursos necesarios para detectar cualquier incidente; además, es esencial analizar cualquier incidente detectado más allá para aprender sobre su gravedad.
3. Containment, Eradication and Recovery: Una vez el incidente es detectado, es crucial frenarlo de afectar otros sistemas, eliminarlo, y recuperar los sistemas afectados. Por ejemplo, cuando notamos que un sistema está infectado con un virus, podríamos querer parar (contener) el virus de que se propague a otros sistemas, limpiar (erradicar) el virus, y asegurarse una recuperación de sistema apropiada.
4. Post-Incident Activity: Después de una recuperación exitosa, se produce un reporte, y la lección aprendida se comparte para prevenir incidentes similares a futuro.

### Malware Analysis

Los Malware incluyen muchos tipos, como:

* Un virus es una pieza de código, o una parte de un programa, que se adjunta a sí mismo a un programa. Es diseñado para esparcirse desde una computadora a otra y trabaja alterando, sobreescribiendo, y eliminando archivos una vez infectan una computadora. Los rangos de resultado van desde una computadora volviéndose lenta hasta inusable.
* Un caballo de Troya es un programa que se muestra como una función deseada, pero que esconde una función maliciosa por debajo. Por ejemplo, una víctima podría descargar un video player desde un sitio web que le permite al atacante tener control completo sobre su sistema.
* Un Ransomware es un programa maliciosos que encripta los archivos del usuario. La encriptación hace los archivos ilegibles sin el conocimiento de la llave de encriptación. El atacante ofrece al usuario la contraseña de desencriptación si el usuario paga un "rescate".

El análisis de malware tiene como objetivo aprender sobre dichos programas maliciosos utilizando diversos medios:

1. Análisis estático: trabaja inspeccionando el programa maliciosos sin ejecutarlo. Esto usualmente requiere conocimiento sólido del lenguaje assembly.
2. Análisis dinámico: Trabaja ejecutando el malware en un ambiente controlado y monitoreando sus actividades. Permite ver cómo el malware se comporta cuando es ejecutado.

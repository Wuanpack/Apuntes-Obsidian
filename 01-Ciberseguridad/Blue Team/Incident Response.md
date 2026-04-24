---
tags:
  - "#blue-team/incident-response"
  - blue-team/roles
---
## Índice
```table-of-contents
```
## ¿Qué es?

Cuando una solución de seguridad encuentra un evento o un grupo de eventos asociados con una posible actividad dañina, dispara una alerta. El equipo de seguridad analiza estas alertas. Algunas de estas pueden ser Falsos positivos, mientras que otros pueden ser Verdaderos Positivos.

## Tipos de Incidentes

Las personas usualmente catalogan cada actividad dañina asociada con el mundo digital a un intento de hacking. Esto quizás puede ser correcto, pero es muy genérico en términos de ciberseguridad. Los incidentes de seguridad pueden ser de diferentes tipos. Estos tipos puede ocurrir de manera independiente o en conjunto dentro de la misma víctima.

### [[Malware]] Infections

Un Malware es un programa malicioso que puede dañar el sistema, red, o aplicación. La mayoría de incidentes son asociados con infecciones de [[malware]]. Existen distintos tipos de [[malware]], cada uno con un potencial único para causar daño. Las infecciones por [[malware]] son mayormente causadas por archivos que pueden ser texto, documentos, ejecutables, etc.

### Security Breaches

Las brechas de seguridad se muestran cuando una persona no autorizada obtiene acceso a datos confidenciales. Las brechas de seguridad son de suma importancia, ya que muchas empresas dependen de sus datos confidenciales, a los que solo debe tener acceso el personal autorizado.

### Data Leaks

Los data leaks son incidentes donde información confidencial de un individuo o una organización es expuesta por entidades no autorizadas. Muchos atacantes usan las filtraciones de datos para daño reputacional de sus víctimas o usan esta técnica para amenazar a sus víctimas y obtener lo que necesiten de ellos. A diferencia de las brechas de seguridad, las filtraciones de datos pueden ser no intencionalmente causadas por errores humanos o malas configuraciones.

### Insider Attacks

Los incidentes desde dentro de una organización se conocen como insider attacks. Imagina a un empleado descontento que infecta toda la red mediante una memoria USB en su último día de trabajo. Este es un ejemplo de ataque interno. Un ataque iniciado intencionalmente por alguien dentro de tu organización entra en esta categoría. Estos ataques pueden ser peligrosos, ya que un empleado interno siempre tiene mayor acceso a los recursos que un empleado externo.

### Denial of Service Attack

La disponibilidad es uno de los tres pilares de la ciberseguridad. Las soluciones de seguridad defensivas y las personas buscan constantemente formas de proteger la información; garantizan que los datos estén disponibles para las personas simultáneamente. Esto se debe a que no tiene sentido proteger algo que no está disponible para nosotros. Los ataques de denegación de servicio, o ataques DoS, son incidentes en los que el atacante satura un sistema/red/aplicación con solicitudes falsas, lo que eventualmente lo vuelve inaccesible para los usuarios legítimos. Esto sucede debido al agotamiento de los recursos disponibles para atender las solicitudes.

## Incident Response Process

A veces, manejar una variedad de incidentes en un entorno puede ser difícil. Debido a la naturaleza particular de los incidentes en las organizaciones, debe existir un proceso estructurado para la respuesta a incidentes. Los marcos de respuesta a incidentes nos ayudan en este sentido. Estos son los enfoques genéricos que se deben seguir ante cualquier incidente para una respuesta eficaz. Analizaremos dos de los marcos de respuesta a incidentes más utilizados: SANS y NIST.

SANS y NIST son organizaciones reconocidas que contribuyen a la ciberseguridad. SANS ha ofrecido diversos cursos y certificaciones en ciberseguridad, y NIST ha desempeñado un papel importante en el desarrollo de estándares y directrices para la misma. Tanto SANS como NIST cuentan con marcos de respuesta a incidentes bastante similares.

El marco de respuesta a incidentes de SANS tiene 6 fases, que se pueden denominar "PICERL" para recordarlas fácilmente.

![[Pasted image 20260419235250.png]]


![[Pasted image 20260419235328.png]]


## Incident Response Techniques

Es difícil ver comportamientos anormales e identificar incidentes manualmente. Hay múltiples soluciones de seguridad que pueden servir con roles únicos en detección de cualquier incidente. Algunos de ellos tienen la capacidad de responder a los incidentes y ejecutar otras fases del lifecycle, como containment, eradication, etc.

* SIEM: Recolecta todos los logs importantes en una locación centralizada y los correlaciona para identificar incidentes.
* AV: Antivirus detecta programas maliciosos conocidos en un sistema y regularmente escanea el sistema por estos.
* EDR: Es desplegado en cada sistema, los protege contra algunas amenazas de nivel avanzado. Esta solución también puede contener y erradicar la amenaza.

Una vez identificados los incidentes, deben seguirse ciertos procedimientos, entre ellos investigar el alcance del ataque, tomar las medidas necesarias para prevenir daños mayores y eliminarlo de raíz.

Estos pasos pueden variar según el tipo de incidente. En este caso, contar con instrucciones paso a paso para cada tipo de incidente le ayudará a ahorrar mucho tiempo. Este tipo de instrucciones se conocen como manuales de procedimientos (playbooks).

Los manuales de procedimientos son las directrices para una respuesta integral ante incidentes.

A continuación se muestra un ejemplo de un plan de acción para un incidente: Correo electrónico de phishing. 

1. Notificar a todas las partes interesadas sobre el incidente de correo electrónico de phishing. 
2. Determinar si el correo electrónico era malicioso mediante el análisis del encabezado y el cuerpo del correo electrónico. 
3. Buscar archivos adjuntos en el correo electrónico y analizarlos. 
4. Determinar si alguien abrió los archivos adjuntos. 
5. Aislar los sistemas infectados de la red. 
6. Bloquear al remitente del correo electrónico.

Por otro lado, los manuales de procedimientos (runbook) son la ejecución detallada, paso a paso, de pasos específicos durante diferentes incidentes. Estos pasos pueden variar según los recursos disponibles para la investigación.
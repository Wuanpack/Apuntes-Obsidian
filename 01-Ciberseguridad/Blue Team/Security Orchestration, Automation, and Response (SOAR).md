## Índice

```table-of-contents
```

## Cómo los SOCs Tradicionales Trabajan

Las organizaciones tienen un Security Operations Center ([[SOC]]) como locación centralizada para monitorizar y proteger sus assets digitales. Los SOCs han evolucionado con el tiempo, con cada nueva generación añadiendo nueva tecnología.

La ventaja principal de una organización al tener un SOC es mejorar su manejo de incidentes de seguridad a través de monitoreo continuo y análisis. Esto se logra al implementar la cantidad de personas correcta, procesos, y tecnologías para apoyar las capacidades SOC.

Algunas de las capacidades de un [[SOC]] incluyen lo siguiente:

* Monitoreo y Detección: Se enfoca en escanear y señalar de forma continua actividades sospechosas dentro de un entorno de red. Esto permite detectar las amenazas emergentes y cómo prevenirlas en sus primeras etapas. La monitorización se realiza principalmente a través del SIEM.
* Recuperación y Remediación: Las organizaciones confían en su SOC para que proporcione un centro de recuperación y remediación cuando ocurren incidentes. Los equipos del SOC actúan como primeros respondedores cuando se identifican amenazas cibernéticas. Realizan operaciones como aislar o desactivar puntos finales infectados, eliminar malware y detener procesos maliciosos. Durante este proceso, suelen utilizar otras soluciones de seguridad como [[Endpoint Detection and Response (EDR)|EDR]], [[Firewall|firewalls]], IAM, etc.
* Inteligencia de Amenazas: La monitorización continua de los entornos requiere un flujo constante de inteligencia sobre amenazas. Esto garantiza que los equipos del SOC dispongan de flujos de datos de amenazas continuos y actualizados, como direcciones IP, [[Hash|hashes]], dominios y otros indicadores.
* Comunicación: Los equipos del [[SOC]] no solo detectan y responden a las amenazas, sino que también se coordinan con los equipos de TI y la gerencia para comunicar eficazmente las amenazas y garantizar que se aborden los incidentes.

## Desafíos que Enfrentan los SOCs

* Alert Fatigue: El uso de numerosas herramientas de seguridad genera una gran cantidad de alertas dentro de un SOC. Muchas de estas alertas son falsos positivos o insuficientes para una investigación, lo que deja a los analistas abrumados e incapaces de abordar cualquier incidente de seguridad grave.
* Muchas Herramientas Desconectadas: Las herramientas de seguridad a menudo se implementan sin integración dentro de una organización. Los equipos de seguridad tienen la tarea de navegar a través de los registros y reglas del firewall, que se manejan independientemente de los registros de seguridad de los puntos finales. Esto también lleva a una sobrecarga de herramientas.
* Procesos Manuales: Los procedimientos de investigación del SOC a menudo no están documentados, lo que conlleva métodos ineficientes para abordar las amenazas. La mayoría se basa en el conocimiento tácito establecido por analistas experimentados, y los procesos nunca se documentan. Esto resulta en una ralentización de la investigación y un aumento de los tiempos de respuesta.
* Escasez de Talento: Los equipos SOC encuentran dificultades para reclutar y ampliar su plantilla de talento para hacer frente al creciente panorama de seguridad y a las sofisticadas amenazas. Si a esto se le suma la sobrecarga de alertas a la que se enfrentan, los analistas de seguridad se ven cada vez más abrumados por las responsabilidades que deben asumir, lo que se traduce en un trabajo menos eficiente y tiempos de respuesta a incidentes más prolongados que permiten a los adversarios causar estragos dentro de una organización.

## ¿Qué es SOAR?

Security Orchestration, Automation, and Response (SOAR) es una herramienta que unifica todas las herramientas de seguridad usadas en [[SOC]]. Con SOAR, los analistas SOC no necesitan cambiar entre SIEM, [[Endpoint Detection and Response (EDR)|EDR]], [[Firewall]], y otras herramientas de seguridad para sus investigaciones. Pueden operar todas estas herramientas dentro de una sola interfaz SOAR. Además de unificar las herramientas de seguridad, también proporciona a los analistas funciones de gestión de incidencias y casos, a través de las cuales pueden documentar, rastrear y resolver sus incidentes de forma estructurada.

![[Pasted image 20260427231414.png|653]]

La principal fortaleza de una herramienta SOAR proviene de las siguientes tres capacidades principales.

### 1. Orchestration

Tradicionalmente, mientras se investiga una alerta, un analista SOC tiene que cambiar entre mútliples herramientas de seguridad para el análisis. Por ejemplo, durante un ataque de fuerza bruta VPN, el analista típicamente cambia entre las siguientes herramientas:

1. SIEM para comprobar si el usuario suele utilizar la IP en cuestión para el registro.
2. Threath Intelligence (TI) Platforms para verificar la reputación de la IP.
3. IAM para deshabilitar el usuario si hubo algún intento exitoso.
4. Sistema de tickets para abrir y realizar un seguimiento del incidente.

Cambiar manualmente entre estas diferentes herramientas ralentiza el proceso. La orquestación resuelve este problema al coordinar todas estas herramientas juntas dentro del SOAR. Conecta diferentes herramientas de varios proveedores dentro de la interfaz unificada de SOAR. Define flujos de trabajo para investigar varios tipos de alertas, conocidos como Playbooks. Estos playbooks son pasos predefinidos que le indican a SOAR cómo investigar una alerta.

Por ejemplo, para una alerta de fuerza bruta VPN, seguiríamos el siguiente playbook:

1. Alerta recibida del SIEM.
2. Consultar al SIEM para verificar si el usuario normalmente usa esa IP.
3. Verificar plataformas TI para ver la reputación de la IP.
4. Consultar al SIEM si hubo intentos exitosos.
5. Escalar para acciones de contención.

### 2. Automatización

El arte de coordinar múltiples herramientas a través de acciones predefinidas (Playbooks), puede ser automatizado. Por ejemplo:

1. El SOAR recibe la alerta del SIEM.
2. Automáticamente consulta al SIEM por el historia de inicios de sesión del usuario.
3. Automáticamente verifica la reputación de la IP a través de plataformas TI.
4. Si la IP es maliciosa, automáticamente desactiva el usuario desde el IAM.
5. Finalmente, automáticamente abre un ticket en el sistema de tickets con todos los detalles para iniciar una investigación.

Esto salva un montón de tiempo a los analistas SOC. Pueden manejar cientos de alertas sin agotarse.

### 3. Response

El SOAR da la habilidad de tomar acciones usando diferentes herramientas desde una interfaz unificada. También automatiza la respuesta.

Las capacidades de orquestación, automatización y respuesta de SOAR resuelven los principales desafíos a los que se enfrenta un equipo SOC. Con SOAR, se elimina la fatiga por exceso de alertas, la mayoría de los procesos están automatizados y todas las herramientas están conectadas para su coordinación.

![[Pasted image 20260427232251.png]]


## ¿Aún necesitamos Analistas SOC?

Mientras que una herramienta SOAR puede automatizar la mayoría de tareas repetitivas, no reemplaza a los analistas SOC. Las investigaciones complejas aún requieren a un analista SOC. SOAR no puede emitir un juicio en algunos puntos críticos, pero un analista sí. Un analista de SOC comprende las amenazas en el contexto empresarial más amplio.

Los manuales de procedimientos para los distintos tipos de alertas también los elaboran los analistas del SOC. Por lo tanto, la respuesta a esta pregunta es que SOAR aliviaría la carga de trabajo del SOC al automatizar tareas repetitivas y organizar todo en una estructura simplificada, pero aún necesitamos analistas del SOC.

## Construyendo SOAR Playbooks

### Phishing Playbook

Los ataques de phishing se mantienen como el vector de ataque más común usado en brechas. Desafortunadamente para los analistas de seguridad, investigar emails phishing se convierte en un consumidor de tiempo e involucra ejercicios manuales como analizar adjuntos y URLs y verificando a través de plataformas de threat intelligence. Mientras se llevan a cabo otras investigaciones, las soluciones SOAR pueden ejecutar estas tareas en segundo plano mediante un manual de procedimientos. Además, se pueden realizar medidas correctivas cuando se identifica un correo electrónico de phishing positivo.

![[Pasted image 20260427233022.png|697]]


### CVE Patching Playbook

Un CVE (Common Vulnerabilities and Exposures) es una vulnerabilidad que ha sido divulgada públicamente y se le asignó un número CVE. Como parte de la gestión de vulnerabilidades, el equipo SOC tiene que abordar las CVE recién publicadas verificando si existen en su red y parcheándolas si las hay.

Un analista debe estar siempre atento a las publicaciones sobre nuevas vulnerabilidades (CVE) y planes de remediación. El proceso puede volverse abrumador, lo que resulta en una acumulación de tareas pendientes y parches que no se aplican, dejando el entorno más vulnerable.

Además, este proceso puede consumir mucho tiempo y recursos del equipo SOC, ya que las CVE se publican con frecuencia. Por lo tanto, para resolver este problema, podemos crear un manual de procedimientos para gestionar las CVE dentro de la herramienta SOAR, tal como lo hicimos para el caso de phishing.

Este manual analizará los detalles de la vulnerabilidad CVE, evaluará su umbral de riesgo, creará un ticket de parcheo y probará el parche antes de implementarlo en el entorno de producción. A continuación, se muestra un ejemplo de un manual creado para la aplicación de parches a vulnerabilidades CVE.

![[Pasted image 20260427233205.png]]


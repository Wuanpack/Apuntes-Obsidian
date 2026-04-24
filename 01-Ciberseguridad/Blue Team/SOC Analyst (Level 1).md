---
tags:
  - blue-team/roles/SOC
---
## Índice
```table-of-contents
```
## Función

Como un analista de seguridad junior, también llamado SOC Level 1 Analyst, trabajas en un equipo [[SOC]] 24/7 y mayormente revisas alertas de seguridad junto a tus colegas.

Existen muchas bases de datos de fuentes abiertas, como AbuselPDB y Cisco Talos Intelligence, donde puedes realizar una revisión de reputación o locación por direcciones IP. La mayoría de analistas de seguridad usan estas herramientas para asistirnos con investigaciones de alertas. También es posible reportar IPs maliciosas.

## Jerarquía de Seguridad

Las prioridades de ciberseguridad son diferentes para cada compañía. Para firmas de abogados, el objetivo es la privacidad de documentos legales. Para fábricas, la disponibilidad de las líneas de producción. Para hospitales, la seguridad de los pacientes. Es por ello que cada compañía un acercamiento único de seguridad y estructura de equipo de seguridad. Ejemplo:


![[Pasted image 20260423212235.png]]

## Blue Team

El Blue Team trata sobre seguridad defensiva, lo que significa que constantemente monitorean por ataques e intentan responderlos rápidamente. 

### SOC

![[Pasted image 20260423212440.png]]

[[SOC]] es el centro de la ciberseguridad de una organización. Son la primera línea de defensa, trabajan con varias alertas, y manejan la mayoría de ataques. Un SOC eficiente usualmente se compone de los siguientes roles:

* L1 Analysts: Miembros junior que clasifican las alertas y pasan los casos complejos al nivel L2.
* L2 Analysts: Miembros con experiencia que investigan los ataques más avanzados.
* Engineers: Expertos en configuración de herramientas de seguridad, como EDR o SIEM.
* Manager: Persona que gestiona el equipo [[SOC]] por completo.

### Cyber Incident Response Team (CIRT)

![[Pasted image 20260423213041.png]]

Si la expertiz [[SOC]] no es suficiente o el incidente se va de control, urgentemente llamas a los "bomberos" (CIRT), también llamados CSIRT o CERT. Estos miembros debería tener un conocimiento amplio de amenazas cibernéticas y manejar brechas sin depender de herramientas como EDR o SIEM. El trabajo CIRT es estresante y responsable, pero también recompensante. 

### Specialized Defensive Roles

![[Pasted image 20260423213247.png]]

Las grandes empresas, las startups centradas en la tecnología y las agencias gubernamentales a menudo requieren roles de Blue Team especializados y específicos, emocionantes y muy valiosos, pero que requieren un profundo conocimiento del tema y una amplia experiencia en campos más amplios como SOC o TI. Estos roles específicos pueden incluir:

* [[Digital Forensics]] Analyst: Descubre amenazas escondidas en disco y memoria.
* Threat Intelligence Analyst: Recopilar datos sobre grupos de amenazas emergentes.
* AppSec Engineer: Mantiene seguro el ciclo de vida de desarrollo de software.
* AI Researcher: Estudia amenazas AI y cómo defenderse contra estas.

## SOC Path

Comenzar como analista SOC L1 puede ser una excelente opción para ampliar tu conocimiento del mundo cibernético y comprender mejor los roles más especializados.

### Internal SOC vs MSSP

No todas las organizaciones tienen la expertiz para operar un SOC por su cuenta y dependen de un Managed Security Services Provider (MSSP), una empresa que ofrece servicios de seguridad externalizados, generalmente SOC, a sus clientes. Trabajar en MSSP es típicamente de alta presión, pero también es una buena opción para empezar rápido tu carrera. 


| Topic                     | Internal SOC                                                                         | MSSP                                                                               |
| ------------------------- | ------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------- |
| Ejemplo de Escenario      | Trabajas en un equipo SOC de un banco y proteges los sistemas del banco.             | Trabajas en un MSSP global protegiendo a sus sesenta clientes en Europa.           |
| Working Pace              | Usualmente tienes turnos calmados sin mucha presión de tiempo.                       | Su turno generalmente comienza con una cola de alertas urgentes para analizar.     |
| Herramientas de Seguridad | Trabajas con algunas herramientas, pero necesitas conocerlas muy bien.               | Tienes que trabajar con sesenta herramientas y plataformas de seguridad distintas. |
| Práctica de Incidentes    | El año pasado, pudiste observar y aprender de tan solo dos importantes ciberataques. | Todas las semanas, lidias con ataques y brechas, y puedes aprender de ellas.       |

## Alert Triage

### From Events to Alerts

Primero, un evento debe ocurrir, como un inicio de sesión, proceso de ejecución, o la descarga de un archivo. Luego, el sistema, como el OS, firewall, o un proveedor cloud debe registrar este evento. Después de esto, todos los registros del sistema deben entregarse a la solución de seguridad como SIEM o EDR. El equipo SOC puede recibir millones de registros por día desde miles de sistemas diferentes.

Alerta, es una notificación generada por la solución de seguridad cuando un evento específico o secuencia de eventos ocurren, es lo que salva a los analistas [[SOC]] de revisar registros manualmente al recalcar solo los eventos anómalos. 

Con las alertas, los analistas pueden categorizar solo docenas de alertas por día en vez de millones de registros.


| Solution     | Ejemplos                 | Descripción                                                                                               |
| ------------ | ------------------------ | --------------------------------------------------------------------------------------------------------- |
| Sistema SIEM | Splunk ES, Elastic       | SIEM tiene un gestor de alertas sólido que son una elección perfecta para la mayoría que equipos [[SOC]]. |
| EDR o NDR    | MS Defender, CrowdStrike | Mientras EDR y NDR proporciona sus propios dashboards de alertsa, es preferido usar un SIEM o un SOAR.    |
| Sistema SOAR | Splunk SOAR, Cortex SOAR | Los equipos grandes [[SOC]] pueden usar SOAR para agregar o centralizar alertas de múltiples soluciones.  |
| Sistema ITSM | Jira, TheHive            | Algunos equipos pueden tener un gestor de tickets custom (ITSM) usando una solución dedicada.             |

### L1 Role in Alert Triage

Los analistas SOC L1 son la primera línea de defensa, y son los quienes trabajan con las alertas la mayoría del tiempo. Dependiendo de varios factores, los analistas L1 podrían recibir de cero a cientos de alertas por día, donde cada una puede revelar un ciberataque. Aun así, todos en el equipo SOC de alguna manera están involucrados con la categorización de alertas:

* SOC L1 Analysts: Revisan las alertas, distinguen las buenas e las malas, y notifica a los analistas L2 en caso de una amenaza real.
* SOC L2 Analysts: Reciben las alertas escaladas por los analistas L1 y realizan un análisis profundo y remediación.
* SOC Engineers: Asegura que las alertas contienen suficiente información requerida para una clasificación eficiente de estas.
* SOC Manager: Trackea la velocidad y calidad de la clasificación de alertas para asegurarse que los ataques reales no se vayan a perder.

### Propiedades de las Alertas

![[Pasted image 20260424174737.png]]



| N°  | Propiedad         | Descripción                                                                                                                                | Ejemplos                                                                                                                         |
| --- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Alert Time        | Muestra el tiempo de la creación de la alerta. La alerta usualmente se dispara unos minutos después del evento.                            | - Alert Time: March 21, 15:35<br>- Event Time: March 21, 15:32                                                                   |
| 2   | Alert Name        | Provee un sumario de qué pasó, basado en el nombre de la regla de detección.                                                               | - Unusual Login Location<br>- Email Marked as Phishing<br>- Windows RDP Bruteforce<br>- Potential Data Exfiltration              |
| 3   | Alert Severity    | Defina la urgencia de la alerta, inicialmente establecida por ingenieros de detección, pero puede ser alterada si el analista lo necesita. | - (🟢) Low / Informational<br>- (🟡) Medium / Moderate<br>- (🟠) High / Severe<br>- (🔴) Critical / Urgent                       |
| 4   | Alert Status      | Informa si alguien está trabajando en la alerta o si se ha realizado la clasificación.                                                     | - (🆕) New / Unassigned<br>- (🔄) In Progress / Pending<br>- (✅) Closed / Resolved<br>- And often other custom statuses          |
| 5   | Alert Verdict     | También llamado alerta de clasificación, explica si la alerta es una amenaza real o sólo ruido.                                            | - (🔴) True Positive / Real Threat<br>- (🟢) False Positive / No Threat<br>- And often other custom verdicts                     |
| 6   | Alert Assignee    | Muestra al analista que fue asignado o si se asignó a si mismo para revisar una alerta.                                                    | - Assignee can sometimes be called alert owner<br>    <br>- Assignee takes responsibility for their alerts                       |
| 7   | Alert Description | Explica de qué se trata la alerta, usualmente en tres secciones a la derecha.                                                              | - The logic of the alert generating rule<br>- Why this activity can indicate an attack<br>- Optionally, how to triage this alert |
| 8   | Alert Fields      | Proporciona comentarios de analistas SOC y valores en los cuales la alerta fue disparada.                                                  | - Affected Hostname<br>- Entered Commandline<br>- And many more, depending on the alert                                          |


![[Pasted image 20260424175829.png]]


## Reporte de Alertas

Primero, el analista L1 recive las alertas en un SIEM, EDR, o una plataforma de gestión de tickets. La mayoría de las alertas son cerradas como Falsos Positivos o son manejadas en el nivel L1, pero las complejas y amenazantes son enviadas a L2 para remediar la mayoría de brechas.

### Reportando Alertas

Antes de cerrar o pasar una alerta a L2, podrías tener que reportarla. Dependiendo de los estándares del equipo y la severidad de la alerta, en vez de un comentario de alerta corto, te podrían requerir documentar tu investigación en detalle, garantizando que toda la evidencia relevante está incluida. Esto es especialmente importante para True Positives, los cuales requieren escalar.

### Alert Escalation

Si la alerta True Positive requiere acciones adicionales o investigación profunda, remitirlo al analista L2 para una revisión adicional siguiendo los procedimientos acordados. Ahí es donde tu informe de alertas resulta útil, ya que L2 lo utilizará para obtener el contexto inicial y gastar menos en el análisis desde cero.

### Comunicación

También es posible que necesite comunicarse con otros departamentos durante o después del análisis. Por ejemplo, pregunte al equipo de TI si confirman la concesión de privilegios administrativos a algunos usuarios o póngase en contacto con Recursos Humanos para obtener más información sobre el empleado recién contratado.


## Guía de Reportes


| Alert Response Purpose                    | Explanation                                                                                                                                                                                           |
| ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Proporcionar contexto para la escalada.   | Un informe bien redactado ahorra mucho tiempo a los analistas de nivel 2. Además, les ayuda a comprender rápidamente lo que sucedió.                                                                  |
| Guarde los hallazgos para los registros.  | Los registros SIEM sin procesar se almacenan durante 3 a 12 meses, pero las alertas se conservan indefinidamente. Por lo tanto, es mejor mantener todo el contexto dentro de la alerta, por si acaso. |
| Mejorar las habilidades de investigación. | Si no puedes explicarlo de forma sencilla, no lo entiendes lo suficientemente bien. Redactar informes es una excelente manera de mejorar las habilidades de nivel 1 resumiendo las alertas.           |

Es recomendable seguir el acercamiento de las 5 Ws e incluir al menos estos elementos en el reporte:

* Who
* What
* When
* Where
* Why


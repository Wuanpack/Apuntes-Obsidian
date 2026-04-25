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

## SOC Workbooks and Lookups

## Identity Inventory

El inventario de identidad es un catálogo de empleados de la corporación, servicios, y sus detalles como privilegios, contactos, y roles dentro de la compañía.

### Ejemplo de Identidades


| Full Name     | Username     | Email                 | Role                     | Location   | Access           |
| ------------- | ------------ | --------------------- | ------------------------ | ---------- | ---------------- |
| Gregory Baker | G.Baker      | g.baker@tryhatme.thm  | Chief Financial Officer  | Europe, UK | VPN, HQ, FINANCE |
| Raymond Lund  | R.Lund       | r.lund@tryhatme.thm   | US Financial Adviser     | US, Texas  | VPN, FINANCE     |
| Kate Danner   | K.Danner     | k.danner@tryhatme.thm | Chief Technology Officer | Europe, UK | VPN, DA, HQ, AWS |
| svc-veeam-06  | svc-veeam-06 | N/A                   | Backup Service Account   | N/A        | VEEAM, DMZ, HQ   |
| svc-nginx-pp  | svc-nginx-pp | N/A                   | Web App Service Account  | N/A        | DMZ              |

## Fuentes de Identidades


| Solución         | Ejemplos               | Descripción                                                                                                                               |
| ---------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| Active Directory | On-prem AD, Entra ID   | Active Directory (AD) es una base de datos de identidades y es utilizada habitualmente por los centros de operaciones de seguridad (SOC). |
| SSO Providers    | Okta, Google Workspace | Alternativa en la nube para AD, una forma sencilla de gestionar y buscar usuarios.                                                        |
| HR Systems       | BambooHR, SAP, HiBob   | Limitado solo a empleados, pero generalmente proporciona datos completos de los empleados.                                                |
| Custom Solution  | CSV or Excel Sheets    | Es común que los equipos de TI o de seguridad mantengan sus propias soluciones.                                                           |

## Inventario de Assets

Es la lista de todos los recursos computacionales dentro del entorno IT de una organización. "Asset" es un término vago y también puede referirse a software, hardware, o empleados, en esta caso sólo nos vamos a enfocar en estaciones de trabajo.

### Ejemplo de Assets

| Hostname    | Location      | IP Address   | OS                  | Owner           | Purpose                                         |
| ----------- | ------------- | ------------ | ------------------- | --------------- | ----------------------------------------------- |
| HQ-FINFS-02 | UK Datacenter | 172.16.15.86 | Windows Server 2022 | Central IT      | Servidor de archivos para registros financieros |
| HQ-ADDC-01  | UK Datacenter | 172.16.15.10 | Windows Server 2019 | Central IT      | Controlador de dominio AD principal             |
| PQ-891D     | London Office | 192.168.5.13 | Windows 11 Pro      | Tech Support    | PC estacionario para contadores                 |
| L007694     | Remote        | N/A          | MacOS 13            | A.Kelly, DevOps | Laptop Corporativa                              |
| L005325     | Remote        | N/A          | MacOS13             | J.Eldridge, HR  | Laptop Corporativa                              |

## Fuentes de Assets

| Solución         | Ejemplos             | Descripción                                                                                  |
| ---------------- | -------------------- | -------------------------------------------------------------------------------------------- |
| Active Directory | On-prem AD, Entra ID | AD no es solo una identidad, sino también una base de datos de inventario de activos sólida. |
| SIEM o EDR       | Elasitc, CrowdStrike | Algunos agentes SIEM o EDR recopilan información sobre los hosts monitorizados.              |
| MDM Solution     | MS Intune, Jamf MDM  | Una clase específica de soluciones creadas para listar y administrar activos.                |
| Custom Solution  | CSV or Excel Sheets  | Al igual que con el inventario de identidades, las soluciones personalizadas son comunes.    |

## SOC Workbooks

Un workbook SOC, también llamado playbook, runbook o workflow, es una documento estructurado que define los pasos requeridos para investigar y remediar amenazas específicas de forma eficiente y consistente.

Como los analistas L1 son considerados especialistas junior y no se espera que clasifiquen todos los escenarios de ataque posible a la perfección, los analistas senior a menudo preparan workbooks para apoyar a sus compañeros con menos experiencia. 

### Workbook Example

![[Pasted image 20260425124009.png]]

El diagrama es un ejemplo típico de un workbook de investigación apuntado a ayudar a los analistas L1 a clasificar alertas sobre correos, webs, o inicios de sesión VPN atípicos. La mayoría de diagramas de workbooks son suplementados con una guía textual detallada y enlaces para los recursos mencionados. También, nota como el workbook está dividido en tres grupos lógicos. Al seguir los siguientes pasos en el orden correcto, puedes garantizar una clasificaci+on de alertas de alta calidad y eliminar casos donde el veredicto está hecho sin evidencia suficiente:

1. Enrichment: Usa Inteligencia de Amenazas e identidad de inventario para obtener información sobre el usuario afectado.
2. Investigación: Usando los datos recolectados y los registros SIEM, haz tu veredicto si el inicio de sesión es esperado.
3. Escalation: Escala la alerta a L2 o comunica el inicio de sesión con el usuario si es necesario.


## Metrics and Objectives

### Core Metrics


| Métrica               | Fórmula                                | Medidas                                         |
| --------------------- | -------------------------------------- | ----------------------------------------------- |
| Alerts Count          | AC = Total Count of Alerts Received    | Carga de trabajo total de los analistas del SOC |
| False Positive Rate   | FPR = False Positives / Total Alerts   | Nivel de sonido en las alertas                  |
| Alert Escalation Rate | AER = Escalated Alerts / Total Alerts  | Experiencia de los analistas L1                 |
| Threat Detection Rate | TDR = Detected Threats / Total Threats | Confiabilidad en el equipo SOC                  |

#### Alerts Count

Imagina empezar el turno y ver 80 alertas sin resolver en queue. Es definitivamente abrumador y propenso a perder amenazas reales detrás de el ruido spam. Por otra parte, considera una semana entera sin alertas. Suena mejor a primera vista, pero también preocupante, ya que puede indicar que hay una falta de visibilidad del SIEM, llevando a brechas no detectadas. La métrica ideal varía dependiendo del tamaño de la compañía, pero en general, una buena métrica es de 5 a 30 alertas por día por analista L1.

#### False Positive Rate

Si 75 de 80 alertas (94%) resultaron ser falsos positivos, como ruido del sistema o actividad típica de TI, eso es una mala señal para su equipo. Con más ruido, los analistas tienden a volverse menos vigilantes y es más probable que pasen por alto la amenaza y traten todas las alertas como "un spam más". Una tasa de falsos positivos del 0% es un ideal inalcanzable, pero el 80% o más es un problema grave, que generalmente se soluciona ajustando las herramientas y las reglas de detección, lo que a menudo se denomina "corrección de falsos positivos".

#### Alert Escalation Rate

Los analistas de nivel 2 dependen de los de nivel 1 para filtrar el ruido y escalar solo las alertas amenazantes y procesables. Al mismo tiempo, como analista de nivel 1, no conviene ser demasiado confiado y priorizar alertas que no se comprenden completamente sin la ayuda de un analista senior. La tasa de escalada de alertas resulta útil para evaluar la experiencia e independencia de los analistas de nivel 1 y la frecuencia con la que deciden escalar la alerta. Por lo general, se busca que sea inferior al 50%, o mejor aún, inferior al 20%.

#### Threat Detection RAte

Imagina que, de seis ataques previstos para 2025, tu equipo SOC detectó y previno cuatro, pasó por alto el quinto debido a una regla de detección defectuosa y el sexto porque uno de los analistas de nivel 1 clasificó erróneamente la brecha como falso positivo.

La métrica resultante es TDR = 4 / 6 = 67%, lo cual es un resultado muy malo. La tasa de detección de amenazas siempre debe ser del 100%, ya que cada amenaza no detectada puede tener consecuencias devastadoras, como la infección por ransomware y la exfiltración de datos.

### Triage Metrics

Recuerda que una alerta por sí misma no va a parar la brecha, y es importante recibir la alerta a tiempo, priorizarla y responder al ataque antes de que los atacantes logren sus objetivos.

Los requisitos para garantizar una detección y remediación rápidas de la amenaza se agrupan comúnmente en un Service Level Agreement (SLA), un documento firmado entre el equipo interno del SOC y la dirección de su empresa, o por el proveedor de servicios gestionados del SOC (MSSP) y sus clientes.

El acuerdo generalmente requiere una detección rápida de amenazas (medida por MTTD), un acuse de recibo oportuno de la alerta por parte de los analistas L1 (medido por MTTA) y, finalmente, una respuesta rápida a la amenaza, como aislar el dispositivo o proteger la cuenta comprometida (medido por MTTR).

![[Pasted image 20260425130901.png]]

### Tabla de Referencia


| Métrica                         | Common SLA | Descripción                                                                                          |
| ------------------------------- | ---------- | ---------------------------------------------------------------------------------------------------- |
| SOC Team Availability           | 24/7       | Horario de trabajo del equipo SOC, a menudo de lunes a viernes (8/5) o en modo 24/7.                 |
| Mean Time to Detect (MTTD)      | 5 minutos  | Tiempo promedio entre el ataque y su detección por las herramientas del SOC.                         |
| Mean Time to Acknowledge (MTTA) | 10 minutos | Tiempo promedio que tardan los analistas de nivel 1 en comenzar la clasificación de la nueva alerta. |
| Mean Time to Respond (MTTR)     | 60 minutos | Tiempo promedio que tarda el SOC en detener la propagación de la brecha de seguridad.                |


---
tags:
  - blue-team/roles/SOC
---
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


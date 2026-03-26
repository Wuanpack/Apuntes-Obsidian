---
tags:
  - frameworks
  - seguridad
  - vectores-ataque
---

## ¿Qué es?

MITRE es una organización sin fines de lucro estadounidense que trabaja con el gobierno de EE.UU. en investigación y desarrollo. ATT&CK son las siglas de Adversarial Tactics, Techniques and Common Knowledge.

Es una base de conocimiento pública que documenta las tácticas, técnicas y procedimientos reales que los atacantes usan en el mundo real, construida a partir del análisis de incidentes reales ocurridos en organizaciones reales.

La diferencia clave con [[ISO#ISO 27001|ISO 27001]] y [[NIST Cybersecurity Framefork (CSF)|NIST]] es que ATT&CK no te dice cómo gestionar la seguridad de una organización, sino cómo piensan y actúan los atacantes.
Se organiza en una matriz donde las columnas son las fases de un ataque y las filas son las técnicas específicas utilizadas en cada fase.

1. Reconocimiento.
2. Acceso Inicial.
3. Ejecución.
4. Persistencia.
5. Escalada de Privilegios.
6. Evasión.
7. Acceso a Credenciales.
8. Descubrimiento.
9. Movimiento Lateral.
10. Recolección.
11. Comando y Control (C2).
12. Exfiltración.
13. Impacto.

Cada técnica está documentada con descripción, ejemplos reales, grupos de atacantes que la usan y mitigaciones posibles.

Tiene tres matices principales:

* ATT&CK for Enterprise: Cubre Windows, Linux, macOS y entornos [[Introducción Cloud|Cloud]]. Es la más usada,
* ATT&CK for Mobile: Cubre Android e iOS.
* ATT&CK for ICS: Cubre sistemas de control industrial como plantas eléctricas o fábricas.
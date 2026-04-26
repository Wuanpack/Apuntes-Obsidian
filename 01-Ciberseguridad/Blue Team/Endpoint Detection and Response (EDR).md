## Íncide
```table-of-contents
```

## ¿Qué es?

Es una solución de seguridad diseñada para monitorear, detectar, y responder a amenazas avanzadas al nivel de endpoint. Como analista SOC, es esencial entender cómo un EDR funciona, ya que es una solución ampliamente adoptada por organizaciones para proteger sus endpoints.

Soluciones EDR en el mercado:

* CrowdStrike Falcon
* SentinelOne ActiveEDR
* Microsoft Defender for Endpoint
* OpenEDR
* Symantec EDR

## Características de un EDR

Hay tres características principales de un EDR, los cuales también se les puede referir como los tres pilares de una solución EDR.

![[Pasted image 20260426152432.png]]

### Visibilidad

Un buen análisis a menudo depende del nivel de disponible de visibilidad de la actividad. Esta es una de lsa catacterísticas de EDR que lo hace único de otras soluciones de seguridad de endpoint.

El nivel de visibilidad que un EDR proporciona es impresionante. Recolecta datos de los endpoints, los cuales incluyen modificaciones de procesos, modificaciones de registros, modificaciones de archivos y carpetas, acciones de usuario, y más. Presenta esta información en un formato muy estructurado para el analista. El analista puede ver el árbol de procesos completo con una timeline de actividades completo de la secuencia de acciones. El analista también puede acceder a los datos históricos de cualquier endpoint para threat hunting o cualquier otro propósito.

![[Pasted image 20260426152826.png]]

Esta captura de pantalla muestra la representación gráfica de un árbol de procesos. Podemos ver cuáles procesos aparecieron en el endpoint. Cada nodo representa un proceso. Las líneas conectándolos representa sus relaciones.

Si presionamos el ícono `+` de cada proceso, seremos capaces de ver todas las conexiones de la red, cambios de registros, de archivos, etc.


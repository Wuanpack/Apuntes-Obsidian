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

### Visibility

Un buen análisis a menudo depende del nivel de disponible de visibilidad de la actividad. Esta es una de lsa catacterísticas de EDR que lo hace único de otras soluciones de seguridad de endpoint.

El nivel de visibilidad que un EDR proporciona es impresionante. Recolecta datos de los endpoints, los cuales incluyen modificaciones de procesos, modificaciones de registros, modificaciones de archivos y carpetas, acciones de usuario, y más. Presenta esta información en un formato muy estructurado para el analista. El analista puede ver el árbol de procesos completo con una timeline de actividades completo de la secuencia de acciones. El analista también puede acceder a los datos históricos de cualquier endpoint para threat hunting o cualquier otro propósito.

![[Pasted image 20260426152826.png]]

Esta captura de pantalla muestra la representación gráfica de un árbol de procesos. Podemos ver cuáles procesos aparecieron en el endpoint. Cada nodo representa un proceso. Las líneas conectándolos representa sus relaciones.

Si presionamos el ícono `+` de cada proceso, seremos capaces de ver todas las conexiones de la red, cambios de registros, de archivos, etc.

### Detection

La característica de detección del EDR gana por sobre capacidades de detección tradicionales. Incorpora detecciones basadas en firmas y en el comportamiento, como actividades inesperadas del usuario. Gracias a sus capacidades de aprendizaje automático, identifica cualquier desviación del comportamiento habitual y la marca al instante. También puede detectar malware sin archivos que reside en la memoria. Además, permite introducir indicadores de compromiso (IOC) personalizados para la detección de amenazas.

![[Pasted image 20260426222617.png]]

### Response

EDR también empodera al analista a tomar acciones para amenazas detectadas. Estas acciones pueden ser tomadas en cualquier endpoint dentro de la consola central EDR.

Como analista, puedes decidir si aislar el endpoint completamente, terminar el proceso, o poner en cuarentena algunos archivos. También puedes conectarte al host de manera remota y ejecutar acciones independientemente. 

![[Pasted image 20260426222757.png]]


## ¿Por qué necesitamos un EDR cuando ya tenemos un Antivirus (AV) en los endpoints?

Ambas soluciones de seguridad tienen el mismo motivo de proteger el endpoint en el cual fueron instalados. Sin embargo, ambas difieren en el nivel de protección que proporcionan.

El antivirus puede detectar algunas amenazas básicas, pero para detectar amenazas avanzadas que evaden las detecciones normales, necesitamos un EDR. A diferencia de la detección basada en firmas de un antivirus, monitorea y registra el comportamiento en el endpoint. Un EDR también proporciona visibilidad de toda la organización sobre cualquier actividad. Por ejemplo, si se detecta un archivo sospechoso en un punto final, el EDR también lo comprobará en todos los demás puntos finales.

### Análisis de un Escenario

* Paso 1: Un usuario recibe un email phishing con un documento Word embebido con un macro malicioso (VBA script).
* Paso 2: El usuario descarga el documento y lo abre.
* Paso 3: El macro malicioso se ejecuta silenciosamente, y aparece PowerShell.
* Paso 4: El macro malicioso corre un comando ofuscado de PowerShell para descargar un sofisticado payload de etapa dos.
* Paso 5: El payload es inyectado en un svchost.exe legítimo.
* Paso 6: El atacante gana acceso remoto del sistema.

![[Pasted image 20260426223846.png]]

| Paso del Ataque | Respuesta del Antivirus                                                                            | Respuesta del EDR                                                                                                                 |
| --------------- | -------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| Paso 1          | No hace nada si el archivo descargado no tiene una firma previa en la base de datos.               | Registra la actividad del documente descargado y lo monitorea.                                                                    |
| Paso 2          | No hace nada al abrir el documento ya que winword.exe es una utilidad legítima.                    | Registra la ejecución de windword.exe y sigue monitoreando.                                                                       |
| Paso 3          | No hace nada si el macro ejecutado no tiene firma previa.                                          | Detecta y embandera la ejecución del macro debido a la relación parent-child inusual de los procesos winword.exe y PowerShell.exe |
| Paso 4          | Típicamente, los AVs no detectan scripts ofuscados de PowerShell.                                  | Embandera la ejecución del script ofuscado.                                                                                       |
| Paso 5          | No va a marcar inyección maliciosa en svchost.exe, ya que no monitorea las inyecciones de memoria. | Detecta el proceso de inyección en svchost.exe                                                                                    |
| Paso 6          | Carece de visibilidad a nivel de red.                                                              | Embandera el comportamiento inesperado de svchost.exe, que está haciendo una conexión hacia el exterior.                          |
| Acción Final    | Puede marcarlo como limpio.                                                                        | Genera una alerta con la cadena de ataque completa y habilita al analista a tomar acciones desde dentro del EDR.                  |

## ¿Cómo funciona un EDR?

### Agentes

Podemos integrar múltiples endpoints con nuestro EDR y gestionarlos a través de una consola centralizada. Hay agentes EDR que tenemos que desplegar dentro de dichos endpoints. Estos agentes también se les refiere como sensores. Son los ojos y oídos de los EDR.

Su trabajo es mantenerse en el endpoint y monitorear todas las actividades. La información sobre estas actividades se envía en detalle a la consola central EDR en tiempo real. Los agentes EDR pueden hacer detecciones básicas basadas en firmas y comportamiento por sí mismos y los envían a la consola EDR, que dispara alertas.

### EDR Console

Todos los datos detallados enviados por los agentes EDR es correlacionada y analizada a través de lógica compleja y algoritmos de machine learning.
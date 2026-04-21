Los comandos en PowerShell son conocidos como `cmdlets` (pronunciado `command-lets`). Siguen una convención de nomenclatura consistente en verbo-sustantivo.

Esta estructura hace fácil de entender qué hace cada `cmdlet`. El `Verb` describe la acción, y `Noun` especifica el objeto al cual se le realiza la acción.

## Basic Cmdlets


| Comando                   | Descripción                                                                                                                                                                                                           |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Get-Command`             | Lista todos los cmdlets, funciones, aliases, y scripts disponibles para ser ejecutados en la sesión Powershell actual.                                                                                                |
| `-CommandType "Function"` | Se muestran solo los comandos disponibles en `Get-Command` que son del tipo "Function".                                                                                                                               |
| `Get-Help`                | Provee información detallada sobre cmdlets, incluyendo su uso, parámetros y ejemplos. Ej: `Get-Help Get-Date`. Al incluir el comando `-examples` se mostrarán las diversas formas en las que se puede usar el cmdlet. |
| `Get-Alias`               | Lista todos los alias disponibles. Un alias es un nombre alternativo o ataco para cmdlets. Por ejemplo, `dir` es un alias para `Get-Children`, y `cd` es un alias para `Set-Location`.                                |
| `Find-Module`             | Una característica poderosa de PowerShell es la posibilidad de extender su funcionalidad al descargar cmdlets adicionales desde repositorios online.                                                                  |
| `Install-Module`          | Para descargar e instalar módulos con cmdlets desde un repositorio.                                                                                                                                                   |

## Navigating the File System and Working with Files


| Comando         | Descripción                                                                                                                                                                                                                   |
| --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Get-ChildItem` | Lista los archivos y directorios en una locación especificada por el parámetro `-Path`. Si no se especifica `-Path`, el cmdlet va a mostrar el contenido del directorio de trabajo actual. Ej: `Get-Children -Path C:\Users`. |
| `Set-Location`  | Comando para navegar a un directorio diferente.                                                                                                                                                                               |
| `New-Item`      | Crea un ítem en PowerShell. Ej: `New-Item -Path ".\captain-cabin\captain-wardrobe" -ItemType "Directory"`.                                                                                                                    |
| `Remove-Item`   | Similar a New-Item, este cmdlet remueve tanto directorios como archivos.                                                                                                                                                      |
| `Copy-Item`     | Copiar archivo o directorio.                                                                                                                                                                                                  |
| `Move-Item`     | Mover archivo o directorio.                                                                                                                                                                                                   |
| `Get-Content`   | Lee y muestra el contenido de un archivo.                                                                                                                                                                                     |
Todos estos cmdlets tienen sus alias respectivos.

## Piping Filtering, and Sorting Data.

Piping es una técnica usada en entornos de líneas de comandos para permitirnos usar la salida de un comando como input de otro. Esto crea una sequencia de operaciones donde el flujo de datos va desde un comando a otro. Se representa por el símbolo `|`.

En PowerShell, piping es incluso más poderoso porque pasa objetos más que sólo texto. Estos objetos no solo cargan datos sino que también propiedades y métodos que describen e interactúan con los datos.

Por ejemplo:

```Powershell
Get-ChildItem | Sort-Object Length
```

`Get-ChilItem` recibe los archivos como objetos, y los envía con `|` a `Sort-Object`, el cual los ordena por su longitud `Length`.

### Operadores útiles

* `-eq`: "igual que". Se usa para incluir objetos basado en los resultados del criterio especificado.
* `-ne`: "no igual". Se usa para excluir objetos basado en los resultados del criterio especificado.
* `-gt`: "mayor que". Filtra sólo los objetos que hayan excedido un valor específico. 
* `-ge`: "mayor o igual que". Es una combinación entre `-gt` y `-eq`.
* `-lt`: "menor que". Es la contraparte de `-gt`. Incluye sólo los objetos que están debajo de cierto valor.
* `le`: "menor o igual que". Es la combinación de `-lt` y `eq`.

Ejemplo que muestra que los objetos también pueden ser filtrados seleccionando propiedades que coinciden (`-like`) un patrón específico:

```PowerShell
Get-ChildItem | Where-Object -Property "Name" -like "ship*"
```

El siguiente cmdlet se usa para seleccionar propiedades específicas de objetos o limitar el número de objetos retornados. Es útil para refinar la salida para que muestre solo lo que necesitamos.

```PowerShell
Get-ChildItem | Select-Object Name,Length
```

## System and Network Information


| Comando                  | Descripción                                                                                                                                                                                                                               |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Get-ComputerInfo`       | Devuelve información del sistema comprensible, incluyendo información del SO, especificaciones de hardware, detalles de la BIOS, y más. Su contraparte tradicional `systeminfo` solo devuelve un pequeño conjunto de los mismos detalles. |
| `Get-LocalUser`          | Lista todas las cuentas de usuarios locales en el sistema.                                                                                                                                                                                |
| `Get-NetIPConfiguration` | Proporciona información detallada sobre las interfaces de red del sistema, incluyendo direcciones IP, servidores DNS, y configuraciones gateway.                                                                                          |
| `Get-NetIPAddress`       | Muestra detalles adicionales sobre las direcciones IP asignada a las interfaces de red, muestra todas las direcciones IP configuradas en el sistema, incluyendo aquellas que no están activas.                                            |

## Real-Time System Analysis

| Comando                | Descripción                                                                                                                                                          |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Get-Process`          | Proporciona una vista detallada de todos los procesos en ejecución, incluyendo el uso de memoria y CPU.                                                              |
| `Get-Service`          | Permite recibir información sobre el estatus de los servicios en una máquina, como los servicios en ejecución, detenidos o pausados.                                 |
| `Get-NetTCPConnection` | Permite monitorear conexiones de red activas, mostrando las conexiones TCP actuales, proporcionando información tanto sobre los puntos finales locales como remotos. |
| `Get-FileHash`         | Genera file hashes, los cuales son particularmente valiosos en respuesta de incidentes, threat hunting, y análisis de malware.                                       |
|                        |                                                                                                                                                                      |

## Scripting

Scripting es el proceso de escribir y ejecutar una serie de comandos contenidos en un archivo de texto, conocido como script, para automatizar tareas.

* Para profesionales de Blue Team, como respuesta de incidentes, analistas de malware, y threat hunters, los scripts de PowerShell pueden automatizar cualquier tarea, incluyendo análisis de logs, detectar anomalías, y extraer indicadores de compromiso (IOCs). Estos scripts también pueden ser usados para realizar ingeniería inversa al código malicioso o automatizar el escaneo de sistemas por signos de intrusión.
* Para el Red Team, incluyendo pentesters y ethical hackers, los scripts de PowerShell pueden automatizar tareas como enumeración de sistemas, ejecutar comandos remotos, y construir scripts ofuscados para saltar defensas. Su integración profunda con todos los tipos de sistemas lo hacen una herramienta poderosa para simular ataques y testear la resiliencia de los sistemas contra amenazas del mundo real.
* Los administradores de sistemas se benefician del scripting en PowerShell para automatizar chequeos de integridad, manejar configuraciones de sistemas, y seguridad de redes, especialmente en entornos remotos o a gran escala. Los scripts de PowerShell pueden ser designados para mejorar políticas de seguridad, monitorear la salud de sistemas, y responder automáticamente a incidentes de seguridad.

`Invoke-Command` es esencial para ejecutar comandos en sistemas remotos, haciéndolo fundamental para administradores de sistemas, ingenieros de seguridad y pentesters. 


Antes de ejecutar comandos, debemos tener en cuenta que solo podemos ejecutarlos dentro de la ruta de Windows. Puede ejecutar comando `set` para verificar su ruta desde la línea de comandos. La salida de la terminal a continuación muestra la ruta donde MS Windows ejecutará los comandos, como lo indica la línea que comienza con `Path=`.

## Información del Sistema

| Comando      | Descripción                                                                            |
| ------------ | -------------------------------------------------------------------------------------- |
| `ver`        | Comando para determinar la versión del sistema operativo.                              |
| `systeminfo` | Lista información detallada del sistema, como información del OS, procesador y memoria |
| `help`       | Proporciona información de ayuda para un comando específico                            |
| `cls`        | Limpia la pantalla                                                                     |

## Network Troubleshooting


| Comando            | Descripción                                                                                                                                                                                                               |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ipconfig`         | Información de la red, como dirección IP, máscara de subnet, default gateway.                                                                                                                                             |
| `ipconfig /all`    | Muestra información adicional sobre la configuración de red.                                                                                                                                                              |
| `ping TARGET_NAME` | Envía un paquete ICMP específico y escucha por respuestas.                                                                                                                                                                |
| `tracert`          | "trace route". Sigue las trazas de la ruta de la red que atraviesa el paquete para llegar a su destino. Espera que los routers en el camino notifiquen si dropearon el paquete porque su TTL (time-to-live) alcanzó cero. |
| `nslookup`         | Busca un host o dominio y devuelve la dirección IP.                                                                                                                                                                       |
| `netstat`          | Este comando muestra las conexiones de red actuales y los puertos que están escuchando.                                                                                                                                   |

## File and Disk Management


| Comando                | Descripción                                                                  |
| ---------------------- | ---------------------------------------------------------------------------- |
| `cd`                   | "current drive". Es el equivalente a preguntarle al sistema "¿donde estoy?". |
| `cd TARGET_DIRECTORY`  | Cambiar al directorio elegido.                                               |
| `cd ..`                | Subir 1 directorio                                                           |
| `dir`                  | Muestra los directorios hijo.                                                |
| `dir /a`               | Muestra los archivos ocultos y de sistema también.                           |
| `dir /s`               | Muestra los archivos en el directorio actual y todos los subdirectorios.     |
| `tree`                 | Representa visualmente los directorios hijos y subdirectorios.               |
| `mkdir DIRECTORY_NAME` | Crear directorio.                                                            |
| `rmdir DIRECTORY_NAME` | Eliminar un directorio.                                                      |
| `type`                 | Ver archivos de texto.                                                       |
| `more`                 | Ver archivos de texto más largos.                                            |
| `copy`                 | Copiar un archivo de una locación a otra.                                    |
| `move`                 | Mover archivos.                                                              |
| `del` o `erase`        | Eliminar archivos.                                                           |

NOTA: podemos usar el carácter `*` para referirnos a múltiples archivos. Por ejemplo, `copy *.md C:\Markdown*` va a copiar todos los archivos con extensión `md` al directorio `C:\Markdown`.

## Task and Process Management


| Comando                    | Descripción                       |
| -------------------------- | --------------------------------- |
| `tasklist`                 | Listar los procesos en ejecución. |
| `tasklist /?`              | Ver los filtros disponibles.      |
| `taskkill /PID target_pid` | Matar un proceso.                 |

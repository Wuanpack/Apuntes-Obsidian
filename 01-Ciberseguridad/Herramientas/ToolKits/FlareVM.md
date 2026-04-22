FlareVM, o "Forensics, Logic Analysis, and Reverse Engineering", destaca como una colección completa y cuidadosamente seleccionada de herramientas especializadas diseñadas exclusivamente para satisfacer las necesidades específicas de ingenieros inversos, analistas de malware, respondedores a incidentes, investigadores forenses y probadores de penetración.

Este conjunto de herramientas, creado por expertos del equipo FLARE de FireEye, es una poderosa ayuda para desentrañar misterios digitales, comprender el comportamiento del malware y profundizar en los detalles complejos de los archivos ejecutables.

## Reverse Engineering & Debugging

La ingeniería inversa es como resolver un puzzle al contrario: empiezas con el producto final y de ahí entiendes cómo funciona. Debugging es identificar errores, entender por qué pasaron, y corregir el código para prevenirlos.

* Ghidra: Suite de ingeniería Inversa open-source desarrollada por la NSA.
* x64dbg: Debugger open-source para binarios en formato x64 y x32.
* OllyDbg: Debugger para ingeniería inversa a nivel de assembly.
* Radare2: Una plataforma sofisticada open-source para ingeniería inversa.
* Binary Ninja: Una herramienta para desensamblar y descompilar binarios.
* PEiD: Herramienta de detección de empaquetadores, criptografía y compiladores.

## Disassemblers & Decompilers

Los desensambladores y descompiladores son herramientas cruciales en análisis de malware. Ayudan al analista a entender el comportamiento del software malicioso, la lógica, y el control de flujo dividiéndolo en un formato más comprensible. Las herramientas mencionadas debajo son comúnmente usadas en esta categoría:

* CFF Explorer: Un editor PE diseñado para analizar y editar archivos Ejecutables Portables (PE).
* Hopper Disassembler: Un debugger, disassembler, y decompiler.
* RetDec: Decompilador open-source para código máquina.

## Static & Dynamic Analysis

Los análisis estáticos y dinámicos son dos métodos cruciales en ciberseguridad para examinar malware. El análisis estático involucra inspeccionar el código sin ejecutarlo, mientras que el análisis dinámico involucra observar su comportamiento mientras se ejecuta. Las herramientas mencionadas debajo son comúnmente usadas en esta categoría:

* Process Hacker: Editor de memoria sofisticado y observador de procesos.
* PEview: Visor de ejecutables portables (PE) para análisis.
* Dependency Walker: Una herramienta para mostrar las dependencias de un ejecutable DLL.
* DIE (Detect It Easy): Una herramienta de detección de empaquetadores, compiladores y criptográficos.

## Forensics & Incident Response

Digital Forensics involucra la recolección, análisis, y preservación de evidencia digital desde varias fuentes como computadores, networks, y dispositivos de almacenamiento. Al mismo tiempo, Incident Response se centra en la detección, contención, erradicación y recuperación de ciberataques. Las herramientas mencionadas debajo son comúnmente usadas en esta categoría:

* Volatility: Framework de análisis de RAM dump para forense de memorias.
* Rekall: Framework para forenses de memorias en respuesta de incidentes.
* FTK Imager: Adquisición de imagen de disco y herramientas de análisis para usos forense.

## Network Analysis

El análisis de redes incluye diferentes métodos y técnicas para estudiar y analizar redes con el fin de descubrir patrones, optimizar el rendimiento y comprender la estructura y el comportamiento subyacentes de la red.

* Wireshark: Analizador de protocolos de red para registro y examinación de tráfico.
* Nmap: Detección de vulnerabilidades y herramienta de mapping de red.
* Netcat: Escribir y leer datos a través de las conexiones de red.

## File Analysis

El análisis de archivos es una técnica usada para examinar archivos por potenciales amenazas de seguridad y garantizar permisos de archivos apropiados.

* FileInsight: Un programa para examinar y editar archivos binarios.
* Hex Fiend: Editor hexadecimal ligero y rápido.
* HxD: Visualización y edición de archivos binarios con un editor hexadecimal.

## Scripting & Automation

La creación de scripts y la automatización implican el uso de scripts como PowerShell y Python para automatizar tareas y procesos repetitivos, haciéndolos más eficientes y menos propensos a errores humanos.

* Python: Principalmente enfocado en la automatización de módulos y herramientas de Python.
* PowerShell Empire: Marco de trabajo para la post-explotación con PowerShell.

## Sysinternals Suite

Sysinternals Suite es una colección de utilidades de sistema avanzadas diseñadas para ayudar a los profesionales de TI y desarrolladores a administrar, solucionar problemas y diagnosticar sistemas Windows.

* Autoruns: Muestra qué archivos ejecutables están configurados para ejecutarse durante el arranque del sistema.
* Process Explorer: Proporciona información sobre los procesos en ejecución.
* Process Monitor: Supervisa y registra la actividad de procesos/hilos en tiempo real.

## Herramientas Comúnmente Usadas

| Herramienta      | Valor Investigativo                                                                                                                                                                              |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Procmon          | Una herramienta útil para el seguimiento de la actividad del sistema, especialmente en lo que respecta a la investigación de malware, la resolución de problemas y las investigaciones forenses. |
| Process Explorer | Permite ver el proceso de la relación padre-hijo, las DLL cargadas y su ruta.                                                                                                                    |
| HxD              | Los archivos maliciosos pueden examinarse o modificarse mediante edición hexadecimal.                                                                                                            |
| Wireshark        | Observar e investigar el tráfico de la red para detectar actividad inusual.                                                                                                                      |
| CFF Explorer     | Puede generar hashes de archivos para la verificación de integridad, autenticar el origen de los archivos del sistema y validar su validez.                                                      |
| PEStudio         | Análisis estático o estudio de las propiedades de los archivos ejecutables sin ejecutarlos.                                                                                                      |
| FLOSS            | Extrae y desofusca todas las cadenas de texto de los programas maliciosos utilizando técnicas avanzadas de análisis estático.                                                                    |

### Process Monitor (Procmon)

Una herramienta de Windows poderosa diseñada para ayudar a registrar problemas con las aplicaciones del sistema. Permite ver, registrar, y mantener un seguimiento del sistema y la actividad de los archivos de Windows en tiempo real. Process Monitor es de ayuda para seguir actividades del sistema, especialmente acerca de investigación de malware, troubleshooting, e investigaciones forense. Realiza un seguimiento en tiempo real del sistema de archivos, el registro y la actividad de subprocesos/procesos.

### Process Explorer (Procexp)

Process Explorer ofrece información detallada sobre los procesos activos que se ejecutan en su ordenador. Le permite profundizar en el funcionamiento interno de su sistema, proporcionando una lista completa de los procesos que se están ejecutando actualmente y sus cuentas de usuario vinculadas. Si alguna vez ha tenido curiosidad por saber qué programa está accediendo a un archivo o carpeta específicos, Process Explorer puede proporcionarle esa información.

### HxD

HxD es un editor hexadecimal rápido y flexible para editar archivos, memoria y unidades de cualquier capacidad. Se puede aplicar a la investigación forense, la recuperación de datos, la depuración y la manipulación precisa de datos binarios. Entre sus características principales se incluyen la visualización del contenido de archivos y memoria, la edición, la búsqueda y la comparación de datos hexadecimales. Veamos cómo funciona la herramienta.

### CFF Explorer

Con la ayuda de la información completa de archivos de CFF Explorer, los investigadores pueden generar hashes de archivos para verificar su integridad, autenticar el origen de los archivos del sistema y validar su validez (por ejemplo, buscando alteraciones inusuales). Esto es importante saberlo al analizar malware, ya que el código peligroso puede estar oculto en archivos del sistema alterados.

### Wireshark

En lo que respecta al análisis del tráfico de red, Wireshark es una herramienta poderosa que los investigadores pueden usar para rastrear conexiones sospechosas, examinar protocolos y detectar posibles ataques o exfiltración de datos. En este caso, TLSv1.2 sugiere una conexión segura y cifrada que puede enmascarar actividades maliciosas o proteger el tráfico legítimo.

### PEStudio

El análisis estático, o el estudio de las propiedades de los archivos ejecutables sin ejecutarlos, se realiza con PEstudio. Esta función resulta útil en diversas situaciones. PEstudio ofrece información variada sobre un archivo sin poner en riesgo la ejecución, lo que ayuda a identificar ejecutables sospechosos o potencialmente dañinos.

### FLOSS

Utilizando técnicas avanzadas de análisis estático, FLARE Obfuscated String Solver (FLOSS, anteriormente FireEye Labs Obfuscated String Solver) extrae y desofusca automáticamente todas las cadenas de los programas maliciosos. Al igual que strings.exe, puede mejorar el análisis estático básico de binarios desconocidos. FLOSS también incluye más scripts de Python en el directorio de scripts, que se pueden usar para cargar la salida del script en otros programas como IDA Pro o Binary Ninja.


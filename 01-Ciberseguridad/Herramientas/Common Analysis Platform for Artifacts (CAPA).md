## Índice
```table-of-contents
```
## ¿Qué es?

CAPA es una herramienta desarrollada por el equipo FireEye Mandiant. Está diseñado para identificar las capacidades presentes en archivos ejecutables como Portable Executables (PE), ELF binaries, .NET modules, shellcode, e incluso reportes sandbox.

Lo hace analizando el archivo y aplicando un conjunto de reglas que describen comportamientos comunes, permitiendo determinar que es capaz de hacer el programa, como comunicación de red, manipulación de archivos, procesos de inyección, y muchos más.

## Ejecutando CAPA

La adición del comando `-h` nos dará más información sobre los parámetros disponibles con la herramienta, con `-v` aumentamos el nivel de detalle del output. También se puede usar `-vv` para más detalles.

```powershell
capa.exe .\cryptbot.bin
```

NOTA: Los resultados obtenidos pueden variar, esto es meramente como guía.

![[Pasted image 20260421205942.png]]

Este proceso puede llevar algunos minutos.

## Diseccionando los resultados de CAPA (1): Información General, MITRE y MAEC

Vamos a diseccionar el output por bloques. El primer bloque contiene información básica sobre el archivo. Incluye:

* Los algoritmos criptográficos, como `md5` y `sha1/256`.
* El campo `analisys` nos dice como CAPA realiza su análisis en el archivo
* El campo `os` revela el contexto del sistema operativo en el que se aplica las capacidades identificadas.
* El campo `arch` nos permite determinar si estamos lidiando con un binario relacionado a arquitectura x86.
* El `path` es donde el archivo analizado estaba albergado.

![[Pasted image 20260421210306.png]]

### [[MITRE ATT&CK]]

El framework [[MITRE ATT&CK|MITRE ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge)]] es un repositorio de conocimiento comprensivo global que documenta meticulosamente las técnicas y tácticas empleadas por actores amenazantes en cada etapa de un ciberataque. Funciona como un playbook, proporcionado vistas detalladas de los métodos de los atacantes.

CAPA usa este formato para el output. Algunos resultados pueden o no pueden contener el Identificador de Técnicas y Sub-Técnicas.


| Formato                                                                                                                    | Ejemplo                                                                                  |
| -------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| **ATT&CK Tactic**::**ATT&CK Technique**::**Technique Identifier**                                                          | Defense Evasion::Obfuscated Files or Information::T1027                                  |
| **ATT&CK Tactic**::**ATT&CK Technique**::**ATT&CK Sub-Technique**::**Technique Identifier**[.]Sub-technique **Identifier** | Defense Evasion::Obfuscated Files or Information::Indicator Removal from Tools T1027.005 |


![[Pasted image 20260421210715.png]]

En el output final de CAPA, referencian al framework [[MITRE ATT&CK|MITRE]]. Esto ayuda a los analistas o defensores mapear el comportamiento del archivo al playbook del adversario, donde pueden angostar la mira de la investigación durante el incidente.

### MAEC

Malware Attribuye Enumeration and Characterization es un lenguaje especializado diseñado para codificar y comunicar detalles complejos concerniendo malware. Esto contiene un rango extensivo de atributos, incluyendo comportamientos, artefactos, e interconexiones entre varias instancias de malware. Este lenguaje funciona como un sistema estandarizado para el seguimiento y análisis de complejidades complicadas de malware.

![[Pasted image 20260421211132.png]]

Los valores más usados de MAEC por CAPA son : Downloader y Launcher


| MAEC Value | Descripción                                                                                                               |
| ---------- | ------------------------------------------------------------------------------------------------------------------------- |
| Launcher   | Exhibe comportamientos que disparan acciones específicas similares al comportamiento de malware.                          |
| Downloader | Presenta comportamientos en los que descarga y ejecuta otros archivos, algo que suele observarse en malware más complejo. |

Cuando CAPA cataloga un archivo con el valor MAEC "launcher", indica que el archivo demostró comportamiento similar pero no limitado a:

* Lanzar payloads adicionales.
* Activar mecanismos de persistencia.
* Conectarse a servidores de Comando y Control (C2).
* Ejecutar funciones específicas.

Cuando CAPA cataloga un archivo con el valor MAEC "downloader", indica que el archivo demostró comportamiento similar pero no limitado a:

* Obtener cargas útiles o recursos adicionales de Internet.
* Obteniendo actualizaciones.
* Ejecutar etapas secundarias.
* Recuperar archivos de configuración.

## Diseccionando los resultados de CAPA (2): Malware Behavior Catalogue

### Malware Behavior Catalogue (MBC)

MBC está designado para soportar varios aspectos del análisis de malware, tales como el etiquetado, el análisis de similitud y la presentación de informes estandarizados. Esencialmente, sirve como un catálogo de objetivos y comportamientos de malware. 

MBC también se puede enlazar a métodos [[MITRE ATT&CK|ATT&CK]] y registrar todos los comportamientos y características de código descubiertas durante análisis de malware. Es importante mencionar que los nombres de comportamientos MBC pueden o no coincidir con las técnicas [[MITRE ATT&CK|ATT&CK]] correspondientes. 

La información de las páginas de comportamiento complementa el contenido de las páginas de ATT&CK. En otras palabras, al registrar comportamientos de malware, los usuarios de MBC harán referencia a ATT&CK, pero MBC no duplica la información de ATT&CK.

El contenido de MBC puede ser representado en dos formatos.


| Formato                                                 | Ejemplo                                                                             |
| ------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| **OBJECTIVE**::**Behavior**::**Method**[**Identifier**] | ANTI-STATIC ANALYSIS::Executable Code Obfuscation::Argument Obfuscation [B0032.020] |
| **OBJECTIVE**::**Behavior**::[**Identifier**]           | COMMUNICATION::HTTP Communication:: [C0002]                                         |

La diferencia entre estos dos formatos es que el primer formato contiene detalles adicionales llamados METHOD, que también puede denominarse subtécnica.

También debemos discutir el Objective, Behavior y Methods para entender mejor esta parte.

### Objective

Los Objective son basados en tácticas [[MITRE ATT&CK|ATT&CK]] en el contexto de comportamiento de malware, aunque no todos son incluidos. Además, MBC cuenta con análisis anticonductuales y antiestáticos. Estos objetivos están diseñados para el análisis de malware con el caso de uso de caracterización de malware. Consulte la tabla a continuación para obtener una explicación de cada uno.


| Objective                | Explicación                                                                                                                                                                                                                                                                                                                                                                |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Anti-Behavioral Analysis | El malware intenta evitar la dirección escondiéndose del análisis de comportamiento usando herramientas como sandboxes o debuggers.                                                                                                                                                                                                                                        |
| Anti-Static Analysis     | El malware intenta obstruir o añadir complejidad al análisis estático, haciéndolo más retador para profesionales de seguridad identificarlo y entender sus comportamientos e intenciones maliciosas.                                                                                                                                                                       |
| Collection               | El malware se enfoca en identificar y recopilar información desde la máquina objetivo o red.                                                                                                                                                                                                                                                                               |
| Command and Control      | El malware suele establecer comunicación con los sistemas comprometidos a través de diversos métodos, como servidores de comando y control, redes peer-to-peer u otros medios. Esta comunicación permite al malware controlar los sistemas comprometidos, lo que posibilita a los atacantes ejecutar comandos, extraer datos o llevar a cabo otras actividades maliciosas. |
| Credential Access        | El objetivo principal del malware es robar credenciales de cuenta, como nombres de usuario y contraseñas.                                                                                                                                                                                                                                                                  |
| Defense Evasion          | El malware tiene como objetivo eludir y sortear los diversos mecanismos de detección y seguridad presentes en el sistema para evitar ser detectado o neutralizado.                                                                                                                                                                                                         |
| Discovery                | El malware busca recopilar información detallada sobre la configuración y el entorno del sistema o de red, incluyendo hardware, software e infraestructura de red.                                                                                                                                                                                                         |
| Execution                | El malware está diseñado para ejecutar comandos o código no autorizados en un sistema informático específico sin el consentimiento del usuario. Esto puede incluir una amplia gama de actividades dañinas, como el robo de información personal, el daño de archivos o el acceso no autorizado al sistema.                                                                 |
| Exfiltration             | El malware está diseñado para infiltrarse en sistemas informáticos o redes con el fin de robar y extraer datos confidenciales. Esto puede incluir información personal, detalles financieros y cualquier otro dato valioso almacenado en el sistema o red objetivo.                                                                                                        |
| Impact                   | El malware tiene como objetivo manipular, interrumpir o dañar los sistemas informáticos y los datos. Puede ingresar a las computadoras a través de correos electrónicos infectados, sitios web comprometidos y otros medios engañosos, lo que conlleva pérdidas financieras, violaciones de la privacidad e inestabilidad del sistema.                                     |
| Lateral Movement         | El malware busca propagarse a través de la red, ya sea de forma activa mediante el acceso a las máquinas o de forma pasiva, como por ejemplo a través de correos electrónicos maliciosos.                                                                                                                                                                                  |
| Persistence              | El malware se desarrolla intencionalmente con la capacidad de permanecer indetectado y operativo en un sistema informático durante un período prolongado.                                                                                                                                                                                                                  |
| Privilege Escalation     | El malware busca infiltrarse en un sistema informático o red para obtener permisos elevados o control. Una vez dentro del entorno objetivo, el malware puede intentar escalar sus privilegios, acceder a información confidencial o tomar el control de los recursos del sistema con fines maliciosos.                                                                     |

#### Micro-Objective

Los microobjetivos están asociados con microcomportamientos, que se refieren a una o varias acciones exhibidas por software potencialmente malicioso que no necesariamente es malicioso y puede servir a diversos objetivos. Ejemplos de binarios son los que se encuentran en las aplicaciones de mensajería. Sin embargo, es importante tener en cuenta que estos comportamientos suelen ser objeto de abuso. Por eso, CAPA podría haber marcado este comportamiento.


| Micro-Objective | Description                                                                                                                                                        |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| PROCESS         | Exhibir comportamientos relacionados con procesos tales como, pero no limitados a, Crear proceso, Establecer contexto de hilo, Terminar proceso y Comprobar mutex. |
| MEMORY          | Exhibir comportamientos tales como, pero no limitados a, Asignar memoria, Cambiar la protección de la memoria y Liberar memoria                                    |
| COMMUNICATION   | Exhibiendo comportamientos tales como (no limitados a (DNS, FTP, HTTP, ICMP, SMTP) tráfico de red                                                                  |
| DATA            | Exhibir comportamientos tales como, pero no limitados a, verificar cadenas, comprimir, decodificar y codificar datos.                                              |

### MBC Behaviors

La columna Comportamientos MBC contiene comportamientos y microcomportamientos con o sin sus métodos e identificadores.


| Objective                             | Behavior                          | Identifiers | Explicación                                                                                                                                                                                                                                                                                                                      |
| ------------------------------------- | --------------------------------- | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ANTI-BEHAVIORAL ANALYSIS              | Virtual Machine Detection         | B0009       | El malware comprueba si se está ejecutando en un entorno virtual. Durante su reconocimiento del sistema, el malware examina diversos artefactos del usuario y del sistema.                                                                                                                                                       |
| ANTI-STATIC ANALYSIS                  | Executable Code Obfuscation       | B0032       | El código ejecutable se ha ocultado intencionadamente para evitar el análisis estático del código. Este es un comportamiento específico relacionado con el código ejecutable de una muestra de malware, incluidas sus secciones de datos y texto.                                                                                |
| EXECUTION                             | Command and Scripting Interpreter | E1059       | El malware puede explotar intérpretes de comandos y scripts para ejecutar comandos, scripts o binarios maliciosos. Su objetivo son los intérpretes integrados como cmd.exe o PowerShell en Windows, o Bash en sistemas tipo Unix. Los atacantes también pueden usar otros lenguajes de scripting como Python, Perl o JavaScript. |
| DISCOVERY                             | File and Directory Discovery      | E1083       | El malware tiene la capacidad de buscar archivos específicos en ubicaciones particulares mediante la enumeración de archivos y directorios.                                                                                                                                                                                      |
| ANTI-STATIC ANALYSIS, DEFENSE EVASION | Obfuscated Files or Information   | E1027       | El malware puede ofuscar archivos o información mediante codificación, cifrado u otros métodos, lo que dificulta su análisis. También puede codificar o cifrar las propias muestras de malware.                                                                                                                                  |

#### Micro-Behavior

El término "comportamientos de bajo nivel" en el análisis de malware se refiere a acciones exhibidas por el malware que no son necesariamente maliciosas y pueden servir a diversos objetivos. Estos comportamientos a menudo se documentan como "microcomportamientos" en el análisis de Características de Comportamiento de Malware (MBC).

Ejemplos de este tipo de comportamientos de bajo nivel incluyen la creación de sockets TCP y la evaluación de condiciones específicas dentro de cadenas de caracteres. Es importante tener en cuenta que el hecho de que un comportamiento se clasifique como de bajo nivel no significa que sea inofensivo, ya que aún puede formar parte de un plan malicioso más amplio.


| Micro-Objective | Micro-Behaviors    | Identifiers | Explicación                                                                                                                                                          |
| --------------- | ------------------ | ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| MEMORY          | Allocate Memory    | C0007       | El malware frecuentemente utiliza la asignación de memoria como parte de su estrategia para descomprimirse y ejecutar sus actividades maliciosas.                    |
| PROCESS         | Create Process     | C0017       | El malware crea un proceso a través de WMI o shellcode. También puede crear un proceso suspendido.                                                                   |
| COMMUNICATION   | HTTP Communication | C0002       | El malware es capaz de iniciar comunicaciones HTTP.                                                                                                                  |
| DATA            | Check String       | C0019       | El malware puede inspeccionar una cadena para identificar características específicas, como contenido ASCII, números de tarjetas de crédito y longitud de la cadena. |
| DATA            | Encode Data        | C0026       | El malware tiene la capacidad de codificar datos utilizando base64 y XOR.                                                                                            |
| FILE SYSTEM     | Create Directory   | C0046       | El malware puede crear un directorio.                                                                                                                                |
| FILE SYSTEM     | Delete File        | C0047       | El malware tiene la capacidad de eliminar un archivo.                                                                                                                |
| FILE SYSTEM     | Read File          | C0051       | El malware puede leer un archivo.                                                                                                                                    |
| FILE SYSTEM     | Writes File        | C0052       | El malware tiene la capacidad de escribir en un archivo.                                                                                                             |

### Methods

Por último, revisemos los MÉTODOS. A continuación se muestran algunos métodos incluidos en los resultados de la muestra anterior. Los métodos están vinculados a comportamientos; por lo tanto, para ver todos los métodos completos, consulte cada comportamiento/microcomportamiento específico de su interés.


| Behavior                        | Methods or sub-technique    | Identifier | Explanation                                                                                                                                   |
| ------------------------------- | --------------------------- | ---------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Executable Code Obfuscation     | Argument Obfuscation        | B0032.020  | Los argumentos simples de número o cadena de texto en las llamadas a la API se calculan en tiempo de ejecución, lo que dificulta el análisis. |
| Executable Code Obfuscation     | Stack Strings               | B0032.17   | Construye y descifra las cadenas en la pila en cada uso, luego descártalas para evitar referencias obvias.                                    |
| HTTP Communication              | Read Header                 | C0002.014  | Encabezado de lectura HTTP                                                                                                                    |
| Encode Data                     | Base 64                     | C0026.001  | El malware puede codificar datos utilizando Base64.                                                                                           |
| Encode Data                     | XOR                         | C0026.002  | El malware puede utilizar XOR para codificar datos.                                                                                           |
| Obfuscated Files or Information | Encoding-Standard Algorithm | E1027.m02  | La codificación de muestras de malware, archivos u otra información utiliza un algoritmo estándar (por ejemplo, base64).                      |

## Ejemplo

![[Pasted image 20260421214056.png]]


| Label         | Value       | Explanation                                                                                                           |
| ------------- | ----------- | --------------------------------------------------------------------------------------------------------------------- |
| MBC Objective | DATA        | Exhibir comportamientos tales como, pero no limitados a, verificar cadenas, comprimir, decodificar y codificar datos. |
| MBC Behavior  | Encode Data | El malware tiene la capacidad de codificar datos utilizando base64 y XOR.                                             |
| Method        | Base64      | El malware puede codificar datos utilizando Base64.                                                                   |
| Identifier    | C0026.001   | El identificador transmite información sobre un comportamiento. También sirve como etiqueta.                          |

## Diseccionando los resultados de CAPA (3): Namespaces

![[Pasted image 20260421214447.png]]

El contenido de este bloque es representado en el siguiente formato


| Format                                                                | Sample                                                        | Explicación                                                                                                                                         |
| --------------------------------------------------------------------- | ------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Capability(Rule Name)**::**TLN(Top-Level Namespace)**/**Namespace** | reference anti-VM strings::Anti-Analysis/anti-vm/vm-detection | **Reference anti-VM strings** = Capability(Rule Name)  <br>**Anti-Analysis** = TLN or Top-Level Namespace  <br>**anti-vm/vm-detection** = Namespace |

### Namespaces

CAPA utiliza espacios de nombres para agrupar elementos con el mismo propósito.


| Top-Level Namespace (TLN) | Explicación                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| anti-analysis             | Contiene un conjunto de reglas diseñadas específicamente para detectar comportamientos que exhibe el malware para evadir el análisis. Estos comportamientos incluyen técnicas de ofuscación, empaquetado y anti-depuración.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| collection                | Contiene un conjunto de reglas relacionadas con los datos que el malware puede enumerar y recopilar para su exfiltración u otros fines. Piénselo como el aspecto de "recopilación de datos" del comportamiento del malware.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| communication             | Contiene un conjunto de reglas que rigen los diferentes comportamientos de comunicación del malware. Esto abarca la forma en que el malware interactúa con las redes, incluyendo la transmisión y recepción de datos, las comunicaciones de comando y control, y otros comportamientos relacionados con la red.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| compiler                  | Contiene un conjunto de reglas y configuraciones para reconocer entornos de compilación o compiladores específicos empleados en la generación de ejecutables. Estos espacios de nombres sirven esencialmente como la "firma" única que identifica el proceso de compilación de un programa.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| data-manipulation         | Contiene un conjunto de reglas que rigen los comportamientos relacionados con la alteración de datos dentro de archivos ejecutables. Este aspecto puede considerarse el componente de "transformación de datos" del comportamiento del malware, que abarca acciones como el cifrado de cadenas y la codificación de datos.                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| executables               | Contiene un conjunto de reglas relativas a los atributos de los archivos ejecutables. Estos atributos incluyen secciones PE o información de depuración asociada al ejecutable.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| host-interaction          | Contiene un conjunto de reglas relacionadas con comportamientos que implican interacciones con el sistema anfitrión. Esto abarca cómo el malware interactúa con su entorno. Específicamente, las reglas en este espacio de nombres pueden capturar comportamientos relacionados con la lectura, escritura o modificación de archivos en el disco, incluyendo la creación, eliminación o modificación de archivos y directorios.                                                                                                                                                                                                                                                                                                                                                                         |
| impact                    | Contiene un conjunto de reglas relacionadas con las posibles consecuencias o efectos del comportamiento de un programa. Piénselo como el aspecto que se centra en el posible daño que puede causar este malware. Puede incluir comportamientos relacionados con el establecimiento de acceso remoto, la exfiltración de datos, la destrucción o la modificación.                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| internal                  | Las reglas contenidas en el sistema no están destinadas al uso directo por parte de los analistas ni a la elaboración de informes. En cambio, estas reglas están pensadas para fines internos dentro de la herramienta CAPA, sirviendo como el aspecto interno del desarrollo y la ejecución de las reglas.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| lib                       | Bloques de construcción para crear otras reglas                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| linking                   | Contiene reglas para identificar comportamientos que implican la vinculación o la carga dinámica de código o bibliotecas externas durante la ejecución del programa. Esta es su función principal y es crucial para la seguridad del programa. Comprender el comportamiento de vinculación es esencial por varias razones. El malware a menudo depende de bibliotecas o componentes externos (como OpenSSL, Zlib u otras bibliotecas de terceros) para llevar a cabo tareas específicas. Detectar estas dependencias ayuda a los analistas a comprender las capacidades del malware. Las bibliotecas externas también introducen una superficie de ataque adicional. Si existe una vulnerabilidad en una biblioteca vinculada, puede ser explotada por el malware o los defensores durante el análisis. |
| load-code                 | Contiene un conjunto de reglas y regulaciones relacionadas con los comportamientos asociados con la carga o ejecución dinámica de código durante la ejecución del programa. Este concepto puede equipararse al aspecto de "inyección de código en tiempo de ejecución" del comportamiento del malware, que implica la introducción de código no autorizado durante la ejecución de un programa.                                                                                                                                                                                                                                                                                                                                                                                                         |
| malware-family            | Contiene un conjunto de reglas relacionadas con comportamientos vinculados a familias o grupos específicos de malware. Sirve para identificar las características distintivas o "firmas" asociadas con familias de malware conocidas, lo que permite una detección y clasificación más precisa de posibles amenazas.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| nursery                   | Este es un campo de entrenamiento que contiene reglas para aquellos que no están del todo pulidos.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| persistence               | Contiene reglas relacionadas con comportamientos asociados con el mantenimiento del acceso o la persistencia dentro de un sistema comprometido. Este espacio de nombres se centra esencialmente en comprender cómo el malware puede establecer y mantener una presencia dentro de un entorno comprometido, lo que le permite persistir y llevar a cabo actividades maliciosas durante un período prolongado.                                                                                                                                                                                                                                                                                                                                                                                            |
| runtime                   | Contiene un conjunto de reglas que buscan identificar el lenguaje o la plataforma en la que se ejecuta el programa.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| targeting                 | Contiene un conjunto de reglas relacionadas con los comportamientos que exhiben los programas que interactúan con los cajeros automáticos.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |


### Ejemplo


| Top-Level Namespace (TLN) | Namespaces           | Rule YAML File                                                                                                  | Explanation                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ------------------------- | -------------------- | --------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Anti-Analysis             | anti-vm/vm-detection | reference-anti-vm-strings-targeting-virtualbox.yml  <br>  <br>reference-anti-vm-strings-targeting-virtualpc.yml | El espacio de nombres "anti-vm/vm-detection" contiene reglas para detectar entornos de máquinas virtuales (VM). Estas reglas se centran en identificar cadenas o patrones específicos que el malware suele utilizar para detectar máquinas virtuales en ejecución. Mediante estas reglas, CAPA puede identificar si el malware busca claves de registro específicas de VMware, la presencia de herramientas de VMware u otros elementos relacionados con las máquinas virtuales. |
|                           | obfuscation          | obfuscated-with-dotfuscator.yml  <br>  <br>obfuscated-with-smartassembly.yml                                    | El malware suele utilizar técnicas de ofuscación para dificultar el análisis. Estas incluyen métodos como el cifrado de cadenas, la ofuscación de código, el empaquetado y trucos anti-depuración. El espacio de nombres de ofuscación aborda estas técnicas, que ocultan u oscurecen el verdadero propósito del código.                                                                                                                                                         |

## Diseccionando los resultados de CAPA (4): Capability

A continuación hay una tabla con la Capability y sus TLN relacionados, namespaces, y las reglas asociadas con el archivo yaml.


| Capability                                     | Top-Level Namespace (TLN) | Namespaces            | Rule YAML file                                                            |
| ---------------------------------------------- | ------------------------- | --------------------- | ------------------------------------------------------------------------- |
| reference anti-VM strings                      | Anti-Analysis             | anti-vm/vm-detection  | reference-anti-vm-strings.yml                                             |
| reference anti-VM strings targeting VMWare     | Anti-Analysis             | anti-vm/vm-detection  | reference-anti-vm-strings-targeting-vmware.yml                            |
| reference anti-VM strings targeting VirtualBox | Anti-Analysis             | anti-vm/vm-detection  | reference-anti-vm-strings-targeting-virtualbox.yml                        |
| reference HTTP User-Agent string               | Communication             | http/client           | reference-http-user-agent-string.yml                                      |
| check HTTP status code                         | Communication             | http                  | check-http-status-code.yml                                                |
| reference Base64 string                        | Data Manipulation         | encoding/base64       | reference-base64-string.yml                                               |
| encode data using XOR                          | Data Manipulation         | encoding/XOR          | encode-data-using-xor.yml                                                 |
| contain a thread local storage (.tls) section  | Executable                | pe/section/tls        | contain-a-thread-local-storage-tls-section.yml                            |
| get common file path                           | Host-Interaction          | file-system           | get-common-file-path.yml                                                  |
| create directory                               | Host-Interaction          | file-system/create    | create-directory.yml                                                      |
| delete file                                    | Host-Interaction          | file-system/delete    | delete-file.yml                                                           |
| read file on Windows                           | Host-Interaction          | file-system/read      | read-file-on-windows.yml                                                  |
| write file on Windows                          | Host-Interaction          | file-system/write     | write-file-on-windows.yml                                                 |
| get thread local storage value                 | Host-Interaction          | process               | get-thread-local-storage-value.yml                                        |
| allocate or change RWX memory                  | Host-Interaction          | process/inject        | allocate-or-change-rwx-memory.yml                                         |
| create process on Windows                      | Host-Interaction          | process create        | create-process-on-windows.yml                                             |
| reference cryptocurrency strings               | Impact                    | impact/cryptocurrency | reference-cryptocurrency-strings.yml                                      |
| link function at runtime on Windows            | Linking                   | runtime-linking       | link-function-at-runtime-on-windows.yml                                   |
| parse PE header                                | load-code                 | load-code/pe          | parse-pe-header.yml  <br>  <br>resolve-function-by-parsing-pe-exports.yml |
| resolve function by parsing PE exports         | load-code                 | load-code/pe          | resolve-function-by-parsing-pe-exports.yml                                |
| run PowerShell expression                      | load-code                 | load-code/PowerShell  | run-powershell-expression.yml                                             |
| schedule task via at                           | persistence               | scheduled-tasks       | schedule-task-via-at.yml                                                  |
| schedule task via schtasks                     | persistence               | scheduled-tasks       | schedule-task-via-schtasks.yml                                            |

### Ejemplo 

![[Pasted image 20260421225040.png]]

Explicación

| Label                   | Value                           | Explanation                                                                                                                                                                                                                                                    |
| ----------------------- | ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Capability              | **reference base64 string**     | Malware has the capability to encode data using a base64 scheme.                                                                                                                                                                                               |
| Top-Level Namespace     | **data-manipulation**           | contains a set of rules that govern the behaviors involved in altering data within executable files. This aspect can be considered the “data transformation” component of malware behaviour, encompassing actions such as String Encryption and Data Encoding. |
| Namespace               | **encoding/base64**             | this namespace consists of rules for encoding and decoding data using Base64 and XOR                                                                                                                                                                           |
| Rule YAML File Matched? | **reference-base64-string.yml** | Remember that the capability's name is also the rule's name with an additional dash (-) character between spaces.                                                                                                                                              |


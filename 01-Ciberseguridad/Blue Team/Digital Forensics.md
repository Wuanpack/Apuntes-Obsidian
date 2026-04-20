## ¿Qué es?

La ciencia forense es la aplicación de métodos y procedimientos para investigar y resolver delitos. La rama de la ciencia forense que investiga los delitos cibernéticos se conoce como informática forense. Un delito cibernético es cualquier actividad delictiva realizada en o mediante un dispositivo digital. Se utilizan diversas herramientas y técnicas para investigar a fondo los dispositivos digitales después de un delito, con el fin de encontrar y analizar pruebas para las acciones legales necesarias.

## Metodología

El equipo de informática forense tiene varios casos que requieren diferentes herramientas y técnicas. Sin embargo, el National Institute of Standards and Technology (NIST) defina un procedimiento general por cada caso. El NIST trabaja definiendo marcos de trabajo para diferentes áreas de la tecnología, incluyendo la ciberseguridad, donde introducen el proceso de digital forensics en cuatro fases.

![[Pasted image 20260419215200.png]]


1. Collection: La primera fase del digital forensics es la recolección de datos. Identificar todos los dispositivos desde los cuales se puede recolectar datos es esencial. Usualmente, un investigador puede encontrar computadores personales, laptops, cámaras digitales, USBs, etc., en una escena del crimen. También es necesario garantizar que los datos originales no se manipulen durante la recolección de pruebas y mantener un documento adecuado que contenga los detalles de los elementos recolectados. También analizaremos los procedimientos de adquisición de pruebas en las próximas tareas.
2. Examination: Los datos recolectados puede sobrecargar a los investigadores debido a su tamaño. Estos datos usualmente necesitan ser filtrados, y los datos de interés necesitan ser extraídos.
3. Analysis: Esta es una fase crítica. Los investigadores ahora tienen que analizar los datos al correlacionarlos con múltiples piezas de evidencia para marcar conclusiones. El análisis depende del escenario del caso y de los datos disponibles. El análisis tiene como objetivo extraer las actividades relevantes para el caso cronológicamente.
4. Reporting: Esta es la última fase de digital forensics, donde se prepara un reporte detallado. Este reporte contiene la metodología de la investigación y los hallazgos detallados a partir de las pruebas recopiladas. También puede contener recomendaciones. Este informe se presenta a las fuerzas del orden y a la alta dirección. Es importante incluir resúmenes ejecutivos como parte del informe, teniendo en cuenta el nivel de comprensión de todos los destinatarios

Como parte de la fase de recolección, vimos que varias piezas de evidencia pueden ser encontradas en la escena del crimen. Analizar estas múltiples categorías de evidencia requiere varias herramientas y técnicas. Estos son diferentes tipos de digital forensics, todos con su propia colección y análisis de metodologías. Algunas de los tipos más comunes son los siguientes:

![[Pasted image 20260419215815.png]]

* Computer Forensics: El tipo más común de forense informático es el forense de computadores, el cual consiste en investigar computadores, los dispositivos más comúnmente usados en crímenes.
* Mobile Forensics: Los mobile forensics involucran investigar dispositivos móviles y extraer data como registros de llamadas, mensajes de texto, locación GPS, y más.
* Network Forensics: Esta área forense cubre la investigación más allá de los dispositivos individuales. Incluye la red completa. La mayoría de evidencia encontrada en la red es por medio de los network traffic logs.
* Database Forensics: Muchos datos críticos son almacenados en bases de datos dedicadas. Database Forensics investiga cualquier intrusión dentro de estas bases de datos que resultan en modificación o exfiltración de datos.
* Cloud Forensics: Cloud Forensics es un tipo de forense que involucra investigar datos almacenados en infraestructura cloud. Este tipo de análisis forense a veces resulta complicado para los investigadores, ya que hay poca evidencia en las infraestructuras en la nube.
* Email forensics: Email, el método de comunicación más común entre profesionales, se ha convertido en una parte importante del digital forensics. Los emails son investigados para determinar si son parte de phishing o campañas fraudulentas.

## Evidence Acquisition

Obtener evidencia es un trabajo crítico. El equipo forense debe recolectar todas las pruebas de forma segura sin alterar los datos originales. Los métodos de obtención de pruebas para dispositivos digitales dependen del tipo de dispositivo digital. Sin embargo, se deben seguir algunas prácticas generales durante la obtención de las pruebas.

### Proper Authorization

El equipo forense debería obtener autorización de las autoridades relevantes antes de recolectar cualquier dato. La evidencia recolectada sin la aprobación previa puede provocar que sea inadmisible en la corte. La evidencia forense contiene datos privados y sensibles de una organización o individuo. La autorización apropiada antes de recolectar data es esencial para investigar dentro de los límites de la ley.

### Cadena de Custodia

Una cadena de custodia es una documento formal que contiene todos los detalles de la evidencia. Algunos detalles clave se listan a continuación:

- Descripción de la evidencia (nombre, tipo).
- Nombre de los individuos que recolectaron la evidencia.
- Fecha y hora de la recolección de datos.
- Locación del almacenamiento de cada pieza de evidencia.
- Tiempos de acceso y el registro de individuos que accedieron a la evidencia.

Esto crea un rastro adecuado de evidencia y ayuda a preservarla. El documento de cadena de custodia puede utilizarse para demostrar la integridad y fiabilidad de la evidencia admitida en el tribunal.

### Uso de Write Blockers

Los bloqueadores de escritura son una parte esencial del conjunto de herramientas del equipo de informática forense. Supongamos que está recopilando evidencia del disco duro de un sospechoso y conectándolo a la estación de trabajo forense. Mientras se realiza la recopilación, algunas tareas en segundo plano en la estación de trabajo forense pueden alterar las marcas de tiempo de los archivos en el disco duro. Esto puede causar obstáculos durante el análisis y, en última instancia, producir resultados incorrectos. 

Supongamos que, en el mismo escenario, los datos se recopilaran del disco duro utilizando un bloqueador de escritura. En este caso, el disco duro del sospechoso permanecería en su estado original, ya que el bloqueador de escritura puede impedir cualquier alteración de la evidencia.

## Windows Forensics

Los tipos más comunes de evidencia recolectadas de escenas de crímen son computadores de escritorio y laptops, ya que la mayoría de actividad criminal involucra un sistema personal. Windows es el sistema operativo más usado y es el más común dentro de investigaciones.

Como parte de la fase de recolección de datos, las imágenes forense de los sistemas operativos Windows son tomadas. Estas imágenes forense son copias bit por bit del sistema operativo completo. Hay dos categorías diferentes de imágenes forense que son tomadas desde un sistema operativo Windows.

* Disk Image: La disk image contiene todo los datos presentes en el dispositivo de almacenamiento del sistema (hdd, sdd, m.2, etc.), Esta data es no volátil, lo que significa que los datos del disco sobrevivirían incluso después de un reinicio del sistema operativo. Por ejemplo, todos los archivos como media, documentos, historial del navegador web, etc.
* Memory Image: Esta memory image contiene todos los datos dentro de la RAM del sistema operativo. Esta memoria es volátil, lo que significa que los datos se pierden después de que el sistema se apaga o reinicia. Por ejemplo, para capturar archivos abiertos, procesos en ejecución, conexiones de red actuales, etc., la imagen de memoria debería priorizarse y ser tomada primero desde los sistemas operativos de los sospechosos; de lo contrario, cualquier reinicio o apagado del sistema podría resultar en que todos los datos volátiles se eliminen. 

Herramientas populares utilizadas para la adquisición y el análisis de imágenes de disco y memoria del sistema operativo Windows.

* FTK Imager: FTK Imager es una herramienta ampliamente usada para tomar imágenes de disco de sistemas operativos Windows. Ofrece una GUI para crear la imagen en varios formatos. Esta herramienta también puede analizar el contenido de una imagen de disco. Puede ser usada para propósitos de adquisición y análisis.
* Autopsy: Autopsy es una popular plataforma de análisis forense digital de código abierto. Un investigador puede importar una imagen de disco adquirida a esta herramienta, y esta realizará un análisis exhaustivo de la misma. Ofrece diversas funciones durante el análisis de imágenes, incluyendo búsqueda por palabras clave, recuperación de archivos eliminados, metadatos de archivos, detección de discrepancias en la extensión y muchas más.
* DumpIt: DumpIt ofrece la utilidad de crear una imagen de memoria de un sistema operativo Windows. Esta herramienta crea imágenes de memoria mediante una interfaz de línea de comandos y algunos comandos. La imagen de memoria también se puede obtener en diferentes formatos.
* Volatility: Volatility es una potente herramienta de código abierto para analizar imágenes de memoria. Ofrece complementos extremadamente útiles. Cada artefacto se puede analizar utilizando un complemento específico. Esta herramienta es compatible con varios sistemas operativos, incluidos Windows, Linux, macOS y Android.


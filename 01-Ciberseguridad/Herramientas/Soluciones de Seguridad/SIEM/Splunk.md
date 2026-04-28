## Índice
```table-of-contents
```

## ¿Qué es?

Splunk es una de las soluciones SIEM líder en el mercado. Permite a los usuarios colectar, analizar, y correlacionar registros de máquina y de red en tiempo real.


## Componentes de Splunk

Splunk tiene tres componentes principales: Forwarder, Indexer y Search Head. Estos componentes trabajan en conjunto para ayudarnos a buscar y analizar los datos. 

![[Pasted image 20260427195336.png]]

## Splunk Forwarder

Splunk Forwarder es un agente liviano instalado en el endpoint que se pretende ser monitoreado, y su tarea principal es colectar los datos y enviarlos a la instancia Splunk. No afecta el rendimiento del endpoint ya que toma pocos recursos para procesar. Algunas fuentes de datos clave son:

-  Web server generating web traffic.
* Windows machine generating Windows Event Logs, PowerShell, and Sysmon data.
* Linux host generating host-centric logs.
* Database generating DB connection requests, responses and errors.

El forwarder colecta los datos de las fuentes de registros y los envía al Splunk Indexer

## Splunk Indexer

El Splunk Indexer juega el rol principal en el procesamiento de datos que recibe de los forwarders. Analiza y normaliza los datos en pares campo-valor, los categoriza y almacena los resultados como eventos, lo que facilita la búsqueda y el análisis de los datos procesados.

Ahora, los datos, los cuales están normalizados y almacenados por el indexer, pueden ser buscados por el Search Head.

## Search Head

El Splunk Search Head es el lugar dentro de la Search & Reporting App donde los usuarios pueden buscar los registros indexados. Las búsquedas se realizan usando el SLP (Search Processing Language), un lenguaje de consultas poderoso para buscar datos indexados. Cuando el usuario realiza una búsqueda, la petición es enviada al indexer, y los eventos relevantes son retornados como pares campo-valor.

![[Pasted image 20260427200130.png]]

El Search Head también permite transformar los resultados en tablas y visualizaciones presentables, como gráficos circulares, de barras y de columnas.

## Navegando Splunk

Cuando accedes a Splunk, vas a ver la pantalla home por defecto:

![[Pasted image 20260427200443.png]]

### Splunk Bar

![[Pasted image 20260427200452.png]]

En la Splunk Bar, tenemos las siguientes opciones disponibles:

* Messages: Ver notificaciones y mensajes a nivel del sistema.
* Settings: Configurar los ajustes de la instancia de Splunk.
* Activity: Revisar el progreso de los trabajos y procesos de búsqueda.
* Help: Ver tutoriales y documentación.
* Find: Buscar en toda la aplicación.

La Splunk Bar permite a los usuarios cambiar entre apps Splunk instaladas en vez de usar el panel de Apps.

### Apps Panel

Este panel muestra las aplicaciones instaladas para la instancia Splunk. La app por defecto en cada instalación Splunk es Search & Reporting.

![[Pasted image 20260427200743.png]]

### Explore Splunk

Este panel contiene enlaces rápidos para añadir datos a la instancia Splunk, añadir nuevas apps Splunk, y acceder a la documentación de Splunk.

![[Pasted image 20260427200835.png]]


## Añadiendo Datos

Splunk puede ingerir cualquier dato. De acuerdo a la documentación de Splunk, cuando los datos son añadidos a Splunk, los datos son procesados y transformados en una serie de eventos individuales. Las fuentes de datos pueden ser registros de eventos, registros de sitios web, registros de firewall, etc. Las fuentes de datos son agrupados en categorías.

Lista de la documentación de Splunk detallando cada categoría de fuente de datos:

![[Pasted image 20260427205316.png]]


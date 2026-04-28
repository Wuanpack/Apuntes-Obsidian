## Índice

```table-of-contents
```

## ¿Qué es?

Elastic Stack (ELK) fue originalmente desarrollada para almacenar, buscar, y visualizar grandes cantidades de datos. Las organizaciones lo usan para monitorear el rendimiento de las aplicaciones y realizar búsquedas en grandes conjuntos de datos. Con el tiempo, sus características se hicieron populares en operaciones de seguridad también. Ahora, muchos equipos [[SOC]] usan ELK casi como una solución SIEM.

Elastic Stack es una colección de diferentes componentes open-source que trabajan juntas para colectar datos de cualquier fuente, almacenarlo y buscarlo, y visualizarlo en tiempo real.

![[Pasted image 20260427211022.png]]


### Elasticsearch

El primer componente, Elasticsearch, es un motor de búsqueda y análisis de texto completo para documentos con formato JSON. Almacena, analiza y correlaciona datos y admite una API RESTful para interactuar con ellos.

### Logstash

Logstash es un motor de procesamiento de datos que toma datos de diferentes fuentes, los filtra o normaliza, y luego los envía al destino, que puede ser Kibana o un puerto de escucha. Un archivo de configuración de Logstash se divide en tres partes, como se muestra a continuación.

1. La sección de Entrada es donde el usuario define la fuente desde la cual se ingieren los datos
2. La sección Filtro es donde el usuario especifica las opciones de filtro para normalizar el registro ingerido anteriormente.
3. La parte de Salida es donde el usuario desea que se envíen los datos filtrados. Puede ser un puerto de escucha, una interfaz de Kibana, una base de datos de Elasticsearch o un archivo.

Logstash admite muchos complementos de entrada, salida y filtrado.

![[Pasted image 20260427211159.png]]


### Beats

Los Beats son agentes basados ​​en el host, conocidos como remitentes de datos, que envían/transfieren datos desde los puntos finales a Elasticsearch. Cada Beat es un agente de propósito único que envía datos específicos a Elasticsearch. Todos los Beats disponibles se muestran a continuación.

![[Pasted image 20260427211249.png]]

### Kibana

Kibana es una herramienta de visualización de datos basada en la web que funciona con Elasticsearch para analizar, investigar y visualizar flujos de datos en tiempo real. Permite a los usuarios crear múltiples visualizaciones y paneles para una mejor visibilidad. Encontrará más información sobre Kibana en las siguientes tareas.

## ¿Cómo trabajan juntas?

* Beats colecta datos de múltiples agentes. Por ejemplo, Winlogbeat colecta Windows Event Logs, y Packetbeat colecta flujo de tráfico de red.
* Logstash recopila datos de beats, puertos o archivos, los analiza/normaliza en pares de campo-valor y los almacena en Elasticsearch.
* Elasticsearch actúa como base de datos usado para buscar y analizar datos.
* Kibana es responsable de mostrar y visualizar los datos almacenados en Elasticsearch. Los datos almacenados en Elasticsearch se pueden transformar fácilmente en diferentes visualizaciones, gráficos de tiempo, infografías, etc., utilizando Kibana.

![[Pasted image 20260427211553.png]]


## Discover Tab

![[Pasted image 20260427212317.png]]

La pestaña Discover es donde el analista SOC gasta la mayoría de su tiempo. Esta pestaña muestra los registros ingeridos, la barra de búsqueda, campos normalizados, y más. Los analistas pueden buscar por los registros, investigar anomalías, y aplicar filtros basados en términos de búsqueda y periodos de tiempo.

Vamos a ver cada elemento marcado en la captura de pantalla:

1. Logs:
	1. Cada file muestra un solo registro conteniendo información sobre el evento, junto con los campos y valores que se encuentran en ese registro.
2. Fields Pane:
	 Este tipo de registro está almacenado en un patrón de índice diferente. Podemos seleccionar el patrón de índice desde el cual necesitamos los registros. Por ejemplo, para los registros VPN, necesitaríamos seleccionar el patrón índice en el cual los registros VPN son almacenados.
3. Search Bar:
	 Es un lugar donde el usuario agrega consultas de búsqueda y aplica filtros para acotar los resultados. En la siguiente tarea, aprenderemos cómo realizar búsquedas mediante consultas.
4. Time Filter:
	 Podemos acotar los resultados en función de cualquier duración de tiempo específica.
5. Time Interval:
	 Este gráfico muestra el número de eventos a lo largo del tiempo.
6. TOP Bar:
	 Esta barra contiene varias opciones para guardar la búsqueda, abrir las búsquedas guardadas, compartir o guardar la búsqueda, etc.
7. Discover Tab:
	 Este es el espacio de trabajo principal en Kibana para explorar, buscar y analizar datos sin procesar.
8. Add Filter:
	 Podemos aplicar filtros a campos específicos para acotar los resultados, en lugar de escribir manualmente consultas completas.

Algunos de los elementos importantes que se encuentran en la pestaña Discover son explicados brevemente a continuación:

### Index Pattern

Por defecto, Kibana requiere un patrón de índice para acceder a los datos almacenados/ingeridos en Elasticsearch. El patrón de índice le indica a Kibana qué datos de Elasticsearch queremos explorar. Cada patrón de índice corresponde a ciertas propiedades definidas de los campos. Un único patrón de índice puede apuntar a varios índices.

Cada fuente de registro tiene una estructura de registro diferente; por lo tanto, cuando los registros se ingieren en Elasticsearch, primero se normalizan en campos y valores correspondientes mediante la creación de un patrón de índice dedicado para la fuente de datos.

En el laboratorio adjunto, exploraremos el patrón de índice vpn_connections, que contiene los registros de VPN.

![[Pasted image 20260427213242.png]]


### Fields Pane

El panel izquierdo de la pestaña Descubrir muestra la lista de campos normalizados que encuentra en los registros disponibles. Haga clic en cualquier campo y se mostrarán los 5 valores principales y el porcentaje de ocurrencia.

Podemos usar estos valores para aplicarles filtros. Al hacer clic en el botón + se agregará un filtro para mostrar los registros que contengan este valor, y al hacer clic en el botón se agregará un filtro para mostrar los resultados que no tengan este valor.

![[Pasted image 20260427213313.png]]

También podemos aplicar filtros a cualquiera de los campos que se muestran en el panel de la izquierda. Solo tenemos que hacer clic en la opción `Add Filter` debajo de la barra de búsqueda, lo que nos permitirá aplicar un filtro a los campos que se muestran a continuación.

![[f8f4399d7fbfc14c0a6659da697af1db.gif]]


### Time Filter

El filtro de tiempo nos permite aplicar un filtro de registro basado en el tiempo. Tiene muchas opciones.

![[Pasted image 20260427213348.png]]


### Timeline

El panel de línea de tiempo proporciona una descripción general de la cantidad de eventos que ocurrieron en la fecha y hora especificadas, como se muestra a continuación. Solo podemos seleccionar la barra para mostrar los registros de ese período. El contador en la parte superior izquierda muestra la cantidad de eventos encontrados en el tiempo especificado.


![[Pasted image 20260427213410.png]]

Esta barra también resulta útil para identificar el pico en los registros. En la captura de pantalla anterior, podemos observar un pico inusual en los registros el 11 de enero de 2022.

### Create Table

Por defecto, los registros se muestran en formato sin procesar. Podemos hacer clic en cualquier registro y seleccionar los campos importantes para crear una tabla que muestre solo esos campos. Este método reduce el ruido y hace que la información sea más presentable y comprensible.

![[ed538dabafffd64020b51f88fabce8f9.gif]]


También puedes guardar el formato de la tabla una vez creada. De esta forma, se mostrarán los mismos campos cada vez que un usuario inicie sesión en el panel de control.

## KQL Overview

En la Search Bar del Discover Tab podemos encontrar cualquier cosa, para ello existe un lenguaje especial que usaremos dentro de la barra de búsqueda para realizar nuestras búsquedas. KQL (Kibana Query Language) es un lenguaje de consulta para búsquedas usado para buscar documentos/logs ingeridos en Elasticseach

![[Pasted image 20260427222057.png]]


Con KQL, podemos buscar registros de dos maneras distintas:

* Free text search
* Field-based search

### Free Text Search

La Free Text Seach permite a los usuarios buscar registros basados solamente en texto. Esto significa que una simple búsqueda del término `security` va a retornar todos los documentos que contienen este término, independientemente del campo. 

KQL busca por el término/palabra completa en los documentos, eso quiere decir que si buscamos `United States`, nos van a aparecer registros, pero si buscamos `United` no nos aparecerá nada. Para ello, KQL permite el uso de `*` para coincidir partes de la palabra. Es decir, que si buscamos `United*` nos aparecerían los mismos registros que la primera vez.

### Operadores Lógicos (AND | OR | NOT)

* AND: Crea una búsqueda que incluye dos términos
* OR: Usa este operador para obtener los resultados de cualquiera de los 2 términos.
* NOT: Remueve un término en particular de los resultados de búsqueda.

### Field-based Search

En la búsqueda basada en campos, vamos a proporcionar el nombre del campo y el valor que estamos buscando en los registros. Esta búsqueda tiene una sintaxis especial tipo `Field: Value`. Usa un dos puntos como separador entre el campo y el valor. 

## Creando Visualizaciones

La pestaña de visualización nos permite visualizar los datos en diferentes formatos, como tablas, gráficos circulares, gráficos de barras, etc. Esta tarea de visualización utilizará las múltiples opciones que ofrece esta pestaña para crear visualizaciones sencillas y presentables.

### Crear Visualización

Hay varias maneras de navegar por la pestaña de visualización. Una manera es cliquear en cualquier campo en la pestaña Discover y cliquear en la visualización como se muestra a continuación:

![[334ed7c0a1e727de35844174434fd4fc.gif]]

### Opción de Correlación
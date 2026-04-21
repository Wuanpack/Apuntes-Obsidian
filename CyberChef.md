## ¿Qué es?

CyberChef es una aplicación basada en web intuitiva y simple diseñada para ayudar con varias tareas de "cyber" operaciones dentro del buscador web. Es como una navaja suiza para datos, como tener una caja de herramientas con muchas herramientas designadas para realizar tareas específicas- 

El rango de tareas van desde simples codificadores como XOR o Base64 hasta operaciones complejas como Encriptación AES o Desencriptación RSA. CyberChef opera en recetas, una serie de operaciones ejecutadas en orden.

Se puede acceder a la herramienta de forma online por medio del navegador web, o crear una copia local.

## Navegando la Superficie

1. Operations
2. Recipe
3. Input
4. Output

### Área de Operaciones

Este es un repositorio práctico y comprensible de todas las operaciones diversas con las que CyberChef está equipado para realizar. Estas operaciones están categorizadas meticulosamente, ofreciendo a los usuarios acceso conveniente a varias capacidades. Los usuarios pueden utilizar la característica buscar para localizar operaciones específicas rápidamente.


| Operaciones     | Descripción                                                                                                    |
| --------------- | -------------------------------------------------------------------------------------------------------------- |
| From Morse Code | Traduce código morse (en mayúsculas) a carácteres alfanuméricos.                                               |
| URL Encode      | Codifica carácteres problemáticos en codificación-percentil, un formato soportado por URIs/URLs.               |
| To Base64       | Esta operación codifica datos crudos en ASCII Base64 string.                                                   |
| To Hex          | Convierte las cadenas de entrada en bytes hexadecimales separados por un delimitador específico.               |
| To Decimal      | Convierte los datos de entrada en un ordinal integer array.                                                    |
| ROT13           | Un simple cifrado de sustitución Cesar el cual rota los carácteres por una cantidad especificada (default 13). |

### Área de Receta

Esta es considerada el corazón de la herramienta. En esta área, puede seleccionar, organizar y ajustar las operaciones sin problemas para adaptarlas a sus necesidades. Aquí es donde usted toma el control, definiendo los argumentos y las opciones de cada operación de forma precisa y con un propósito definido.

El área de recetas es un espacio designado para seleccionar y organizar operaciones específicas y luego definir sus respectivos argumentos y opciones para personalizar aún más su comportamiento. En el área de recetas, puede arrastrar las operaciones que desea utilizar y especificar argumentos y opciones.

Las características incluyen lo siguiente:

- Guardar receta: Esta característica permite al usuario guardar las operaciones seleccionadas.
- Cargar receta: Permite al usuario cargar recetas previamente guardadas.
- Limpiar receta: Esta característica permiten a los usuarios limpiar la receta elegida durante su uso.

El botón BAKE! procesa los datos con la receta dada. Adicionalmente, podemos tickear la checkbox Auto Brake para que la receta se cocine sin cliquear BAKE! manualmente cada vez.

### Input Area

Esta área proporciona un espacio user-friendly donde podemos ingresar texto y archivos al copiarlos, escribirlos, o arrastrarlos.

Adicionalmente, tiene las siguientes características:

- Añadir una nueva pestaña de input: Esto es donde una pestaña adicional es creada por el usuario para usar diferentes valores desde la pestaña anterior.
- Abrir una carpeta como input: Esta característica permite a los usuarios cargar una carpeta entera como valor de input.
- Abrir archivo como input: Esta característica permite al usuario cargar el archivo como su valor input.
- Limpiar input y output: Esta característica permite al usuario limpiar cualquier valor input insertado y el correspondiente valor output.
- Reset pane layout: Esta característica trae a la interfaz de la herramienta a sus tamaños de ventanas por defecto.

### Ouput Area

Este es un espacio visual que muestra los resultados del procesamiento de datos. Presenta de forma ordenada los resultados de cualquier manipulación o transformación que haya aplicado a los datos de entrada, lo que permite una visualización clara e intuitiva de la información procesada.

Las características incluyen:

- Guardar output en un archivo: Permite al usuario guardar los resultados en un archivo .dat
- Copiar raw output al clipboard: Esta catacterística permite a los usuarios copiar el raw output directamente en el clipboard, permitiendo rápidamente copiar los resultados para usarlos en otra aplicación o documentos.
- Reemplazar input con output: Esta característica permite a los usuarios rápidamente sobreescribir les datos de entrada basado en los resultados de las operaciones.
- Maximise output pane: Esta característica trae a la interfaz de la herramienta a sus tamaños de ventanas por defecto.

## Extractors

| Specific                | Description                                                                                                               |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| Extract IP addresses    | Extrae todas las direcciones IPv4 e IPv6                                                                                  |
| Extract URLs            | Extrae las URLs del input. El protocolo (HTTP, FTP, etc.) es requerido, de otra forma va a haber muchos falsos positivos. |
| Extract email addresses | Extrae las direcciones de correo del input.                                                                               |

## Date and Time


| Specific            | Description                                                                          |
| ------------------- | ------------------------------------------------------------------------------------ |
| From UNIX Timestamp | Convierte un timestamp UNIX a un datetime string                                     |
| To UNIX Timestamp   | Parsea un datetime string en UTC y lo retorna con el correspondiente UNIX timestamp. |
Un UNIX timestamp es un valor de 32-bit que representa el número de segundos desde el 1 de enero de 1970 UTC (la época UNIX).

## Data Format


|     |     |
| --- | --- |
|     |     |

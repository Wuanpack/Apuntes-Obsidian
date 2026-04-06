JavaScript (JS) es un lenguaje de scripting popular que le permite a los desarrolladores web añadir características interactivas a sitios web que contengan HTML y CSS. Una vez los elementos HTML son creados, se les puede crear interactividad como validacion, acciones OnClick, animaciones, etc, a través de JS. 

## Variables

Las variables son contenedores que permiten almacenar datos en ellos. Como cualquier otro lenguaje, las variables en JS son similar a contenedores para guardar datos. Hay tres formas de declarar variables en JS:

* `var`: function-scoped.
* `let`: block-scoped.
* `const`: block-scoped.

## Data Types

En JS, los tipos de datos definen el tipo de valor que una variable puede mantener. Ejemplos:

* string
* number
* boolean
* null
* undefined
* object

## Functions

Una función representa un bloque de código diseñado para realizar una tarea específica. Dentro de una función, agrupas código que necesita realizar una misma tarea.

## Loops

Los loops permiten ejecutar un bloque de código múltiples veces siempre que una condición sea `True`. Los loops comunes en JS son `for`, `while` y `do...while`, los cuales son usados para repetir tareas, como ir a través de una lista de elementos.

## Request-Response Cycle

En desarrollo web, el ciclo request-response es cuando el navegador de un usuario (el cliente) envía una petición a un servidor web, y el servidor responde con la información requerida. 

## JavaScript Overview

JS es un lenguaje interpretado, es decir que el código es ejecutado directamente en el buscador sin una compilación previa. 

JS es ejecutado principalmente en el lado del cliente, lo que hace que sea fácil inspeccionar e interactuar con HTML de forma directa dentro del buscador. 

Usualmente, JS no es usado para renderizar contenido; trabaja con HTML y CSS para crear páginas web interactivas y dinámicas. Hay dos formas de integrar  JS en HTML: internamente y externamente.

## Internal JavaScript

Internal JS se refiere a incrustar el código JS directamente dentro de un documento HTML. Este método es preferible para principiantes porque les permite ver cómo el script interactúa directamente con HTML. El scrip se inserta entre etiquetas `<script>`. Estas etiquetas pueden ser colocadas dentro de la sección `<head>`, típicamente usada para scripts que necesitan ser cargados antes de que el contenido de la página se renderice, o dentro de la sección `<body>`, donde el script puede ser utilizado para interactuar con elementos que están cargados en la página web.


## External JavaScript

El External JS involucra crear y guardar código JS en un archivo separado con la extensión `.js`. Este método ayuda a los desarrolladores a mantener el documento HTML limpio y organizado.

El archivo JS externo puede ser almacenado o hosteado en el mismo servidor web que el documento HTML o almacenado en un servidor web externo como la nube.

## Verificando Internal o External JS

Cuando hacemos un pentesting a una aplicación web, es importante revisar si el sitio usa JS interno o externo. Esto puede ser fácilmente verificado al ver el código fuente de la página. En un navegador cualquiera, dentro de la página basta con dar clic derecho y presionar  "Ver código fuente de la página".

Dentro del código fuente, cualquier JS escrito directamente en la página va a aparecer entre etiquetas `<script>` sin el atributo `src`. Si ves la etiqueta `<script>` junto con el atributo `src`, indica que la página está cargando contenido externo JS en un archivo separado.

## Abusando de Funciones de Diálogo

Uno de los objetivos principales de JS es ofrecer cuadros de diálogo para interacción con usuarios y actualizar dinámicamente el contenido en páginas web. JS ofrece funciones built-in como `alert`, `prompt`, y `confirm` para facilitar esta interacción.

Estas funciones permiten a los desarrolladores a mostrar mensajes, recopilar input, y obtener confirmación del usuario. Sin embargo, si no se implementa de forma segura, los atacantes pueden explotar estas características para ejecutar atacas XSS.

### Alert

La función alert muestra un mensaje en un cuadro de diálogo con un botón "`OK`", típicamente usado para transmitir información o advertir al usuario. Por ejemplo, si queremos mostrar "`Hello THM`" al usuario, usaríamos un `alert("HelloTHM");`.

### Prompt

La función prompt muestra un cuadro de diálogo que le pide al usuario un input. Retorna el valor entregado cuando el usuario presiona "`OK`", o null si el usuario presiona "`Cancel`". Por ejemplo, para pedir al usuario que ingrese su nombre, podríamos usar `prompt("What is your name?");`.

### Confirm

La función confirm muestra un cuadro de diálogo con un mensaje y dos botones: "`OK`" y "`Cancel`". Retorna true si el usuario presiona "`OK`" y false si presiona "`Cancel`". Por ejemplo, para pedir la confirmación de un usuario, usaríamos `confirm("Are you sure?")`.

## Bypassing Control Flow Statements

El flujo de control en JS se refiere al orden en que las instrucciones y los bloques de código se ejecutan en función de ciertas condiciones. JS ofrece muchas estructuras de control de flujo, como declaraciones `if-else` y `switch` para realizar decisiones, y loops como `for`, `while` y `do-while` para repetir acciones. El uso adecuado del control de flujo asegura que el programa puede manejar varias condiciones de forma efectiva.


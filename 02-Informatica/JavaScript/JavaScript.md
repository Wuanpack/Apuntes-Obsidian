## Índice
```table-of-contents
```
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

## Exploring Minified Files

La Minimización en JS es el proceso de comprimir archivos JS removiendo todos los carácteres innecesarios, como espacios, líneas vacías, comentarios, e incluso arcortando nombre de variables. Esto ayuda a reducir el tamaño del archivo y mejora el tiempo de carga de las páginas web, especialmente en ambientes de producción. 

De la misma forma, la ofuscación es usada en JS para hacerlo más difícil de entender añadiendo código no deseado, renombrando variables y funciones con nombres sin importancia, e incluso insertando código dummy.

Ejemplo de un código ofuscado con una herramienta online:

Código legible:

``` Javascript
function hi() { 
	alert("Welcome to THM"); 
} 
hi();
```

Código ofuscado:

``` JavaScript
(function(_0x114713,_0x2246f2){var _0x51a830=_0x33bf,_0x4ce60b=_0x114713();while(!![]){try {var _0x51ecd3=-parseInt(_0x51a830(0x88))/(-0x1bd3+-0x9a+0x2*0xe37)*(parseInt(_0x51a830(0x94))/ (-0x15c1+-0x2*-0x3b3+0xe5d))+parseInt(_0x51a830(0x8d))/(0x961*0x1+0x2*0x4cb+0x4bd*-0x4)* (-parseInt(_0x51a830(0x97))/(-0x22b3+0x16e9+0x1*0xbce))+parseInt(_0x51a830(0x89))/ (-0x631+0x20cd+0x8dd*-0x3)*(-parseInt(_0x51a830(0x95))/(-0x8fc+0x161+0x7a1))+- parseInt(_0x51a830(0x93))/(-0x1c38+0x193+0x1aac)*(parseInt(_0x51a830(0x8e))/ (-0x1*-0x17a6+-0x167e+-0x3*0x60))+-parseInt(_0x51a830(0x91))/(-0x2*-0x1362+-0x4a8*0x5+-0xf73)* (parseInt(_0x51a830(0x8b))/(-0xb31*0x2+0x493*0x5+0x1*-0x73))+parseInt(_0x51a830(0x8f))/ (-0x257a+-0x1752+0x3cd7)+parseInt(_0x51a830(0x90))/(-0x2244+-0x15f9+0x3849);if(_0x51ecd3 ===_0x2246f2)break;else _0x4ce60b['push'](_0x4ce60b['shift']());}catch(_0x38d15c) {_0x4ce60b['push'](_0x4ce60b['shift']());}}}(_0x11ed,-0x17d11*-0x1+0x2*0x2e27+0x100f*0x17)); function hi(){var _0x48257e=_0x33bf,_0xab1127={'xMVHQ':function(_0x4eefa0,_0x4e5f74) {return _0x4eefa0(_0x4e5f74);},'FvtWc':_0x48257e(0x96)+_0x48257e(0x92)};_0xab1127[_0x48257e(0x8c) ](alert,_0xab1127[_0x48257e(0x8a)]);}function _0x33bf(_0xb07259,_0x5949fe){var _0x3a386b =_0x11ed();return _0x33bf=function(_0x4348ee,_0x1bbf73){_0x4348ee=_0x4348ee-(0x11f7+- 0x1*0x680+-0x3a5*0x3);var _0x423ccd=_0x3a386b[_0x4348ee];return _0x423ccd;},_0x33bf (_0xb07259,_0x5949fe);}function _0x11ed(){var _0x4c8fa8=['7407EbJESQ','\x20THM', '2700698TTmqXC','10ILFtfZ','190500QONgph','Welcome\x20to', '4492QOmepo','21623eEAyaP','65XMlsxw','FvtWc','2410qfnGAy','xMVHQ','321PfYXZg', '8XBaIAe','1946483GviJfa','15167592PYYhTN'];_0x11ed=function(){return _0x4c8fa8;};return _0x11ed();}hi();
```

## Desofuscando el Código

También podemos desofuscar un código ofuscado usando una herramienta online, por ejemplo con [https://obf-io.deobfuscate.io/](https://obf-io.deobfuscate.io/), donde se inserta el código para desofuscar y se presiona el boton "Deobfuscate".


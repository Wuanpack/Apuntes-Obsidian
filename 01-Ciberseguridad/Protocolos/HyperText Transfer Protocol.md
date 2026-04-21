Los mensajes HTTP son paquetes de información intercambiada entre el usuario (el cliente) y el servidor web. Estos mensajes son importantes para entender como las aplicaciones web trabajan porque muestran como las peticiones de usuarios y las respuestas de los servidores son comunicados.

Hay dos tipos de mensajes HTTP:

* HTTP Requests: Enviado por el usuario para disparar acciones en la aplicación web.
* HTTP Responses: Enviado por el servidor en respuesta de la petición del usuario

![[Pasted image 20260406050040.png]]

Cada mensaje sigue un formato específico que ayuda tanto al usuario como al servidor a comunicarse de forma fluida.

### Start Line

La línea de comienzo es como la introducción del mensaje. Dice que tipo de mensaje está siendo enviado, si es una petición desde el usuario o una respuesta desde el servidor. Esta línea también da detalles importante sobre como debería manejarse el mensaje.

### Headers

Los encabezados están compuestos por pares clave-valor que ofrecen información extra del mensaje HTTP. Dan instrucciones tanto para el cliente como para el servidor sobre el manejo de la petición o la respuesta. Estos headers cubren todo tipo de cosas, como seguridad, tipos de contenido, y más.

### Empty Line

La línea vacía es un pequeño divisor que separa el header del body. Es esencial porque muestra donde el header termina y donde el contenido real del mensaje comienza. Sin esta línea vacía, el mensaje puede verse enredado, y el cliente o el servidor pueden malinterpretarlo, causando errores.

### Body

El body es donde la información real es almacenada. En una petición, el body puede incluir información que el usuario quiere enviar al servidor (como un formulario). En una respuesta, es donde el servidor pone el contenido que el usuario ha requerido (como una página web o información de una API).

## HTTP Request: Request Line and Methods

![[Pasted image 20260406050711.png]]


### Request Line

La request line (o línea inicial) es la primera parte de una peticion HTTP que le dice al servidor con qué tipo de petición está lidiando. Tiene tres partes principales:

* El método HTTP.
* El URL path.
* La versión HTTP.

### HTTP Methods

Los métodos HTTP le dicen al servidor qué acción quiere realizar el usuario en el recurso identificado por el URL path. A continuación se listan algunos de los métodos más comunes y sus posibles problemas de seguridad:

#### GET

Utilizado para obtener datos de un servidor sin hacer ningún cambio. Asegúrate de exponer sólo la información que el usuario tiene permitido ver. Evita poner información sensible como tokens o contraseñas en las peticiones GET, ya que se pueden mostrar en texto plano.

#### POST

Envía datos al servidor, usualmente para crear o actualizar algo. Siempre valida y limpia el input para evitar ataques como inyección por SQL o XSS.

#### PUT

Reemplaza o actualiza algo en el servidor. Asegúrate de que el usuario está autorizado a hacer cambios antes de aceptar la petición.

#### DELETE

Elimina algo del servidor. Al igual que con PUT, asegúrate que sólo los usuarios autorizados pueden eliminar recursos.

#### PATCH

Actualiza parte de un recurso. Es útil para realizar cambios pequeños sin reemplazas todo, pero siempre valida los datos para evitar inconsistencias.

#### HEAD

Trabaja como el GET pero sólo recupera headers, no el contenido entero. Es útil para revisar metadata sin descargar la respuesta completa.

#### OPTIONS

Te dice qué métodos están disponibles para un recurso específico, ayudar a clientes a entender qué pueden hacer con el servidor.

#### TRACE

Similar a OPTIONS, muestra los métodos que están permitidos, a menudo para debugging. Muchos servidores tienen deshabilitada esta opción por razones de seguridad.

#### CONNECT

Usado para crear una conexión segura, como HTTPS. No es común, pero es crítico para comunicación encriptada.

Cada uno de estos métodos tiene su propio conjunto de reglas de seguridad. Por ejemplo, las peticiones PATCH deberían ser validadas para evitar inconsistencias, y OPTIONS y TRACE deberían ser desactivadas si no se necesitan para evitar posibles riesgos de seguridad.

### URL Path

La URL path le dice al servidor dónde encontrar el recurso que está solicitando el usuario. Por ejemplo, en la URL `https://tryhackme.com/api/users/123`, el path `/api/users/123` identifica a un usuario específico.

Los atacantes a menudo intentan manipular el path URL para explotar vulnerabilidades, así que es crucial: 

* Validar la URL path para prevenir accesos no autorizados.
* Sanitizar el path para evitar ataques por inyección.
* Proteger información sensible mediante la realización de evaluaciones de privacidad y riesgos.

### HTTP Version

La versión HTTP muestra la versión del protocolo usado para la comunicación entre el cliente y el servidor. Aquí tienes un breve resumen de los más comunes:

* HTTP/0.9 (1991): La primera versión, solo soportaba peticiones GET.
* HTTP/1.0 (1996): Añadió headers y un mejor soporte para diferente tipos de contenidos, mejorando el almacenamiento en caché.
* HTTP/1.1 (1997): Trajo conexiones persistentes, codificación de transferencia por fragmentos y mejor almacenamiento en caché. Todavía se usa ampliamente hoy en día.
* HTTP/2 (2015): Introdujo características como multiplexación, compresión de encabezados y priorización para un rendimiento más rápido.
* HTTP/3 (2022): Construido en HTTP/2, pero usa un nuevo protocolo (QUIC) para conexiones más rápidas y más seguras.

A pesar de que HTTP/2 y HTTP/3 ofrecen mejores velocidades y seguridad, muchos sistemas aún usan HTTP/1.1 porque está bien soportado y trabaja con la mayoría de setups existentes.

Sin embargo, mejorar a HTTP/2 o HTTP/3 puede incrementar significativamente el rendimiento y la seguridad a medida que más sistemas los adoptan.


## HTTP Request: Headers and Body

### Request Headers

Los Request Headers permiten información extra para ser transmitida al servidor web sobre la petición. Algunos headers comunes son los que se muestran a continuación:


| Request Header | Example                                                                        | Description                                                                                                       |
| -------------- | ------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------- |
| Host           | Host: tryhackme.com                                                            | Especifica el nombre del servidor web que está siendo pedido.                                                     |
| User-Agent     | User-Agent: Mozilla/5.0                                                        | Comparte información sobre el navegador web desde el que viene la petición.                                       |
| Referer        | Referer: https://google.com/                                                   | Indica la URL desde donde se realiza la petición.                                                                 |
| Cookie         | Cookie: user_type=student; room=introtowebapplication; room_status=in_progress | La información que el servidor web solicitó previamente al navegador web que almacenara se guarda en las cookies. |
| Content-Type   | Content-Type: application/json                                                 | Describe qué tipo o formato de información está en la petición.                                                   |


### Request Body

En las peticiones HTTP como POST o PUT, donde datos se envían al servidor web, los datos se localizan dentro del Body de la petición HTTP. El formato de los datos puede tomar muchas formas, pero algunas de las más comunes son URL Encoded, Form Data, JSON o XML.

#### URL Encoded (application/x-www-form-urlencoded)

Un formato donde los datos se estructuran en pares llave y valor donde (key=value). Múltiples pares son separados usando un símbolo (&), como `key1=value&key2=value2`. Los carácteres especiales son percent-encoded. Ejemplo:

```http
POST /profile HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 33

name=Aleksandra&age=27&country=US
```

#### Form Data (multipart/form-data)

Permite enviar varios bloques de datos separados por una cadena delimitadora. Esta cadena delimitadora es el encabezado definido en la solicitud. Este formato se puede utilizar para enviar datos binarios, como al subir archivos o imágenes a un servidor web. Ejemplo:

```http
POST /upload HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW

----WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="username"

aleksandra
----WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="profile_pic"; filename="aleksandra.jpg"
Content-Type: image/jpeg

[Binary Data Here representing the image]
----WebKitFormBoundary7MA4YWxkTrZu0gW--
```

#### JSON (application/json)

En este formato, los datos se pueden enviar usando la estructura JSON (JavaScript Object Notation). Los datos son formateados en pares nombre:valor. Múltiples pares son separados por comas, y contenidos dentro de paréntesis curvos {}. Ejemplo:

```http
POST /api/user HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0
Content-Type: application/json
Content-Length: 62

{
    "name": "Aleksandra",
    "age": 27,
    "country": "US"
}
```

#### XML (application/xml)

En el formato XML, los datos se estructuran dentro de etiquetas llamadas tags, que tienen una etiqueta de apertura y una de cierre. Estas etiquetas pueden anidarse unas dentro de otras. En el siguiente ejemplo, se puede ver la apertura y el cierre de las etiquetas para enviar información sobre una usuaria llamada Aleksandra. Ejemplo: 

```http
POST /api/user HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0
Content-Type: application/xml
Content-Length: 124

<user>
    <name>Aleksandra</name>
    <age>27</age>
    <country>US</country>
</user>
```

## HTTP Response: Status Line and Status Codes

Cuando interactúas con una aplicación web, el servidor devuelve una respuesta HTTP para hacerte saber si la petición fue exitosa o si algo salió mal. Estas respuestas incluyen un código de estatus y una explicación corta (llamada la Reason Phase) que da una vista general de cómo el servidor manejó tu respuesta.

### Status Line

La primera línea dentro de cualquier respuesta HTTP se llama Status Line. Te da tres piezas clave de información:

1. HTTP Version: Cuál versión de HTTP esta siendo usada.
2. Status Code: Un número de tres dígitos que muestra el resultado de la petición.
3. Reason Phrase: Un mensaje corto explicando el código de estatus en términos legibles para humanos.


### Status Codes and Reason Phrases

El código de estatus es un número que indica si la petición fue exitosa o falló, mientras que la Reason Phrase explica qué pasó. Estos códigos recaen dentro de 5 categorías principales:

* Informational Responses (100-199): Estos códigos significan que el servidor recibió parte de la petición y está esperando por el resto. Es una señal de "continúe".
* Successful Responses (200-299): Estos códigos significan que todo funcionó como esperaba. El servidor procesó la petición y envió de vuelta los datos pedidos.
* Redirection Messages (300-399): Estos códigos te dicen que el recurso que solicitaste ha sido movido a una locación diferente, usualmente ofreciendo la nueva URL.
* Client Error Responses (400-499): Estos códigos indican un problema con la petición. Quizás la URL es errónea, o te está faltando alguna información requerida, como la auteticación.
* Server Error Responses (500-599): Estos códigos significan que el servidor encontró un error mientras intentaba completar la petición. Estos son usualmente problemas del lado del servidor y no culpa del cliente.

### Common Status Codes

Aquí hay algunos de los códigos de estatus más comunes:

* 100 (Continue): El servidor recibió la primera parte de la petición y está listo para el resto.
* 200 (OK): La petición fue exitosa, y el servidor está enviando los recursos solicitados.
* 301 (Moved Permanently): El recurso que estás solicitando ha sido movido permanentemente a una URL nueva. Usa la URL nueva desde ahora.
* 404 (Not Found): El servidor no puedo encontrar el recurso en la URL dada. Verifica nuevamente que estás en la dirección correcta.
* 500 (Internal Server Error): Algo salió mal en el terminal del servidor, y no puedo procesas tu petición.

## HTTP Response: Headers and Body

### Response Headers

Cuando un servidor web responde una petición HTTP, incluye los headers de respuesta HTTP, los cuales son básicamente pares key-value. Estos headers ofrecen información importante sobre la respuesta y le dicen al cliente (usualmente el navegador) cómo manejarlo.


![[5f04259cf9bf5b57aed2c476-1741854427607.svg]]

### Required Response Headers

Algunas headers de respuesta son cruciales para asegurarse que la respuesta HTTP funciona apropiadamente. Estos proveen información esencial que tanto el cliente como el servidor necesitan procesar todo correctamente. Ejemplos:

* Date:
	* Ejemplo: `Date: Fri, 23 Aug 2024 10:43:21 GTM`
	* Este header muestra la fecha exacta y la hora de cuando la respuesta fue generada por el servidor.
* Content-Type:
	* Ejemplo: `Content-Type: text/html; charset=utf-8`
	* Le dice al cliente qué tipo de contenido está obteniendo, ya sea HTML, JSON, o alguno más. Esto incluye también el conjunto de carácteres (como UTF-8) para ayudar al navegador a mostrarlo apropiadamente.
* Server:
	* Ejemplo: Server: nginx
	* Este header muestra qué tipo de sofware de servidor está manejando la petición. Es bueno para debugging, pero también puede revelar información del servidor que puede ser útil para atacantes, por lo que muchas personas lo quitan o lo ocultan.

Además de los esenciales, hay otros headers comúnes que dan instrucciones adicionales al cliente o buscador y ayuda a controlar cómo la respuesta debería ser manejada:

* Set-Cookie:
	* Ejemplo: `Set-Cookie: sessionID=38af1337es7a8`
	* Este envía cookies desde el servidor al cliente, donde el cliente lo almacena y lo envía de vuelta en peticiones futuras. Para mantener las cosas seguras, asegúrate que las cookies están seteadas con la flag ``HttpOnly`` (para que no puedan ser accesibles por JavaScript) y la flag ``Secure`` (Para que sólo se envíen en HTTPS).
* Cache-Control:
	* Ejemplo: ``Cache-Control: max-age=600``
	* Este encabezado le indica al cliente cuánto tiempo puede almacenar en caché la respuesta antes de volver a consultar con el servidor. También puede evitar que se almacene en caché información confidencial si es necesario (usando `no-cache`).
* Location:
	* Ejemplo: `Location: /index.html`
	* Este es usado en respuestas de redirección (3xx). Le dice al cliente donde ir si el recurso ha sido movido. Si los usuarios pueden modificar este header durante las peticiones, tenga cuidado de validarlo y sanitizarlo, de lo contrario, podría terminar con vulnerabilidades open redirect, donde los atacantes pueden redireccionar usuarios a sitios dañinos.

### Response Body

El responde body HTTP es donde los datos viven, cosas como HTML, JSON, imágenes, etc., que el servidor envía de vuelta al cliente. Para prevenir ataques de inyección como Cross-Site Scripting (XSS), siempre desinfecte y elimine cualquier dato (especialmente el contenido generado por el usuario) antes de incluirlo en la respuesta.

## Security Headers

Los encabezados de seguridad HTTP ayudan a mejorar la seguridad general de la aplicación web ofreciendo mitigaciones ante ataques como XSS, clickjacking, y otros. Puedes usar sitios como [https://securityheaders.io/](https://securityheaders.io/) para analizar los headers de seguridad de cualquier sitio.

### Content-Security-Policy (CSP)

Un encabezado CSP es una capa adicional de seguridad que puede ayudar a mitigar contra ataques comunes como XS. Código malicioso puede ser hosted en un sitio web separado o dominio e inyectado a sitios web vulnerables. Un CSP provee una manera para administradores para decir qué dominios o fuentes son consideradas seguras y provee una capa de mitigación para dichos ataques.

Dentro del header en sí, podrías ver propiedades como `default-src` o `script-src` definidas y muchas más. Cada una de estas dan una opción al administrador de definir varios niveles de granularidad, que dominios están permitidos y qué tipo de contenidos. El uso de "self" es una palabra clave especial que refleja el mismo dominio en el que está alojado el sitio web.

Ejemplo de headerCSP: 

`Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.tryhackme.com; style-src 'self'`

Vemos el uso de:

* default-src
	* Que especifica la política predeterminada de self, lo que significa solo el sitio web actual.
* script-src
	* Que especifica la política sobre dónde se pueden cargar los scripts, que es desde la propia plataforma junto con los scripts alojados en ``https://cdn.tryhackme.com``
* style-src
	* Que especifica la política sobre dónde se pueden cargar las hojas de estilo CSS del sitio web actual (self).

### Strict-Transport-Security (HSTS)

Los encabezados HSTS aseguan que los navegadores web siempre se van a conectar sobre HTTPS. Ejemplo: 

`Strict-Transport-Security: max-age=63072000; includeSubDomains; preload`

* max-age: 
	* Esta es el tiempo de expiración en segundos para esta configuración.
* includeSubDomains:
	* Una configuración opcional que instruye a navegadores para aplicar esta configuración a todos los subdominios.
* preload:
	* Esta configuración opcional permite a los sitios web a ser incluidos en listas de pre carga.
	* Los buscadores usan listas de precarga para forzar HSTS antes de siquiera tener su primera visita al sitio web.

### X-Content-Type-Options

El header X-Content-Type-Options puede ser usado para instruir a buscadores de no adivinar el tipo MIME de un recurso sino que usando el Content-Type header. Ejemplo:

`X-Content-Type-Options: nosniff`

* nosniff
	* Esta directiva indica al navegador que no intente detectar ni adivinar el tipo MIME.

### Referrer-Policy

Este encabezado controla la cantidad de información que se envía al servidor web de destino cuando un usuario es redirigido desde el servidor web de origen, por ejemplo, al hacer clic en un hipervínculo. El encabezado permite al administrador web controlar qué información se comparte. A continuación, se muestran algunos ejemplos de Referrer-Policy:

* `Referrer-Policy: no-referrer`
	* Desactiva por completo cualquier información siendo enviada sobre el remitente.
* `Referrer-Policy: same-origin`
	* Esta política solo va a enviar información del remitente cuando la destinación es parte del mismo origen. Esto resulta útil cuando se desea que se transmita información de referencia cuando los hipervínculos se encuentran dentro del mismo sitio web, pero no fuera de él, hacia sitios web externos.
* `Referrer-Policy: strict-origin`
	* Esta política solo envía el referente como origen cuando el protocolo permanece igual. Por lo tanto, se envía un referente cuando una conexión HTTPS se dirige a otra conexión HTTPS.
* `Referrer-Policy: strict-origin-when-cross-origin`
	* Esto es similar a strict-origin, excepto para las solicitudes del mismo origen, donde envía la ruta URL completa en el encabezado de origen.


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

![[Pasted image 20260406050711.png]]

## Request Line and Methods

![[Pasted image 20260406050711.png]]


### Request Line

La request line (o línea inicial) es la primera parte de una peticion HTTP que le dice al servidor con qué tipo de petición está lidiando. Tiene tres partes principales:

* El método HTTP.
* El URL path.
* La versión HTTP.

### HTTP Methods

Los métodos HTTP le dicen al servidor qué acción quiere realizar el usuario en el recurso identificado por el URL path. A continuación se listan algunos de los métodos más comunes y sus posibles problemas de seguridad:

#### GET

Utilizado
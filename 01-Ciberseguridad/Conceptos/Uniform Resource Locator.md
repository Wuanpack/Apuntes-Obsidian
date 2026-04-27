## Índice
```table-of-contents
```

Un Uniform Resource Locator (URL) es una dirección web que te permite acceder a todo tipo de contenido online, ya sea una página web, una foto, u otro tipo de medio. Guía a tu buscador web al lugar correcto en el Internet.

### Anatomía de una URL

![[Pasted image 20260406013311.png]]

## Scheme

El scheme es el protocolo usado para acceder al sitio web. Los más comunes son HTTP (HyperText Transfer Protocol) y HTTPS (Hypertext Transfer Protocol Secure). HTTPS es más seguro porque encripta la conexión, lo cual es la razón de por qué los buscadores y expertos en ciberseguridad lo recomiendan. 

## User

Algunas URLs pueden incluir los detalles de inicio de sesión de un usuario (por lo general el nombre de usuario) para sitios que requieren autenticación. Esto pasa mayormente en URLs que necesitan credenciales para acceder a ciertos recursos. 

Sin embargo, esto es raro hoy en día porque poner los detalles de inicio de sesión en la URL no es muy seguro, ya que puede exponer información sensible, lo cual es un riesgo de seguridad.

## Host/Domain

El host o domain es la parte más importante de la URL porque te dice a qué sitio web estás accediendo. Todos los nombres de dominio tienen que ser únicos y registrados a través de registros de dominios.

Desde un punto de vista de la seguridad, busca nombres de dominios que aparentan ser casi como los reales pero con pequeñas diferencias (este es llamado typosquatting). Estos dominios falsos son usados con frecuencia en ataques de phishing para engañar a las personas a dar información personal.

## Port

El número del puerto ayuda a direccionar a tu buscador al servicio correcto del servidor web. Es como decirle al servidor que puerta usar para comunicación. Los números de puertos van desde el 1 al 65.535, pero los más comunes son el 80 para HTTP y el 443 para HTTPS.

## Path

El path apunta al archivo específico o página del servidor que estás intentando acceder. Es como un roadmap que le muestra al buscador donde ir. Los sitios web necesitan asegurar estos paths para asegurarse que sólo los usuarios autorizados puedan acceder a recursos sensibles.

## Query String

La query string es la parte de la URL que empieza con un signo de pregunta (?). Por lo general es usado para cosas como buscar términos o inputs de formularios. Ya que los usuarios pueden modificar estas query strings, es importante manejarlas con seguridad para prevenir ataques como inyecciones, donde código malicioso podría ser añadido.

## Fragment

El fragment empieza con el símbolo hash (#) y ayuda a apuntar a una sección específica de la página web, como saltar directamente a un título o tabla en particular. Es importante revisar y limpiar cualquier información aquí para evitar problemas como ataques de inyección.


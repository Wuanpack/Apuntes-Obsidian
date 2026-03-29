---
tags:
  - criptografia
  - seguridad
---
## ¿Qué es?

Una función criptográfica hash, usualmente conocida como hash, es un algoritmo matemático que transforma cualquier bloque arbitrario de datos en una nueva serie de carácteres con una longitud fija. Independientemente de la longitud de los datos de entrada, el valor hash de salida tendrá siempre la misma longitud.

## Función hash

Las funciones hash son diferentes de la encriptación. No hay llave, y está hecho para ser imposible (o computacionalmente inviable) ir desde el output de vuelta el input.

Una función hash toma una entrada de información de cualquier tamaño y sumariza o digiere esta data. El output tiene un tamaño fijo. Es difícil predecir el output para cualquier input y vice versa. Los buenos algoritmos de hashing serán relativamente rápidos de computar y prohibitivamente lentos de revertir. 

La salida de una función hash suele ser de bytes sin procesar, que luego se codifican. Las codificaciones más comunes son base64 o hexadecimal. md5sum, sha1sum, sha256sum y sha512sum generan sus resultados en formato hexadecimal. Recuerda que el formato hexadecimal imprime cada byte sin procesar como dos dígitos hexadecimales.

## Importancia del Hashing

El hashing juega un papel vital en el uso diario de Internet. Como otras funciones criptográficas, el hashing se mantiene escondido del usuario. El hashing ayuda a proteger la [[Seguridad de la Información#Integridad|integridad]] de la información y asegurar la [[Seguridad de la Información#Confidencialidad|confidencialidad]] de las contraseñas.

Consideremos esto. Cuando iniciamos sesión en una página web, el servidor usa el hashing para verificar la contraseña. De hecho, como buenas prácticas de seguridad, un servidor no guarda tu contraseña; de hecho guarda el valor hash de la contraseña. Cuando queremos iniciar sesión, va a calcular el valor hash de la contraseña que enviamos con el valor hash guardado. Similarmente, cuando iniciamos sesión en la computadora, el hashing juega un rol en verificar tu contraseña. 

## ¿Qué es la Colisión Hash?

Una colisión hash es cuando dos inputs diferentes dan como resultado el mismo output. Las funciones hash están diseñadas para evitar colisiones de la mejor forma posible. Además, las funciones hash están diseñadas para prevenir que un atacante sea capaz de crear una colisión de forma intencional. Sin embargo, debido a que el número de inputs es prácticamente ilimitado y el número de outputs posibles es limitado, esto lleva a un efecto pigeonhole.

El efecto pigeonhole dicta que el número de items (pigeons) es más alto que el número de contenedores (pigeonholes); algunos contenedores deben guardar más de un ítem. En otras palabras, en este contexto, hay un número fijo para diferentes valores de salida para la función hash, pero podemos tener cualquier tamaño de entrada.

El MD5 y SHA1 han sido atacados y ahora se consideran inseguros debido a la habilidad de ingeniar colisiones hash. Sin embargo, ningún ataque a dado una colisión en ambos algoritmos simultáneamente.
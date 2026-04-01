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


## Usando Hashing para Almacenar Contraseñas

Es evidente que guardar contraseñas en texto plano, con sistemas de encriptación obsoletos o usando algoritmos de hashing inseguros, son prácticas de seguridad terribles. Bastantes filtraciones de datos han dejado contraseñas en texto plano. 

Probablemente estés familiar con la lista de contraseñas "rockyou.txt" en Kali Linux, entre otras distribuciones de seguridad ofensiva. Esta lista de contraseñas viene de RockYou, una compañía que desarrolló aplicaciones de social media y widgets. Guardaron las contraseñas en texto plano, y la compañía tuvo una filtración de datos. El texto contiene más de 14 millones de contraseñas. Este listado se puede encontrar en el directorio `/usr/share/wordlists`

Aquí es cuando entra el hashing. En vez de guardar la contraseña, se guarda el valor del hash usando una función hashing segura.

El problema viene cuando dos usuarios usan la misma contraseña, ya que la función hash siempre retorna el mismo output cuando se ingresa el mismo input, por lo que se guardaría el mismo valor hash de las contraseñas de ambos usuarios. 

Lo anterior significa que, si alguien rompe ese hash, podría ganar acceso a más de una cuenta. Esto también significa que alguien puede crear una Tabla Arcoíris para romper hashes.

Una Rainbow Table es una tabla de búsqueda que relaciona hashes con textos planos, lo que permite averiguar rápidamente la contraseña de un usuario a partir de su hash. Esta tabla ahorra espacio en el disco duro en lugar de descifrar un hash, pero su creación requiere tiempo. 

Sitios como CrackStation y Hashes.com internamente usa tablas arcoíris masivas para proveer un descifrado ráido de contraseñas para hashes no salteadas. Hacer una búsqueda en una lista ordenada de hashes es más rápido que intentar romper el hash.

## Protegiendo Contra Rainbow Tables

Para protegerse de tablas arcoíris, añadimos salt a las contraseñas. El salt es un valor generado aleatoriamente almacenado en la base de datos y debería ser único para cada usuario. en teoría, puedes usar el mismo salt para todos los usuarios, pero las contraseñas duplicadas aún tendrían el mismo hash y las tablas arcoíris aún se podrían crear para contraseñas con ese salt.

El salt se añade al inicio o al final de la contraseña antes de ser hasheado, esto significa que todos los usuarios van a tener diferentes hashes de contraseñas incluso si tienen la misma contraseña. Funciones hash como Bcrypt y Scrypt manejan esto de forma automática. Salts no necesitan estar mantenerse privadas.

## Reconociendo Hashes de Contraseñas

Desde la perspectiva de la ciberseguridad defensiva, hemos cubierto el cómo se guardan las contraseñas de forma segura para sistemas de autenticación. Abordemos esto desde la perspectiva de la seguridad ofensiva; si empezamos con un hash, como podemos reconocer su tipo, eventualmente romperlo, y recuperar la contraseña original?

Herramientas de reconocimiento de hash automatizadas como hashID existen pero no son fiables para muchos formatos. Para hashes que tienen prefijos, las herramientas son fiables. Utilice una combinación adecuada de contexto y herramientas. Si encuentra el hash en la base de datos de una aplicación web, es más probable que sea MD5 que NTLM (NT LAN Manager). Las herramientas de reconocimiento automático de hashes a menudo confunden estos tipos de hash, lo que subraya la importancia de aprender por cuenta propia.

### Contraseñas de Linux

En Linux, los hashes de contraseñas se guardan en `etc/shadow`, donde normalmente solo puede leerlo el root. Antes se guardaban en `/etc/passwd`, donde era legible para todos.

El archivo shadow contienen la información de la contraseña. Cada línea contiene 9 campos, separados por colons (:). Los dos primeros campos son el nombre del login y la contraseña encriptada. Más información sobre los demás campos se pueden encontrar ejecutando `man 5 shadow` en un sistema Linux.

El campo de la contraseña encriptada contiene la frase hasheada con 4 componentes: el prefijo (algorithm id), opciones (parámetros), salt y el hash.Se guarda en el formato `$prefix$options$salt$hash`. El prefijo hace fácil de reconocer contraseñas estilo Linux y Unix; especifica el algoritmo de hashing usado para generar el hash.

### MS Windows Passwords

Las contraseñas de MS Windows son hasheadas usando NTLM, una variante de MD4. Se ven idénticas a los hashes MD4 y MD5, así que es muy importante usar el contexto para determinar el tipo de hash.

En MS Windows, las contraseñas se guardan en SAM (Security Accounts Manager). MS Windows intenta evitar que los usuarios comunes los extraigan, pero existen herramientas como Mimikatz para eludir la seguridad de MS Windows. Cabe destacar que los hashes que se encuentran allí se dividen en hashes NT y hashes LM.

Un buen lugar para encontrar más formatos de hash y prefijos de contraseñas es la página Hashcat Example Hashes. Para otros tipos de hashes, normalmente necesitarías verificar la longitud, la codificación o incluso investigar la aplicación que la generó. Nunca subestimes el poder de la investigación.


## Password Cracking

Ya mencionamos las tablas arcoíris como método para romper hashes que no usan salt, pero que pasa si hay salt involucrado?

No puedes "desencriptar" hashes de contraseñas. No están encriptadas. Tienes que descifrar los hashes aplicando hash a muchas entradas diferentes (como rockyou.txt, que cubre muchas contraseñas posibles), potencialmente añadiendo el salt si hay alguno y comparándolo con el hash objetivo. Una vez que coincide, sabes qué contraseña era. Herramientas como Hashcat y [[John The Ripper]] son comúnmente usadas para estos propósitos.

### Descifrando Contraseñas con GPUs

Las GPUs modernas (Graphic Processing Units) tienen miles de núcleos. Se especializan en el procesamiento de imágenes digitales y aceleración de gráficos por computadora. Aunque no pueden hacer el mismo tipo de trabajo que una CPU, son muy buenos en algunos cálculos matemáticos que involucran funciones hash. Puedes usar la tarjeta gráfica para descifrar muchos tipos de hashes rápidamente. Algunos algoritmos de hashin, como Bcrypt, están diseñados para que el hashing en una GPU no provea ninguna mejora de velocidad que si se usara una CPU; esto ayuda a resistir el cracking.

### Descifrando en VMs

Vale la pena mencionar que en las Máquinas Virtuales normalmente no se tiene acceso a la tarjeta gráfica del host. Dependiendo del software de virtualización que uses, puedes configurarlo, pero es engorroso. Además, se produce una degradación del rendimiento al usar la CPU desde un sistema operativo virtualizado, y cuando el objetivo es descifrar un hash, se necesita cada ciclo de CPU adicional.

Si quieres ejecutar Hashcat (se abre en una pestaña nueva), lo mejor es hacerlo en tu equipo para aprovechar al máximo tu GPU, si está disponible. Si prefieres Windows, estás de suerte; hay versiones para Windows disponibles en el sitio web y puedes ejecutarlo desde PowerShell. Puedes hacer que Hashcat funcione con OpenCL en una máquina virtual, pero es probable que la velocidad sea inferior a la de ejecutarlo en tu equipo.

[[John The Ripper]] utiliza la CPU por defecto y funciona en una máquina virtual sin necesidad de configuración adicional, aunque es posible que obtenga mejores velocidades ejecutándolo en el sistema operativo anfitrión para evitar la sobrecarga de la virtualización y aprovechar al máximo los núcleos e hilos de su CPU.

## Hashing for Integrity Checking

El Hashing se puede usar para verificar que los archivos no hayan sido cambiados. Si pones los mismos datos, siempre obtienes los mismos datos de salida. Incluso si un solo bit cambia, el hash cambiará significativamente. Esto significa que puedes usarlo para chequear que os archivos no hayan sido modificados o para asegurar que los archivos que descargaste son idénticos a los del servidor web. También se puede usar el hashing para encontrar archivos duplicados; si dos documentos tienen el mismo hash, entonces son el mismo documento. Esto es muy conveniente para encontrar y eliminar archivos duplicados.

### HMACs

HMAC (Keyed-Hash Message Authentication Code) es un tipo de código de autenticación de mensajes (MAC) que utiliza una función hash criptográfica en combinación con una clave secreta para verificar la autenticidad e [[Seguridad de la Información#Integridad|integridad]] de los datos.

Un HMAC puede ser usado para asegurar que la persona que haya creado el HMAC es quien dice ser. Además, prueba que el mensaje no fue modificado o corrompido. Esto se logra a través del uso de una clave secreta para provar la autenticidad y un algoritmo de hash para producir un hash y probar la [[Seguridad de la Información#Integridad|integridad]].

Los siguientes pasos dan una idea de cómo HMAC funciona:

1. La clave secreta se rellena hasta alcanzar el tamaño de bloque de la función hash.
2. La clave rellena se combina mediante XOR con una constante (normalmente un bloque de ceros o unos).
3. El mensaje se cifra utilizando la función hash con la clave XOR.
4. El resultado del paso 3 se vuelve a aplicar la misma función hash, pero utilizando la clave rellena y combinada mediante XOR con otra constante.
5. El resultado final es el valor HMAC, normalmente una cadena de tamaño fijo.

Técnicamente hablando, la función HMAC se calcula mediante la siguiente expresión: 

*HMAC(K,M) = H((K⊕opad)||H((K⊕ipad)||M))*

Nótese que M y K representan el mensaje y la clave, respectivamente.


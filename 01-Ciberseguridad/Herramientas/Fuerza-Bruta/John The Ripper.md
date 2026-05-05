---
tags:
  - criptografia
  - herramientas
  - herramientas/descrifrado
  - vectores-ataque
  - herramientas/fuerza-bruta
---
## Índice
```table-of-contents
```
## ¿Qué es?

John the Ripper es una herramienta de descifrado de hashes muy conocida, apreciada y versátil. Combina una velocidad de descifrado rápida con una extraordinaria gama de tipos de hash compatibles.

Si tienes la versión cifrada de una contraseña, por ejemplo, y conoces el algoritmo de cifrado, puedes usarlo para cifrar una gran cantidad de palabras, lo que se conoce como diccionario. Luego, puedes comparar estos hashes con el que intentas descifrar para ver si coinciden. Si coinciden, sabes qué palabra corresponde a ese hash: ¡lo has descifrado! Este proceso se llama ataque de diccionario, y John the Ripper, o John como se le suele llamar, es una herramienta para realizar ataques de fuerza bruta rápido en varios tipos de hash.

La versión más popular de John The Ripper es Jumbo John.

## Descifrando Hashes Básicos

### John Basic Sintax

```bash
john [options] [file path]
```

`john`: invoca el programa John The Ripper
`options`: Especifica las opciones a usar
`[file path]`: El archivo que contiene el hash que queremos descrifrar; si está en el mismo path, entonces basta con el nombre del archivo.

### Automatic Cracking

John tiene características built-in para detectar que tipo de hash se le estpa dando y así seleccionar las reglas y formatos apropiadas para descifrarlo por ti; esta no siempre es la mejor idea ya que puede ser poco fiable, pero si no puedes identificar el tipo de hash con el que estás trabajando y quieres intentar descifrarlo, puede ser una buena opción, para ello sigue la siguiente sintáxis:

```bash
john --wordlist=[path to wordlist] [path to file]
```

* `--wordlist=`: Especifica usando el modo wordlist, leyendo desde el archivo que provees en el path especificado.
* `[path to wordlist]`: El path al listado de palabras que estas usando.

Ejemplo de uso:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt
```

### Identificando Hashes

A veces, John no se lleva bien con el reconocimiento y la carga automática de hashes. Pero podemos usar otras herramientas para identificar el hash y luego poner el formato específico en John. Hay múltiples formas de hacer esto, como usar un identificador de hash online como hashes.com. También existen herramientas como hash-identifier, una herramienta Python muy fácil de usar y mostrando los diferentes tipos de hashes que probablemente corresponde al hash que ingresaste.

Para usar hash-identifier, puedes usar wget o curl para descargar el archivo Python `hash-id.py` de su página Gitlab. Luego, ejecutarlo con `python3 hash-id.py` e ingresar el hash que estamos intentando identificar.

### Especificando el Formato de Descifrado

Una vez identificamos el hash con el que estamos lidiando, podemos decirle a John que lo use mientras descifra el hash usando la siguiente sintáxis:

```bash
john --format=[format] --wordlist=[path to wordlist] [path to file]
```

* `--format=`: Esta es la flag que le dice a John que le estamos pasando un hash con un formato específico y que lo use para descifrarlo.
* `[format]`: El formato en el que está el hash.

Ejemplo de uso:

```bash
john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt
```

Nota en formatos:

Cuando le decimos a John que use formatos, si estamos lidiando con un tipo de hash estándar, como md5, tenemos que agregar el prefijo `raw-` para decirle a John que solo estamos lidiando con el tipo de hash estándar, aunque esto no siempre aplica. Para chequear si necesitas añadir o no el prefijo, puedes listar todos los formatos de John usando `john --list=formats` y, chequear manualmente, o usar grep para tu tipo de hash usando algo como `john --list=formats | grep -iF "md5"`.

## Cracking Windows Authentication Hashes

Ahora entendimos la sintáxis básica de John The Ripper, ahora vamos con algo más complicado. Los hashes de autenticación son las versiones hash de contraseñas almacenadas por sistemas operativos; algunas veces es posible crackearlas usando métodos de fuerza bruta. 

Para manipular estos hashes, usualmente ya debes ser un usuario con privilegios.

### NTHash / NTLM

NTHash es el formato hash moderno de las máquinas con sistema operativo Windows usado para almacenar usuarios y contraseñas de servicios. También se le refiere comúnmente como NTLM, el cual hace referencia a la versión anterior del formato de Windows para hacer hash a contraseñas conocido como LM, de ahí NT/LM.

La designación NT para productor Windows originalmente significaba New Technology. Era usado para denotar productos no hechos desde el sistema operativo MS-DOS. Eventualmente, la línea "NT" se convirtió en el tipo de sistema operativo estándar para ser lanzado por Microsoft, por lo que el nombre fue olvidado, pero sigue viviendo en los nombres de algunas tecnologías de Microsoft.

En Windows, SAM (Security Account Manager) es usado para almacenar información de las cuentas de usuarios, incluyendo nombres de usuarios y contraseñas con hash. Puedes obtener hashes NTHash/NTLM volcando la base de datos SAM en una máquina Windows, usando una herramienta como Mimikatz o la base de datos de Active Directory: NTDS.dit. Puede que no necesites descifrar el hash para continuar con la escalada de privilegios, ya que a menudo puedes realizar un ataque de "pass the hash" en su lugar, pero a veces, descifrar el hash es una opción viable si existe una política de contraseñas débil.


## Cracking /etc/shadow Hashes

El archivo `/etc/shadow` es un archivo en las máquinas Linux donde se almacenan los hash de contraseñas. También guarda otra información, como la fecha del último cambio de contraseña y la información de expiración de contraseña. Contiene una entrada por lína por cada usuario o cuenta de usuario del sistema. Este archivo usualmente es sólo accesible por el usuario root, así que es necesario tener suficientes privilegios para acceder a los hashes. Sin embargo, si lo tienes, hay una chance de que seas capaz de descifrar algunos de los hashes.

### Unshadowing

John puede ser muy exigente con los formatos de datos que necesita para poder trabajar con ellos; por esta razón, para descifrar contraseñas de `/etc/shadow`, debe combinarlo con el archivo `/etc/passwd` para que John entienda los datos que se le proporcionan. Para ello, utilizamos una herramienta integrada en el conjunto de herramientas de John llamada `unshadow`. La sintaxis básica de `unshadow` es la siguiente:

```bash
unshadow [path to passwd] [path to shadow]
```

* `unshadow`: Invoca la herramienta unshadow.
* `[path to passwd]`: El archivo que contiene la copia del archivo `/etc/passwd` que tomaste desde la máquina objetivo.
* `[path to shadow]`: El archivo que contiene la copia del archivo `/etc/shadow` que tomaste desde la máquina objetivo.

Ejemplo de uso:

```bash
unshadow local_passwd local_shadow > unshadowed.txt
```

Cuando se usa `unshadow`, puedes usar los archivos `/etc/passwd` y `/etc/shadow` por completo, asumiendo que los tienes disponibles, o puedes usar una línea relevante de cada una, por ejemplo:

**FILE 1 - local_passwd**

Contiene la línea `/etc/passwd` del usuario root:

`root:x:0:0::/root:/bin/bash`

**FILE 2 - local_shadow**

Contiene la línea `/etc/shadow` del usuario root:
`root:$6$2nwjN454g.dv4HN/$m9Z/r2xVfweYVkrr.v5Ft8Ws3/YYksfNwq96UL1FX0OJjY1L6l.DS3KEVsZ9rOVLB/ldTeEL/OIhJZ4GMFMGA0:18576::::::`

### Cracking

Podemos entonces introducir la salida de `unshadow`, en nuestro ejemplo llamada `unshadowed.txt`, directamente en John. No debería ser necesario especificar un modo aquí, ya que hemos creado la entrada específicamente para John; sin embargo, en algunos casos, será necesario especificar el formato, como hemos hecho anteriormente con: `format=sha512crypt`.

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt
```


## Single Crack Mode

Hasta ahora hemos usado el modo de listas de palabras de John para hacer ataques de fuerza bruta a hashes simples y no tan simples. Pero John tiene otro modo, llamado Single Crack mode. En este modo, John utiliza únicamente la información proporcionada en el nombre de usuario para intentar descifrar posibles contraseñas de forma heurística, modificando ligeramente las letras y los números contenidos en el nombre de usuario.

### Word Mangling

La mejor forma de explicar el modo Single Crack y word mangling es a través de un ejemplo:

Considera el nombre de usuario "Markus":

Algunas contraseñas posibles serían:

* Markus1, Markus2, Markus3 (etc.).
* MArkus, MARkus, MARKus (etc.).
* Markus!, Marku$, Markus* (etc.).

Esta técnica se llama word mangling (manipulación de palabras). John está construyendo su diccionario basado en la información que se le proporciona y usa un conjunto de reglas llamadas "word mangling", el cual define como puede mutar la palabra con la que empezó para generar una lista de palabras basada en factores relevantes para el objetivo que estás intentando descifrar. Esto aprovecha la debilidad de las contraseñas, que pueden basarse en información sobre el nombre de usuario o el servicio al que se accede.

### GECOS

La implementación de John para la manipulación de palabras también ofrece compatibilidad con el campo GECOS del sistema operativo UNIX, así como con otros sistemas operativos similares a UNIX, como Linux.

GECOS significa General Electric Comprehensive Operating System. Anteriormente, examinamos las entradas de `/etc/shadow` y `/etc/passwd`. Si observa con atención, notará que los campos están separados por dos puntos (:). El quinto campo del registro de la cuenta de usuario es el campo GECOS. Almacena información general sobre el usuario, como su nombre completo, número de oficina y número de teléfono, entre otros datos. John puede usar la información almacenada en esos registros, como el nombre completo y el nombre del directorio personal, para agregarla a la lista de palabras que genera al descifrar los hashes de `/etc/shadow` con el modo Single Crack.

### Usando el modo Single Crack

Para usar el modo de descifrado único, usamos prácticamente la misma sintaxis que hemos usado hasta ahora; por ejemplo, si quisiéramos descifrar la contraseña del usuario llamado "Mike", usando el modo único, usaríamos:

```bash
john --single --format=[format] [path to file]
```

* `--single`: Esta flag le hace saber a John que queremos usar el modo de descifrado hash único.
* `--format=[format]`: Como siempre, es vital identificar el formato apropiado.

Ejemplo de uso:

```bash
john --single --format=raw-sha256 hashes.txt
```

NOTA: 

Si estás descifrando hashes en modo de descifrado individual, necesitas cambiar el formato del archivo que le proporcionas a John para que entienda qué datos usar para crear una lista de palabras. Esto se hace anteponiendo al hash el nombre de usuario al que pertenece, así que, según el ejemplo anterior, cambiaríamos el archivo hashes.txt.

**DE** `1efee03cdcb96d90ad48ccc7b8666033`

**A** `mike:1efee03cdcb96d90ad48ccc7b8666033`

## Custom Rules

### ¿Qué son?

Como vimos en el modo Single Crack, puedes tener algunas ideas sobre algunos patrones de manipulación buenos o qué patrones tus contraseñas a menudo usan que pueden ser replicadas con un patrón de manipulación particular. Las buenas noticias es que tu puedes definir tus reglas, las cuales John usará para crear contraseñas dinámicamente. La habilidad para definir dichas reglas es beneficioso cuando sabes más información sobre la estructura de la contraseña o cualquiera sea tu objetivo.

### Common Custom Rules

Muchas organizaciones van a requerir cierto nivel de complejidad de contraseñas para intentar combatir ataques por diccionario. En otras palabras, cuando se crea una cuenta nueva o cambias tu contraseña, si intentas ingresar una contraseña como `polopassword`, probablemente no funcione. La razón sería la complejidad de contraseñas forzada. Como resultado, podrías recibir un prompt diciéndote que las contraseñas deben tener al menos un carácter de cada uno como se indica:

* Lowercase letter.
* Uppercase letter.
* Number.
* Symbol.

La complejidad de contraseñas está bien. Sin embargo, podemos explotar el hecho de que la mayoría de usuario van a ser predecibles en la ubicación de estos símbolos. Para la criteria de arriba, la mayoría de usuarios usaría algo como:

`Polopassword1!`

Considera la contraseña con la letra capital primero y un número seguido por un símbolo al final. Este patrón familiar de la contraseña, añadidos y antepuestos por modificadores, es un patrón memorable que la gente usa y re-usa cuando crea contraseñas. Este patrón nos permite explotar la previsibilidad de la complejidad de las contraseñas.

### Cómo crear Custom Rules

Las Custom Rules están definidas en el archivo `john.conf`. Este archivo puede ser encontrado en `/etc/john/john.conf`.

Hay que tener en cuenta que hay un nivel masivo de control granular en estas reglas.

La primera linea:

`[List.Rules:TMHRules` se usa para definir el nombre de tu regla; esto es lo que usarás para llamar la regla custom un argumento John.

Luego usamos una coincidencia de patrones de estilo expresiones regulares para definir dónde se modificará la palabra; nuevamente, aquí solo cubriremos los modificadores principales y más comunes:

* `Az`: Toma la palabra y le añade los carácteres que definas.
* `A0`: Toma la palabra y le antepone los carácteres que definas.
* `c`: Pone en mayúscula el carácter posicionalmente.

Estas pueden ser usadas combinadas para definir dónde y qué quieres modificar en la palabra.

Finalmente, debemos definir qué carácteres deben ser añadidos, antepuestos o incluidos de otra forma. Hacemos esto añadiendo conjuntos de carácteres en brackets `[]` donde estos deberían ser usados. Estos siguen los patrones de modificación dentro de double quotes `" "`.  Aquí hay algunos ejemplos:

* `[0-9]`: Va a incluir números del 0 al 9.
* `[0]`: Va a incluir solo el número 0.
* `[A-z]`: Va a incluir letras en mayúscula y minúscula.
* `[A-Z]`: Va a incluir sólo letras en mayúscula.
* `[a-z]`: Va a incluir sólo letras en minúscula.

Poniendo todo esto junto, para generar la lista de palabras desde las reglas con las que coincidiríamos el primer ejemplo de contraseña `Polopassword1!` (asumiendo que la palabra `polopassword` estaba en nuestra wordlist), crearíamos una regla de entrada que se vería así:

`[List.Rules:PoloPassword]`
`cAz"[0-9] [!£$%@]"`

Utiliza lo siguiente:

* `c`: Capitaliza la primera letra.
* `Az`: Añade al final de la palabra.
* `[0-9]`: Un número en el rango de 0 a 9.
* `[!£$%@]`: La contraseña es seguida de uno de estos símbolos.

### Usando Custom Rules

Podemos llamar esta regla custom en un argumento de John usando la flag `--rule=PoloPassword`.

Un comando completo sería: `john --wordlist=[path to wordlist] --rule=PoloPassword [path to file]`

## Cracking Password Protected Zip Files

Podemos usar John para descrifrar la contraseña de archivos Zip protegidos por contraseña. Una vez más, utilizaremos una parte independiente del conjunto de herramientas de John para convertir el archivo Zip a un formato que John pueda entender, pero utilizaremos la sintaxis con la que ya estás familiarizado a todos los efectos.

### Zip2John

Al igual que con la herramienta `unshadow` que usamos previamente, usaremos `zip2john` para convertir el archivo Zip en formato hash para que John pueda entenderlo y, con suerte, descrifrar. el uso primario es algo como:

```bash
zip2john [options] [zip file] > [output file]
```

* `[options]`: Permite pasar opciones de suma de verificación específicas a zip2john; esto no debería ser necesario con frecuencia.
* `[zip file]`: El path al archivo Zip del cual queremos obtener el hash.
* `>`: Esto redirecciona el output desde este comando a otro archivo.
* `[output file]`: Este es el archivo que va a almacenar el output.

Ejemplo de uso:

`zip2john zipfile.zip > zip_hash.txt`

### Cracking

Entonces somos capaces de tomar el archivo de salida desde `zip2john`, en el ejemplo anterior, `zip_hash.txt`, y como hicimos con `unshadow`, ponerlo directo en John como hicimos un input especialmente para eso.

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
```


## Cracking a Password-Protected RAR Archive

Podemos usar un proceso similar al que usamos con los archivos ZIP.

### Rar2John

El uso es igual que con `zip2john`, pero en vez de esa herramienta usaremos `rar2john` para convertir el archivo RAR en un formato hash que John pueda entender, por lo tanto, la sintaxis básica sería:

```bash
rar2john [rar file] > [output file]
```


## Cracking SSH Key Passwords

Exploremos otro uso de John que aparece con cierta frecuencia en los desafíos CTF: usar John para descifrar la contraseña de la clave privada SSH de los archivos `id_rsa`. 

A no ser de que esté configurado de otra forma, puedes autenticar tu SSH login usando una contraseña. Sin embargo, puedes configurarlo para que tenga autenticación basada en claves, lo cual te permite usar tu clave privada, `id_rsa`, como clave de autenticación para iniciar sesión en una máquina remote usando SSH. Sin embargo, hacer esto usualmente requiere una contraseña para acceder a la clave privada; aquí, usaremos John para descifrar esta contraseña para permitir la autenticación con SSH usando la clave.

### SSH2John

Como el nombre sugiere, `ssh2john` convierta la clave privada `id_rsa`, el cual se usa para iniciar sesión en una sesión SSH, en un formato hash con el que John pueda trabajar. La sintáxis es como podrías esperar. Nótese que si no tienes `ssh2john` instalado, puedes usar `ssh2john.py`, localizado en `/usr/share/john/ssh2john.py`.

```bash
ssh2john [id_rsa private key file] > [output file]
```

Ejemplo de uso:

```bash
/otp/john/ssh2john.py id_rsa > id_rsa_hash.txt
```


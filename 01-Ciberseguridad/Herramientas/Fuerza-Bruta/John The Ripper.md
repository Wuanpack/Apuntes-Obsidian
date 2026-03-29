---
tags:
  - criptografia
  - herramientas
  - herramientas/descrifrado
  - vectores-ataque
  - herramientas/fuerza-bruta
---
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


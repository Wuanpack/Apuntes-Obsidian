---
tags:
  - conceptos
  - vectores-ataque
  - redes
  - seguridad
  - criptografia/criptografia-asimetrica
---
## Índice
```table-of-contents
```
## ¿Qué es?

ED22519 es el algoritmo de clave pública usado para la generación de firmas digital. Cuando intentamos una conexión y aparece esto:

```bash
sudo ssh 10.10.244.173 
The authenticity of host '10.10.244.173 (10.10.244.173)' can't be established. ED25519 key fingerprint is SHA256:lLzhZc7YzRBDchm02qTX0qsLqeeiTCJg5ipOT0E/YM8. This key is not known by any other name. Are you sure you want to continue connecting (yes/no/[fingerprint])? yes Warning: Permanently added '10.10.244.173' (ED25519) to the list of known hosts.
```

El cliente de SSH no reconoce la clave y pregunta por confirmación para saber si queremos continuar con la conexión de todas formas.

Esta advertencia se debe a la probabilidad de un ataque [[Man in The Middle]]; un servidor malicioso podría haber interceptado la conexión y haber respondido pretendiendo ser el servidor objetivo.

Una vez la respuesta es "yes", el cliente SSH guardará esta firma de clave pública para este host. En el futuro, se conectará de forma silenciosa a no ser de que este host responda con una clave pública diferente.

### Autenticando el Cliente

En muchos casos, los usuarios SSH se autentican usando nombres de usuarios y contraseñas, como se haría en el inicio de sesión de una máquina física. Sin embargo, considerando los problemas heredados con las contraseñas, esto no cae dentro de las mejores prácticas de seguridad.

En algún punto, uno seguramente va a topar con una máquina con SSH configurado con una clave de autenticación en cambio. Esta autenticación usa claves privadas y públicas para probar que el cliente es válido y un usuario autorizado en el servidor. Por defecto, las claves SSH son RSA. Se puede escoger el argoritmo para generar y añadir una frase para encriptar la clave SSH.

`ssh-keygen` es el programa generalmente usado para generar pares de claves. Soporta varios algoritmos, como:

* DSA (Digital Signature Algorithm): Es un algoritmo de criptografía de clave pública especialmente diseñado para firmas digitales.
* ECDSA (Elliptic Curve Digital Signature Algorithm): Es una variante del DSA que usa criptografía de curva elíptica para proveer tamaños de claves más pequeños por la misma equivalencia en seguridad.
* ECDSA-SK (ECDSA with Security Key): Es una extensión dek ECDSA, Incorpora seguridad de claves basadas en hardware para una mejor protección de claves privadas.
* Ed25519: Es un sistema de firma de clave pública uando EdDSA (Edwards-curve Digital Signature Algorithm) con Curve25519
* Ed25519-SK (Ed25519 with Security Key): Es una variante del Ed25519. Similar al ECDSA-SK, usa claves de seguridad basadas en hardware para mejorar la protección de claves privadas.
* [[Criptografía Asimétrica#RSA|RSA]]

Ejemplo de implementación:


```bash
ssh-keygen -t ed25519 
Generating public/private ed25519 key pair.  
Enter file in which to save the key (/home/wuanpack/.ssh/id_ed25519):
Enter passphrase for "/home/wuanpack/.ssh/id_ed25519" (empty for no passphrase):    
Enter same passphrase again:    
Your identification has been saved in /home/wuanpack/.ssh/id_ed25519  
Your public key has been saved in /home/wuanpack/.ssh/id_ed25519.pub  
The key fingerprint is:  
SHA256:fNp3AxZ0qsc3ApVCxkbyNkxvKTdC/4qjteSaxKi/jCQ wuanpack@fedora  
The key's randomart image is:  
+--[ED25519 256]--+  
|        .+* o..  |  
|         B+=.+   |  
|         .O.X    |  
|       . . X +   |  
|        S o * +  |  
|       o + + = . |  
|  E . . + * o o  |  
|   o + . * + . . |  
|    o.+.+.o      |  
+----[SHA256]-----+
```

De esta forma, podemos ver que la llave privada se guardó en `/home/wuanpack/.ssh/id_ed25519` y la llave pública en `home/wuanpack/.ssh/id_ed25519.pub`.

### SSH Private Keys

Evidentemente es importante recalcar que nunca se debe compartir la clave privada bajo ninguna circunstancia. Alguien con la clave privada puede logearse en servidores que lo acepten, a no ser de que la clave sea encriptada por medio de una frase.

Hay que tener en cuenta que la frase usada para desencriptar la clave privada no te identifica al servidor para nada; solo desencripta la clave privada. La frase nunca es transmitida y nunca abandona el sistema. NOTA: La frase es como una contraseña.

Usando herramientas como [[John The Ripper]] se puede atacar una clave SSH encriptada para intentar encontrar la frase, recalcando la importancia de usar una frase compleja para mantener la clave privada, privada.

Cuando se genera una clave SSH para ingresar a una máquina remota, deberías generar las claves en tu máquina y luego copiarla la clave pública, ya que esto significa que la clave privada nunca existirá en la máquina de destino usando `ssh-copy-id`. Sin embargo, esto no es tna importante para las claves temporales generadas para acceder a máquinas CTF.

Los permisos deben estar configurados correctamente para usar una clave SSH privada; de lo contrario, su cliente SSH ignorará el archivo y mostrará una advertencia. Solo el propietario debe poder leer o escribir en la clave privada (600 o más estricto). `ssh i privateKeyFileName user@host` es la forma de especificar una clave para el cliente OpenSSH estándar de Linux.

#### Claves de Confianza para el Host Remoto

La carpeta `~/.ssh` es por defecto el lugar para almacenar las claves para OpenSSH. Las carpeta `authorized_keys` en este directorio mantiene las claves públicas que están permitidas para acceder al servidor si la key authentication está activada. Por defecto en muchas distribuciones de Linux, la key authentication está activada ya que es más segura que usar una contraseña para autenticar. Solo la key authentication debería ser aceptada si quieres permitir acceso SSH para el usuario root.

### Usando Claves SSH para tener un "Mejor Shell"

Durante CTFs, pentesting y ejercicios de red teaming, las claves SSH con una excelente forma de "mejorar" un reverse shell, asumiendo que el usuario tenga el inicio de sesión habilitado. Tenga en cuenta que www-data normalmente no permite esto, pero los usuarios normales y el usuario root sí lo permiten. Dejar una clave SSH en el archivo `authorized_keys` de una máquina puede ser una puerta trasera útil, y no tendrá que lidiar con ninguno de los problemas de las shells inversas inestables como Control-C o la falta de autocompletado con la tecla Tab.
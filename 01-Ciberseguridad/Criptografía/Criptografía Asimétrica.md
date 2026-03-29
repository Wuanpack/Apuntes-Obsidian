---
tags:
  - criptografia/criptografia-asimetrica
  - seguridad
  - redes
---
## ¿Qué es?

La encriptación asimétrica es el proceso de usar una clave pública de par de llaves pública/privada para encriptar texto plano y, luego, usar la clave privada correspondiente para desencriptar el cifrado. La encriptación asimétrica depende de la criptografía asimétrica, también denominada criptografía de clave pública.


## Flujo de Trabajo

1. El remitente recupera la clave pública del destinatario.
2. El remitente usa la clave pública para encriptar el texto plano.
3. El remitente envía el texto cifrado al destinatario.
4. El destinatario usa su clave privada para desencriptar el cifrado. ahora, el destinatario puede ver el texto sin formato.

## RSA

RSA es un algoritmo de encripción asimétrica que proporciona transmisión de información segura en canales inseguros.

Se basa en un problema matemático complejo de factorización de un número grande. Multiplicar dos números primos es una tarea sencilla; sin embargo, encontrar los factores de un número gigante requiere de mucha potencia computacional.

En la pŕactica, se usan números primos de alrededor de 300 dígitos, por lo que encontrar los factores de el número resultante es una tarea compleja.

Entonces ¿cómo funciona el RSA?

## Funcionamiento del RSA

1. Generación de las llaves: Dos números primos grandes se escogen y son multiplicados entre sí para crear un módulo. La llave pública y privada son derivadas de este módulo y otro número llamado el exponente público.
2. Encripción: El remitente usa la llave pública del recipiente para encriptar el mensaje, transformándolo en un formato ilegible.
3. Desencripción: El recipiente usa su llave privada para convertir el texto cifrado de vuelta a su mensaje original.

El RSA se construye usando principios fundamentales matemáticos.

### 1. Generación de Llaves

Dos números primos grandes, *p* y *q*, se escogen y son multiplicados entre sí para formar el módulo:

*n = p * q* 

El *totiente* de *n* se calcula como:

**ϕ(n) = (p − 1) × ( q − 1)**

o

**ϕ(n) = n − p − q + 1**
### 2. Llaves Públicas y Privadas

La llave pública se compone de *(n, e)*, donde *e* es un exponente públic (a menudo escogido como 65537 para eficiencia y seguridad). La llave privada es un número *d* que satisface la siguiente ecuación:

**e×d≡1 mod ϕ(n)**

En otras palabras, *d* es el inverso modular de *e módulo ϕ(n)*.

### 3. El reto de Derivar la Llave Privada

Para calcular *d*, uno debe conocer ϕ(n), lo cual implica conocer los factores primos *p* y *q* de *n*. Para primos suficientemente grandes, factorizar *n* en *p* y *q* es computacionalmente inviable con la tecnología actual.

### Algoritmo Extendido Euclideano

En teoría, si puedes factorizar *n* y determinar ϕ(n), usaríamos el Algoritmo Extendido Euclideano para computar *d* como el inverso modular de *e modulo ϕ(n)*


## Diffie-Hellman Key Exchange

El intercambio de llaves apunta a establecer un secreto compartido entre dos partes. Este método permite a las dos partes establecer un secreto compartido a través de un canal de comunicación inseguro sin requerir un secreto compartido pre existente y sin un observador que pueda obtener esta llave. Consecuentemente, esta llave puede ser usada para encripción simétrica en las comunicaciones siguientes.

1. Alice y Bob acuerdan las variables públicas: un numero primo largo *p* y un generador *g*, donde 0 < g < p. Estos valores van a ser divulgados públicamente por el canal de comunicación.
2. Cada parte escoge un entero privado. Cada uno de estos valores representa la llave privada y no debe ser divulgada.
3. Cada parte calcula su llave pública usando su llave privada del paso 2 y las variables acordadas en el paso 1. Alice calcula **_A_ = _g__a_ mod _p_** y Bob calcula **_B_ = _g__b_ mod _p_**. Estas son las llaves públicas.
4. Alice y Bob envían sus llaves entre sí. Bob recibe **_A_ = _g__a_ mod _p_** y Alice recibe **_B_ = _g__b_ mod _p_**. Este paso se llama intercambio de llaves.
5. Alice y Bob finalmente calculan el secreto compartido usando la llave pública recibida y su propia llave privada. Alice calcula **_B__a_ mod _p_** y Bob calcula **_A__b_ mod _p_**. Ambos cálculos dan el mismo resultado **_g__a__b_ mod _p_**.

El intercambio de llaves Diffie-Hellman es usado a menudo en conjunto con RSA. Diffie-Hellman se usa para el acuerdo de llaves, mientras que RSA se usa para firmas digitales, transporte de llaves, autenticación, entre otros usos.Por ejemplo, RSA ayuda a probar la identidad de la persona a la que se le está hablando, ya que se puede confirmar en base a su llave pública. Esto podría prevenir que alguien ataque la conexión con un ataque [[Man in The Middle]] en contra de Alicia pretendiendo ser Bob. En resumen, Diffie-Hellman y RSA son incorporados en muchos protocolos de seguridad y estándares para proveer una solución de seguridad comprensiva.

## SSH

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

## Firmas Digitales y Certificados

### ¿Qué es?

Las firmas digitales son una forma de verificar la autenticidad e [[Seguridad de la Información#Integridad|integridad]] de un mensaje o documento digital. Probando la autenticidad de archivos significa que sabemos quién los creó o modificó. Usando criptografía asimétrica, se puede producir una firma para las claves privadas, la cual se puede verificar usando nuestra clave pública. Solo tú deberías tener acceso a tu clave privada, lo cual prueba que firmaste el archivo. En muchos países modernos, las firmas digitales y físicas tienen el mismo peso legal.

La forma más simple de firma digital es encriptando el documento con la clave privada. Si alguien quiere verificar esta firma, lo desencriptarían con tu clave pública y verificaría que los archivos coincide.

Algunos artículos usan términos como firma electrónica y firma digital indistintamente. Se refieren a copiar una imagen de la firma en la parte superior de un documento. Este acercamiento no prueba la [[Seguridad de la Información#Integridad|integridad]] de un documento, ya que cualquiera puede copiar y pegar la imagen.

### Certificados

Los certificados son una aplicación esencial de la criptografía de clave pública, y también están ligados a las firmas digitales. Un lugar común en el que se usan es HTTPS.

Cómo sabe el navegador web que el servidor con el que se está comunicando es quien dice ser? La respuesta recae en los certificados.

El servidor web tiene un certificado que dice que es la página que dice ser. Los certificados tienen una cadena de confianza, empezando con un root CA (Certificate Authority). Desde el momento de la instalación, su dispositivo, sistema operativo y buscador web automáticamente confía en varios CAs raíz. 

Los certificados solo son confiables cuando las CA raíz afirman confiar en la organización que los firmó. En cierto modo, se trata de una cadena; por ejemplo, el certificado está firmado por una organización, la organización es de confianza para una CA, y la CA es de confianza para su navegador. Por lo tanto, su navegador confía en el certificado. En general, existen largas cadenas de confianza. Puede consultar las autoridades de certificación en las que confía Mozilla Firefox aquí (se abre en una pestaña nueva) y en las de Google Chrome aquí (se abre en una pestaña nueva).

Supongamos que tienes un sitio web y quieres usar HTTPS. Este paso requiere un certificado TLS. Puedes obtener uno de las distintas autoridades de certificación por una tarifa anual. Además, puedes obtener tus propios certificados TLS para los dominios que posees usando Let's Encrypt (se abre en una pestaña nueva) de forma gratuita. Si administras un sitio web, vale la pena configurarlo y cambiar a HTTPS, como haría cualquier sitio web moderno.

## PGP Y GPG

PGP significa Pretty Good Privacy. Es un software que implementa encripción para encriptar archivos, realizando firma digital y más- GnuPG o GPG es una implementación open-source del estándar OpenPGP.

GPG se usa comúnmente en email para proteger la [[Seguridad de la Información#Confidencialidad|confidencialidad]] de los mensajes de correo electónico. Además, puede ser usado para firmar un mensaje email y confirmar su [[Seguridad de la Información#Integridad|integridad]].

Cuando se genera un GPG con `gpg --full-gen-key`. Se le pregunta sobre el propósito de usar GPG, si solo para firmar o para firmar y cifrar. Además de seleccionar el algoritmo criptográfico, debíamos elegir una fecha de caducidad para la clave generada. Finalmente, proporcionamos información personal: nuestro nombre, dirección de correo electrónico y un comentario, generalmente sobre el propósito de esta clave.

Puedes necesitar usar GPG para desencriptar archivos en CTFs. Con PGP/GPG, las claves privadas pueden ser protegidas con frases en una forma similar a como cuando se protegen las claves privadas SSH. Si la clave es protegida con una frase, se puede intentar crackearla con [[John The Ripper]] y `gpg2john`. 


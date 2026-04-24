---
tags:
  - criptografia/criptografia-asimetrica
  - seguridad
  - redes
---
## Índice
```table-of-contents
```
## ¿Qué es?

La encriptación asimétrica es el proceso de usar una clave pública de par de llaves pública/privada para encriptar texto plano y, luego, usar la clave privada correspondiente para desencriptar el cifrado. La encriptación asimétrica depende de la criptografía asimétrica, también denominada criptografía de clave pública.

## Flujo de Trabajo

1. El remitente recupera la clave pública del destinatario.
2. El remitente usa la clave pública para encriptar el texto plano.
3. El remitente envía el texto cifrado al destinatario.
4. El destinatario usa su clave privada para desencriptar el cifrado. ahora, el destinatario puede ver el texto sin formato.

Dentro de los algoritmos de encriptación asimétrica existentes, los más destacados son:

* [[RSA]]
* [[Diffie-Hellman Key Exchange]]
* [[ED22519]]
* [[DSA (Digital Signature Algorithm)]]
* [[ECDSA-SK (ECDSA with Security Key)]]
* [[ED25519-SK (ED25519 with Security Key)]]

Los últimos son especialmente utilizados en entornos como [[SSH]].
## Firmas Digitales y Certificados

### ¿Qué son?

Las firmas digitales son una forma de verificar la [[Autenticidad]] e [[Seguridad de la Información#Integridad|integridad]] de un mensaje o documento digital. Probando la autenticidad de archivos significa que sabemos quién los creó o modificó. Usando criptografía asimétrica, se puede producir una firma para las claves privadas, la cual se puede verificar usando nuestra clave pública. Solo tú deberías tener acceso a tu clave privada, lo cual prueba que firmaste el archivo. En muchos países modernos, las firmas digitales y físicas tienen el mismo peso legal.

La forma más simple de firma digital es encriptando el documento con la clave privada. Si alguien quiere verificar esta firma, lo desencriptarían con tu clave pública y verificaría que los archivos coincide.

Algunos artículos usan términos como firma electrónica y firma digital indistintamente. Se refieren a copiar una imagen de la firma en la parte superior de un documento. Este acercamiento no prueba la [[Seguridad de la Información#Integridad|integridad]] de un documento, ya que cualquiera puede copiar y pegar la imagen.

### Certificados

Los certificados son una aplicación esencial de la criptografía de clave pública, y también están ligados a las firmas digitales. Un lugar común en el que se usan es HTTPS.

¿Cómo sabe el navegador web que el servidor con el que se está comunicando es quien dice ser? La respuesta recae en los certificados.

El servidor web tiene un certificado que dice que es la página que dice ser. Los certificados tienen una cadena de confianza, empezando con un root CA ([[Certificate Authority]]). Desde el momento de la instalación, su dispositivo, sistema operativo y buscador web automáticamente confía en varios CAs raíz. 

Los certificados solo son confiables cuando las CA raíz afirman confiar en la organización que los firmó. En cierto modo, se trata de una cadena; por ejemplo, el certificado está firmado por una organización, la organización es de confianza para una CA, y la CA es de confianza para su navegador. Por lo tanto, su navegador confía en el certificado. En general, existen largas cadenas de confianza.

Supongamos que tienes un sitio web y quieres usar HTTPS. Este paso requiere un certificado [[TLS]]. Puedes obtener uno de las distintas autoridades de certificación por una tarifa anual. Además, puedes obtener tus propios certificados [[TLS]] para los dominios que posees usando Let's Encrypt (se abre en una pestaña nueva) de forma gratuita. Si administras un sitio web, vale la pena configurarlo y cambiar a HTTPS, como haría cualquier sitio web moderno.

## PGP Y GPG

PGP significa Pretty Good Privacy. Es un software que implementa encripción para encriptar archivos, realizando firma digital y más- GnuPG o GPG es una implementación open-source del estándar OpenPGP.

GPG se usa comúnmente en email para proteger la [[Seguridad de la Información#Confidencialidad|confidencialidad]] de los mensajes de correo electónico. Además, puede ser usado para firmar un mensaje email y confirmar su [[Seguridad de la Información#Integridad|integridad]].

Cuando se genera un GPG con `gpg --full-gen-key`. Se le pregunta sobre el propósito de usar GPG, si solo para firmar o para firmar y cifrar. Además de seleccionar el algoritmo criptográfico, debíamos elegir una fecha de caducidad para la clave generada. Finalmente, proporcionamos información personal: nuestro nombre, dirección de correo electrónico y un comentario, generalmente sobre el propósito de esta clave.

Puedes necesitar usar GPG para desencriptar archivos en CTFs. Con PGP/GPG, las claves privadas pueden ser protegidas con frases en una forma similar a como cuando se protegen las claves privadas SSH. Si la clave es protegida con una frase, se puede intentar crackearla con [[John The Ripper]] y `gpg2john`. 


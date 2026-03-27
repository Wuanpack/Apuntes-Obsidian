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


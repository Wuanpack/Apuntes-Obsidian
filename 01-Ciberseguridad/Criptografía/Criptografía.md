---
tags:
  - seguridad
  - criptografia
  - redes
---
## ¿Qué es?

La criptografía es la técnica y ciencia de proteger información mediante algoritmos matemáticos y códigos, convirtiéndola en un formato ilegible para personas no autorizadas. 

Su objetivo es garantizar la [[Seguridad de la Información#Confidencialidad|confidencialidad]], [[Seguridad de la Información#Integridad|integridad]], [[Autenticación|autenticación]] y [[No Repudio|no repudio]] de los datos, siendo esencial para ciberseguridad, transacciones bancarias, mensajes privados y navegación web segura.

Por ejemplo, cuando se manejan tarjetas de crédito, la compañía debe seguir y hacer cumplir el [[Payment Card Industry Data Security Standard (PCI DSS)]]. En este caso, el [[Payment Card Industry Data Security Standard (PCI DSS)|PCI DSS]]asegura un nivel mínimo de seguridad para almacenar, procesar y transmitir información relacionada a tarjetas de crédito.

## Definiciones

* **Plaintext**: Es el mensaje o la información original, legible, antes de que sea encriptada. Puede ser un documento, una imagen, un contenido multimedia o cualquier otra información binaria.

* **Ciphertext**: Es la desordenada, ilegible version del mensaje después de la encriptación. Idealmente, nosotros no podríamos obtener ninguna información sobre el texto plano original, excepto por su tamaño aproximado.

* **Cipher**: Es un algoritmo o método para convertir texto plano en texto cifrado y al revés. Un algoritmo es usualmente desarrollado por un matemático.

* **Key**: Es una cadena de bits que el algoritmo usa para encriptar o desencriptar la información. En general, el algoritmo usado es de conocimiento público; sin embargo, la llave debe mantenerse en secreto a no ser de que sea la llave pública de la [[Criptografía Asimétrica|encriptación asimétrica]].

* **Encryption**: Es el proceso de convertir texto plano en texto cifrado usando un algoritmo y una llave. A diferencia de la llave.

* **Desencryption**: Es el proceso reverso a la encripción, convirtiendo el texto cifrado de vuelta a texto plano usando un algoritmo y una llave.

## Encripción Simétrica

La encripción simétrica, también conocida como criptografía simétrica, usa la la misma llave para encriptar y para desencriptar la información.

Mantener en secreto la llave es un deber; también se le llama llave privada de criptografía. 

Es por eso, que comunicar la llave a las partes interesadas puede ser un desafío, ya que requiere un canal de comunicación seguro.

Algunos ejemplos de este tipo de encripción son el DES (Data Encryption Standard), 3DES (Triple DES) y el AES (Advanced Encryption Standard).

* DES fue adoptado como estándar en 1977 y usa una llave de 56 bits. Con el avance del poder computacional, en 1999, una llave DES era exitosamente quebrada en menos de 24 horas, motivando el cambio al 3DES.

* 3DES es DES pero aplicada tres veces; consecuentemente, el tamaño de la llave es 168 bits, aunque la seguridad efectiva son 112 bits. 3DES fue más una solución ad-hoc cuando DES ya no era considerado seguro. 3DES quedó obsoleto en 2019 y se debió haber reemplazado por AES; sin embargo, aún se pueden encontrar sistemas legacy que lo usen.

* AES fue adoptado como estándar en 2001. Su llave puede ser de 128, 192 o 256 bits.

## Encriptación Asimétrica

A diferencia de la encriptación simétrica, la [[Criptografía Asimétrica|encriptación asimétrica]] usa pares de llaves, una para encriptar y otra para desencriptar. Para proteger la [[Seguridad de la Información#Confidencialidad|confidencialidad]], este tipo de encripción encripta información usando una llave pública, de ahí que también se le llame [[Criptografía Asimétrica|criptografía de llave pública]].

Algunos ejemplos son el [[RSA]], [[Diffie-Hellman Key Exchange]] y [[Elliptic Curve Cryptography (ECC)]].

La [[Criptografía Asimétrica|encriptación asimétrica]] tiende a ser más lenta, y muchos de estos algoritmos usan llaves más largas que la encriptación simétrica.

El [[RSA]] usa llaves de 2048, 3072 y 4096 bits; 2047 bits se consideran el tamaño de llave mínimo recomendado.

[[Diffie-Hellman Key Exchange]] también recomiendan llaves de al menos 2048 bits, pero usan 3072 y 4096 bits para mejor seguridad.

Por otro lado, [[Elliptic Curve Cryptography (ECC)]] puede alcanzar una seguridad similar con llaves más cortas. Por ejemplo, con una llave de 256 bits, ECC provee un nivel de seguridad comparable a una llave de 3072 bits de RSA.

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


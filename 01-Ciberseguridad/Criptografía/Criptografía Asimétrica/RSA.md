---
tags:
  - criptografia
  - criptografia/criptografia-asimetrica
  - seguridad
---

## ¿Qué es?

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


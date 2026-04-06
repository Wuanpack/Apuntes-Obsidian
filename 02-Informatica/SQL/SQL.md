Las bases de datos son una colección organizada de información estructurada o datos que son fácilmente accesibles y pueden ser manipulados o analizados.

## Tipos de Bases de Datos

Existen varios tipos de bases de datos que se pueden construir, pero de momento nos enfocaremos en los dos tipos primarios: bases de datos relacionales (también llamados SQL) y bases de datos no relacionales (también llamados NoSQL).

### Bases de Datos Relacionales

Almacenan datos estructurados, lo que significa que los datos insertados en esta base de datos siguen una estructura. Por ejemplo, información de un usuario que consiste de first_name, last_name, email_address, username y password. Los datos estructurados se guardan en filas y columnas en una table; las relaciones pueden ser hechas entre 2 o más tablas, de ahí el nombre de bases de datos relacionales.

### Bases de Datos No Relacionales

En vez de almacenar datos de la forma anterior, se almacena datos en un formato no-tabular. Por ejemplo, si documentos están siendo escaneados, los cuales pueden contener varios tipos y cantidades de datos, son almacenados en bases de datos que ocupan un formato no-tabular. Aquí hay un ejemplo de cómo podría verse:

```bash
 {
    _id: ObjectId("4556712cd2b2397ce1b47661"),
    name: { first: "Thomas", last: "Anderson" },
    date_of_birth: new Date('Sep 2, 1964'),
    occupation: [ "The One"],
    steps_taken : NumberLong(4738947387743977493)
}
```

En términos de qué base de datos debería escogerse, siempre depende del contexto en el que la base de datos se va a usar. Las bases de datos relacionales son usados por lo general cuando los datos que van a ser almacenados van a tener un formato consistente, donde la precisión es importante, como cuando se procesan transacciones e-commerce. Las bases de datos no relacionales, por otro lado, son más usados cuando los datos que van a ser recibidos pueden variar en su formato pero necesitan ser colectados y organizados en el mismo espacio, como plataformas de social media colectando contenido generado por usuarios.

![[Pasted image 20260406200225.png]]
## ¿Qué es SQL?

Las bases de datos son usualmente controlados usando un Database Management System (DBMS). Sirviendo como una interfaz entre el usuario final y la base de datos, un sistema de gestión de bases de datos (DBMS, por sus siglas en inglés) es un programa informático que permite a los usuarios recuperar, actualizar y gestionar los datos almacenados. Algunos ejemplos de DBMS son MySQL, MongoDB, Oracle Database y MariaDB.

La interacción entre el usuario se puede realizar usando SQL (Structured Query Language). SQL es un lenguaje de programación que se puede utilizar para consultar, definir y manipular los datos almacenados en una base de datos relacional.

### Beneficios de SQL en Bases de Datos Relacionales

SQL es casi tan omnipresente como las propias bases de datos. Aquí hay algunos beneficios de aprender y usar SQL:

* Es rápido: Las bases de datos relacionales pueden retornar enormes lotes de datos casi instantáneamente debido a como el pequeño espacio de almacenamiento es usado en altas velocidades de procesamiento.
* Fácil de aprender: A diferencia de muchos lenguajes, SQL está escrito 
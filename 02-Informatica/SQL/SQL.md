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
* Fácil de aprender: A diferencia de muchos lenguajes, SQL está escrito en Inglés plano, haciéndolo más fácil de entender. La alta naturaleza legible del lenguaje significa que los usuarios pueden concentrarse en aprender las funciones y sintaxis.
* Confiable: Como se mencionó anteriormente, las bases de datos relacionales pueden garantizar un cierto nivel de precisión en los datos al definir una estructura estricta dentro de la cual deben ajustarse los conjuntos de datos para poder ser insertados.
* Flexible: SQL provee todo tipo de capacidades cuando se trata de hacer una query a una base de datos; esto permite a los usuarios realizar una gran cantidad de tareas de análisis de datos muy eficientemente.


## Database and Table Statements

### Database Statements

Crear base de datos:

``` sql
CREATE DATABASE database_name;
```

Mostrar bases de datos:

```sql
SHOW DATABASES;
```

En la lista devuelta, podrás ver la bases de datos que hayas creado y otras que están incluidas por defecto (mysql, information_scheme, performance_scheme y sys), los cuales son usados para varios propósitos que permiten a mysql funcionar.

Usar base de datos:

```sql
USE database_name;
```

Eliminar base de datos:

```sql
DROP database database_name;
```

### Table Statements

Crear tabla:

```sql
CREATE TABLE example_table_name (
	example_column1 data_type,
	example_column2 data_type,
	example_column3 data_type
);
```

Mostrar tablas:

```sql
SHOW TABLES;
```

Describir: Si queremos saber que columnas están contenidas dentro de una tabla y sus tipos de datos, podemos usar el comando `DESCRIBE`, el cual puede ser abreviado a `DESC`

```sql
DESCRIBE table_name;
```

Modificar tabla:

```sql
ALTER TABLE table_name;
ADD column1 data_type;
```

Eliminar tablas:

```sql
DROP TABLE table_name;
```


## Operaciones CRUD

CRUD significa Create, Read, Update and Delete, los cuales son considerados operaciones básicas en cualquier sistema que maneja datos.

### Create Operation (INSERT)

La operación Create va a crear nuevos registros en una tabla:

```sql
INSERT INTO table_name (column1, column2, column3)
	VALUES (value1, value2, value3);
```

### Read Operation (SELECT)

```sql
SELECT * FROM table_name;
```

### Update Operation (UPDATE)

```sql
UPDATE table_name
	SET column_name = "example_text"
	WHERE id = 1;
```

### Delete Operation (DELETE)

```sql
DELETE FROM table_name WHERE id = 1;
```


## Cláusulas

Una cláusula es una parte de una instrucción que especifica los criterios de los datos que se manipulan, generalmente mediante una instrucción inicial. Las cláusulas nos ayudan a definir el tipo de datos y cómo deben recuperarse u ordenarse.

### DISTINCT Clause

La cláusula `DISTINCT` puede ser usado para evitar registros duplicados cuando se haga una query, retornando sólo valores únicos.

```sql
SELECT DISTINCT column FROM table_name;
```

### GROUP BY Clause

La cláusula `GROUP BY` agrega datos desde múltiples registros y agrupa los resultados de las querys en columnas. Puede ser útil para agregar funciones.

```sql
SELECT column, COUNT(*)
	FROM table_name
	GROUP BY column;
```

### ORDER BY Clause

La cláusula `ORDER BY` puede ser usado para ordenar los registros retornados por una query de forma ascendente o descendente. Usando las funciones `ASC` y `DESC` podemos lograr eso.

```sql
SELECT *
	FROM table_name
	ORDER BY column ASC;
```

```sql
SELECT *
	FROM table_name
	ORDER BY column DESC;
```

### HAVING Clause

La cláusula `HAVING` es usada con otras cláusulas para filtrar grupos o resultados de registros basados en una condición. En el caso de `GROUP BY`, evalúa la condición de `TRUE` o `FALSE`, a diferencia de la cláusula `WHERE` `HAVING` filtra el resultado después de que el añadido fue realizado.

```sql
SELECT column, COUNT(*)
	FROM table_name
	GROUP BY column
	HAVING column LIKE '%Hack%';
```

## Operadores Lógicos

### LIKE Operator

El operador `LIKE` es usado comúnmente en conjunto con cláusulas como `WHERE` con el objetivo de filtrar por patrones específicos dentro de una columna. 

```sql
SELECT *
	FROM table_name
	WHERE column LIKE "%descripcion%";
```

### AND Operator

El operador `AND` usa múltiples condiciones dentro de una query y retorna `TRUE` si todas son true.

```sql
SELECT *
	FROM table_name
	WHERE column1 = "example1" AND column2 = "example2";
```

### OR Operator

El operador `OR` combina múltiples condiciones dentro de queries y retorna `TRUE` si al menos una de esas condiciones es true.

```sql
SELECT *
	FROM table_name
	WHERE column1 LIKE "%descripcion1%" OR column2 LIKE "%descripcion2%";
```

### NOT Operator

El operador `NOT` revierte el valor del operador booleano, permitiéndonos excluir una condición específica.

```sql
SELECT *
	FROM table_name
	WHERE NOT column LIKE "%descripcion%"
```

### BETWEEN Operator

El operador `BETWEEN` nos permite probar si un valor existe dentro de un rango definido

```sql
SELECT *
	FROM table_name
	WHERE column BETWEEN 2 AND 4;
```

## Comparison Operators

Los operadores de comparación son usados para comparar valores y revisar si están dentro de un criterio especificado.

### Equal To Operator

el operador `=` compara dos expresiones y determina si son iguales, o puede revisar si un valor coincide con otro en una columna específica.

```sql
SELECT *
	FROM table_name
	WHERE column = "Descripcion";
```

### Not Equal To Operator

El operador `!=` compara expresiones y prueba si no son iguales; también revisa si un valor difiere de uno dentro de una columna.

```sql
SELECT *
	FROM table_name
	WHERE column != "Descripcion";
```

### Less Than Operator

El operador `<` compara si una expresión tiene un valor menor que otro.

```sql
SELECT *
	FROM table_name
	WHERE column < "Valor a comparar";
```

### Greater Than Operator

El operador `>` compara si una expresión con dado tiene un valor mayor que otro.

```sql
SELECT *
	FROM table_name
	WHERE column > "Valor a comparar";
```


### Less Than or Equal To and Greater Than Equal To Operators

```sql
SELECT *
	FROM table_name
	WHERE column <= "Valor a comparar";
```

```sql
SELECT *
	FROM table_name
	WHERE column >= "Valor a comparar";
```


## String Functions

### CONCAT() Function

Esta funcion se usa para juntar dos o más strings. Es útil para combinar texto de diferentes columnas.

```sql
SELECT CONCAT(column1, "Texto entre medio", column2, "Texto final.") AS alias FROM table_name;
```

### GROUP_CONCAT() Function

Esta función nos ayuda a concatenar datos desde múltiples filas en un campo.

```sql
SELECT column1, GROUP_CONCAT(column2 SEPARATOR ", ") AS alias
	FROM table_name
	GROUP BY category;
```


### SUBSTRING() Function

Esta función recuperará una subcadena de una cadena dentro de una consulta, comenzando en una posición determinada. También se puede especificar la longitud de esta subcadena. Ejemplo:

```sql
mysql> SELECT SUBSTRING(published_date, 1, 4) AS published_year FROM books; 
+----------------+ 
| published_year | 
+----------------+ 
| 2014           | 
| 2021           | 
| 2016           | 
| 2021           | 
| 2021           | 
+----------------+ 

5 rows in set (0.00 sec)
```

### LENGTH() Function

Esta función retorna el número de carácteres de un string. Esto incluye espacios y signos de puntuación.

```sql
SELECT LENGTH(column) AS alias FROM table_name;
```

## Aggregate Functions

Estas funciones agregan el valor de varias filas dentro de un criterio específico en una query; Puede combinar múltiples valores dentro de un resultado.

### COUNT() Function

Esta función retorna el número de registros dentro de una expresión.

```sql
SELECT COUNT(*) AS alias FROM table_name;
```

### SUM() Function

Esta funciona suma todos los valores (no NULL) de una columna determinada.

```sql
SELECT SUM(column) AS alias FROM table_name;
```

### MAX() Function

Esta función calcula el valor máximo dentro de una columna dada en una expresión.

```sql
SELECT MAX(column) AS alias FROM table_name;
```

### MIN() Function

Esta función calcula el valor mínimo dentro de una columna dada en una expresión.

```sql
SELECT MIN(column) AS alias FROM table_name;
```
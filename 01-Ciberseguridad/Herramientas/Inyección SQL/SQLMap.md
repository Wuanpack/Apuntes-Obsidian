## Índice
```table-of-contents
```
## SQL Injection Vulnerability

Ejemplo de una página web que pide una usuario y contraseña para iniciar sesión:

* Username: John
* Password: Un@detectable444

Una vez ingresamos el usuario con la contraseña, el sitio web los recibe y hace una query SQL con las credenciales para enviarlas a la base de datos

```sql
SELECT * FROM users WHERE username = 'John' AND password = 'Un@detectable444';
```

A veces, cuando el input no esta sanitizado, es decir, que el user input no es validado, los atacantes pueden manipularlo y escribir queries SQL que podrían ser ejecutadas en la base de datos y realizar las acciones deseadas por el atacante.

Asumamos que la página web ser sitio carece de validación y sanitización de input. Esto significa que es vulnerable a inyección SQL. El atacante no conoce la contraseña de John, por lo que va a colocar lo siguiente en los campos de inicio de sesión:

* Username = John
* Password = abc' OR 1=1;-- -

Con la información anterior, el atacante ingresa una contraseña cualquiera `abc` e inyecta la cadena `' OR 1=1; -- -`.

```sql
SELECT * FROM users WHERE username = 'John' AND password = 'abc' OR 1=1; -- -';
```


## Automated SQL Injection Tool

SQLMap es una herramienta automatizada para detectar y explotar vulnerabilidades de inyección SQL en aplicaciones web. Esto simplifica el proceso de identificar estas vulnerabilidades.

Como en cualquier herramienta basada en línea de comandos, podemos usar `--help` para listar todas las flags que podemos usar. Si no queremos añadir manualmente las flags por cada comando, podemos usar el `--wizard` con SQLMap.

Cuando usamos esta flag, la herramienta nos guiará por cada paso y preguntará preguntas para completar el scan, haciéndolo una opción perfecta para beginners.

La flag `--dbs` ayuda a extraer todos los nombres de bases de datos. Una vez conocemos los nombres, podemos extraer información sobre las tablas de la base de datos usando `-D database_name --tables`.

Después de obtener las tablas, si queremos enumerar los registros en dichas tablas, podemos usar `-D database_name -T table_name --dump`. Las diferentes flags en la herramienta SQLMap nos permite extraer información detallada desde las bases de datos.

En escenarios reales, muchas aplicaciones web recaen en las cookies para mantener sesiones de usuarios, aplicar autenticación, o aplicar controles de acceso. Cuando se testean dichas aplicaciones, simplemente proporcionando la URL con SQLMap podría no ser suficiente, debido a que las peticiones no autenticadas podrían ser redireccionadas, denegadas, o retornar contenido diferente. SQLMap soporta el testing basado en cookies con la flag `--cookie`, la cual permite incluir cookies de sesiones (como `PHPSESSID`, `JSESSIONID` o tokens de autenticación) directamente en la petición.

Esto garantiza que SQLMap interactúe con la aplicación en el mismo contexto autenticado o autorizado que un usuario normal.
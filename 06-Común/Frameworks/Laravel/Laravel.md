---
tags:
  - laravel
  - desarrollo
  - frameworks
---

## ¿Qué es?

Laravel es un [[Frameworks|Framework]] de desarrollo web escrito en PHP, creado por Taylor Otwell en 2011. Es actualmente el [[Frameworks|Framework]] PHP más popular del mundo y está diseñado para hacer el [[Desarrollo de Software Web]] más simple, ordenado y rápido siguiendo el patrón MVC (Model-View-Controller).

Existe debido a que PHP es poderoso pero caótico. Sin estructura, un proyecto PHP termina siendo un desorden de archivos mezclando lógica, consultas a base de datos y HTML en el mismo lugar. Laravel resuelve eso imponiendo una estructura clara y entregando herramientas resueltas para los problemas más comunes del desarrollo web.

Laravel se ha popularizado debido a su potencia, flexibilidad y facilidad de uso. Es ideal para desarrolladores que buscan construir aplicaciones web robustas y modernas de manera eficiente.

Algunas ventajas de trabajar con Laravel son:

* Desarrollo rápido: Laravel facilita el desarrollo ágil de aplicaciones web con su sintáxis clara y sus numerosas características listas para usar.
* Escalabilidad: Permite escalar desde proyectos pequeños hasta aplicaciones empresariales complejas.
* Comunidad Activa: Cuenta con una gran comunidad de desarrolladores que contribuyen con paquetes, tutoriales y soporte.

---

### [[Instalación de Laravel|Instalación de Laravel en Windows / Linux]]

---

## El patrón MVC

Es el concepto central de Laravel. Separa la aplicación en tres capas con responsabilidades distintas.

Usuario
   ↓ (solicitud HTTP)
Router
   ↓
Controller  ←→  Model  ←→  Base de datos
   ↓
  View
   ↓ (respuesta HTML)
Usuario

* Model: Representa los datos y la lógica de negocio. Se comunica con la base de datos. Por ejemplo, un modelo Usuario sabe cómo crear, leer, actualizar y eliminar usuarios. 

* View: Es lo que ve el usuario, el HTML. En Laravel, las vistas usan el motor de plantillas Blade. No contiene lógica de negocio, solo presentación.

* Controller: Es el intermediario. Recibe la solicitud del usuario, le pide datos al Model y se los pasa al View para mostrarlos.

---

## Beneficios del MVC

* Separación de preocupaciones: Permite dividir la aplicación en componentes que se ocupan de aspectos específicos (datos, presentación, control) sin que uno afecte al otro.
* Facilita el mantenimiento: Al separar los componentes, facilita las modificaciones y actualizaciones en la aplicación sin afectar otras partes.
* Reutilización de código: Los componentes pueden ser reutilizados en diferentes partes de la aplicación o en diferentes proyectos.

---

## Ejemplo de Flujo de Trabajo MVC

1. El usuario visita /usuarios.
2. public/index.php recibe la solicitud.
3. Router busca en routes/web.php quién maneja /usuarios.
4. Pasa por los [[Middleware]] definidos.
5. El Controlador recibe la solicitud del usuario.
6. El Controlador consulta el Model.
7. El Model consulta la BD con Eloquent.
8. El Controller pasa los datos a la View (Blade).
9. Blade genera el HTML final.
10. El usuario ve la página.

---

## Componentes de Laravel

### Routing

Laravel proporciona un enrutador potente y flexible que permite definir rutas de manera sencilla y clara, asociando cada ruta con una acción del controlador.

El componente routing tiene como función dirigir las solicitudes HTTP entrantes a la acción correspondiente del controlador o a una función de cierre (closure), permitiendo gestionar la navegación y la lógica de la aplicación de manera estructurada.

Define qué código se ejecuta según la [[URL]] que visita el usuario. Se configura en `routes/web.php`

```php
// Cuando el usuario visita /usuarios, ejecuta el método index del controlador
Route::get('/usuarios', [UsuarioController::class, 'index']);
Route::post('/usuarios', [UsuarioController::class, 'store']);
Route::delete('/usuarios/{id}', [UsuarioController::class, 'destroy']);
```

### Controladores

Los controladores en Laravel son clases que agrupan la lógica de manejo de solicitudes relacionadas. Cada método de un controlador puede manejar una acción específica, como mostrar una página, procesar un formulario, etc.

Los controladores permiten mantener la lógica de la aplicación separada de la lógica de presentación, facilitando así la reutilización del código y del mantenimiento.

Reciben las solicitudes y coordinan una respuesta.

```php
class UsuarioController extends Controller
{
    // Muestra la lista de usuarios
    public function index()
    {
        $usuarios = Usuario::all();
        return view('usuarios.index', compact('usuarios'));
    }

    // Guarda un nuevo usuario
    public function store(Request $request)
    {
        Usuario::create($request->validated());
        return redirect('/usuarios');
    }
}
```

### Eloquent ORM

Eloquent es el ORM (Object-Relational Mapping) incluido en Laravel, que simplifica la interacción con bases de datos relacionales utilizando modelos de datos en lugar de escribir consultas SQL directamente.

El ORM de Laravel Permite definir modelos PHP para representar tablas de bases de datos y establecer relaciones entre ellos, facilitando la creación, consulta, actualización y eliminación (CRUD) de registros de manera intuitiva.

Permite interactuar con la base de datos usando PHP en lugar de escribir SQL directamente.

```php
// Sin Eloquent (SQL puro)
$usuarios = DB::select('SELECT * FROM usuarios WHERE activo = 1');

// Con Eloquent (mucho más legible)
$usuarios = Usuario::where('activo', true)->get();

// Crear un registro
Usuario::create(['nombre' => 'Juan', 'email' => 'juan@mail.com']);

// Eliminar
Usuario::find(1)->delete();
```

### Blade Templating Engine

Blade es el motor de plantillas de Laravel que proporciona una sintáxis simple y poderosa para definir las vistas de la aplicación, adicionalmente nos permite incluir estructuras de control, como bucles y condicionales, herencia de plantillas, y directivas que facilitan la inclusión de contenido dinámico y la reutilización de código HTML.

```html
<!-- resources/views/usuarios/index.blade.php -->
@extends('layouts.app')

@section('contenido')
    <h1>Lista de usuarios</h1>

    @foreach($usuarios as $usuario)
        <p>{{ $usuario->nombre }}</p>
    @endforeach

    @if($usuarios->isEmpty())
        <p>No hay usuarios registrados</p>
    @endif
@endsection
```

### Migraciones y Esquemas

Laravel incluye un sistema de migraciones que permite gestionar la estructura de la base de datos mediante código PHP, manteniendo control de versiones y facilitando la colaboración con equipos de desarrollo.

Las migraciones permiten crear y modificar tablas de base de datos de manera programática, evitando el uso de SQL directo y asegurando que todos los miembros del equipo de desarrollo tengan la misma estructura de base de datos.

son archivos PHP que definen la estructura de la base de datos. En lugar de crear tablas manualmente en SQL, las defines en código y Laravel las ejecuta.

```php
Schema::create('usuarios', function (Blueprint $table) {
    $table->id();
    $table->string('nombre');
    $table->string('email')->unique();
    $table->string('password');
    $table->timestamps(); // created_at y updated_at automáticos
});
```

Para ejecutarlas:

```bash
php artisan migrate
```
### Artisan

Es la interfaz de línea de comandos de Laravel. Automatiza tareas repetitivas:

```bash
# Crear archivos
php artisan make:controller UsuarioController
php artisan make:model Usuario
php artisan make:migration crear_tabla_usuarios

# Base de datos
php artisan migrate          # Ejecutar migraciones
php artisan migrate:rollback # Deshacer última migración
php artisan db:seed          # Poblar con datos de prueba

# Desarrollo
php artisan serve            # Levantar servidor local
php artisan route:list       # Ver todas las rutas definidas
php artisan tinker   
```

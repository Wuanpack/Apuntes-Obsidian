---
tags:
  - laravel
  - frameworks
  - desarrollo
---
## Índice
```table-of-contents
```
## Windows

### 1. Instalar PHP

Ir a [https://windows.php.net/download](https://windows.php.net/download), descargar la versión Thread Safe en zip de la versión más reciente.
Descomprimir el zip y mover la carpeta a `C:\php`
Agregar PHP al PATH para poder usarlo desde cualquier terminal:

- Busca **"Variables de entorno"** en el menú inicio
- Click en **"Variables de entorno"**
- En **"Variables del sistema"** busca `Path` y haz doble click
- Click en **"Nuevo"** y agrega `C:\php`
- Acepta todo y cierra

Verificar en una terminal nueva: php -v

### 2. Configurar PHP

Dentro de `C:\php` busca el archivo `php.ini-development`, cópialo y renómbralo a `php.ini`.

Ábrelo con el bloc de notas y busca estas líneas. Quítales el `;` del inicio para activarlas:

```ini
;extension=curl      →   extension=curl
;extension=mbstring  →   extension=mbstring
;extension=openssl   →   extension=openssl
;extension=pdo_sqlite →  extension=pdo_sqlite
;extension=fileinfo  →   extension=fileinfo
;extension=zip       →   extension=zip
```

Guarda el archivo.

### 3. Instalar Composer

Ve a [https://getcomposer.org/Composer-Setup.exe](https://getcomposer.org/Composer-Setup.exe) y descarga el instalador. Ejecútalo, detecta PHP automáticamente en `C:\php\php.exe` y lo instala como comando global.

Verifica:

```powershell
composer -v
```

### 4. Instalar Laravel

````powershell
composer global require laravel/installer
```

Luego agrega la carpeta de Composer al PATH igual que hiciste con PHP. La ruta a agregar es:
```
C:\Users\TU_USUARIO\AppData\Roaming\Composer\vendor\bin
````

Reemplaza `TU_USUARIO` con tu nombre de usuario de Windows. Verifica:

```powershell
laravel -v
```

### 5. Crear un proyecto

```powershell
cd C:\Users\TU_USUARIO\Documents
mkdir Proyectos
cd Proyectos
laravel new mi-app
```

Cuando pregunte por el starter kit selecciona **None**, base de datos **SQLite** y testing **Pest**, igual que en Fedora.

Luego:

```powershell
cd mi-app
php artisan serve
```

Abre el navegador en `http://localhost:8000` y debería aparecer la pantalla de bienvenida de Laravel.

### 6. Instalar VSCodium en Windows

Descarga el instalador desde [https://vscodium.com](https://vscodium.com), ejecútalo y durante la instalación marca la opción **"Agregar al PATH"** y **"Abrir con VSCodium"** en el menú contextual.

Instala las mismas extensiones que tienes en Fedora: PHP Intelephense, Laravel, Laravel Blade Snippets, GitLens, DotENV y SQLite Viewer.

## Linux (Fedora)

```bash
# PHP y extensiones necesarias para Laravel
sudo dnf install php php-cli php-mbstring php-xml php-bcmath php-curl php-zip php-pdo unzip -y

# Verificar instalación
php -v
```

```bash
# Composer (gestor de dependencias de PHP)
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php composer-setup.php
sudo mv composer.phar /usr/local/bin/composer

# Verificar
composer -v
```

```bash
# Laravel via Composer
composer global require laravel/installer

# Agregar al PATH para poder usar el comando laravel desde cualquier lugar
echo 'export PATH="$HOME/.config/composer/vendor/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# Verificar
laravel -v
```

```bash
laravel new nombre-proyecto
cd nombre-proyecto
php artisan serve
```

Ese último comando levanta un servidor local en `http://localhost:8000` para ver tu app en el navegador.
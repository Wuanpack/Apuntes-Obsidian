## Índice

```table-of-contents
```

## Herramientas

|Herramienta|¿Qué es?|¿Por qué se usa?|
|---|---|---|
|vscode / vscodium|Editor de código|Entorno de desarrollo con soporte para extensiones y TypeScript|
|git|Sistema de control de versiones|Guarda el historial de cambios y permite colaborar|
|node.js|Entorno para ejecutar JavaScript / TypeScript fuera del navegador|Base para todo backend en JS / TS|
|typescript|JavaScript con tipos|Ayuda a encontrar errores antes de ejecutar el código|
|express|Microframework web para Node.js|Liviano, flexible, ampliamente usado en la industria|
|eslint|Analizador de código estático|Obliga a escribir código consistente y limpio|
|nodemon|Reinicia el servidor automáticamente al guardar|Ahorra tiempo durante el desarrollo|
|yarn|Gestor de paquetes (alternativa a npm)|Más rápido y con lockfile más predecible|
|nvm|Gestor de versiones de Node.js|Permite tener varias versiones de Node instaladas|
|docker|Plataforma de contenedores|Empaqueta la app con todo su entorno para que funcione igual en cualquier máquina|
|prisma|ORM para Node.js|Permite interactuar con la base de datos usando TypeScript en lugar de SQL puro|
|postgresql|Base de datos relacional|Almacena los datos de la app|
|tsx|Ejecutor de TypeScript|Compila y ejecuta archivos .ts al vuelo sin generar dist/|
|handlebars|Motor de plantillas|Genera HTML dinámico en el servidor|
|dotenv|Cargador de variables de entorno|Lee el .env y lo pone disponible en process.env|
|bcryptjs|Librería de hashing|Hashea contraseñas antes de guardarlas en la DB|
|zod|Librería de validación|Valida y tipifica datos de entrada como formularios o requests|

---

## Instalación

> Basta con copiar el `package.json` + `yarn.lock` al proyecto y correr `yarn install` para instalar todas las dependencias.

### nvm

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.4/install.sh | bash  # Instalar o actualizar nvm
nvm install --lts          # Instala la versión LTS más reciente de Node
nvm use --lts              # Activa la versión LTS
nvm list                   # Lista las versiones instaladas
nvm current                # Muestra la versión activa
nvm install 24             # Instala la v24
node -v                    # Muestra la versión activa
```

### yarn

```bash
sudo npm install --global yarn  # Instala Yarn globalmente
yarn --version                  # Verifica la instalación
```

### git (Fedora)

```bash
sudo dnf install git
```

---

## Inicializar un proyecto desde cero

```bash
yarn init -y                    # Inicializa el proyecto con valores por defecto
npx gitignore node              # Genera el .gitignore para Node
```

### Dependencias base

```bash
# Producción
yarn add express express-handlebars dotenv @prisma/client bcryptjs zod

# Desarrollo
yarn add -D typescript tsx nodemon prisma \
  @types/node @types/express @types/express-handlebars @types/bcryptjs \
  eslint @eslint/js eslint-config-standard eslint-plugin-import \
  eslint-plugin-n eslint-plugin-promise
```

### TypeScript

```bash
npx tsc --init              # Genera el tsconfig.json
```

### Prisma

```bash
npx prisma init             # Inicializa Prisma (crea schema.prisma y prisma.config.ts)
```

---

## Comandos frecuentes

### yarn

```bash
yarn install                # Instala las dependencias del package.json
yarn add <paquete>          # Agrega una dependencia
yarn add -D <paquete>       # Agrega una dependencia de desarrollo
yarn remove <paquete>       # Elimina una dependencia
yarn dev                    # Ejecuta el script "dev"
yarn build                  # Ejecuta el script "build"
yarn start                  # Ejecuta el script "start"
yarn lint                   # Ejecuta el linter
yarn lint:fix               # Corrige errores de linting automáticamente
yarn list <paquete>         # Ver la versión instalada de un paquete
```

### TypeScript

```bash
npx tsc                     # Compila el proyecto
yarn tsc --noEmit           # Verifica tipos sin compilar
```

### git

```bash
git init                    # Inicializa un repositorio
git clone <url>             # Clona un repositorio
git status                  # Ver el estado del repositorio
git add .                   # Agrega todos los cambios al staging
git commit -m "mensaje"     # Hace un commit
git push                    # Sube los cambios al repositorio remoto
git pull                    # Trae los cambios del repositorio remoto
git log --oneline           # Ver historial de commits resumido
git branch                  # Ver ramas
```

### Prisma

```bash
npx prisma generate                     # Genera el cliente de Prisma
npx prisma migrate dev --name <nombre>  # Crea una migración y la aplica
npx prisma db push                      # Aplica el schema sin crear migración
npx prisma db pull                      # Importa el schema desde la DB existente
npx prisma db seed                      # Ejecuta el seed
npx prisma studio                       # Abre la UI visual de la base de datos
```

---

## Notas

- `node_modules/` nunca se sube al repositorio, se genera con `yarn install`
- `dist/` nunca se sube al repositorio, se genera con `yarn build`
- `src/generated/` nunca se sube al repositorio, se genera con `npx prisma generate`
- `.env` nunca se sube al repositorio, se documenta con un `.env.example`
- `yarn.lock` sí se sube al repositorio, garantiza versiones exactas de dependencias
# template-service

Pasos para la generarción de un nuevo servicio con NodeJS.

## Crear repo con README.md

Ingresando al Gitlab corporativo y dentro del grupo MOVAR_APP seleccionar `New project`, ingresar un nombre y descripción acorde al servicio a crear y marcar `Initialize repository with a README`

![New project](../template-service/doc/images/new_project.png)

## Clonar el repo

Una vez creado el repositorio en Gitlab clonarlo en el equipo  

`git clone https://devops.movistar.com.ar/gitlab/movar_app/NUEVO_SERVICIO.git`

Donde NUEVO_SERVICIO es el servicio creado recientemente.

## Iniciar el proyecto

Iniciar el proyecto dentro del directorio raíz para generar el archivo `package.json`

`npm init`

## Agregar script para iniciar el servicio

Dentro del archivo `package.json` agregar el script de __start__

```
{
  ...
  "scripts": {
    ...
    "start": "node app.js"
    ...
  }
  ...
}
```

## Agregar archivo `.gitignore`

En la raiz del proyecto, crear un archivo y nombrarlo `.gitignore` con el siguiente contenido.

```
[ignore]
.*/__tests__/.*

[untyped]
.*/node_modules/*
.*/packages/.*

[include]

[libs]

[lints]

[options]

[strict]
```

## Instalar dependencias

### ExpressJS

Referencia https://expressjs.com/en/starter/installing.html

Instalación `npm install express --save`

### Node-fetch

Referencia https://www.npmjs.com/package/node-fetch

Instalación `npm install node-fetch --save`

### Flow

Referencia https://flow.org/en/docs/install/

Instalación de babel `npm install --save-dev @babel/core @babel/cli @babel/preset-flow`

Luego crear un archivo `.babelrc` en la raíz del proyecto con el siguiente contenido
```
{
  "presets": ["@babel/preset-flow"]
}
```
Instalación de flow `npm install --save-dev flow-bin`

Dentro del archivo `package.json` agregar el script de __flow__
```
{
  ...
  "scripts": {
    ...
    "flow": "flow"
    ...
  }
  ...
}
```

Y luego ejecutar `npm run flow init`

### Prettier

Referencia https://prettier.io/docs/en/install.html

Instalación `npm install --save-dev --save-exact prettier`

Crear archivo `.prettierrc.json` con el siguiente contenido
```
{
    "printWidth": 120,
    "singleQuote": true,
    "quoteProps": "consistent",
    "jsxSingleQuote": true,
    "trailingComma": "es5",
    "bracketSpacing": false,
    "arrowParens": "avoid",
    "proseWrap": "always",
    "tabWidth": 4
}
```

Crear archivo `.prettierignore` con el contenido
```
# Ignore artifacts:
build
coverage

# Ignore all HTML files:
*.html
```

Dentro del archivo `package.json` agregar los script de __prettier__
```
{
  ...
  "scripts": {
    ...
    "prettier": "npx prettier --write '**/*.js' '**/*.json' '**/*.md' '**/*.yml'",
    "prettier-check": "prettier --check '**/*.js' '**/*.json' '**/*.md' '**/*.yml'"
    ...
  }
  ...
}
```

### Jest

Referencia https://jestjs.io/docs/es-ES/getting-started

Instalación `npm install --save-dev jest`

Dentro del archivo `package.json` agregar el script de __test__
```
{
  ...
  "scripts": {
    ...
    "test": "jest"
    ...
  }
  ...
}
```
Luego agregar en `package.json`
```
"jest": {
        "testEnvironment": "node",
        "coveragePathIgnorePatterns": [
            "/node_modules/"
        ]
    }
```

### Dotenv

Referencia https://www.npmjs.com/package/dotenv

Instalación `npm install dotenv`

Crear el archivo `.env` en el directorio raíz del proyecto con el contenido
```
PORT=8080
```

### ESLint

Referencia https://eslint.org/docs/user-guide/getting-started

Instalación `npm install eslint --save-devp`

Setup para generar el archivo de configuración `npx eslint --init`

![](../template-service/doc/images/eslint_setup.png)

Dentro del archivo `package.json` agregar los script de __lint__
```
{
  ...
  "scripts": {
    ...
    "lint": "eslint",
    ...
  }
  ...
}
```

## Estructura de directorios

La estructura de directorios recomendada para cualquier servicio es la siguiente

```
repo-root/
 ├─ controllers/
 │   ├─ __test__/
 │   │   └─ controller.test.js      <─── test de los controllers
 │   ├─ controller.js               <─── archivos de controladores
 │   └─ ...
 ├─ database/
 │   ├─ __test__/
 │   │   └─ database.test.js        <─── test de la base de datos
 │   ├─ database.js                 <─── archivos de base de datos
 │   └─ ...
 ├─ docs/
 │   ├─ doc.md                      <─── documentos del servicio
 │   └─ ...
 ├─ model/
 │   ├─ __test__/
 │   │   └─ model.js                <─── test del modelo
 │   ├─ model.js                    <─── archivos del modelo
 │   └─ ...
 ├─ routes/
 │   ├─ packageD/
 │   │   └─ route.test.js           <─── test de las rutas
 │   ├─ route.js                    <─── archivos de las rutas
 │   └─ ...
 ├─ server/
 │   ├─ __test__/
 │   │   └─ server.test.js          <─── test del servidor
 │   ├─ server.js                   <─── configuración del servidor
 │   └─ ...
 ├─ package.json                    <─── configuración del repositorio
 ├─ app.js                          <─── configuración del servicio
 ├─ README.md                       <─── README general del repositorio
 └─ ...

```

## Iniciando el servicio

Para una prueba básica inicial del servicio, copiar los archivos `app.js` y `/server/index.js` de este repositorio.
 Acceso mediante http://localhost:8080
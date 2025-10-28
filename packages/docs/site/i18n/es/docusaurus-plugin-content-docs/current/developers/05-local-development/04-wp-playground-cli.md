---
title: Playground CLI
slug: /developers/local-development/wp-playground-cli
description: Una herramienta de línea de comandos para desarrollo y pruebas de WordPress con configuración rápida, configuración flexible y dependencias mínimas.
---

<!-- # Playground CLI -->

# Playground CLI

<!-- [@wp-playground/cli](https://www.npmjs.com/package/@wp-playground/cli) is a command-line tool that simplifies the WordPress development and testing flow. You can use Playground CLI to auto-mount a directory with a plugin, theme, or WordPress installation. If you need flexibility, you can use mounting commands to personalize your local environment. -->

[@wp-playground/cli](https://www.npmjs.com/package/@wp-playground/cli) es una herramienta de línea de comandos que simplifica el flujo de desarrollo y pruebas de WordPress. Puedes usar Playground CLI para auto-montar un directorio con un plugin, tema o instalación de WordPress. Si necesitas flexibilidad, puedes usar comandos de montaje para personalizar tu entorno local.

<!-- **Key features:** -->

**Características principales:**

<!-- -   **Quick setup**: Set up a local WordPress environment in seconds. -->
<!-- -   **Flexibility**: Allows for configuration to adapt to different scenarios. -->
<!-- -   **Simple environment**: No extra configuration, just a compatible Node version, and you are ready to use it. -->

-   **Configuración Rápida**: Configura un entorno WordPress local en segundos.
-   **Flexibilidad**: Permite la configuración para adaptarse a diferentes escenarios.
-   **Entorno Simple**: Sin configuración extra, solo una versión compatible de Node, y estás listo para usarlo.

<!-- ## Requirements -->

## Requisitos

<!-- The Playground CLI requires Node.js 20.18 or higher, which is the recommended Long-Term Support (LTS) version. You can download it from the [Node.js website](https://nodejs.org/en/download). -->

El Playground CLI requiere Node.js 20.18 o superior, que es la versión recomendada de Soporte a Largo Plazo (LTS). Puedes descargarlo desde el [sitio web de Node.js](https://nodejs.org/en/download).

<!-- ## Quick start -->

## Inicio Rápido

<!-- To run the Playground CLI, open a command line and use the following command: -->

Para ejecutar el Playground CLI, abre una línea de comandos y usa el siguiente comando:

```bash
npx @wp-playground/cli@latest server
```

![Playground CLI en Acción](@site/static/img/developers/npx-wp-playground-server.gif)

<!-- With the previous command, you only get a fresh WordPress instance to test. Most developers will want to test their own work. To test a plugin or a theme, navigate to your project folder and run the CLI with the `--auto-mount` flag: -->

Con el comando anterior, solo obtienes una instancia fresca de WordPress para probar. La mayoría de los desarrolladores querrán probar su propio trabajo. Para probar un plugin o un tema, navega a la carpeta de tu proyecto y ejecuta el CLI con la bandera `--auto-mount`:

```bash
cd my-plugin-or-theme-directory
npx @wp-playground/cli@latest server --auto-mount
```

<!-- ### Auto-mounting different project types -->

### Auto-montaje de diferentes tipos de proyectos

<!-- The `--auto-mount` flag intelligently detects your project type and mounts it appropriately: -->

La bandera `--auto-mount` detecta inteligentemente tu tipo de proyecto y lo monta apropiadamente:

<!-- **Plugin directory:** -->

**Directorio de plugin:**

```bash
cd my-plugin
npx @wp-playground/cli@latest server --auto-mount
```

<!-- **Theme directory:** -->

**Directorio de tema:**

```bash
cd my-theme
npx @wp-playground/cli@latest server --auto-mount
```

<!-- **wp-content directory:** -->

**Directorio wp-content:**

```bash
cd my-site/wp-content
npx @wp-playground/cli@latest server --auto-mount
```

<!-- **Full WordPress installation:** -->

**Instalación completa de WordPress:**

```bash
cd my-wordpress
npx @wp-playground/cli@latest server --auto-mount
```

<!-- **Static HTML/PHP project:** -->

**Proyecto estático HTML/PHP:**

```bash
cd my-static-site
npx @wp-playground/cli@latest server --auto-mount
```

<!-- ### Choosing a WordPress and PHP version -->

### Elegir una Versión de WordPress y PHP

<!-- By default, the CLI loads the latest stable version of WordPress and PHP 8.3 due to its improved performance. To specify your preferred versions, you can use the flag `--wp=<version>` and `--php=<version>`: -->

Por defecto, el CLI carga la última versión estable de WordPress y PHP 8.3 debido a su rendimiento mejorado. Para especificar tus versiones preferidas, puedes usar las banderas `--wp=<version>` y `--php=<version>`:

```bash
npx @wp-playground/cli@latest server --wp=6.8 --php=8.3
```

<!-- ### Setting a custom site URL -->

### Configurar una URL de sitio personalizada

<!-- You can configure a custom site URL for your development environment, which is useful for testing domain-specific functionality or simulating production environments: -->

Puedes configurar una URL de sitio personalizada para tu entorno de desarrollo, lo cual es útil para probar funcionalidad específica de dominio o simular entornos de producción:

```bash
npx @wp-playground/cli@latest server --site-url=https://my-local-dev.test
```

<!-- You can also specify a custom port: -->

También puedes especificar un puerto personalizado:

```bash
npx @wp-playground/cli@latest server --port=3000 --site-url=http://localhost:3000
```

<!-- ### Loading blueprints -->

### Cargar Blueprints

<!-- One way to take your Playground CLI development experience to the next level is to integrate with [Blueprints](/blueprints/getting-started/). For those unfamiliar with this technology, it allows developers to configure the initial state for their WordPress Playground instances. -->

Una forma de llevar tu experiencia de desarrollo con Playground CLI al siguiente nivel es integrar con [Blueprints](/blueprints/getting-started/). Para aquellos que no estén familiarizados con esta tecnología, permite a los desarrolladores configurar el estado inicial para sus instancias de WordPress Playground.

<!-- Using the `--blueprint=<blueprint-address>` flag, developers can run a Playground with a custom initial state. We'll use the example below to do this. -->

Usando la bandera `--blueprint=<blueprint-address>`, los desarrolladores pueden ejecutar un Playground con un estado inicial personalizado. Usaremos el ejemplo a continuación para hacer esto.

**(my-blueprint.json)**

```json
{
	"landingPage": "/wp-admin/options-general.php?page=akismet-key-config",
	"login": true,
	"plugins": ["hello-dolly", "https://raw.githubusercontent.com/adamziel/blueprints/trunk/docs/assets/hello-from-the-dashboard.zip"]
}
```

<!-- CLI command loading a blueprint: -->

Comando CLI cargando un blueprint:

```bash
npx @wp-playground/cli@latest server --blueprint=my-blueprint.json
```

<!-- ### Mounting folders manually -->

### Montar carpetas manualmente

<!-- Some projects have a specific structure that requires a custom configuration; for example, your repository contains all the files in the `/wp-content/` folder. So in this scenario, you can specify to the Playground CLI that it will mount your project from that folder using the `--mount` flag. -->

Algunos proyectos tienen una estructura específica que requiere una configuración personalizada; por ejemplo, tu repositorio contiene todos los archivos en la carpeta `/wp-content/`. Entonces en este escenario, puedes especificar al Playground CLI que montará tu proyecto desde esa carpeta usando la bandera `--mount`.

```bash
npx @wp-playground/cli@latest server --mount=.:/wordpress/wp-content/plugins/MY-PLUGIN-DIRECTORY
```

<!-- **Multiple mounts:** -->

**Múltiples montajes:**

<!-- You can mount multiple directories at once: -->

Puedes montar múltiples directorios a la vez:

```bash
npx @wp-playground/cli@latest server \
  --mount=./my-plugin:/wordpress/wp-content/plugins/my-plugin \
  --mount=./my-theme:/wordpress/wp-content/themes/my-theme
```

<!-- ### Mounting before WordPress installation -->

### Montar antes de la instalación de WordPress

<!-- Consider mounting your WordPress project files before the WordPress installation begins. This approach is beneficial if you want to override the Playground boot process, as it can help connect Playground with `WP-CLI`. The `--mount-before-install` flag supports this process. -->

Considera montar tus archivos de proyecto de WordPress antes de que comience la instalación de WordPress. Este enfoque es beneficioso si quieres sobrescribir el proceso de arranque de Playground, ya que puede ayudar a conectar Playground con `WP-CLI`. La bandera `--mount-before-install` soporta este proceso.

```bash
npx @wp-playground/cli@latest server --mount-before-install=.:/wordpress/
```

<!-- ### Symlink support for monorepos -->

### Soporte de enlaces simbólicos para monorepos

<!-- If you're working in a monorepo or complex project structure where packages are symlinked, you can enable symlink following: -->

Si estás trabajando en un monorepo o estructura de proyecto compleja donde los paquetes están enlazados simbólicamente, puedes habilitar el seguimiento de enlaces simbólicos:

```bash
npx @wp-playground/cli@latest server \
  --follow-symlinks \
  --mount-before-install=./packages/my-plugin:/wordpress/wp-content/plugins/my-plugin
```

:::caution

<!-- Using `--follow-symlinks` can expose files outside mounted directories to Playground and could be a security risk. Only use this flag when you trust the symlink targets. -->

Usar `--follow-symlinks` puede exponer archivos fuera de los directorios montados a Playground y podría ser un riesgo de seguridad. Solo usa esta bandera cuando confíes en los destinos de los enlaces simbólicos.
:::

<!-- ### Understanding data persistence and SQLite location -->

### Entender la Persistencia de Datos y Ubicación de SQLite

<!-- By default, Playground CLI stores WordPress files and the SQLite database in **temporary directories on your operating system**: -->

Por defecto, Playground CLI almacena archivos de WordPress y la base de datos SQLite en **directorios temporales en tu sistema operativo**:

```
<OS-TEMP-DIR>/playground-<random-id>/
├── wordpress/          # Instalación WordPress
├── internal/          # Configuración del runtime de Playground
└── tmp/              # Archivos temporales PHP
```

<!-- **Finding your temp directory:** -->

**Encontrar tu Directorio Temporal:**

<!-- The actual location depends on your OS (these are examples or common possibilities): -->

La ubicación real depende de tu SO (estos son ejemplos o posibilidades comunes):

<!-- -   **macOS/Linux**: May be under `/tmp/` or `/private/var/folders/` (varies by system) -->
<!-- -   **Windows**: `C:\Users\<username>\AppData\Local\Temp\` -->

-   **macOS/Linux**: Puede estar bajo `/tmp/` o `/private/var/folders/` (varía según el sistema)
-   **Windows**: `C:\Users\<username>\AppData\Local\Temp\`

<!-- To see the exact temp directory path being used, run the CLI with the `--verbosity=debug` flag: -->

Para ver la ruta exacta del directorio temporal que se está usando, ejecuta el CLI con la bandera `--verbosity=debug`:

```bash
npx @wp-playground/cli@latest server --verbosity=debug
```

<!-- This will output something like: -->

Esto mostrará algo como:

```
Native temp dir for VFS root:
/private/var/folders/c8/mwz12ycx4s509056kby3hk180000gn/T/node-playground-cli-site-62926--62926-yQNOdvJVIgYC
Mount before WP install: /home ->
/private/var/folders/c8/mwz12ycx4s509056kby3hk180000gn/T/node-playground-cli-site-62926--62926-yQNOdvJVIgYC/home
Mount before WP install: /tmp ->
/private/var/folders/c8/mwz12ycx4s509056kby3hk180000gn/T/node-playground-cli-site-62926--62926-yQNOdvJVIgYC/tmp
Mount before WP install: /wordpress ->
/private/var/folders/c8/mwz12ycx4s509056kby3hk180000gn/T/node-playground-cli-site-62926--62926-yQNOdvJVIgYC/wordpress
```

<!-- **Where is the SQLite database stored?** -->

**¿Dónde se Almacena la Base de Datos SQLite?**

<!-- The database location depends on what you mount: -->

La ubicación de la base de datos depende de lo que montes:

<!-- -   **Auto-mounting wp-content or full WordPress**: -->
<!-- -   Database: `<your-local-project>/wp-content/database/.ht.sqlite` -->
<!-- -   ✅ **Persisted locally** in your project folder -->

-   **Montaje automático de wp-content o WordPress completo**:

    -   Base de datos: `<tu-proyecto-local>/wp-content/database/.ht.sqlite`
    -   ✅ **Persistido localmente** en la carpeta de tu proyecto

<!-- -   **Auto-mounting plugin/theme only**: -->
<!-- -   Database: `<OS-TEMP-DIR>/playground-<id>/wordpress/wp-content/database/.ht.sqlite` -->
<!-- -   ⚠️ **Lost when server stops** (temp directories are cleaned up) -->

-   **Montaje automático solo de plugin/tema**:

    -   Base de datos: `<OS-TEMP-DIR>/playground-<id>/wordpress/wp-content/database/.ht.sqlite`
    -   ⚠️ **Perdido cuando el servidor se detiene** (los directorios temporales se limpian)

<!-- -   **Custom mounts**: Database location follows your mount configuration -->

-   **Montajes personalizados**: La ubicación de la base de datos sigue tu configuración de montaje

<!-- **Automatic cleanup:** -->

**Limpieza Automática:**

<!-- Playground CLI automatically removes temp directories that are: -->

Playground CLI elimina automáticamente los directorios temporales que son:

<!-- -   Older than two days -->
<!-- -   No longer associated with a running process -->

-   Más antiguos de dos días
-   Ya no están asociados con un proceso en ejecución

<!-- **Recommendation:** To persist both your code and database when developing plugins or themes, mount the entire `wp-content` directory instead of just the plugin/theme folder. -->

**Recomendación:** Para persistir tanto tu código como la base de datos al desarrollar plugins o temas, monta el directorio `wp-content` completo en lugar de solo la carpeta del plugin/tema.

<!-- **Example: Mounting wp-content for persistence** -->

**Ejemplo: Montar wp-content para persistencia**

```bash
# Monta tu directorio wp-content completo
cd my-wordpress-project
npx @wp-playground/cli@latest server --mount=./wp-content:/wordpress/wp-content
```

<!-- ## Verbosity and debugging -->

## Verbosidad y depuración

<!-- The CLI supports different verbosity levels to control output, for `quiet`, `normal` and `debug` mode. The default mode is `normal`. For quiet mode, run the server with no output (useful for scripts and automation): -->

El CLI soporta diferentes niveles de verbosidad para controlar la salida, para los modos `quiet`, `normal` y `debug`. El modo por defecto es `normal`. Para el modo silencioso, ejecuta el servidor sin salida (útil para scripts y automatización):

```bash
npx @wp-playground/cli@latest server --verbosity=quiet
```

<!-- Get detailed logging information for troubleshooting, with `debug` mode: -->

Obtén información de registro detallada para solucionar problemas, con el modo `debug`:

```bash
npx @wp-playground/cli@latest server --verbosity=debug
```

<!-- ## Commands and arguments -->

## Comandos y Argumentos

<!-- The Playground CLI is simple, configurable, and unopinionated. You can set it up according to your unique WordPress setup. With the Playground CLI, you can use the following top-level commands: -->

Playground CLI es simple, configurable y sin opiniones. Puedes configurarlo de acuerdo a tu configuración única de WordPress. Con el Playground CLI, puedes usar los siguientes comandos de nivel superior:

<!-- -   **`server`**: (Default) Starts a local WordPress server. -->
<!-- -   **`run-blueprint`**: Executes a Blueprint file without starting a web server. -->
<!-- -   **`build-snapshot`**: Builds a ZIP snapshot of a WordPress site based on a Blueprint. -->

-   **`server`**: (Por defecto) Inicia un servidor WordPress local.
-   **`run-blueprint`**: Ejecuta un archivo Blueprint sin iniciar un servidor web.
-   **`build-snapshot`**: Construye una instantánea ZIP de un sitio WordPress basado en un Blueprint.

<!-- The `server` command supports the following optional arguments: -->

El comando `server` soporta los siguientes argumentos opcionales:

-   `--port=<port>`: El número de puerto para que el servidor escuche. Por defecto es 9400.
-   `--version`: Mostrar número de versión.
-   `--outfile`: Al construir, escribir en este archivo de salida.
-   `--site-url=<url>`: URL del sitio a usar para WordPress. Por defecto es `http://127.0.0.1:{port}`.
-   `--wp=<version>`: La versión de WordPress a usar. Por defecto es la última.
-   `--php=<version>`: Versión de PHP a usar. Opciones: `8.4`, `8.3`, `8.2`, `8.1`, `8.0`, `7.4`, `7.3`, `7.2`. Por defecto es `8.3`.
-   `--auto-mount[=<path>]`: Montar automáticamente un directorio. Si no se proporciona una ruta, monta el directorio de trabajo actual. Puedes montar un directorio WordPress, un directorio de plugin, un directorio de tema, un directorio wp-content, o cualquier directorio que contenga archivos PHP y HTML.
-   `--mount=<mapping>`: Montar manualmente un directorio (puede usarse múltiples veces). Formato: `"/host/path:/vfs/path"`.
-   `--mount-before-install`: Montar un directorio al runtime PHP antes de la instalación de WordPress (puede usarse múltiples veces). Formato: `"/host/path:/vfs/path"`.
-   `--mount-dir`: Montar un directorio al runtime PHP (puede usarse múltiples veces). Formato: `"/host/path"` `"/vfs/path"`.
-   `--mount-dir-before-install`: Montar un directorio antes de la instalación de WordPress (puede usarse múltiples veces). Formato: `"/host/path"` `"/vfs/path"`
-   `--blueprint=<path>`: La ruta a un archivo JSON Blueprint para ejecutar.
-   `--blueprint-may-read-adjacent-files`: Bandera de consentimiento: Permitir que recursos "empaquetados" en un blueprint local lean archivos en el mismo directorio que el archivo blueprint.
-   `--login`: Iniciar sesión automáticamente del usuario como administrador.
-   `--skip-wordpress-setup`: No descargar ni instalar WordPress. Útil si estás montando un directorio WordPress completo.
-   `--skip-sqlite-setup`: No configurar la integración de base de datos SQLite.
-   `--verbosity=<level>`: Salida de logs y mensajes de progreso. Opciones: `quiet`, `normal`, `debug`. Por defecto es `normal`.
-   `--debug`: Imprimir el log de errores de PHP si ocurre un error durante el arranque.
-   `--follow-symlinks`: Permitir que Playground siga enlaces simbólicos montando automáticamente directorios y archivos vinculados simbólicamente encontrados en directorios montados.
-   `--internal-cookie-store`: Habilitar manejo interno de cookies. Cuando está habilitado, Playground administrará cookies internamente usando un HttpCookieStore que persiste cookies entre solicitudes. Cuando está deshabilitado, las cookies se manejan externamente (por ejemplo, por un navegador en entornos Node.js). Por defecto es false.
-   `--xdebug`: Habilitar Xdebug. Por defecto es false.
-   `--experimental-devtools`: Habilitar herramientas de desarrollo experimentales del navegador. Por defecto es false.
-   `--experimental-multi-worker=<number>`: Habilitar soporte experimental multi-worker que requiere un directorio `/wordpress` respaldado por un sistema de archivos real. Pasa un número positivo para especificar el número de workers a usar. De lo contrario, por defecto es el número de CPUs menos uno.

:::info

<!-- On Windows, the path format `/host/path:/vfs/path` can cause issues. To resolve this, use the flags `--mount-dir` and `--mount-dir-before-install`. These flags let you specify host and virtual file system paths in an alternative format`"/host/path"` `"/vfs/path"`. -->

En Windows, el formato de ruta `/host/path:/vfs/path` puede causar problemas. Para resolver esto, usa las banderas `--mount-dir` y `--mount-dir-before-install`. Estas banderas te permiten especificar rutas del host y del sistema de archivos virtual en un formato alternativo `"/host/path"` `"/vfs/path"`.
:::

<!-- ## Need some help with the CLI? -->

## ¿Necesitas ayuda con el CLI?

<!-- With the Playground CLI, you can use the `--help` flag to get the full list of available commands and arguments. -->

Con el Playground CLI, puedes usar la bandera `--help` para obtener la lista completa de comandos y argumentos disponibles.

```bash
npx @wp-playground/cli@latest --help
```

<!-- ## Programmatic usage with JavaScript -->

## Uso Programático con JavaScript

<!-- The Playground CLI can also be controlled programmatically from your JavaScript/TypeScript code using the `runCLI` function. This gives you direct access to all CLI functionalities within your code, which is useful for automating end-to-end tests. Let's cover the basics of using `runCLI`. -->

El Playground CLI también puede ser controlado programáticamente desde tu código JavaScript/TypeScript usando la función `runCLI`. Esto te da acceso directo a todas las funcionalidades del CLI dentro de tu código, lo cual es útil para automatizar pruebas end-to-end. Cubramos los conceptos básicos del uso de `runCLI`.

<!-- ### Running a WordPress instance with a specific version -->

### Ejecutar una instancia de WordPress con una versión específica

<!-- Using the `runCLI` function, you can specify options like the PHP and WordPress versions. In the example below, we request PHP 8.3, the latest version of WordPress, and to be automatically logged in. All supported arguments are defined in the `RunCLIArgs` type. -->

Usando la función `runCLI`, puedes especificar opciones como las versiones de PHP y WordPress. En el ejemplo a continuación, solicitamos PHP 8.3, la última versión de WordPress, y ser automáticamente conectado. Todos los argumentos soportados están definidos en el tipo `RunCLIArgs`.

```TypeScript
import { runCLI, RunCLIArgs, RunCLIServer } from "@wp-playground/cli";

let cliServer: RunCLIServer;

cliServer = await runCLI({
    command: 'server',
    php: '8.3',
    wp: 'latest',
    login: true
} as RunCLIArgs);
```

<!-- To execute the code above, you can set your preferred method. A simple way to execute this code is to save it as a `.ts` file and run it with a tool like `tsx`. For example: `tsx my-script.ts` -->

Para ejecutar el código anterior, puedes establecer tu método preferido. Una forma simple de ejecutar este código es guardarlo como un archivo `.ts` y ejecutarlo con una herramienta como `tsx`. Por ejemplo: `tsx my-script.ts`

<!-- **Testing with specific PHP versions:** -->

**Probando con versiones específicas de PHP:**

```TypeScript
import { runCLI } from "@wp-playground/cli";

const cliServer = await runCLI({
  command: 'server',
  php: '8.0',
  skipWordPressSetup: true,
  skipSqliteSetup: true,
});

// Probar versión de PHP
await cliServer.playground.writeFile(
  '/wordpress/version.php',
  '<?php echo phpversion(); ?>'
);

const versionUrl = new URL('/version.php', cliServer.serverUrl);
const response = await fetch(versionUrl);
const version = await response.text();
console.log('Versión de PHP:', version); // Salida: 8.0.x
```

<!-- ### Setting a custom site URL programmatically -->

### Configurar una URL de sitio personalizada programáticamente

```TypeScript
const cliServer = await runCLI({
  command: 'server',
  'site-url': 'https://my-staging.example.com',
  port: 9500
});

// Verificar que la URL del sitio está configurada correctamente
await cliServer.playground.writeFile(
  '/wordpress/check-url.php',
  '<?php require_once "/wordpress/wp-load.php"; echo get_option("siteurl"); ?>'
);

const checkUrl = new URL('/check-url.php', cliServer.serverUrl);
const response = await fetch(checkUrl);
console.log('URL del sitio:', await response.text());
```

<!-- ### Controlling verbosity programmatically -->

### Controlar la verbosidad programáticamente

```TypeScript
import { runCLI } from "@wp-playground/cli";
import { logger } from '@php-wasm/logger';

const cliServer = await runCLI({
  command: 'server',
  verbosity: 'debug' // o 'quiet' o 'normal'
});

// Agregar registro personalizado
logger.debug('Mensaje de depuración personalizado');
```

<!-- ### Setting a blueprint -->

### Configurar un Blueprint

<!-- You can provide a blueprint in two ways: either as an object literal directly passed to the `blueprint` property, or as a string containing the path to an external `.json` file. -->

Puedes proporcionar un blueprint de dos maneras: ya sea como un objeto literal pasado directamente a la propiedad `blueprint`, o como una cadena que contiene la ruta a un archivo `.json` externo.

```TypeScript
import { runCLI, RunCLIServer } from "@wp-playground/cli";

let cliServer: RunCLIServer;

cliServer = await runCLI({
  command: 'server',
  wp: 'latest',
  blueprint: {
    steps: [
        {
          "step": "setSiteOptions",
          "options": {
              "blogname": "Título del Blueprint",
              "blogdescription": "Una gran descripción de blog"
          }
        }
    ],
  },
});
```

<!-- For full type-safety when defining your blueprint object, you can import and use the `BlueprintDeclaration` type from the `@wp-playground/blueprints` package: -->

Para una seguridad de tipos completa al definir tu objeto blueprint, puedes importar y usar el tipo `BlueprintDeclaration` del paquete `@wp-playground/blueprints`:

```TypeScript
import type { BlueprintDeclaration } from '@wp-playground/blueprints';

const myBlueprint: BlueprintDeclaration = {
  landingPage: "/wp-admin/",
  steps: [
    {
      "step": "installTheme",
      "themeData": {
        "resource": "wordpress.org/themes",
        "slug": "twentytwentyone"
      },
      "options": {
        "activate": true
      }
    }
  ]
};
```

<!-- ### Mounting a plugin programmatically -->

### Montar un plugin programáticamente

<!-- You can mount local directories programmatically using `runCLI`. The options `mount` and `mount-before-install` are available. The `hostPath` property expects a path to a directory on your local machine. This path should be relative to where your script is being executed. -->

Puedes montar directorios locales programáticamente usando `runCLI`. Las opciones `mount` y `mount-before-install` están disponibles. La propiedad `hostPath` espera una ruta a un directorio en tu máquina local. Esta ruta debe ser relativa a donde se está ejecutando tu script.

```TypeScript
cliServer = await runCLI({
  command: 'server',
  login: true,
  'mount-before-install': [
    {
      hostPath: './[my-plugin-local-path]',
      vfsPath: '/wordpress/wp-content/plugins/my-plugin',
    },
  ],
});
```

<!-- **Auto-mounting programmatically:** -->

**Auto-montaje programático:**

```TypeScript
import { runCLI } from "@wp-playground/cli";
import process from 'node:process';

// Cambiar a tu directorio de proyecto
process.chdir('./my-plugin');

const cliServer = await runCLI({
  command: 'server',
  autoMount: '' // Cadena vacía activa la detección automática
});
```

<!-- ### Combining mounts with blueprints -->

### Combinar montajes con blueprints

<!-- You can combine mounting parts of the project with blueprints, for example: -->

Puedes combinar el montaje de partes del proyecto con blueprints, por ejemplo:

```TypeScript
import { runCLI, RunCLIArgs, RunCLIServer } from "@wp-playground/cli";

let cliServer: RunCLIServer;

cliServer = await runCLI({
    command: 'server',
    php: '8.3',
    wp: 'latest',
    login: true,
    mount: [
        {
            "hostPath": "./plugin/",
            "vfsPath": "/wordpress/wp-content/plugins/playwright-test"
        }
    ],
    blueprint: {
        steps: [
            {
                "step": "activatePlugin",
                "pluginPath": "/wordpress/wp-content/plugins/playwright-test/plugin-playwright.php"
            }
        ]
    }
} as RunCLIArgs);
```

<!-- **Multiple mounts with blueprints:** -->

**Múltiples montajes con blueprints:**

```TypeScript
const cliServer = await runCLI({
  command: 'server',
  mount: [
    {
      hostPath: './my-plugin',
      vfsPath: '/wordpress/wp-content/plugins/my-plugin'
    },
    {
      hostPath: './my-theme',
      vfsPath: '/wordpress/wp-content/themes/my-theme'
    }
  ],
  blueprint: {
    steps: [
      {
        step: 'activatePlugin',
        pluginPath: '/wordpress/wp-content/plugins/my-plugin/plugin.php'
      },
      {
        step: 'activateTheme',
        themeFolderName: 'my-theme'
      }
    ]
  }
});
```

<!-- **Complex blueprint with multiple configurations:** -->

**Blueprint complejo con múltiples configuraciones:**

```TypeScript
const cliServer = await runCLI({
  command: 'server',
  php: '8.3',
  wp: 'latest',
  login: true,
  mount: [
    {
      hostPath: './my-plugin',
      vfsPath: '/wordpress/wp-content/plugins/my-plugin'
    }
  ],
  blueprint: {
    landingPage: '/wp-admin/plugins.php',
    steps: [
      {
        step: 'activatePlugin',
        pluginPath: '/wordpress/wp-content/plugins/my-plugin/plugin.php'
      },
      {
        step: 'setSiteOptions',
        options: {
          blogname: 'Sitio de Prueba de Plugin',
          permalink_structure: '/%postname%/'
        }
      },
      {
        step: 'runPHP',
        code: '<?php update_option("my_plugin_setting", "test_value"); ?>'
      }
    ]
  }
});
```

<!-- ### Mode selection (Blueprint v2) -->

### Selección de modo (Blueprint v2)

<!-- You can specify different modes when working with Blueprint v2: -->

Puedes especificar diferentes modos cuando trabajas con Blueprint v2:

<!-- **Creating a new site:** -->

**Crear un nuevo sitio:**

```TypeScript
import { runCLI } from "@wp-playground/cli";

const cliServer = await runCLI({
  command: 'server',
  'experimental-blueprints-v2-runner': true,
  mode: 'create-new-site',
  'mount-before-install': [
    {
      hostPath: './my-new-site',
      vfsPath: '/wordpress'
    }
  ]
});
```

<!-- **Applying to an existing site:** -->

**Aplicar a un sitio existente:**

```TypeScript
const cliServer = await runCLI({
  command: 'server',
  'experimental-blueprints-v2-runner': true,
  mode: 'apply-to-existing-site',
  'mount-before-install': [
    {
      hostPath: './existing-wordpress',
      vfsPath: '/wordpress'
    }
  ],
  blueprint: {
    steps: [
      {
        step: 'setSiteOptions',
        options: {
          blogname: 'Nombre de Sitio Actualizado'
        }
      }
    ]
  }
});
```

<!-- ## Automated testing -->

## Pruebas automatizadas

<!-- ### Integration testing with Vitest -->

### Pruebas de integración con Vitest

<!-- The programmatic API is excellent for automated testing. Here's a complete example using Vitest: -->

La API programática es excelente para pruebas automatizadas. Aquí hay un ejemplo completo usando Vitest:

```TypeScript
import { describe, test, expect, afterEach } from 'vitest';
import { runCLI, RunCLIServer } from "@wp-playground/cli";

describe('Pruebas de Mi Plugin', () => {
  let cliServer: RunCLIServer;

  afterEach(async () => {
    if (cliServer) {
      await cliServer[Symbol.asyncDispose]();
    }
  });

  test('el plugin se activa con éxito', async () => {
    cliServer = await runCLI({
      command: 'server',
      mount: [
        {
          hostPath: './my-plugin',
          vfsPath: '/wordpress/wp-content/plugins/my-plugin'
        }
      ],
      blueprint: {
        steps: [
          {
            step: 'activatePlugin',
            pluginPath: '/wordpress/wp-content/plugins/my-plugin/plugin.php'
          }
        ]
      }
    });

    const homeUrl = new URL('/', cliServer.serverUrl);
    const response = await fetch(homeUrl);

    expect(response.status).toBe(200);
    const html = await response.text();
    expect(html).toContain('Mi Plugin');
  });

  test('la página de configuración del plugin se carga', async () => {
    cliServer = await runCLI({
      command: 'server',
      login: true, // Auto-login como admin
      mount: [
        {
          hostPath: './my-plugin',
          vfsPath: '/wordpress/wp-content/plugins/my-plugin'
        }
      ],
      blueprint: {
        steps: [
          {
            step: 'activatePlugin',
            pluginPath: '/wordpress/wp-content/plugins/my-plugin/plugin.php'
          }
        ]
      }
    });

    const settingsUrl = new URL(
      '/wp-admin/options-general.php?page=my-plugin',
      cliServer.serverUrl
    );
    const response = await fetch(settingsUrl);

    expect(response.status).toBe(200);
  });
});
```

<!-- ### Testing theme customizations -->

### Probar personalizaciones de temas

```TypeScript
test('el tema muestra encabezado personalizado', async () => {
  cliServer = await runCLI({
    command: 'server',
    mount: [
      {
        hostPath: './my-theme',
        vfsPath: '/wordpress/wp-content/themes/my-theme'
      }
    ],
    blueprint: {
      steps: [
        {
          step: 'installTheme',
          themeData: {
            resource: 'vfs',
            path: '/wordpress/wp-content/themes/my-theme'
          }
        },
        {
          step: 'activateTheme',
          themeFolderName: 'my-theme'
        }
      ]
    }
  });

  const homeUrl = new URL('/', cliServer.serverUrl);
  const response = await fetch(homeUrl);
  const html = await response.text();

  expect(html).toContain('<header class="site-header">');
});
```

<!-- ### Testing a plugin with different WordPress/PHP versions -->

### Probar un plugin con diferentes versiones de WordPress/PHP

```TypeScript
test('el plugin funciona con WordPress 6.4 y PHP 8.0', async () => {
  cliServer = await runCLI({
    command: 'server',
    php: '8.0',
    wp: '6.4',
    mount: [
      {
        hostPath: './my-plugin',
        vfsPath: '/wordpress/wp-content/plugins/my-plugin'
      }
    ],
    blueprint: {
      steps: [
        {
          step: 'activatePlugin',
          pluginPath: '/wordpress/wp-content/plugins/my-plugin/plugin.php'
        }
      ]
    }
  });

  const homeUrl = new URL('/', cliServer.serverUrl);
  const response = await fetch(homeUrl);

  expect(response.status).toBe(200);
});
```

<!-- ## Advanced configuration -->

## Configuración avanzada

<!-- ### Skip WordPress and SQLite setup -->

### Omitir configuración de WordPress y SQLite

<!-- When you only need to test PHP code without WordPress, you can skip the setup for faster testing: -->

Cuando solo necesitas probar código PHP sin WordPress, puedes omitir la configuración para pruebas más rápidas:

```TypeScript
const cliServer = await runCLI({
  command: 'server',
  skipWordPressSetup: true,
  skipSqliteSetup: true,
  php: '8.3'
});

// Escribir y probar scripts PHP personalizados
await cliServer.playground.writeFile(
  '/wordpress/test.php',
  '<?php echo "Hola desde PHP!"; ?>'
);

const testUrl = new URL('/test.php', cliServer.serverUrl);
const response = await fetch(testUrl);
console.log(await response.text()); // Salida: Hola desde PHP!
```

<!-- ### Error handling -->

### Manejo de errores

```TypeScript
import { runCLI } from "@wp-playground/cli";

try {
  const cliServer = await runCLI({
    command: 'server',
    debug: true // Habilitar registro de errores PHP
  });

  // Tu código de prueba aquí

} catch (error) {
  console.error('Error al iniciar el servidor:', error);
}
```

<!-- ### Following symlinks programmatically -->

### Seguir enlaces simbólicos programáticamente

```TypeScript
const cliServer = await runCLI({
  command: 'server',
  followSymlinks: true,
  'mount-before-install': [
    {
      hostPath: './symlinked-directory',
      vfsPath: '/wordpress/wp-content/plugins/my-plugin'
    }
  ]
});
```

:::caution

<!-- Using symlinks can expose files outside mounted directories. Only enable this feature when you trust the symlink targets. -->

Usar enlaces simbólicos puede exponer archivos fuera de los directorios montados. Solo habilita esta función cuando confíes en los destinos de los enlaces simbólicos.
:::

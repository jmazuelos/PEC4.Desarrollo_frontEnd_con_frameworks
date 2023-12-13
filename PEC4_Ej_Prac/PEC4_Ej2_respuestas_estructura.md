# 1. ¿Qué comando debes utilizar para crear un nuevo proyecto Angular utilizando Angular CLI denominado ecommerce? Con Angular Cli crea el proyecto angular ecommerce y explica brevemente la estructura y ficheros que ha generado Angular CLI:

• Ficheros de configuración en la raíz del proyecto:
  - tsconfing.app.json: configuración específica de TypeScript para la aplicación de Angular.
  - angular.json: configuración principal de Angular.
  - package.json: configuración de npm.
  - .editorconfig: configuración del editor para mantener la consistencia en diferentes editores de código.
  - .gitignore: configuración de los archivos y directorios que Git debe ignorar al realizar seguimiento  de cambios.
  - tsconfig.json: configuración de TypeScript para el proyecto de Angular.
  -tsconfig.spec.json: configuración específica de TypeScript para las pruebas unitarias en el proyecto de Angular

• Directorio node_modules: contiene todas las dependencias de Node.js y paquetes de JavaScript.
• Directorio src: contiene todos los archivos y carpetas que constituyen el código fuente de la aplicación.
  - index.html: punto de entrada de la aplicación, conteniendo el marcado HTML básico que enlaza Angular con los scripts y estilos necesarios.
  - main.ts: punto de entrada de la aplicación, conteniendo el código TypeScript que inicia la aplicación y realiza la configuración inicial del entorno de ejecución.
  - styles.css: contiene los estilos globales aplicados a toda la aplicación.
  - Directorio assets: almacena recursos estáticos que la aplicación pueda necesitar (imágenes, archivos de estilo, fuentes, archivos de datos como json, git, etc.). 
  - Directorio app: organiza los componentes, servicios, directivas y otros elementos de Angular. 
    ▪ Ficheros app.component.*: conjunto de archivos que definen el componente principal de la aplicación.
    ▪ Fichero app.module.ts: define el módulo principal de la aplicación que agrupa y organiza los componentes, servicios y otros recursos de la aplicación, además, se especifican las dependencias del módulo y se configuran las rutas, entre otras cosas.

# 2. Explica cada uno de los siguientes decoradores generados por Angular CLI, detallando cada una de las propiedades que se definen:

• app.module.ts - @NgModule: decorador que se utiliza para definir metadatos sobre un módulo, que es una forma de organizar y encapsular componentes, servicios, directivas y otros bloques de construcción dentro de la aplicación.
  - declarations: define los componentes, directivas y pipes que pertenecen a este módulo.
  - imports: importa otros módulos cuyos elementos son necesarios para este módulo.
  - providers: registra los proveedores de servicios para la inyección de dependencias.
  - bootstrap: especifica el componente principal que Angular debe inicializar y renderizar cuando se inicia la aplicación.
• app.component.ts - @Component: decorador que se utiliza para definir metadatos sobre un componente, que encapsula la lógica y la presentación de una parte específica de la interfaz de usuario. 
  - selector: selector CSS que identifica el elemento en el DOM donde se renderizará el componente.
  - templateUrl: URL del archivo HTML que define la apariencia del componente.
  - styleUrls: lista de URLs de archivos CSS que se aplican al componente.

# 3. ¿Es posible poder inyectar el template y los estilos en línea de un componente sin necesidad de especificarlos en templateUrl, styleUrls? ¿Es recomendable hacer esto?

Sí, se podrían inyectar directamente en el decorador, pero el reciclaje de los mismos se volvería más complejo al estar directamente inline, además, la legibilidad y mantenibilidad del código puede ser más difícil a medida que vayan creciendo. Por tanto, sería razonable su uso en componentes simples y pequeños, pero para los más complejos no es nada recomendable.
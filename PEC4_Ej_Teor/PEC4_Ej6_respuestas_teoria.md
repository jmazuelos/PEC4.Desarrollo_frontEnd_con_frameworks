# 1. ¿Cuáles son los style encapsulation de los componentes? Pon un ejemplo de uso de cada uno de ellos.
 - Emulated: modo de encapsulación predeterminado de Angular. Los estilos CSS de nuestro componente se aplican solo a la plantilla del componente, evitando que afecten a otros. 

//Archivo del componente generado my-component.component.ts
@Component({
 selector: 'my-component',
 template: <p>the color of the paragraph is blue</p>,
 styles: ['p { color: blue; }'],
 encapsulation: ViewEncapsulation.Emulated //No es necesario porque es el modo predeterminado
})
export class MyComponent {
  // Código del componente
}

//Archivo app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { MyComponent } from './my-component.component';

@NgModule({
  declarations: [MyComponent],
  imports: [BrowserModule],
  bootstrap: [MyComponent]
})
export class AppModule { }

//Plantilla del componente principal app.component.html, incluyendo el componente 'my-component'
<!DOCTYPE html>
<html>
  <head>
  </head>
  <body>
    <my-app>
      <p>the color of the paragraph is not blue</p>
      <my-component></my-component>
    </my-app>
  </body>
</html>

En este ejemplo, el estilo definido en el componente 'my-component' (color azul para los elementos <p>) se aplica solo a ese componente específico y no afecta a otros componentes de la aplicación, como en el caso del elemento <p> que se encuentra justo debajo de <my-app>.

 - None: en este modo los estilos no están encapsulados y se aplican globalmente a la aplicación, de manera que los estilos definidos en un componente pueden afectar a otros componentes.

//Archivo del componente generado my-component.component.ts
@Component({
 selector: 'my-component',
 template: <p>the color of the paragraph is blue</p>,
 styles: ['p { color: blue; }'],
 encapsulation: ViewEncapsulation.None
})
export class MyComponent {
  // Código del componente
}

//Archivo app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { MyComponent } from './my-component.component';

@NgModule({
  declarations: [MyComponent],
  imports: [BrowserModule],
  bootstrap: [MyComponent]
})
export class AppModule { }

//Plantilla del componente principal app.component.html, incluyendo el componente 'my-component'
<!DOCTYPE html>
<html>
  <head>
  </head>
  <body>
    <my-app>
      <p>the color of the paragraph is blue</p>
      <my-component></my-component>
    </my-app>
  </body>
</html>

En este caso, el estilo definido en el componente 'my-component' (color azul para los elementos <p>) afectará no solo al componente actual, sino que se aplicará globalmente en toda la aplicación. 

 - Native: los estilos se aplican utilizando el Shadow DOM (explicado en la siguiente cuestión), lo que proporciona un mayor nivel de encapsulación.

//Archivo del componente generado my-component.component.ts
@Component({
 selector: 'my-component',
 template: <p>the color of the paragraph is blue</p>,
 styles: ['p { color: blue; }'],
 encapsulation: ViewEncapsulation.Native
})
export class MyComponent {
  // Código del componente
}

//Archivo app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { MyComponent } from './my-component.component';

@NgModule({
  declarations: [MyComponent],
  imports: [BrowserModule],
  bootstrap: [MyComponent]
})
export class AppModule { }

//Plantilla del componente principal app.component.html, incluyendo el componente 'my-component'
<!DOCTYPE html>
<html>
  <head>
  </head>
  <body>
    <my-app>
      <p>the color of the paragraph is not blue</p>
      <my-component></my-component>
    </my-app>
  </body>
</html>

El estilo definido en el componente 'my-component' (color azul para los elementos <p>) se aplicará utilizando el Shadow DOM. La encapsulación de estilos nativa asegura que estos estilos no afecten a otros componentes en la aplicación y proporciona un alto grado de encapsulación. 

# 2. ¿Qué es el shadow DOM?

Shadow DOM es una tecnología que soluciona el alcance que tienen HTML, CSS y JavaScript de aplicar estilos de manera global, proporcionando la capacidad de aplicar un estilo a un componente (evitando que los estilos se filtren y afecten al resto de la aplicación) y también la capacidad de aislar y hacer que el DOM sea autónomo.

# 3. ¿Qué es el changeDetection?

changeDetection identifica y reacciona a los cambios en el estado de la aplicación para actualizar la interfaz de usuario. Se utiliza para determinar cómo se deben actualizar las vistas cuando cambian los datos en la aplicación, optimizando el rendimiento y evitando la actualización innecesaria de la interfaz de usuario.

# 4. ¿Qué diferencias existen entre las estrategias Default y OnPush? ¿Cuándo debes usar una y otra? Ventajas e inconvenientes.

Change​DetectionStrategy.Default hace que Angular decida cuándo necesita actualizar la interfaz de usuario, mientras que ChangeDetectionStrategy.OnPush permite ser explícitos y decirle a Angular cuándo necesita actualizar la interfaz de usuario manualmente. Esto significa que después del renderizado inicial, dependerá del desarrollador informarle a Angular cuando debe cambiar el valor.

En aplicaciones pequeñas o medianas, Change​DetectionStrategy.Default es adecuada. En aplicaciones grandes, OnPush puede proporcionar mejor rendimiento. Además, si los datos cambian con poca frecuencia, OnPush puede ser la mejor opción.

- Ventajas de Change​DetectionStrategy.Default: mayor sencillez de uso (no requiere configuración), actualizaciones automáticas.
- Inconvenientes de Change​DetectionStrategy.Default: menor rendimiento en aplicaciones pesadas, actualizaciones innecesarias.

- Ventajas de Change​DetectionStrategy.OnPush: mayor rendimiento, mayor control sobre cuándo se deben realizar las verificaciones de cambios.
- Inconvenientes de Change​DetectionStrategy.OnPush: complejidad adicional por la configuración, menor automatización.

# 5. Explica con detalle el ciclo de vida de los componentes. Haz hincapié en cuándo se disparan los hooks OnChanges, OnInit, AfterViewInit y OnDestroy, puesto que son los más utilizados

En Angular, el ciclo de vida de un componente se compone de varios pasos que se ejecutan en un orden específico, incluyendo 'hooks' de ciclo de vida como OnInit, AfterContentInit, y OnDestroy. Algunos de estos 'hooks', terminados en "Init," se llaman solo una vez durante la inicialización del componente, mientras que otros, como OnDestroy, se ejecutan solo una vez al destruir el componente.

Cada paso del ciclo de vida requiere que se implemente una interfaz correspondiente, que proporciona una función específica que debe ser implementada en el componente.

Además, hay conceptos adicionales llamados ViewChildren y ContentChildren. ViewChildren se refiere a componentes secundarios cuyos selectores aparecen directamente en la plantilla del componente, mientras que ContentChildren se refiere a componentes secundarios proyectados en la vista pero no incluidos directamente en la plantilla del componente.

- OnChanges: se llama justo después del constructor a configurar y cada vez que cambian las propiedades de entrada de una directiva. Se llama antes del OnInit.
- OnInit: se ejecuta después de que el componente se ha inicializado. Permite realizar cualquier inicialización única específica de su componente o directiva, cargándose datos desde el servidor, por ejemplo, en lugar del constructor.
- AfterViewInit: se activa después de que todos los componentes secundarios que se usan directamente en la plantilla del componente hayan terminado de inicializarse y sus vistas se hayan actualizado con enlaces.
- OnDestroy: se llama cuando un componente está a punto de ser destruido y eliminado de la interfaz de usuario.
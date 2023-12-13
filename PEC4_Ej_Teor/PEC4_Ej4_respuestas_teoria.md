# 1. Explica qué son y cuándo se deberían utilizar las siguientes variables locales de la directiva estructural NgFor:
  • index: devuelve el índice actual del elemento en la iteración. Se debería utilizar para conocer los índices de los elementos a medida que se recorre la iteración.
  • even: permite verificar si el índice actualizado en la iteración es par. Se debería utilizar en situaciones donde se requiere aplicar una lógica específica según la paridad.
  • odd: mismo caso que el anterior, pero dependiendo de la imparidad.
  • first: indica si el elemento actualizado en la iteración es el primero. Se debería utilizar para aplicar una lógica determinada a los primeros elementos.
  • last: mismo caso que el anterior, pero aplicado a los últimos elementos.

# 2. ¿Para qué sirve la opción trackBy de la directiva estructural NgFor? Pon ejemplos de uso.
trackBy se encarga de gestionar eficientemente la actualización de listas, permitiendo a los desarrolladores especificar un criterio personalizado para identificar elementos y evitar la recreación innecesaria de instancias durante cambios en los datos ya que, de forma predeterminada, Angular reutilizará la referencia del elemento anterior de un objeto mientras los datos del mismo no cambien. En caso contrario, se pueden recrear instancias de elementos innecesariamente, perdiendo eficiencia.

Ejemplo 1. Suponiendo el caso del ejercicio 3, si el código de la clase de article-item.components.ts es el siguiente: 

export class ArticleItemComponent {
  @Input() articles: Array<Article>

  trackArticleByQuantityInCart(index, article) {
    return article.quantityInCart;
  }

  //Resto de código (otros métodos y propiedades)
}

y, además de la lista de objetos (de tipo Article) inicializada en app.component.ts, se modifica el código de article-item.components.html:

<div class="article-item" *ngFor = *ngFor="let article of articles; index as i; trackBy: trackArticleByQuantityInCart">
  <!-- resto de código html  -->
</div>

'trackBy: trackArticleByQuantityInCart' se asegura de que Angular llame a esta función para descubrir cómo identificar elementos individuales, en lugar de usar el objeto referencia.

Esto garantiza que incluso si recargamos todos los articles del servidor (cambiando así todas las referencias de objetos), Angular seguirá mirando el código article para decidir si reutilizar o no los elementos presentes en el DOM.

Ejemplo 2. Caso más sencillo.

//Función del componente en el archivo item.component.ts
trackByFn(index, item) {
  return item.id; // Debe ser un identificador único para cada elemento
}

//Etiqueta que contiene ngFor en el template del componente (archivo item.component.html)
<div *ngFor="let item of items; trackBy: trackByFn">{{ item.name }}</div>

'trackBy: trackByFn' es una función que devuelve un identificador único para cada elemento. Angular utilizará esta información para realizar actualizaciones eficientes del DOM, evitando recrear elementos innecesariamente, incluso, cuando se cambien las referencias del objeto.

# 3. ¿Es posible ejecutar dos directivas estructurales simultáneamente? Explica la razón tanto si es posible como si no lo es.

En general, Angular permite la ejecución simultánea de dos o más directivas estructurales en el mismo elemento. Por ejemplo, puedes tener un *ngIf y un *ngFor aplicados al mismo elemento. Sin embargo, la razón por la que esto puede ser problemático es que algunas directivas estructurales pueden afectar la estructura del DOM, y la ejecución simultánea de ciertas combinaciones podría no dar como resultado el comportamiento deseado. Por ejemplo, *ngIf podría afectar la existencia de un elemento antes de que *ngFor tenga la oportunidad de iterar sobre él.

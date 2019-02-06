# Borrando objectos de nuestra base de datos

En esta lección, terminaremos de crear nuestra aplicación, la única funcionalidad que falta es la capacidad de eliminar contenido de la base de datos.

Afortunadamente, ya hemos hecho todo el trabajo posible para esto, todo lo que necesitamos ahora es una forma de hacer clic en una función que elimine el programa de televisión.

Primero, abre `app.component.html` y busca nuestra tarjeta TVShow, recuerda que se ve así:

```html
<div class="card" *ngFor="let show of showList | async">
  <img (click)="updatePicture(show.id)" [src]="show.picture" width="50px" height="50px" />
  <input (change)="updateName(show.id, $event.target.value)" [value]="show.name" />
</div>
```

Agreguemos un botón dentro de esa tarjeta que active una función `remove()` que pasa el ID del programa:

```html
<div class="card" *ngFor="let show of showList | async">
  <img (click)="updatePicture(show.id)" [src]="show.picture" width="50px" height="50px" />
  <input (change)="updateName(show.id, $event.target.value)" [value]="show.name" />
  <button (click)="remove(show.id)">❌</button>
</div>
```

No hay nada extraño, estamos creando un botón, y llamando a la función `remove()`, ahora vamos a pasar a nuestro archivo `app.component.ts` y creamos esa función de eliminación:

```js
remove(id: string) {
  this.showCollection.doc(id).delete();
}
```

La función va a nuestro programa de TV específico y llama al método `.delete()`. ¡Y eso es! Cada vez que haga clic en la X, se eliminará el programa de la base de datos de Firestore.

## No borrar por accidente

Ok, esto no es necesario, pero es una buena práctica, así que agreguemos una alerta de confirmación antes de llamar a la función de eliminación.

Lo último que queremos hacer es hacer clic por accidente y perder permanentemente un registro de la base de datos.

Usaremos el indicador de confirmación nativo del navegador, así que haz que la función `remove()` tenga este aspecto:

```js
remove(id: string) {
  if(confirm('Are you sure to delete the show from your list?')){
    this.showCollection.doc(id).delete();
  }
}
```

De esa manera, la aplicación mostrará una alerta preguntadote si estás segur@ de querer eliminar el registro.

## Siguientes pasos

Enhorabuena, ya has terminado con el taller. Ahora deberías tener una aplicación completamente funcional. Si está preparado para un nuevo desafío, pasemos a una sección de bono donde aprenderás un poco más sobre las mejores prácticas de Angular.

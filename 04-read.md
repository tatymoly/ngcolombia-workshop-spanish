# Leyendo tu data

En la lección anterior, aprendimos a almacenar datos en Firestore. Ahora es el momento de aprender a leer esos datos y mostrarlos dentro de nuestra aplicación.

Recuerda en la última lección cuando hicimos esto:

```js
constructor(private db: AngularFirestore) {
  this.showCollection = db.collection('shows');
  this.showList = this.showCollection.valueChanges();
}
```

Ese trozo de código allí es suficiente para crear una referencia a nuestros programas de televisión y luego transformarlo en un "Observable" que podemos mostrar en nuestra página.

Todo lo que necesitas hacer ahora es agregar el marcado (_El HTML_) y la aplicación mostrará las tarjetas que comienza a crear.

Así que muevete a nuestro archivo `app.component.ts` y agrega el siguiente código:

```html
<div class="card" *ngFor="let show of showList | async">
  <img [src]="show.picture" width="50px" height="50px" />
  <input [value]="show.name" />
</div>
```

Esto es lo que está pasando:

- `*ngFor="let show of showList | async"` le está diciendo a nuestra aplicación angular que el `<div>` va a ver la propiedad `showList` y se repetirá con cada programa que encuentre dentro.
- El pipe `async` le dice a la aplicación que `showList` tiene un valor asíncrono.
- `<img [src]="show.picture" width="50px" height="50px" />` está accediendo a la propiedad `picture` de nuestro programa y configurándola como la fuente de la imagen.
- `<input [value]="show.name" />` está creando una entrada rellenada previamente con el nombre de nuestro programa de televisión.

Ahora mismo deberías poder ver los programas de televisión que agregas a tu base de datos, así que adelante, haz clic en el botón '**ADD**' unas cuantas veces y observa cómo comienzan a aparecer las tarjetas en tu página.

## Actualizando objetos desde nuestra base de datos.

Ahora que podemos ver nuestras tarjetas, el siguiente paso sería poder actualizar parte de la información del programa, como el nombre del programa y la imagen (_recuerden, estamos mostrando una imagen al azar_)

Para eso modifiquemos el HTML que acabamos de escribir, queremos agregar controladores de eventos en la imagen y la entrada para que cuando los usuarios hagan clic en la imagen o escriban el nombre del programa, podamos llamar a las funciones que guardan esa información en Firebase.

En este momento se ve así:

```html
<div class="card" *ngFor="let show of showList | async">
  <img [src]="show.picture" width="50px" height="50px" />
  <input [value]="show.name" />
</div>
```

Agreguemos un controlador de clic para la imagen que activa una función llamada `updatePicture()` y tome el ID del programa como un parámetro:

```html
<div class="card" *ngFor="let show of showList | async">
  <img (click)="updatePicture(show.id)" [src]="show.picture" width="50px" height="50px" />
  <input [value]="show.name" />
</div>
```

Ahora vamos a crear un controlador de cambios en el input, que llama a la función `updateName()` cuando cambiamos el nombre del programa:

```html
<div class="card" *ngFor="let show of showList | async">
  <img (click)="updatePicture(show.id)" [src]="show.picture" width="50px" height="50px" />
  <input (change)="updateName(show.id, $event.target.value)" [value]="show.name" />
</div>
```

Observe cómo estamos pasando la identificación del programa y el texto que se encuentra en el input.

Ahora debemos ir a nuestra página `app.component.ts` y crear ambas funciones, comencemos con la imagen de actualización uno:

```js
updatePicture(id: string) {
  const picture = prompt('Please enter an image URL:')
  if (picture) {
    this.showCollection.doc(id).update({ picture });
  }
}
```

Esa función es:

- Llamar a la alerta de aviso nativa del navegador que le solicita la nueva URL de la imagen.
- Obtener todo lo que escribes y asignar a la variable `imagen`.
- Si escribes algo, esto irá dentro del documento de Firestore y actualizará la propiedad `picture`.

Vamos a hacer lo mismo para nuestra la función de actualización de nombre:

```js
updateName(id: string, name: string) {
  this.showCollection.doc(id).update({ name });
}
```

Estamos creando una función que entra en nuestro programa y actualiza la propiedad del nombre.

## `.set()` vs `.update()`

Es posible que haya notado que hemos usado 2 formas diferentes de agregar datos a Firestore, una usando el método `.set()` y la otra usando el método `.update()

¿Cuál es la diferencia entre estos dos?

Bueno, `.set()` es destructivo y `.update()` no lo es.

Eso significa que cuando uses `.set({name: 'Jorge'})` borrará todas las propiedades de ese objeto y dejará solo la propiedad de nombre.

Y cuando uses `.update({name: 'Jorge'})` buscará la propiedad `name` y cambiará su valor, todas las demás propiedades seguirán siendo las mismas.

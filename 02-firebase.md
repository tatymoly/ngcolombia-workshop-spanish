# Fire-qué!?

Para esta aplicación, usaremos Firebase como nuestro backend. Si no sabes qué es Firebase, es una plataforma completa proporcionada por Google que puede manejar casi todos los aspectos de la infraestructura de tu aplicación.

Por ejemplo, proporcionan una base de datos, almacenamiento de archivos, notificaciones push, hosting, entre otras cosas.

Para este taller, usaremos Firestore, su nueva base de datos NoSQL que tiene funciones integradas en tiempo real y fuera de línea.

Esto nos da dos cosas listas para usar, el contenido que cambia en la base de datos se actualiza en tiempo real en cada aplicación que está conectada y se sincroniza sin conexión sin que tu hagas un trabajo adicional.

Puedes obtener más información sobre Firebase en [https://firebase.google.com/](https://firebase.google.com/) y utilizarlo para futuros proyectos.

Ya que queremos enfocarnos en la construcción de la aplicación real en este taller, ya hemos creado una aplicación Firebase para que te conectes, y compartiremos las credenciales contigo más adelante en este paso.

Esto te ayudará a ahorrar algo de tiempo que se puede usar para finalizar la aplicación :)

## Instalando Firebase

Lo primero que debemos hacer para comenzar a usar Firebase es instalarlo en nuestro proyecto, ya que Stackblitz maneja esa parte por nosotros, solo necesitamos decirle los nombres de los paquetes.

Ve a la sección "**DEPENDENCIES**" en el panel izquierdo y en el cuadro de entrada que dice "_enter package name_" escribe **firebase**, luego presiona enter.

![Install Firebase](img/install-firebase.png)

Eso te da acceso a todo el SDK de Firebase para el desarrollo web. Ahora, podemos llevar las cosas un paso más allá e instalar @angular/ fire.

`@angular/fire` es una librería creada por personas tanto de los equipos Firebase como Angular, y te brinda una mejor integración con Firebase cuando trabajas en proyectos Angular.

Puedes instalarlo escribiendo `@angular/fire` en el cuadro de entrada que dice "_enter package name_" de la misma manera que instalamos Firebase.

Una vez que ambos estén instalados, puedes ingresar a `package.json` y ver los nombres de los paquetes allí. Si no los ves, no dudes en pedir ayuda a uno de los mentores :)

## Conecta tu app con Firebase

Ahora que Firebase está instalado, necesitamos que nuestra aplicación Angular sepa cómo se comunicará con él. Para eso, iremos al archivo `app.module.ts` e inicializaremos Firebase.

Es un proceso de 2 pasos, primero, debemos importar los paquetes que vamos a utilizar, así que adelante, agrega esto a tus imports:

```js
import { AngularFireModule } from '@angular/fire';
import { AngularFirestoreModule } from '@angular/fire/firestore';
```

`@angular/fire` es modular, lo que significa que solo importamos lo que usaremos, en este caso, necesitamos la funcionalidad base y Firestore.

Y segundo, agregaremos tanto `AngularFireModule` como` AngularFirestoreModule` a nuestra array de imports. Ahora mismo se ve así:

```js
@NgModule({
  imports: [BrowserModule, ReactiveFormsModule],
  declarations: [AppComponent, CardComponent, AddShowComponent],
  bootstrap: [AppComponent],
})
```

Queremos que se vea así:

```js
@NgModule({
  imports: [
    BrowserModule,
    AngularFireModule.initializeApp({
      apiKey: 'AIzaSyBIM6XVuaqeBDtyyB9Ef1U5oUv9Cue9BK8',
      authDomain: 'first-firebase-angular.firebaseapp.com',
      databaseURL: 'https://first-firebase-angular.firebaseio.com',
      projectId: 'first-firebase-angular',
      storageBucket: 'first-firebase-angular.appspot.com',
      messagingSenderId: '306103315077',
    }),
    AngularFirestoreModule,
  ],
  declarations: [AppComponent, CardComponent, AddShowComponent],
  bootstrap: [AppComponent]
})
```

Estamos agregando `AngularFireModule` y llamando al método `.initializeApp()` para conectar nuestra aplicación a Firebase. El método `.initializeApp ()` toma un objeto como parámetro, ese objeto es nuestro objeto de credencial, que le permite a Angular saber **a qué** aplicación Firebase necesita conectarse.

Copiaremos esas mismas credenciales, la idea es que todos compartamos la misma aplicación y trabajemos más rápido de esa manera.

También estamos agregando `AngularFirestoreModule` para informarle a Angular que usaremos la base de datos Firestore en nuestro proyecto.

Al final, todo el archivo debería verse así:

```js
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { AngularFireModule } from '@angular/fire';
import { AngularFirestoreModule } from '@angular/fire/firestore';

@NgModule({
  imports: [
    BrowserModule,
    AngularFireModule.initializeApp({
      apiKey: 'AIzaSyBIM6XVuaqeBDtyyB9Ef1U5oUv9Cue9BK8',
      authDomain: 'first-firebase-angular.firebaseapp.com',
      databaseURL: 'https://first-firebase-angular.firebaseio.com',
      projectId: 'first-firebase-angular',
      storageBucket: 'first-firebase-angular.appspot.com',
      messagingSenderId: '306103315077',
    }),
    AngularFirestoreModule,
  ],
  declarations: [AppComponent],
  bootstrap: [AppComponent],
  providers: [],
})
export class AppModule {}
```

## Siguientes pasos

Una vez que estés listo, continúa con el siguiente paso donde comenzaremos a construir la parte **C** de CRUD, agregaremos la funcionalidad para crear un programa de televisión y guardarlo en la base de datos.

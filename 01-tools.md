# Las herramientas que usaremos


Para este taller usaremos Angular y Firebase, pero en lugar de hacer que instales un montón de paquetes, herramientas y editor, usaremos **Stackblitz**.

## ¿Qué es Stackblitz?

Es un editor de código que no necesitas instalar. Se ejecuta en el navegador web y maneja todo por ti.

Y cuando decimos todo, lo decimos en serio. Te da el editor, instala los paquetes por ti e incluso tiene una vista donde puedes ver el resultado de tu aplicación en tiempo real con live-reload (es una palabra elegante para referirse a las actualizaciones de la vista cuando escribes nuevo código :-P_)

Lo primero que debes hacer es dirigirte a [https://stackblitz.com/](https://stackblitz.com/) donde verás algo como esto:

![Stackblitz project type selection](img/stackblitz-create.png)

Dirigete a "START A NEW PROJECT" y haz clic en Angular, se creará un nuevo proyecto Angular con todas las dependencias.

Verás algo como esto:

![Angular Folder Structure](img/stackblitz-angular-folder.png)

En el panel izquierdo, tendrás la estructura de carpetas, puedes hacer clic en cualquier archivo allí y se abrirá para ti.

En el panel central, verás el archivo abierto. Ese es tu código, y cada edición que hagas allí aparecerá en vivo en el panel de la derecha.

En el panel derecho, tendrás una vista en tiempo real de tu aplicación.

Adelante, juega con él, abre el archivo `app.component.html` y cambia el texto dentro de las etiquetas` <p> </p> `a lo que desees, lo verás actualizado en tiempo real a tu derecha.

## ¿Y los estilos?

El objetivo de este taller es que te sientas cómod@ al escribir código contra un backend en la nube, no nos centraremos en los estilos, pero, dado que queremos que todo se vea bien, le daremos el CSS predeterminado para la aplicación, si observas `app.component.css` notarás todos los estilos ya aplicados allí.

Una vez que estés listo, continúa con el siguiente paso, donde aprenderás cómo conectar Firebase con tu aplicación Angular.

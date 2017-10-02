# Organizar la vista

Antes de comenzar, debemos saber como están organizadas las vistas en Android.

Para crear una vista, debemos editar el archivo **activity_main.xml** que nos creó *Android Studio* cuando creamos nuestro proyecto. Cada actividad o fragmento tienen que tener una vista asociada. Cuando la aplicación corre nuestra clase *Java*, infla la vista y la muestra al usuario. También podemos crear los objetos de nuestra vista desde la clase Java que infla el layout.

Hay distintas formas de organizar nuestro layout. Android cuenta con una serie de contenedores que agrupará en contenido, y en ellos será donde coloquemos nuestros elementos de **UI** (*User Interface*).

Podemos tener un diseño linar (**LinearLayout**) que colocará los elementos uno detrás de otro, bien de forma horizontal o de forma vertical. Podemos organizar nuestros elementos como en una tabla o grid (Google Fotos) con **GridLayout** o **TableLayout**. Hay layouts especiales para mostrar un fragment (**FrameLayout**). Por último, podemos colocar nuestros elementos de forma relativa, algo así como se hace en web, con **RelativeLayout**.

![Screenshot](img/layouts.jpg)

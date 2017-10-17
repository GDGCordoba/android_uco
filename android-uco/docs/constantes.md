# Usando constantes como recursos

## ¿Por qué usar constantes?

Al usar archivos de recursos para guardar nuestros valores como constantes, nos vamos a asegurar de que podamos usar estos valores en cualquier sitio de nuestra aplicación. Así, si alguna vez necesitamos cambiar el valor del recurso, sólo tendremos que efectuar un cambio en el archivo correspondiente y no preocuparnos por el comprobar que se haya cambiado en toda la app.

## Tipos de recursos

Dentro de la carpeta **res** de nuestro proyecto podemos albergar varios tipos de recursos.

* animator/: archivos XML para trabajar con animaciones de propiedades. Sirven para animar casi cualquier cosa.
* anim/: archivos para las animaciones de interpolación de movimientos. Son animaciones que definimos con puntos de comienzo o el tiempo de la animación.
* color/: aquí se definen los colores para nuestra paleta.
* drawable/: archivos de mapas de bits (.png, .jpg, .gif)
* minmap/: archivos de elementos de diseño para distintas densidades.
* layout/: archivos XML que definen la interfaz de usuario.
* menu/: archivos que definen los menus de la aplicación.
* raw/: archivos arbitrarios para guardar sin procesar.
* values/: archivos XML que contienen valore simples como strings, valores enteros o colores (arrays.xml, colors.xml, dimens.xml, strings.xml, styles.xml)
* xml/: archivos XML arbitrarios que pueden ser leidos en tiempo de ejecución.

## Cambia tus colores
Entra en [este](https://www.materialpalette.com/) enlace y elige una gama de colores que te guste para tu app.

Cuando la tengas abre tu archivo **res/values/colors.xml** y cambia los colores!

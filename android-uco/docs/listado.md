# Crear un listado de elementos

Para crear una lista de elementos, tenemos varias opciones. Podemos usar *ListView*, *RecyclerView*, o *GridView*.

Nuestra implementación va a ser un listado vertical con datos. Un ejemplo de lo que queremos montar sería:

![Screenshot](img/recycler.png)

## Diferencia entre ListView y RecyclerView

Tanto el ListView como el RecyclerView nos sirven en caso de querer hacer listado como el de la imagen. Las diferencias son que el RecyclerView es una implementación más nueva, da más flexibilidad con animaciones, y además, como en su nombre se indica, recicla los items de la tabla por lo que supone un ahorro en memoria. El RecyclerView sólo tiene declarados los items visibles, y uno por encima y por debajo. Cuando el usuario hace scroll, las celdas que ya no se ven se reutilizan para mostrar las nuevas.

En esta guía vamos a usar RecyclerView por estas razones.

# Inflando la vista

¿Que significa inflar la vista? Básicamente es rellenar nuestros layouts con datos. Los datos que vamos a mostrar son las razas de perro que nos traeremos con Retrofit.

Vamos a nuestra actividad y creamos las siguientes funciones:

```Java
private void setAdapter(){
  //aqui configuraremos el adaptador de nuestros datos
}

private void setRecyclerView(){
  //aqui inicializaremos nuestro recyclerview
}

private void getDogBreeds(){
  //desde aquí llamaremos al servidor y traeremos los datos
}
```

Para poder inicializar el **RecyclerView**, tenemos que hacer un **binding**. Un binding es hacer referencia al layout desde nuestra clase Java. Tenemos una forma nativa del SDK que puede resultar bastante tediosa.

```Java
  private RecyclerView recyclerView;

  @Override
  protected void onCreate(Bundle savedInstanceState){
    ...

    recyclerView = (RecyclerView) findViewById(R.id.dogList);
  }
```

Otra forma, mucho más sencilla, es hacerlo con [Butterknife](http://jakewharton.github.io/butterknife/). Con Butterknife nos ahorramos hacer el ```findViewById()``` y si instalamos el plugin correspondiente en Android Studio no tenemos que llegar a escribir nada.

Para instalar Butterknife, añadimos la dependencia:

```Java
compile 'com.jakewharton:butterknife:8.8.1'
annotationProcessor 'com.jakewharton:butterknife-compiler:8.8.1'
```

Una vez añadida la dependencia, debemos dejar la clase así:

```Java
public class MainActivity extends AppCompatActivity {

    @BindView(R.id.dogList)
    RecyclerView dogList;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        ButterKnife.bind(this);
    }

    private void setAdapter() {

    }

    private void setRecyclerView() {

    }

    private void getDogBreeds() {

    }
}
```

Como véis, es necesario hacer ```ButterKnife.bind(this);``` justo después de hacer el ```setContentView()```. Esto es así ya que con ese método, Butterknife hace por su cuenta los ```findViewById()```.

## Declarar el adapter

Un adapter es una clase intermedia entre nuestro layout y los datos. Nos ayuda a distribuir la información en el layout y lo administra internamente. Si tenemos un listado muy grande, el Adapter irá creando cada item del listado y reciclando los que ya no se ven en pantalla. Se encarga de, a partir de un array de datos, setear los textos, imágenes, colores o cualquier cosa que queramos editar en nuestros layouts.

Para crear el adaptador, creamos un nuevo package llamado **adapter** y dentro de él creamos una nueva clase de Java llamada **DogListAdapter.java**.

Para que una clase de Java sea un adaptador, debe heredar de ```RecyclerView.Adapter<>``` e implementar un ViewHolder. Un ViewHolder es la clase del elemento que estamos mostrando. En nuestro caso, nuestro ViewHolder será una clase con un campo ```String``` que será la raza de perro que estemos mostrando.

Nuestra clase se quedará así:

```Java
public class DogListAdapter extends RecyclerView.Adapter<DogListAdapter.ViewHolder> {

    @Override
    public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        return null;
    }

    @Override
    public void onBindViewHolder(ViewHolder holder, int position) {

    }

    @Override
    public int getItemCount() {
        return 0;
    }


    public class ViewHolder extends RecyclerView.ViewHolder {
        public ViewHolder(View itemView) {
            super(itemView);
        }
    }
}
```

Todos esos métodos son obligatorios implementarlos:

* **onCreateViewHolder**: este método se dispara cuando el adaptador va a crear un item. Aquí normalmente lo que hacemos es decirle al adaptador qué layout debe usar para mostrar en pantalla.

* **onBindViewHolder**: aquí, el elemento ya está creado, pero está vacío. Nos sirve para setear los datos que queremos mostrar, o asignar los eventos de onClick o alguna cosa que necesitemos.

* **getItemCount**: este método es super importante, ya que aquí el adaptador sabe cuantas veces debe disparar los dos métodos de arriba. Si nos equivocamos y siempre retorna 0, nunca se nos mostrará nada en pantalla. Normalmente, lo que se hace es crear un array interno de elementos, setear los valores a ese array y luego retornar aquí su tamaño.

* **Clase ViewHolder**: como hemos dicho, es una clase que nos sirve para bindear los campos que vamos a mostrar en pantalla.

### Rellenar el Adapter con datos

Lo primero de todo, necesitamos un array de string para guardar las razas de perro.

```Java
private List<String> dogBreeds;
```

Y creamos un método para poder insertar los datos desde la actividad, que es donde los vamos a traer.

```Java
public void setDogBreeds(List<String> dogBreedsArray){
    this.dogBreeds = dogBreedsArray;
    this.notifyDataSetChanged();
}
```

La llamada ```this.notifyDataSetChanged()``` nos sirve para reiniciar el adapter, y que se vuelvan a disparar los métodos de **onCreateViewHolder** y **onBindViewHolder**.

También tenemos que cambiar el método **getItemCount** para que retorne el tamaño de ese array y no 0.

```Java
@Override
public int getItemCount() {
    return this.dogBreeds.size();
}
```

### Asignando el layout al adapter

Debemos cambiar el método **onCreateViewHolder** y dejarlo asi:

```Java
@Override
public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
    View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.item_dog, parent, false);

    return new ViewHolder(view);
}
```

Estamos usando la clase **LayoutInflater** para coger el layout que hemos hecho antes de **item_dog** y asignarselo al item que estamos creando.

### Asignando los datos

Usando ButterKnife, debemos añadir al ViewHolder el campo de TextView que antes hemos creado en el layout.

```Java
public class ViewHolder extends RecyclerView.ViewHolder {

    //seteamos el valor aquí
    @BindView(R.id.dogBreedName)
    TextView dogBreedName;

    private View view;

    public ViewHolder(View itemView) {
        super(itemView);
        ButterKnife.bind(this, itemView);
        this.view = itemView;
    }
}
```

Ahora en **onBindViewHolder** rellenamos el TextView con el valor que corresponda:

```Java
@Override
public void onBindViewHolder(ViewHolder holder, int position) {
    holder.dogBreedName.setText(this.dogBreeds.get(position));
}
```

Por último, nos queda declarar en el constructor el array vacío, para que no tengamos un error al asignar valores a algo que está a null (NullPointerException)

```Java
public DogListAdapter() {
    this.dogBreeds = new ArrayList<>();
}
```

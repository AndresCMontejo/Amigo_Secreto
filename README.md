# Proyecto Amigo Secreto de Alura LATAM

El siguiente proyecto es una aplicación que funciona de la siguiente manera:

Se agregan nombres de amigos en un campo, y posteriormente, el botón "Añadir" agregará los nombres en pantalla, como se muestra a continuación.

![image](https://github.com/user-attachments/assets/4b7492d2-3996-489b-9c0d-160255fdd96a)

Una vez que se han agregado los nombres a la lista, se puede hacer clic en el botón "Sortear amigo", el cual elegirá un amigo al azar, como se muestra a continuación.

![image](https://github.com/user-attachments/assets/76b7911a-071e-4e69-b1fb-e535860128c7)

## Funcionalidades del programa

- **Validación de campo vacío**: Si se deja el campo en blanco, el sitio mostrará una alerta indicando que no hay información en el campo.

![image](https://github.com/user-attachments/assets/2658ac4d-0844-4bfc-80b8-522ad9f7adda)

- **Validación de lista vacía**: Si se hace clic en "Sortear amigo" sin haber agregado ningún nombre, el programa mostrará una alerta que dirá "No hay amigos agregados".

![image](https://github.com/user-attachments/assets/a8e08de6-9829-4640-96b1-a19300d51ed8)

- **Limpieza automática del campo**: Cuando se escribe un nombre y se hace clic en "Añadir", el campo se limpiará automáticamente.

## Funciones adicionales

Se agregaron funciones adicionales al proyecto original:

- **Evitar nombres repetidos**: Solo se puede agregar un nombre sin repetirlo. Si se intenta agregar un nombre que ya existe, el programa mostrará una alerta. Esto funciona independientemente de si el nombre está en mayúsculas, minúsculas o una combinación de ambas.

![image](https://github.com/user-attachments/assets/53464bcc-db25-47d3-9ebd-5ac98f1e9c7d)

- **Mínimo de dos amigos para sortear**: Para que el botón "Sortear amigo" funcione, debe haber al menos dos nombres en la lista. Si solo hay un nombre, el programa mostrará una alerta indicando que se necesitan al menos dos amigos para realizar el sorteo.

![image](https://github.com/user-attachments/assets/6a25465a-970e-416a-a5e0-e33becb2989f)

- **Botón de resetear**: Después de realizar el sorteo, el botón "Sortear amigo" se convertirá automáticamente en un botón de "Resetear". El botón "Añadir" se desactivará y se mostrará un mensaje que dirá "Clic en resetear". Al hacer clic en "Resetear", el programa volverá a su estado inicial, limpiando la lista, el campo y el resultado.

![image](https://github.com/user-attachments/assets/a59980c1-0462-454c-b78a-86c49f85d98f)

## Explicación del código en JavaScript

El programa funciona con una lista, donde se almacenan los nombres agregados. A continuación, se explica el código:

### Agregar nombres

Explicación de código en JavaScript:
-	El programa funciona con una lista, es decir, elabore una variable, donde se almacenarán los nombres agregados en forma de lista.
-	Posteriormente se llama la función de la línea 24 del maquetado HTML, misma que hará funcionar nuestro botón “añadir”.
-	Creo una variable, que servirá para tomar los nombres agregados, en la variable “amigoAgregado” utilizo la función. toUpperCase(); con el objetivo de que todo los nombres agregados se conviertan en mayúsculas, así evitar repetir los nombre ya sea en minúsculas o con mayúsculas en algunas letras
-	Uso la condiciones if, else if, else, para que el programa muestre las alertas, es decir si en nuestra variable en este caso que representa nuestro campo en HTML está vacío, el programa mostrará la alerta de que dicho campo esta vacío, en el else if, agrego la función de includes, esta línea nos ayuda a no repetir los nombres, en pocas palabras la línea quiere decir, si en la lista amigos se incluye (nombre_repetido) este mostrará la alerta de que no se pueden repetir nombres. 
-	La línea else hará la función de que en caso de que no se cumplan las dos condiciones anteriores, amigo.push agregara el nombre a la lista.
-	La línea 15 servirá para limpiar el campo cada vez que demos clic en añadir nombre.

```JavaScript
let amigos = [];
function agregarAmigo() {
    let agregandoAmigos = document.getElementById("amigo");
    let amigoAgregado = agregandoAmigos.value.toUpperCase();
    if (amigoAgregado === "") {
        alert("Ingrese un nombre, el campo esta vacio :(");
    } else if (amigos.includes(amigoAgregado)) {
        alert(`No puedes agregar ${amigoAgregado} dos veces :c`)
    } else {
    amigos.push(amigoAgregado);
    console.log(amigos);
    }
    agregandoLista();
    agregandoAmigos.value = "";
}
````
### Mostrar la lista

-	En línea 14 se manda a llamar la siguiente función: 
La función de agregandoLista(), permite que los nombres agregados en el campo se agreguen en nuestro sitio y sean visibles.
-	En la línea 18 buscamos nuestro elemento HTML por id.
-	El ciclo for funciona de la siguiente forma en este programa. Declaramos una variable i = 0, y si esta variable es menos a la longitud de nuestra lista llamada “amigos”, esta variable se le sumara 1.
-	En la línea 22, creamos un elemento llamado “li” que se ira agregando a nuestro HTML cada que el botón “añadir” sea cliqueado, por esta razón en la línea 14 se agrego la función “agregandoLista()”, dentro de la función “agregarAmigo()” que dicha función representa nuestro botón “añadir”
-	La línea 23 visualizará el amigo agregado, accediendo a cada nombre a través del índice, es decir, si nosotros agregamos nuestro primer nombre, por ejemplo “Amanda”, este nombre al pulsar añadir se agregara a la lista amigos, al agregar este nombre, la longitud de nuestra lista será 1, pues ya hay un elemento, y el índice de ese elemento en este caso el nombre de “Amanda”, esta en el numero 0, que es el valor inicial de nuestro ciclo for en la variable i = 0, y así sucesivamente, el programa entrará en función cuando se de clic en el botón “añadir”, al volver a colocar otro nombre y dar click en añadir, nuestra lista ahora tendrá una longitud de 2, y el segundo nombre estará en el índice numero 1, en pocas palabras nuestra variable i nunca será igual o mayor a amigos.length, y esto permitirá que nuestra lista sea visible accediendo a ellas a través del índice. 
```JavaScript
function agregandoLista(){
    let addlista = document.getElementById("listaAmigos")
    addlista.innerHTML = "";

    for (let i = 0; i < amigos.length; i++) {
        let visualizandoLista = document.createElement("li");
        visualizandoLista.textContent = amigos[i];
        addlista.appendChild(visualizandoLista);
    } 
}
````

### Sortear amigo

-	La función sortearAmigo() hará funcionar nuestro botón “Sortear amigo” de la siguiente forma:
-	La línea 28 genera un numero al azar, se crea una variable para almacenar ese valor al azar, Math.random nos generará un numero aleatorio entre 0 y 1, incluyendo el 0 pero no el 1, es decir nos brindará números flotantes o decimales, y al multiplicar por la longitud de nuestra lista, nos dará como resultado un numero flotante, y es ahí donde Math.floor nos permitirá redondear ese valor decimal, al valor entero más cercano.
-	La línea 29 almacenará nuestro nombre al azar, accediendo a ese nombre a través de índice, el numero de índice será el que se originó en nuestra línea 28
-	A partir de la línea 30, se empieza a crear condiciones if, else-if, else, depende de estas condiciones la forma en que se comportará nuestro botón “sortear amigos”.
-	Si en la línea 30 la lista amigos es igual a 0, es decir no hay ningún elemento en ella, al hacer clic en el botón, aparecerá la alerta de que no hay amigos.
-	La condición else-if compara estrictamente amigos.length con el numero 1, es decir si la longitud de nuestra lista es estrictamente igual a 1, nos dará una alerta de que por lo menos tiene que existir 2 amigos para poder sortear.
-	La condición else funciona en caso de que ninguna de las dos condiciones anteriores no se cumpla, en la línea 35 desactivamos el botón añadir, con el propósito de que ya no puedan agregar más personas.
-	La línea 36 accede al id del botón “añadir”
-	La línea 37 se le cambia el nombre a dicho botón, por “Clic en resetear”
-	La línea 32 accede al id resultado con el objetivo de agregar y mostrar el amigo secreto, agregando en la línea 39 un innerHTML para hacer posible el objetivo, se concatena la frase que se mostrara como resultado agregando la variable de la línea 36 que es la que accede a un nombre de la lista que se accede a través de índice.
-	La línea 40 accede a nuestro botón “sortear amigos” por ID, y con un innerHTML en la línea 41 cambiamos el contenido del botón, accedemos a un nuevo icono que contiene una imagen de reiniciar, al igual que su nombre, cambiando a resetear.
-	La línea 42 cambia la función sortearAmigo() por resetearSorteo(), ahora nuestro botón ya tiene un nombre diferente y una función distinta, por lo que podemos crear nuestro programa para resetear todo. 
  ```JavaScript
function sortearAmigo() {
let azar = Math.floor(Math.random()*amigos.length);
let nombreRandom = amigos[azar];
    if (amigos == 0) {
    alert("No hay amigos agregados :(");
    } else if (amigos.length === 1){
        alert("Para hacer el sorteo tienes que agregar por lo menos 2 amigos.")
    } else {
        document.querySelector("#aañadir").setAttribute("disabled", "true");
        let desactivar = document.getElementById("aañadir");
        desactivar.innerHTML = "Click en resetear :)";
        let resultadofinal = document.getElementById("resultado");
        resultadofinal.innerHTML = `Tu amigo secreto es ${nombreRandom}`;
        let boton = document.getElementById("sorteodeAmigos");
        boton.innerHTML = `<img id="icono" src="assets/deshacerr.png" alt="Ícono para resetear"> Resetear`;
        boton.onclick = resetearSorteo;
        return;
    }  
}
````
-	Antes de colocar condiciones a nuestra nueva función llamada resetearSorteo. Se realiza una nueva función llamada Inicial(), con el objetivo de volver a un punto inicial del programa.
-	La línea 47 activa de nuevo nuestro botón “Añadir” que por ahora tiene otro nombre “Clic en resetear”
-	La línea 48 limpia nuestra lista
-	La línea 49 limpia el resultado que se visualiza en nuestro sitio
-	La línea 50 limpia nuestra lista de amigos que se visualiza en el sitio
-	La línea 51 limpia todo el historial de la consola.
```JavaScript
function inicial(){
    document.getElementById('aañadir').removeAttribute('disabled');
    amigos = [];
    document.getElementById("resultado").textContent = "";
    document.getElementById("listaAmigos").textContent = "";
    console.clear();
}
````
Al pulsar clic en nuestro nuevo botón “resetear”, entrara en función lo siguiente:
-	En la línea 54 creamos el programa y funcionamiento de la función nueva llamada resetearSorteo() misma que fue creada por la condición else de nuestra función sortearAmigo() 
-	La línea 55 llama a la función inicial().
-	La línea 57 llama a nuestro botón añadir por su ID, reutilizando la misma variable de la línea 36, y con un innerHTML de la línea 58 le colocamos el nombre original al botón, en este caso “Añadir”
-	La línea 59 se llama de nuevo la variable de la línea 40, esta llama por ID nuestro botón de “Sortear amigos”.
-	La línea 60 a través de un .innerHTML volvemos su estado original a dicho botón, le cambiamos su icono, y le devolvemos su nombre original, es este caso “Sortear amigo”.
-	La línea 62 se crea de nuevo la función sortearAmigo()
-	La línea 63 borra cualquier cosa que se haya escrito en el campo después de que el botón sorteo haya entrado en acción.
```JavaScript
function resetearSorteo() {
    inicial();
    // Cambiar el texto del botón y el ícono a su estado original
    desactivar = document.getElementById("aañadir");
    desactivar.innerHTML = "Añadir";
    boton = document.getElementById("sorteodeAmigos");
    boton.innerHTML = `<img id="icono" src="assets/play_circle_outline.png" alt="Ícono para sortear"> Sortear amigo`;
    // Cambiar la función del botón para sortear de nuevo
    boton.onclick = sortearAmigo;
    document.getElementById("amigo").value = "";
}

resetearSorteo();
````
## Nota
El programa incluye `console.log` para facilitar la comprensión de su funcionamiento.

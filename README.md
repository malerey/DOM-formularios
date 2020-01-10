# DOM: formularios

#### Formularios
* Los formularios en HTML son una manera muy buena de obtener datos por parte del usuario.
* Por medio de ECMAScript podemos manejar los valores y eventos del formulario como también los de sus elementos
* También podemos validar los datos que el usuario ingresa
* Para poder interactuar con un formulario lo primero que tenemos que hacer es seleccionarlo

**Ejemplo:**
```js
var form = document.querySelector('form');
```

* Otra forma de seleccionar los formularios es por medio del objeto `document` y la propiedad `forms`
* La propiedad forms retorna una colección de todos los formularios que tiene el documento

**Ejemplo:**
```js
  var formulario = document.forms[0];
  var formularios = document.forms;
```

* Los elementos del tipo formulario tienen un atributo llamado `elements` y tiene la colección de elementos que tiene el formulario seleccionado

**Ejemplo:**
```js
var form = document.querySelector('form');
var elementos = form.elements;
// retorna el elemento del formulario que está en el índice indicado
var elemento = form.elements[indice];
```

* El objeto formulario tiene atributos como `action`, `target`, `encoding` y `method`
* Al ser un objeto de Javascript podemos acceder a todos ellos de la misma forma que lo hacemos con cualquier otro objeto
  * **action:** Establece la URL del documento que va a procesar la información enviada por el formulario
  * **encoding:** Establece el tipo MIME con el que se va a encriptar los datos
  * **method:** Establece cual es el método de HTTP que se va a utilizar para enviar los datos. Puede ser get o post
  * **name:** Establece el nombre del formulario

**Ejemplo:**
```html
<form action="guardar_usuario.html" method="get" enctype="application/x-www-form-urlencoded" name="login"></form>
```
```js
var form = document.querySelector('form');

console.log(form.action); // guardar_usuario.html
console.log(form.encoding); // get
console.log(form.method); // application/x-www-form-urlencoded
console.log(form.name); // login
```

* Los elementos del formulario tienen un atributo llamado `value` que nos permite establecer u obtener el valor de un elemento
* Con la propiedad value podemos obtener el valor de varios de los elementos de un formulario como por ejemplo:
  * inputs de texto, password, hidden
  * checkbox
  * radio
  * textarea

**Ejemplo:**
```html
<form action="guardar_usuario.html" method="get" enctype="application/x-www-form-urlencoded" name="login">
  <input type="text" id="username" name="username" />
  <input type="password" id="pass" name="pass" />
  <input type="submit" name="submit" value="Enviar" />
</form>
```
```js
var form = document.querySelector('form');
var username = form.elements[0];

username.value; // Obtenemos un string vacío
username.value = 'pepe'; // Establecemos el valor del input username en pepe
```

* Por medio del evento `submit` del formulario podemos mandar los datos a otro documento
* Podemos cortar la ejecución del `submit` de un formulario retornando un valor `false`

**Ejemplo:**
```html
<form action="guardar_usuario.html" method="get" enctype="application/x-www-form-urlencoded" name="login">
  <input type="text" id="username" name="username" />
  <input type="password" id="pass" name="pass" />
  <input type="submit" name="submit" value="Enviar" />
</form>
```
```js
var form = document.querySelector('form');

form.onsubmit = function() {
	// Este evento maneja la forma en que se va a submitear el formulario
  // Retornamos false para evitar que se ejecute el evento submit del formulario
  return false;
}
```

* Al igual que el resto de los eventos podemos controlar que no se ejecute el evento por default con el método del eventos preventDefault()
**Ejemplo:**
```html
<form action="guardar_usuario.html" method="get" enctype="application/x-www-form-urlencoded" name="login">
  <input type="text" id="username" name="username" />
  <input type="password" id="pass" name="pass" />
  <input type="submit" name="submit" value="Enviar" />
</form>
```
```js
var form = document.querySelector('form');

form.onsubmit = function(evento) {
  evento.preventDefault();
  return false;
}
```

* Para poder obtener el valor de un elemento `select` podemos utilizar la propiedad `selectedIndex`
* Esta propiedad retorna el índice numérico de la opción seleccionada
* Otra de las propiedades que tiene el objeto `select` es `options` que retorna la colección de elementos options
* Combinando estos dos atributos podemos obtener el valor del `option` seleccionado en el elemento `select`
* Al igual que el resto de los elementos HTML del formulario, el objeto option tiene un atributo value que nos da el valor del mismo

**Ejemplo:**
```html
<form action="guardar_usuario.html" method="get" enctype="application/x-www-form-urlencoded" name="login">
  <select name="paises" id="paises">
    <option value="ar">Argentina</option>
    <option value="br">Brasil</option>
    <option value="cl">Chile</option>
  </select>
</form>
```
```js
var select = document.querySelector('select');

console.log(select.selectedIndex);  // retorna el índice del valor seleccionado
console.log(select.options);  // retorna la colección de elementos options

select.options[indice]; // retorna el option seleccionado
console.log(select.options[indice].value); // retorna el valor del elemento seleccionado.
```


* Los elementos `checkbox` tienen la propiedad `value` que nos retorna su valor como ya vimos
* Podemos establecer si un `checkbox` está seleccionado o no utilizando la propiedad `checked`
* Esta propiedad retorna un valor boolean
* También podemos asignarle un valor boolean para establecer su estado

**Ejemplo:**
```html
<form action="guardar_usuario.html" method="get" enctype="application/x-www-form-urlencoded" name="login">
  <input type="checkbox" name="sexo" value="f" checked> Femenino
  <input type="checkbox" name="sexo" value="m"> Masculino
</form>
```
```js
var checkboxes = document.querySelectorAll("input[type='checkbox']")
var femenino = checkboxes[0];
var masculino = checkboxes[1];

console.log(femenino.checked);  // retorna el valor true
femenino.checked = false; // establece un nuevo valor al elemento.
console.log(femenino.value); // f

masculino.checked;  // retorna el valor false
masculino.checked = true; // establece un nuevo valor al elemento.
console.log(masculino.value); // m
```

* Podemos utilizar el selector de css `:checked` para obtener el checkbox seleccionado de la siguiente forma:

**Ejemplo:**
```html
<form action="guardar_usuario.html" method="get" enctype="application/x-www-form-urlencoded" name="login">
  <input type="checkbox" name="sexo" value="f" checked> Femenino
  <input type="checkbox" name="sexo" value="m"> Masculino
</form>
```
```js
var sexo = document.querySelector('input:checked');

console.log(sexo.checked);  // retorna el valor true
sexo.checked = false; // establece un nuevo valor al elemento.
console.log(sexo.value); // f
```

* Los elementos del formulario pueden manejar eventos por medio de los métodos: onfocus, onblur, onchange, oninput
* También se pueden escribir utilizando el método addEventListener(callback)
  * **focus:** se dispara al establecer el foco en un elemento
  * **blur:** se dispara al remover el foco sobre un elemento
  * **change:** se dispara cuando cambia el valor de un elementos
  * **input:** se dispara al ingresar datos a un elemento

**Ejemplo:**
```html
<form action="guardar_usuario.html" method="get" enctype="application/x-www-form-urlencoded" name="login">
  <input type="text" id="username" name="username" />
  <input type="password" id="pass" name="pass" />
  <input type="submit" name="submit" value="Enviar" />
</form>
```
```js
var form = document.querySelector('form');
var username = form.elements[0];

username.onfocus = function() {
  // código que maneja el focus del elemento
  console.log('Hicieron foco en el campo username');
}

username.onblur = function() {
  // código que maneja el blur del elemento
  console.log('Se perdió el foco del campo username');
}

username.oninput = function() {
  // código que maneja el ingreso de datos a un elemento
  console.log('Están cambiaron el valor del campo username');
}
```

* Por medio del evento `change` podemos manejar el cambio de selección de un elemento select

**Ejemplo:**
```html
<form action="guardar_usuario.html" method="get" enctype="application/x-www-form-urlencoded" name="login">
  <select name="paises" id="paises">
    <option value="ar">Argentina</option>
    <option value="br">Brasil</option>
    <option value="cl">Chile</option>
  </select>
</form>
```
```js
var select = document.querySelector('select');

select.onchange = function() {
  var index = select.selectedIndex;
  var valor = select.options[index].value;
  console.log(index);
  console.log(valor);
}
```

* Para validar si un campo de texto está vacio podemos combinar la propiedad `value` y la propiedad `length` de los strings

**Ejemplo:**
```html
<form action="guardar_usuario.html" method="get" enctype="application/x-www-form-urlencoded" name="login">
  <input type="text" id="username" name="username" />
  <input type="password" id="pass" name="pass" />
  <input type="submit" name="submit" value="Enviar" />
</form>
```
```js
var form = document.querySelector('form');

form.onsubmit = function(evento) {
  evento.preventDefault();
  var username = form.elements[0];

  if (username.value.length === 0) {
    console.log('Username incorrecto');
    return false;
  }

  return true;
}
```


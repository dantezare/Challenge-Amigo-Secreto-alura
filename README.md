# 🎯 CHALLENGE AMIGO SECRETO - DANTE ZARE

[![JavaScript](https://img.shields.io/badge/Code-JavaScript-yellow?logo=javascript)](https://developer.mozilla.org/es/docs/Web/JavaScript)
[![HTML](https://img.shields.io/badge/Markup-HTML5-orange?logo=html5)](https://developer.mozilla.org/es/docs/Web/HTML)
[![Estado](https://img.shields.io/badge/Estado-Completado-brightgreen)](#)

Aplicación para **sortear amigos secreto de forma aleatoria**.  
El objetivo principal es fortalecer las habilidades en **lógica de programación** y manipulación del DOM en JavaScript.

---

## 🚀 Características

- ➕ **Agregar amigos** a una lista dinámica.
- 👀 **Visualizar** en tiempo real los nombres ingresados.
- 🎲 **Sortear** un amigo al azar.
- 🧹 Validación de entradas vacías para evitar errores.

---

## 🗂️ Estructura del Proyecto

### 📂 Proyecto
### 📄 index.html   → Página principal con el formulario, lista y botón de sorteo.
### 🎨 style.css    → (Opcional) Estilos: colores, tipografía y diseño de la interfaz.
### ⚙️ script.js    → Lógica en JavaScript:
• Array `amigos` para guardar los nombres.

• `agregarAmigo()` valida y agrega nuevos nombres.

• `mostrarListaAmigos()` refresca la lista en pantalla.

• `sortearAmigo()` elige un amigo al azar y lo muestra.
### 📝 README.md    → Documentación completa del proyecto.


## 🧩Detalle de la Logica del Codigo
Inicialmente procedemos a  declarar la variable de tipo array, que almacenará los nombres de los amigos ingresados.
```javascript
let amigos = [];
```
### `agregarAmigo()`
Esta función se encarga de **capturar y validar el nombre ingresado** en el campo de texto, agregarlo al arreglo `amigos` y actualizar la lista visible en la página.

**Pasos principales:**
1. **Captura del dato**: obtiene el valor del input con id `amigo` y lo recorta con `trim()` para eliminar espacios innecesarios.  
2. **Validación**: si el campo está vacío, muestra una alerta y termina la ejecución.  
3. **Actualización del array**: agrega el nombre al arreglo global `amigos`.  
4. **Limpieza**: vacía el campo de entrada para permitir nuevas incorporaciones.  
5. **Refresco de la lista**: llama a `mostrarListaAmigos()` para que el DOM muestre la lista actualizada en tiempo real.
```javascript
function agregarAmigo() {
    // Capturar el valor del campo de entrada
    const input = document.getElementById('amigo');
    const nombre = input.value.trim();

    // Validar la entrada
    if (nombre === "") {
        alert("Por favor, inserte un nombre.");
        return;
    }

    // Actualizar el array de amigos
    amigos.push(nombre);

    // Limpiar el campo de entrada
    input.value = "";
    console.log(amigos);
    mostrarListaAmigos() // Llamar a la función para mostrar la lista actualizada
}
```
### `mostrarListaAmigos()`
Esta función se encarga de **actualizar dinámicamente el listado de amigos en el DOM**, reflejando en tiempo real los nombres almacenados en el arreglo `amigos`.

**Pasos principales:**
1. **Obtención del contenedor:** localiza el elemento HTML con el id `listaAmigos` donde se mostrarán los nombres.  
2. **Limpieza previa:** vacía el contenido de la lista (`innerHTML = ""`) para evitar duplicados.  
3. **Recorrido del arreglo:** itera el array `amigos` con un bucle `for`.  
4. **Creación de elementos:** por cada nombre crea un nuevo elemento `<li>` y asigna el texto del amigo correspondiente.  
5. **Inserción en el DOM:** agrega cada `<li>` al elemento de la lista, actualizando la visualización en la página.

```javascript
// Función para mostrar la lista de amigos en el HTML
function mostrarListaAmigos() {
    // Obtener el elemento de la lista
    const lista = document.getElementById('listaAmigos');
    
    // Limpiar la lista existente
    lista.innerHTML = "";

    // Iterar sobre el arreglo amigos y agregar cada nombre como <li>
    for (let i = 0; i < amigos.length; i++) {
        const li = document.createElement('li');
        li.textContent = amigos[i];
        lista.appendChild(li)
        ;
    }
}
```
### `sortearAmigo()`
Esta función realiza el **sorteo aleatorio de un amigo** de la lista y muestra el resultado en el HTML.

**Pasos principales:**
1. **Validación de datos:** comprueba que el arreglo `amigos` no esté vacío.  
   - Si no hay elementos, muestra una alerta y detiene la ejecución con `return`.  
2. **Cálculo del índice aleatorio:** usa `Math.random()` para generar un número aleatorio y `Math.floor()` para convertirlo en un índice válido del array.  
3. **Selección del amigo:** obtiene el nombre del arreglo en la posición aleatoria y lo guarda en `amigoSorteado`.  
4. **Actualización del DOM:** localiza el elemento con id `resultado` y reemplaza su contenido con un `<li>` que contiene el nombre del amigo sorteado.
```javascript
// Función para sortear un amigo al azar
function sortearAmigo() {
    // Validar que haya amigos disponibles
    if (amigos.length === 0) {
        alert("No hay amigos para sortear.");
        return;
    }

    // Generar un índice aleatorio
    const indiceAleatorio = Math.floor(Math.random() * amigos.length);

    // Obtener el nombre sorteado
    const amigoSorteado = amigos[indiceAleatorio];

    // Mostrar el resultado en el elemento con id "resultado"
    const resultado = document.getElementById('resultado');
    resultado.innerHTML = `<li>${amigoSorteado}</li>`;
}
```
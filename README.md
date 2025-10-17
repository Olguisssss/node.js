https://ejecutortecnico.github.io/pri/mision3/clase1.html
Crear un proyecto con Vite
software:  nodejs,  npm
desde cmd(windows + R): create vite@latest proyecto-react -- --template react
abrir en visual studio la carpeta que se creó del proyecto react
desde el terminal de vscode instalar libreria:   npm install axios
correr proyecto :   npm run dev

en React los nombres todos deben empezar con letra mayuscula, igualmente las funciones

Con este comando ejecuto el proyecto creado:
"npm run build"
y esto crea la carpeta dist con el archivo index.html
react es una librería de javascript para construir interfaces de usuario

¿qué es un componente? 
Los componentes son la piedra angular de cualquier aplicación en React. Representan piezas independientes y reutilizables de la interfaz de usuario (UI), que se combinan 
para formar interfaces completas. React se basa en la idea de descomponer la UI en pequeños bloques con su propia lógica y estructura.

Concepto de Componentización
Proceso de dividir la interfaz en componentes reutilizables y modulares.
Cada componente maneja su propia lógica, estado y estilo.
Facilita el mantenimiento, la escalabilidad y las pruebas.

Ejemplo:

<ProductCard /> — muestra información de un producto.
<ShoppingCart /> — gestiona los artículos seleccionados.
<UserProfile /> — muestra los datos del usuario.

Jerarquía de Componentes
En React, los componentes se organizan en un árbol jerárquico donde los padres contienen hijos.

Los datos fluyen de los padres hacia los hijos a través de props.
Un componente puede contener múltiples componentes hijos.

Tipos de Componentes en React
Componentes Funcionales: basados en funciones de JavaScript.
Componentes de Clase: basados en clases ES6, con ciclo de vida y estado interno.
Ambos pueden hacer lo mismo, pero los componentes funcionales son el estándar actual con Hooks.

Ejemplo de Componente Funcional
export default function Saludo() {
  return <h2>¡Hola desde un componente funcional!</h2>;
}

Props y Estado
Props: datos que el componente padre pasa al hijo.
Estado (State): datos internos del componente que pueden cambiar con el tiempo.

function Saludo({ nombre }) {
  return <h3>Hola, {nombre}!</h3>;
}

// Uso
<Saludo nombre="Ana" />

Las props son inmutables, mientras que el estado cambia con funciones como setState o useState.


LECCION 2

Hooks en Componentes Funcionales
Objetivos
Entender qué son los Hooks y por qué se usan.
Usar useState para manejar estado.
Usar useEffect para efectos secundarios.
Explorar otros hooks básicos: useRef, useContext.

¿Qué son los Hooks?
Funciones especiales de React que permiten “enganchar” lógica en componentes funcionales.
Antes, solo los componentes de clase podían manejar estado y ciclo de vida.
Ahora los Hooks hacen a los componentes funcionales igual de potentes.

Reglas de los Hooks
⚠️ Solo se llaman en la parte superior del componente (no dentro de bucles ni condicionales).
⚠️ Solo se usan dentro de componentes funcionales o de otros hooks.

useState
Maneja estado local en un componente.

import { useState } from "react";

export default function Contador() {
  const [count, setCount] = useState(0);
  return (
    <button onClick={() => setCount(count + 1)}>
      Clics: {count}
    </button>
  );
}

useState con objetos
const [usuario, setUsuario] = useState({
  nombre: "Ana",
  edad: 25
});

function actualizarNombre() {
  setUsuario({ ...usuario, nombre: "María" });
}

Usa el operador ... (spread) para no perder propiedades previas.

useEffect
Permite ejecutar código cuando el componente se renderiza o cambian dependencias

import { useState, useEffect } from "react";

export default function DatosUsuario({ id }) {
  const [usuario, setUsuario] = useState(null);

  useEffect(() => {
    fetch(`/api/usuarios/${id}`)
      .then(res => res.json())
      .then(data => setUsuario(data));
  }, [id]);

  return usuario ? <p>{usuario.nombre}</p> : <p>Cargando...</p>;
}

https://ejecutortecnico.github.io/pri/mision3/clase3.html

Manejo de Eventos en React
Objetivos
Comprender cómo se manejan los eventos en React.
Usar funciones para responder a interacciones del usuario.
Aprender a pasar parámetros en eventos.
Conocer eventos comunes como onClick, onChange, onSubmit.

Eventos en React
Se parecen a los del DOM, pero con sintaxis camelCase.
Ejemplo: en HTML se usa onclick, en React es onClick.
React usa un sistema de eventos sintéticos para unificar navegadores.

Ejemplo: onClick
export default function Boton() {
  function manejarClick() {
    alert("¡Botón clickeado!");
  }

  return <button onClick={manejarClick}>Haz clic aquí</button>;
}

Acceso al objeto evento
export default function Input() {
  function manejarCambio(e) {
    console.log("Valor:", e.target.value);
  }

  return <input type="text" onChange={manejarCambio} />;
}

El parámetro e es un evento sintético con propiedades similares a un evento del DOM.

Prevenir comportamiento por defecto

export default function Enlace() {
  function manejarClick(e) {
    e.preventDefault(); // evita que el link navegue
    alert("Navegación bloqueada");
  }

  return (
    <a href="https://react.dev" onClick={manejarClick}>
      Ir a React
    </a>
  );
}

Pasar parámetros en eventos

export default function Producto({ id }) {
  function manejarClick(idProducto) {
    console.log("Producto clickeado:", idProducto);
  }

  return (
    <button onClick={(e) => manejarClick(id)}>
      Ver Producto
    </button>
  );
}

Eventos comunes en React
onClick → clic en un botón o elemento.
onChange → cambios en inputs, selects.
onSubmit → envío de formularios.
onMouseOver / onMouseOut → interacción con el mouse.
onKeyDown, onKeyUp → interacción con el teclado.

Ejemplo: Formulario con onSubmit

export default function Formulario() {
  function manejarSubmit(e) {
    e.preventDefault();
    alert("Formulario enviado");
  }

  return (
    <form onSubmit={manejarSubmit}>
      <input type="text" placeholder="Escribe algo" />
      <button type="submit">Enviar</button>
    </form>
  );
}

para pasar parametros usamos la funcion flecha:  <button onClick={(e) => manejarClick(id)}>

https://ejecutortecnico.github.io/pri/mision3/clase4.html
Listas y Renderizado Condicional en React
Objetivos
Aprender a recorrer arreglos con map() para renderizar listas.
Entender la importancia de las keys en los elementos de lista.
Usar condicionales para mostrar u ocultar contenido dinámicamente.

Renderizado de Listas
En React, puedes mostrar listas de elementos usando el método map() de los arreglos.
const frutas = ["🍎", "🍌", "🍊"];

export default function ListaFrutas() {
  return (
    <ul>
      {frutas.map((fruta, index) => (
        <li key={index}>{fruta}</li>
      ))}
    </ul>
  );
}

Cada elemento renderizado debe tener una propiedad key única.

Importancia de las Keys
Las keys ayudan a React a identificar qué elementos cambian, se agregan o eliminan.
Mejoran el rendimiento y evitan errores de renderizado.
Siempre deben ser únicas dentro del mismo nivel de lista.

{productos.map((item) => (
  <li key={item.id}>{item.nombre}</li>
))}

Renderizado Condicional
Puedes mostrar elementos de forma condicional usando operadores lógicos:
export default function Mensaje({ isLogged }) {
  return (
    <div>
      {isLogged ? (
        <h3>Bienvenido de nuevo 👋</h3>
      ) : (
        <h3>Por favor, inicia sesión</h3>
      )}
    </div>
  );
}

También se puede usar el operador && para mostrar algo solo si una condición es verdadera.

{tareas.length > 0 && <p>Tienes {tareas.length} tareas pendientes</p>}


Combinar Listas y Condicionales

const tareas = ["Estudiar", "Leer", "Practicar React"];

export default function ListaTareas() {
  return (
    <div>
      {tareas.length === 0 ? (
        <p>No hay tareas pendientes.</p>
      ) : (
        <ul>
          {tareas.map((t, i) => (
            <li key={i}>{t}</li>
          ))}
        </ul>
      )}
    </div>
  );
}

🔹 Este patrón es muy común en React: mostrar listas o mensajes alternativos dependiendo del estado.

Buenas Prácticas
Evita usar el índice del arreglo (index) como key, si puedes usar un ID único.
Usa fragmentos <></> si no necesitas un contenedor adicional.
Mantén el JSX legible separando las funciones de renderizado complejas.

Resumen de la Lección
map() permite renderizar listas de elementos.
Las keys únicas son necesarias para un renderizado eficiente.
El renderizado condicional permite mostrar contenido dinámico.
Combinar listas y condicionales crea interfaces interactivas y limpias.
🚀 Con esto ya puedes mostrar datos dinámicos en React de forma profesional.




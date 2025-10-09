https://ejecutortecnico.github.io/pri/mision3/clase1.html
Crear un proyecto con Vite
software:  nodejs,  npm
desde cmd: create vite@latest proyecto-react -- --template react
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


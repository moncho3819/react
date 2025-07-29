1. ¿Qué es React?
React es una biblioteca de JavaScript desarrollada por Meta (antes Facebook) para construir interfaces de usuario, especialmente aquellas que necesitan actualizarse de manera eficiente cuando cambian los datos. Se centra principalmente en el desarrollo de interfaces de usuario (UI) basadas en componentes reutilizables.

React permite crear aplicaciones web de una sola página (SPA, Single Page Applications) que se sienten rápidas y fluidas, ya que evita recargar toda la página cuando se realizan cambios en la interfaz.

2. ¿Por qué usar React?
Algunas razones por las que muchos desarrolladores eligen React:

Componentes reutilizables: Puedes dividir la interfaz en piezas pequeñas e independientes llamadas componentes, que se pueden reutilizar en diferentes partes de la aplicación.

Actualizaciones eficientes: React usa un sistema llamado Virtual DOM, que compara los cambios en la interfaz y actualiza solo lo necesario en el DOM real, mejorando el rendimiento.

Gran comunidad y ecosistema: Al ser tan popular, tiene muchas herramientas, librerías y soporte disponibles.

SEO y rendimiento: Aunque es una SPA, puede optimizarse para el SEO con herramientas como Next.js.

Aprendizaje progresivo: Puedes usarlo gradualmente en proyectos existentes sin reescribir toda la aplicación.

3. ¿Qué necesito saber antes?
Antes de comenzar a usar React, es recomendable tener conocimientos sólidos en:

HTML: Para estructurar el contenido de la interfaz.

CSS: Para darle estilo a los componentes.

JavaScript (ES6+): React está basado en JavaScript moderno, por lo que deberías entender:

Variables (let, const)

Funciones flecha

Desestructuración

Módulos (import / export)

Funciones y clases

Promesas y manejo de eventos

Opcional pero útil:

Conocer Git para control de versiones.

Conocimientos básicos de Node.js y npm para gestionar dependencias e iniciar proyectos con herramientas como create-react-app
1. ¿Qué es JSX?
JSX (JavaScript XML) es una extensión de sintaxis para JavaScript creada por el equipo de React que permite escribir un marcado similar a HTML directamente dentro del código JavaScript 
Reddit
+15
Luis Llamas
+15
es.legacy.reactjs.org
+15
. Por ejemplo:

jsx
Copiar
Editar
const elemento = <h1>Hola, mundo!</h1>;
Este fragmento parece HTML, pero no lo es: se convierte ("transpila") a una llamada a React.createElement(...), que React interpreta para generar elementos virtuales del DOM 
Wikipedia
. JSX permite expresar lógica dinámica mediante llaves {}, hacer condiciones, iteraciones, y brinda una forma más legible y segura de crear interfaces 
es.legacy.reactjs.org
Wikipedia
.

2. ¿Qué es un componente funcional?
Un componente funcional es simplemente una función de JavaScript que recibe un objeto props y devuelve JSX (una descripción de UI) 
Reddit
+15
Wikipedia
+15
es.react.dev
+15
. No requiere clases, y desde React 16.8 puede manejar estado interno y efectos usando Hooks como useState o useEffect.

Ejemplo:

jsx
Copiar
Editar
function Saludo({ nombre }) {
  return <h1>Hola, {nombre}!</h1>;
}
O en sintaxis de flecha:

jsx
Copiar
Editar
const Saludo = ({ nombre }) => <h1>Hola, {nombre}!</h1>;
React internamente lo transforma en llamadas a React.createElement(...), y al encontrarse un componente así, React lo ejecuta pasando props como argumento 
Wikipedia
+3
Wikipedia
+3
Wikipedia
+3
Reddit
+10
Reddit
+10
Kinsta®
+10
.

3. ¿Qué son los props en React?
Los props (abreviatura de “properties”) son un objeto de propiedades que se pasan a un componente desde su componente padre. Son inmutables dentro del hijo y se usan para configurar el comportamiento o los datos que muestra. Por ejemplo:

jsx
Copiar
Editar
<Saludo nombre="Carolina" />
Dentro del componente tienes acceso a props.nombre, que en este caso es "Carolina" 
Wikipedia
es.legacy.reactjs.org
. Se pueden pasar valores dinámicos dentro de llaves {}:

jsx
Copiar
Editar
<MyComponente valor={2 + 3} />
Aquí, props.valor será 5 
Luis Llamas
+14
es.legacy.reactjs.org
+14
es.legacy.reactjs.org
+14
.

4. ¿Cómo se actualiza la pantalla automáticamente al cambiar datos?
React mantiene un Virtual DOM, una estructura en memoria que representa la UI. Cada vez que cambia el estado o las props de un componente:

React vuelve a ejecutar la función del componente, generando una nueva estructura Virtual DOM.

Compara (diffing) esta estructura con la anterior.

Actualiza solo los elementos del DOM real que cambiaron 
Reddit
+5
Wikipedia
+5
Wikipedia
+5
Wikipédia
.

Este proceso (reconciliación) es lo que permite que el navegador se actualice de forma eficiente sin recargar toda la página.

5. ¿Qué hace useState?
useState es un Hook que permite mantener un estado local dentro de un componente funcional 
Wikipedia
Wikipedia
+4
es.legacy.reactjs.org
+4
Adictos al trabajo
+4
. Se usa así:

jsx
Copiar
Editar
import { useState } from 'react';

const Componente = () => {
  const [count, setCount] = useState(0);
  // count es el valor actual del estado
  // setCount es la función para actualizarlo
};
Cuando se llama a la función setCount(newValue), React actualiza el estado y vuelve a renderizar (re-render) el componente con el nuevo valor. Esto hace que React vuelva a comparar el Virtual DOM y actualice la UI en pantalla automáticamente 
Reddit
+12
es.legacy.reactjs.org
+12
Reddit
+12
.

📦 Ejemplo completo integrando todo
jsx
Copiar
Editar
import React, { useState } from 'react';

function Contador({ inicio = 0 }) {
  const [count, setCount] = useState(inicio);

  return (
    <div>
      <h1>Contador: {count}</h1>
      <button onClick={() => setCount(count + 1)}>Incrementar</button>
      <button onClick={() => setCount(count - 1)}>Decrementar</button>
      <button onClick={() => setCount(inicio)}>Reiniciar</button>
    </div>
  );
}

export default Contador;
Aquí usamos JSX para definir la UI del componente.

Contador es un componente funcional que recibe props (como inicio si se desea).

props.inicio permite pasar un valor inicial al contador.

Internamente usamos useState para manejar el estado count.

Cada vez que haces clic en un botón, llamas a setCount(...), React actualiza el estado y vuelve a renderizar solo lo necesario.
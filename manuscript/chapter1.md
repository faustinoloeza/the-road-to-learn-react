# Introducción a React

El capitulo te da una introducción a React. Podrías preguntarte: ¿Por qué debo aprender React en primer lugar? El capítulo podría darte la respuesta a esa pregunta. Después te sumergiras en el ecosistema iniciando tu primera aplicación React. En el camino se te dará una introducción a JSX y ReactDOM. Prepárate para tu primer componente React.

## Hola, mi nombre es React.

**¿Por qué deberías molestarte en aprender React?** En los últimos años las single page aplications ([SPA](https://es.wikipedia.org/wiki/Single-page_application)) se han vuelto populares. Frameworks como Angular, Ember y Backbone ayudaron a los desarrolladores JavaScript a construir aplicaciones web modernas más allá del uso de jQuery. La lista no es exhaustiva. Existe una amplia gama de frameworks SPA. Cuando consideramos las fechas de lanzamiento, la mayoría de ellos están en la primera generación de SPAs: Angular 2010, Backbone 2010, Ember 2011.

La versión inicial de React fue creada en 2013 por Facebook. React no es un framework SPA, pero sí una librería para la vista. Es la V en [MVC](https://es.wikipedia.org/wiki/Modelo%E2%80%93vista%E2%80%93controlador) (modelo vista controlador). Sólo te permite renderizar componentes como elementos visibles en un navegador. Sin embargo, todo el ecosistema alrededor de React hace posible crear aplicaciones de una sola página(SPA).

¿Pero por que deberías considerar usar React sobre la primera generación de Frameworks SPA? Mientras que la primera generación de frameworks trató de resolver muchas cosas a la vez, React solo te ayuda a construir tu capa de vista. Es una biblioteca y no un Framework. La idea detrás de ella: Su vista es una jerarquía de componentes ensamblables.

En React, puedes centrarte en tu vista antes de introducir más aspectos en tu aplicación. Cada otro aspecto es otro componente de su SPA. Estos bloques de construcción son esenciales para construir una aplicación madura. Vienen con dos ventajas.

Primera puedes aprender los bloques de construcción paso a paso. No tienes que preocuparte de entenderlos por completo. Es diferente de un framework que te da cada bloque de construcción desde el principio. Este libro se centra en React como el primer bloque de construcción. Más bloques de construcción vienen con el tiempo.

En segundo lugar todos los bloques de construcción son intercambiables. Esto hace que el ecosistema alrededor de React sea un lugar muy innovador. Múltiples soluciones están compitiendo entre sí. Puedes elegir la solución más atractiva para ti y tu caso de uso.

La primera generación de Frameworks SPA llegó a nivel empresarial. Son más rígidos. React permanece innovador y se adoptó por varias empresas líderes de pensamiento tecnológico como [Airbnb, Netflix y por supuesto Facebook](https://github.com/facebook/react/wiki/Sites-Using-React). Todos ellos invierten en el futuro de React y se conforman con React y su propio ecosistema.

React es probablemente una de las mejores opciones para la construcción de aplicaciones de una sola página hoy en día. Sólo ofrece la capa de vista, pero el ecosistema de React es un framework completo, flexible e intercambiable . React tiene una API simple, un ecosistema impresionante y una gran comunidad. Puedes leer acerca de mis experiencias del por qué me mudé de Angular a React. Recomiendo encarecidamente tener una comprensión de por qué elegiría React sobre otro Framework o biblioteca. Después de todo, todo el mundo está interesado en experimentar a donde nos guiará React en 2017 y más allá.

### Ejercicios

* Leer acerca de [por qué me moví de Angular a React](https://www.robinwieruch.de/reasons-why-i-moved-from-angular-to-react/)

## Requerimientos

Antes de que empieces a leer el libro, debes familiarizarte con HTML, CSS y JavaScript (ES5). El libro enseñará JavaScript ES6 y un poco mas. Si vienes de un marco o biblioteca SPA diferente, ya deberías estar familiarizado con los conceptos básicos. Si acabas de comenzar en el desarrollo web, deberías sentirte cómodo con HTML, CSS y JavaScript ES5 para aprender React. Les animo a que se unan al canal oficial para del libro [Slack ](https://slack-the-road-to-learn-react.wieruch.com/) para obtener ayuda o ayudar a otros.

Cada desarrollador necesita herramientas para crear aplicaciones. Necesitarás un editor (IDE) y una herramienta de terminal (línea de comandos). Puedes leer mi configuración de desarrollador para organizar tus herramientas: [Configuración del desarrollador](https://www.robinwieruch.de/developer-setup/). Se ajusta para los usuarios de Mac, pero puedes sustituir la mayoría de las herramientas para otro sistema operativo.

El editor se utiliza para organizar y escribir tu código. La terminal se utiliza para ejecutar comandos. Un comando puede iniciar tu aplicación, ejecutar pruebas o instalar otras bibliotecas para tu proyecto.

Por último, pero no menos importante, necesitarás instalar [node and npm](https://nodejs.org/es/). Ambos se utilizan para administrar las bibliotecas que necesitarás en el camino para aprender React. Se instalarán paquetes de node externos a través de npm (gestor de paquetes de node). Estos paquetes de node pueden ser bibliotecas o entornos completos.

Puedes verificar tus versiones de node y npm en la línea de comandos. Si no obtienes ninguna salida en la terminal, primero debes instalar node y npm. Estas son mis versiones:

~~~~~~~~
node --version
*v8.1.3
npm --version
*v5.0.4
~~~~~~~~

## node y npm

Este capítulo te dará un pequeño curso intensivo en nodo y npm. No es exhaustivo, pero obtendrás todas las herramientas necesarias. Si estás familiarizado con ambos, puedes omitir el capítulo.

El **manejador de paquetes de node** (npm) permite instalar **paquetes externos** desde la línea de comandos. Estos paquetes pueden ser un conjunto de funciones de utilidad, bibliotecas o entornos completos. Son las dependencias de tu aplicación. Puedes instalar estos paquetes en tu carpeta de paquetes de node global o en tu carpeta de proyecto local.

Los paquetes de node globales son accesibles desde cualquier lugar del terminal y solo hay que instalarlos una vez. Puedes instalar un paquete globalmente escribiendo en tu terminal:

~~~~~~~~
npm install -g <paquete>
~~~~~~~~

La  bandera `-g` indica a npm que debe instalar el paquete globalmente. Los paquetes locales se utilizan en tu aplicación. Por ejemplo, React como una librería será un paquete local que puede ser requerido en tu aplicación para su uso. Puedes instalarlo a través de la terminal escribiendo:

~~~~~~~~
npm install <paquete>
~~~~~~~~

En el caso de React sería:

~~~~~~~~
npm install react
~~~~~~~~

El paquete instalado aparecerá automáticamente en una carpeta llamada *node_modules/*. Pero ten cuidado. Siempre que instales un paquete local no debes olvidar la bandera `--save`:

~~~~~~~~
npm install --save <package>
~~~~~~~~

La bandera `--save` le indica a npm que debe almacenar el paquete requerido en un archivo llamado *package.json*. El archivo se puede encontrar en la carpeta del proyecto.

Sin embargo no todas las carpetas del proyecto vienen con un archivo package.json. Hay un comando npm para inicializar un proyecto npm y así un  archivo *package.json*. Solo cuando tienes ese archivo, puedes instalar un nuevo paquete localmente vía npm.

~~~~~~~~
npm init -y
~~~~~~~~

La bandera `-y` es un acceso directo para inicializar todos los valores predeterminados en tu *package.json*. Si no la usas, tienes que decidir cómo configurar el archivo.

Algo más sobre el archivo *package.json*. El archivo permite que compartas tu proyecto con otros desarrolladores sin compartir todos los paquetes node. El archivo contiene todas las referencias de los paquetes node utilizados en tu proyecto. Estos paquetes son llamados dependencias. Cualquiera puede copiar tu proyecto sin las dependencias. Las dependencias son referenciadas en el archivo *package.json*. Alguien que copie tu proyecto puede instalar todos los paquetes usando `npm install` en la línea de comandos.

Quiero cubrir un comando npm más para prevenir confusiones:

~~~~~~~~
npm install --save-dev <package>
~~~~~~~~

La bandera `--save-dev` indica que el paquete node es solo usado en el entorno de desarrollo. No será usado en producción cuando deployes tu aplicación en un servidor. Que tipo de paquete sería ese? Imagina que quieres testear tu aplicación con la ayuda de un paquete node. Necesitas instalar ese paquete a través npm, pero quieres excluirlo de tu entorno de producción. Allí ya no desearás testear tu aplicación. Ya debería estar probada y funcionar para todos los usuarios. Este es solo un caso de uso donde querrás usar la bandera `--save-dev`. 

Encontraras mas comandos npm en el camino. Pero estos serán suficientes por ahora.

### Ejercicios:

* Configurar un proyecto npm inicial 
  * crear una nueva carpeta con `mkdir <nombre_de_la_carpeta>`
  * navegue a la carpeta con `cd <nombre_de_la_carpeta>`
  * ejecute `npm init -y`
  * instale un paquete local como React con `npm install --save react`
  * échale un vistazo al archivo *package.json* y a la carpeta *node_modules/*
  * descubre como desinstalar el paquete node *react*
* leer mas sobre [npm](https://docs.npmjs.com/)

## Instalación

Hay varios enfoques para comenzar con una aplicación React.

La primera es usar un CDN. Eso puede sonar más complicado de lo que es. Un CDN es una [red de entrega de contenidos](https://es.wikipedia.org/wiki/Red_de_entrega_de_contenidos). Muchas compañías tienen CDNs que almacenan públicamente archivos para los usuarios. Estos archivos pueden ser librerías como React. Después de todo una librería puede ser solo un archivo JavaScript. Se pueden alojar en algún lugar y se pueden requerir en tu aplicación.

Cómo usar un CDN para comenzar con React? Puedes insertar la etiqueta `<script>` en su código HTML que apunta a una url de CDN. Para empezar en React necesitas dos archivos (librerías): *react* y *react-dom*.

```js
<script src="https://unpkg.com/react@15/dist/react.js"></script>
<script src="https://unpkg.com/react-dom@15/dist/react-dom.js"></script>
```

Pero por qué deberías usar un CDN cuando tienes npm para instalar paquetes node (librerías)?

Cuando tu aplicación tiene un archivo *package.json*, puedes instalar *react* y *react-dom* desde la línea de comandos. El requisito es que la carpeta se inicialice como proyecto npm con un archivo *package.json*. Puedes instalar múltiples paquetes en una línea con npm.

~~~~~~~~
npm install --save react react-dom
~~~~~~~~

Ese enfoque se utiliza a menudo para añadir React a una aplicación existente.

Desafortunadamente eso no es todo. Tendrías que lidiar con [Babel](http://babeljs.io/) para hacer tu aplicación compatible con JSX - la sintaxis de React - y JavaScript ES6. Babel transpila tu código para que los navegadores puedan interpretar ES6 y JSX. No todos los navegadores son capaces de interpretar la sintaxis. La configuración incluye una gran cantidad de configuración y herramientas. Puede ser abrumador para los principiantes molestarse con toda la configuración de React.

Por esta razón, Facebook introdujo *create-react-app* como una solución de configuración cero. El siguiente capítulo te mostrará cómo configurar tu aplicación.

### Ejercicios:

* leer mas sobre [React installations](https://facebook.github.io/react/docs/installation.html)

## Instalación de configuración-cero

En el camino de aprender React usaras [create-react-app](https://github.com/facebookincubator/create-react-app) tpara arrancar tu aplicación. Se trata de un kit de inicio, pero de configuración cero para React, introducido por Facebook en 2016. La gente [lo recomienda a los principiantes en un 96%](https://twitter.com/dan_abramov/status/806985854099062785). En *create-react-app* las herramientas y la configuración evolucionan en segundo plano mientras que el foco está en la implementación de la aplicación

Para empezar, necesitaras instalar el paquete a tus paquetes globales node. Después de eso siempre los tendrás disponibles en la línea de comandos para inicializar nuevas aplicaciones React.

~~~~~~~~
npm install -g create-react-app
~~~~~~~~

Puedes comprobar la versión de *create-react-app* para verificar una instalación correcta en la linea de comandos:

~~~~~~~~
create-react-app --version
~~~~~~~~

Debe darte la versión. La mía es la: 1.3.3.

Ahora puedes iniciar tu primera aplicación React. La llamamos *hackernews*, pero puedes elegir otro nombre. Después simplemente navega hacia la carpeta:

~~~~~~~~
create-react-app hackernews
cd hackernews
~~~~~~~~

Ahora puedes abrir la aplicación en tu editor. La siguiente estructura de carpetas, o variación de esta depende de la versión de create-react-app, debería mostrarte:

~~~~~~~~
hackernews/
  README.md
  node_modules/
  package.json
  .gitignore
  public/
    favicon.ico
    index.html
  src/
    App.css
    App.js
    App.test.js
    index.css
    index.js
    logo.svg
~~~~~~~~

Al principio todo lo que necesitas se encuentra en la carpeta *src/*.

El foco principal se encuentra en el archivo *src/App.js* para implementar componentes React. Se utilizará para implementar tu aplicación, pero más adelante desees dividir tus componentes en varios archivos.

Adicionalmente encontrarás un archivo *src/App.test.js* para pruebas y un *src/index.js* como punto de entrada al mundo de React. Conocerás ambos archivos en un capítulo posterior. Además, hay un archivo *src/index.css* y un archivo *src/App.css* para darle estilos a tu aplicación y componentes. Todos vienen con estilo por defecto cuando se abren.

Al lado de la carpeta *src/* encontrarás el archivo *package.json*  y la carpeta  *node_modules/* para administrar tus paquetes node. La aplicación *create-react-app* es un proyecto npm. Puedes usar npm para instalar y desinstalar paquetes node en tu proyecto.

El proyecto  *create-react-app* viene con los siguientes scripts npm para su línea de comandos:

```js
// Ejecuta la aplicacion en http://localhost:3000
npm start

// Ejecuta las pruebas
npm test

// Crea la aplicación para la producción
npm run build
```

Los scripts también se definen en el *package.json*. Tu aplicación React está inicializada.

### Ejercicios:

* `npm start` inicia tu aplicación y visita la pagina en tu navegador 
* ejecuta el comando interactivo `npm test`
* familiarizate con la estrutura de carpetas
* familiarizate con el contenido de los archivos
* leer mas sobre [los comandos y create-react-app](https://github.com/facebookincubator/create-react-app)

## Introducción a JSX

Ahora conocerás a JSX. Es la sintaxis de React. Como he mencionado antes *create-react-app* ya ha iniciado una aplicación estándar.Todos los archivos vienen con implementaciones predeterminadas. Vamos a sumergirnos en el código fuente.

El único archivo que tocará al principio será el archivo *src/App.js*.

```js
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <div className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h2>Welcome to React</h2>
        </div>
        <p className="App-intro">
          To get started, edit <code>src/App.js</code> and save to reload.
        </p>
      </div>
    );
  }
}

export default App;
```

No te dejes confundir por las declaraciones de import/export y declaración de clases. Estas características son JavaScript ES6. Volveremos a verlas en un capítulo posterior.

En el archivo tienes un **componente ES6 class** con el nombre App. Es una declaración de componente. Básicamente después de haber declarado un componente, puedes utilizarlo como elemento en cualquier parte de tu aplicación. Producirá una **instancia** de tu **componente** o en otras palabras: El componente se instancia.

El **elemento** que devuelve se especifica en el método `render()`. Los elementos son de lo que están hechos los componentes. Es útil comprender las diferencias entre componente, instancia y elemento.

Muy pronto veras donde se utiliza el componente App. De lo contrario, no verá la salida renderizada en el navegador, verdad? El componente App es sólo la declaración, pero no el uso. Se podría instanciar el componente en algún lugar de tu JSX con `<App />`.

El contenido en el bloque render se parece bastante a HTML, pero es JSX. JSX te permite mezclar HTML y JavaScript. Es potente pero confuso cuando estás acostumbrado a HTML simple. Es por eso que un buen punto de partida es utilizar HTML básico en tu JSX. A continuación, puedes empezar a insertar expresiones JavaScript entre llaves.

Primero vamos a eliminar todo el desorden en el archivo.

```js
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <h2>Welcome to the Road to learn React</h2>
      </div>
    );
  }
}

export default App;
```

Ahora sólo devuelve HTML sin JavaScript. Hagamos una variable "Bienvenido al camino para aprender React". Una variable puede utilizarse en su JSX.

```js
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
    var helloWorld = 'Bienvenido al camino para aprender React';
    return (
      <div className="App">
        <h2>{helloWorld}</h2>
      </div>
    );
  }
}

export default App;
```

Debería funcionar cuando inicies tu aplicación en la línea de comandos.

Además, es posible que hayas notado el atributo `className`. Refleja el atributo estándar `class` en HTML. Debido a razones técnicas, JSX tuvo que reemplazar un puñado de atributos HTML internos. Puede encontrar todos los [atributos HTML compatibles en la documentación de React](https://facebook.github.io/react/docs/dom-elements.html). En tu camino para aprender React te encontrarás con más atributos JSX.

### Ejercicios:

* Definir más variables y renderizarlas en tu JSX
  * Utilizar un objeto complejo para representar a un usuario con nombre y apellido
* leer mas sobre [JSX](https://facebook.github.io/react/docs/introducing-jsx.html)
* leer mas sobre [React componentes, elementos e instancias](https://facebook.github.io/react/blog/2015/12/18/react-components-elements-and-instances.html)

## ES6 const y let

Supongo que notaste que declaramos la variable `helloWorld` con `var`. JavaScript ES6 viene con dos opciones más para declarar sus variables: `const` y `let`. En JavaScript ES6 rara vez encontrarás `var`. Daremos una explicación para `const` y `let`:

Una variable declarada con `const` no se puede volver a asignar o volver a declarar. No puede ser mutada (cambiada, modificada). Adoptas estructuras de datos inmutables al usarlo. Una vez que se define la estructura de datos, no se puede cambiar.

```js
// No permitido
const helloWorld = 'Welcome to the Road to learn React';
helloWorld = 'Bye Bye React';
```

Una variable declarada con `let` puede mutar.

```js
// Permitido
let helloWorld = 'Welcome to the Road to learn React';
helloWorld = 'Bye Bye React';
```

Lo usarás cuando necesites reasignar una variable.

Sin embargo, hay que tener cuidado con `const`. Una variable declarada con `const` no se puede modificar. Pero cuando la variable es un array o un objeto, el valor que tiene puede ser alterado. El valor que tiene no es inmutable.

```js
// allowed
const helloWorld = {
  text: 'Welcome to the Road to learn React'
};
helloWorld.text = 'Bye Bye React';
```

Pero ¿cuando usar cada una? Hay diferentes opiniones sobre su uso. Sugiero usar `const` cada que puedas. Indica que desea mantener su estructura de datos inmutable aunque los valores en objetos y arreglos se pueden modificar. Si desea modificar la variable, puede utilizar `let`.

La inmutabilidad es adoptada en React y su ecosistema. Es por eso que `const` debe ser tu opción por defecto cuando se define una variable. Sin embargo, en objetos complejos los valores internos pueden ser modificados. Ten cuidado con este comportamiento.

En su aplicación debe utilizar `const` sobre `var`.

```js
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
# leanpub-start-insert
    const helloWorld = 'Welcome to the Road to learn React';
# leanpub-end-insert
    return (
      <div className="App">
        <h2>{helloWorld}</h2>
      </div>
    );
  }
}

export default App;
```

### Ejercicios:

* leer mas sobre ES6 [const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
* leer mas sobre ES6 [let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
* investigue más sobre estructuras de datos inmutables
  * ¿Por qué tienen sentido en la programación en general?
  * ¿Por qué se utilizan en React y su ecosistema?

## ReactDOM

Antes de continuar con el componente App, es posible que desee ver dónde se utiliza. Se encuentra en tu punto de entrada al mundo de React: el archivo *src/index.js*.

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import './index.css';

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

Básicamente `ReactDOM.render()` usa un nodo DOM en tu HTML para reemplazarlo con tu JSX. Así es como puedes integrar fácilmente React en cualquier aplicación externa. No está prohibido utilizar `ReactDOM.render()` varias veces en tu aplicación. Puedes utilizarlo en varios lugares para iniciar la sintaxis JSX simple, un componente React, múltiples componentes React o una aplicación completa.

`ReactDOM.render()` espera dos argumentos.

El primer argumento es JSX que se renderizara. El segundo argumento especifica el lugar en el que la aplicación React se insertará en tu código HTML. Espera un elemento con un `id='root'`. Puedes abrir tu archivo *public/index.html* para encontrar el atributo id.

En la implementación `ReactDOM.render()` ya tiene tu componente App. Sin embargo, sería bueno pasar JSX más simple, siempre y cuando sea JSX. No tiene que ser una instancia de un componente.

```js
ReactDOM.render(
  <h1>Hello React World</h1>,
  document.getElementById('root')
);
```

### Ejercicios:

* abre el *public/index.html* para ver dónde se conectan las aplicaciones React en tu HTML
* leer mas sobre [renderizando elementos en React](https://facebook.github.io/react/docs/rendering-elements.html)

## Módulo Hot Reloading

Hay una cosa que usted puede hacer en el archivo *src/index.js* para mejorar su experiencia como desarrollador.

En *create-react-app* ya es una ventaja que el navegador actualice automáticamente la página cuando cambia el código fuente. Inténtelo cambiando la variable `helloWorld` en tu archivo *src/App.js*. El navegador debe actualizar la página. Pero puedes hacerlo mejor.

Modulo Hot Reloading (HMR) es una herramienta para recargar su aplicación en el navegador. El navegador no actualiza la página. Puede activarlo fácilmente en *create-react-app*. En tu *src/index.js* - tu punto de entrada de React -  tienes que agregar una pequeña configuración.

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import './index.css';

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
if (module.hot) {
  module.hot.accept()
}
```

Eso es todo. Intente cambiar de nuevo la variable `hellowWorld` en tu archivo *src/App.js*. El navegador no debe actualizar la página, pero la aplicación vuelve a cargar y muestra la salida correcta. HMR viene con múltiples ventajas:

Imagine que está depurando su código con declaraciones `console.log()`. Estas declaraciones permanecerán en la consola de desarrolladores, incluso si cambia su código, porque el navegador ya no actualiza la página. Eso puede ser conveniente para fines de depuración.

En una aplicación en crecimiento, una actualización de página demora su productividad. Tienes que esperar hasta que la página se cargue. Una recarga de página puede tardar varios segundos en una aplicación grande. HMR quita esta desventaja.

El mayor beneficio es que puede mantener el estado de la aplicación con HMR. Imagine que tiene un diálogo en su aplicación con varios pasos y que está en el paso 3. Básicamente es un mago. Sin HMR cambiaría el código fuente y su navegador actualizará la página. Usted tendría que abrir el cuadro de diálogo de nuevo y sin tener que navegar desde el paso 1 al paso 3. Con HMR su diálogo permanece abierto en el paso 3. Mantiene el estado de la aplicación aunque el código fuente cambie. La aplicación misma se vuelve a cargar, pero no la página.

### Ejercicios:

* cambia el código fuente de *src/App.js* algunas veces para ver HMR en acción
* ver los primeros 10 minutos de [Live React: Hot Reloading with Time Travel](https://www.youtube.com/watch?v=xsSnOQynTHs) po Dan Abramov

## JavaScript complejo en JSX

Volvamos al componente App. Hasta ahora se han renderizado algunas variables primitivas en su JSX. Ahora usted comenzará a renderizar una lista de artículos.La lista será datos artificiales en el principio, pero más tarde obtendrás los datos de una API externa. Eso será mucho más emocionante.

Primero tienes que definir la lista de elementos.

```js
import React, { Component } from 'react';
import './App.css';

const list = [
  {
    title: 'React',
    url: 'https://facebook.github.io/react/',
    author: 'Jordan Walke',
    num_comments: 3,
    points: 4,
    objectID: 0,
  },
  {
    title: 'Redux',
    url: 'https://github.com/reactjs/redux',
    author: 'Dan Abramov, Andrew Clark',
    num_comments: 2,
    points: 5,
    objectID: 1,
  },
];

class App extends Component {
  ...
}
```

Los datos artificiales reflejarán los datos que extraeremos más adelante de la API. Un elemento de la lista tiene un título, una url y un autor. Además viene con un identificador, puntos (que indican la popularidad de un artículo) y un recuento de comentarios.

Ahora puede utilizar la función de `map` JavaScript incorporada en su JSX. Te permite iterar sobre tu lista de elementos para mostrarlos. Como se mencionó, usará llaves para encapsular la expresión JavaScript en su JSX.

```js
class App extends Component {

  render() {
    return (
      <div className="App">
        { list.map(function(item) {
          return <div>{item.title}</div>;
        })}
      </div>
    );
  }
}

export default App;
```

Eso es bastante poderoso en JSX. Por lo general, es posible que haya utilizado `map` para convertir una lista de elementos a otra lista de elementos. Esta vez utiliza `map` para convertir una lista de elementos en elementos HTML.

Hasta ahora, sólo se mostrará el `título` de cada elemento. Pero vamos a mostrar algunas más de las propiedades del artículo.

```js
class App extends Component {

  render() {
    return (
      <div className="App">
        { list.map(function(item) {
          return (
            <div>
              <span>
                <a href={item.url}>{item.title}</a>
              </span>
              <span>{item.author}</span>
              <span>{item.num_comments}</span>
              <span>{item.points}</span>
            </div>
          );
        })}
      </div>
    );
  }
}

export default App;
```

Puede ver cómo la función map está simplemente en línea en su JSX. Cada propiedad de elemento se muestra en una etiqueta `<span>`. Además, la propiedad url del elemento se utiliza en el atributo `href` de la etiqueta de anclaje.

React hará todo el trabajo por usted y mostrara cada elemento. Pero debe agregar un helper para que React alcance su máximo potencial y mejore su rendimiento. Debe asignar un atributo key a cada elemento de lista. Así, React es capaz de identificar los elementos añadidos, cambiados y eliminados cuando la lista cambia. Los elementos artificiales de la lista ya vienen con un identificador.

```js
{
  list.map(function(item) {
    return (
      <div key={item.objectID}>
        <span>
          <a href={item.url}>{item.title}</a>
        </span>
        <span>{item.author}</span>
        <span>{item.num_comments}</span>
        <span>{item.points}</span>
      </div>
    );
  });
}
```

Debe asegurarse de que el atributo key es un identificador estable. No cometa el error de usar el índice de elementos en el array. El índice del array no es del todo estable. Por ejemplo, cuando la lista cambia su orden, React tendrá dificultades para identificar los elementos correctamente.

```js
// don't do this
{ list.map(function(item, key) {
  return (
    <div key={key}>
      ...
    </div>
  );
})}
```

Ahora mostrarás los dos elementos de la lista. Puedes iniciar tu aplicación, abrir tu navegador y ver los dos elementos de la lista desplegados.

### Ejercicios:

* leer mas sobre [React lists and keys](https://facebook.github.io/react/docs/lists-and-keys.html)
* recapitular el [standard built-in Array functionalities in JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
* Utilice más expresiones JavaScript por tu cuenta en JSX

## ES6 Arrow Functions

JavaScript ES6 introduce arrow functions. Una expresión arrow function es más corta que una expresión de funcion.

```js
// function expression
function () { ... }

// arrow function expression
() => { ... }
```

Pero tienes que ser consciente de sus funcionalidades. Uno de ellos es un comportamiento diferente con el objeto `this`. Una function expression siempre define su propio objeto `this`. Arrow function expressions aún tienen el objeto `this` del contexto cerrado. No se confunda al usar `this` en una arrow function.

Hay otro hecho valioso sobre las arrow function con respecto al paréntesis. Puedes quitar los paréntesis cuando la función sólo obtiene un argumento, pero tienen que mantenerlos cuando tengas múltiples argumentos.

```js
// allowed
item => { ... }

// allowed
(item) => { ... }

// not allowed
item, key => { ... }

// allowed
(item, key) => { ... }
```

Sin embargo, echemos un vistazo a la función `map`. Puedes escribirla más concisamente con una ES6 arrow function.

```js
{ list.map(item => {
  return (
    <div key={item.objectID}>
      <span>
        <a href={item.url}>{item.title}</a>
      </span>
      <span>{item.author}</span>
      <span>{item.num_comments}</span>
      <span>{item.points}</span>
    </div>
  );
})}
```

Además, puede eliminar el *cuerpo del bloque* de la ES6 arrow function. En un *cuerpo conciso* un return implícito se adjunta así que usted puede quitar la declaración return. Eso sucederá más a menudo en el libro, así que asegúrese de entender la diferencia entre un cuerpo de bloque y un cuerpo conciso.

```js
{ list.map(item =>
  <div key={item.objectID}>
    <span>
      <a href={item.url}>{item.title}</a>
    </span>
    <span>{item.author}</span>
    <span>{item.num_comments}</span>
    <span>{item.points}</span>
  </div>
)}
```

Ahora su JSX se ve más conciso y legible. Omite la sentencia function, las llaves y la declaración return.

### Ejercicios:

* leer mas sobre [ES6 arrow functions](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

## ES6 Classes

JavaScript ES6 introdujo clases. Una clase se utiliza comúnmente en lenguajes de programación orientados a objetos. JavaScript fue y es muy flexible en sus paradigmas de programación. Puedes hacer programación funcional y programación orientada a objetos lado a lado para sus casos de uso particulares.

Aunque React adopta la programación funcional, por ejemplo con estructuras de datos inmutables, las clases se utilizan para declarar componentes. Se les llama componentes clase ES6. React mezcla las partes buenas de ambos paradigmas de programación.

Consideremos la siguiente clase Developer para examinar una clase de JavaScript ES6 sin pensar en un componente

```js
class Developer {
  constructor(firstname, lastname) {
    this.firstname = firstname;
    this.lastname = lastname;
  }

  getName() {
    return this.firstname + ' ' + this.lastname;
  }
}
```

Una clase tiene un constructor para hacerla instanciable. El constructor puede tomar argumentos para asignarlos a la instancia de clase. Además, una clase puede definir funciones. Dado que la función está asociada a una clase, se llama método. A veces se referencia como un metodo de clase.

La clase Developer es sólo la declaración de clase. Puedes crear varias instancias de la clase invocándola. It is similar to the ES6 class component, que tiene una declaración, pero tienes que usarlo en otro lugar para instanciarlo.

Veamos cómo se puede instanciar la clase y cómo se pueden utilizar sus métodos.

```js
const robin = new Developer('Robin', 'Wieruch');
console.log(robin.getName());
// output: Robin Wieruch
```

React utiliza clases de JavaScript ES6 para componentes de clase ES6. Ya has utilizado un componente de clase ES6.

```js
import React, { Component } from 'react';

...

class App extends Component {
  render() {
    ...
  }
}
```

La clase App se extiende de `Component`. Básicamente, se declara el componente App, pero se extiende desde otro componente.¿Qué significa extender? En la programación orientada a objetos tienes el principio de herencia. Se utiliza para pasar funcionalidades de una clase a otra clase.

La clase App extiende la funcionalidad de la clase Component. Para ser más específico, hereda funcionalidades de la clase Component. El componente se utiliza para extender una clase ES6 básica a una clase de componente ES6. Tiene todas las funcionalidades que un componente necesita tener. Una de estas funcionalidades, un método, que ya utilizaste: el metodo `render()`. Pero aprenderás más funcionalidades.

La clase `Component` encapsula todas las funcionalidades de React que un desarrollador no necesita ver. Permite a los desarrolladores utilizar clases como componentes en React.

Los métodos que un `Component` React expone es la interfaz pública. Uno de estos métodos tiene que sobrescribirse, los otros no necesitan ser sobrescritos. Aprenderá acerca de estos últimos cuando el libro llegue a los métodos del ciclo de vida en un capítulo posterior. El metodo `render()`iene que ser sobrescrito, porque define la salida de un React `Component`.

Ahora conoce los conceptos básicos de las clases de JavaScript ES6 y cómo se utilizan en React para extenderlas a componentes. Como dije, aprenderá más sobre los métodos de Componente cuando el libro describa los métodos del ciclo de vida React.

### Ejercicios:

* leer mas sobre [ES6 classes](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes)


Has aprendido a arrancar tu propia aplicación React! Repasemos los últimos capítulos:

* React
  * create-react-app arranca una aplicación React
  * JSX mezcla HTML y JavaScript para definir los componentes React
  * componentes, instancias y elementos son cosas diferentes
  * `ReactDOM.render()` es un punto de entrada para una aplicación React
  * funciones JavaScript incorporadas se pueden utilizar en JSX
    * map puede utilizarse para renderizar una lista de elementos como elementos HTML
* ES6
  * Declaraciones de variables con `const` y `let` para casos de uso particulares
  * arrow functions pueden utilizarse para acortar las declaraciones de funciones
  * las clases se utilizan para definir componentes en React

Tiene sentido hacer una pausa en este punto. Internalizar lo aprendido y aplicarlos por su cuenta. Puedes experimentar con el código fuente que ha escrito hasta ahora.

Puede encontrar el código fuente en el [repositorio oficial](https://github.com/rwieruch/hackernews-client/tree/0c5a701170dcc72fe68bdd594df3a6522f58fbb3).

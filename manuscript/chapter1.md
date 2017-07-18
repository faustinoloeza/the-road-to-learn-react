# Introducción a React

El capitulo te da una introducción a React. Podrias preguntarte: ¿Por que debo aprender React en primer lugar? El capitulo podria darte la respuesta a esa pregunta. Despues te sumergiras en el ecosistema iniciando tu primera aplicación React. En el camino se te dara una introducción a JSX y ReactDOM. Preparate para tu primer componente React.

## Hola, mi nombre es React.

**¿Por qué deberías molestarte en aprender React?** En los ultimos años las single page aplications ([SPA](https://es.wikipedia.org/wiki/Single-page_application)) se han vuelto popular. Frameworks como Angular, Ember y Backbone ayudaron a los desarrolladores JavaScript a construir aplicaciones web modernas más allá del uso de jQuery. La lista no es exhaustiva. Existe una amplia gama de  SPA frameworks. Cuando consideras las fechas de lanzamiento, La mayoría de ellos están entre la primera generación de SPAs: Angular 2010, Backbone 2010, Ember 2011.

La versión inicial de React fue en 2013 por Facebook. React no es un SPA framework pero si una libreria para la vista. Es la V en [MVC](https://es.wikipedia.org/wiki/Modelo%E2%80%93vista%E2%80%93controlador) (modelo vista controlador). Sólo le permite renderizar componentes como elementos visibles en un navegador. Sin embargo, todo el ecosistema alrededor de React hace posible crear aplicaciones de una sola página(SPA).

Pero por que deberias considerar usar React sobre la primera generacion de Frameworks SPA? Mientras que la primera generación de frameworks trató de resolver muchas cosas a la vez, React solo te ayuda a construir tu capa de vista. Es una biblioteca y no un Framework. La idea detrás de ella: Su vista es una jerarquía de componentes componibles.

En React, puedes centrarte en tu vista antes de introducir más aspectos en su aplicación. Cada otro aspecto es otro componente de su SPA. Estos bloques de construcción son esenciales para construir una aplicación madura. Vienen con dos ventajas.

Primero puedes aprender los bloques de construcción paso a paso. No tienes que preocuparte de entenderlos por completo. Es diferente de un marco que le da cada bloque de construcción desde el principio. Este libro se centra en React como el primer bloque de construcción. Más bloques de construcción siguen con el tiempo.

En segundo lugar todos los bloques de construcción son intercambiables. Hace que el ecosistema alrededor de React sea un lugar tan innovador. Múltiples soluciones están compitiendo entre sí. Puede elegir la solución más atractiva para usted y su caso de uso.

La primera generación de Frameworks de SPA llegó a nivel empresarial. Son más rígidos. Reac permanece innovador y se adopto por varias empresas líderes de pensamiento tecnológico como [Airbnb, Netflix y por supuesto Facebook](https://github.com/facebook/react/wiki/Sites-Using-React). Todos ellos invierten en el futuro de React y se conforman con React y su propio ecosistema.

React es probablemente una de las mejores opciones para la construcción de aplicaciones de una sola página hoy en día. Sólo ofrece la capa de vista, pero el ecosistema de React es un framework completo, flexible e intercambiable . React tiene una API simple, un ecosistema impresionante y una gran comunidad. Puedes leer acerca de mis experiencias del por qué me mudé de Angular a React. Recomiendo encarecidamente tener una comprensión de por qué elegiría React sobre otro Framework o biblioteca. Después de todo, todo el mundo está interesado en experimentar a donde nos guiará React en 2017 y más allá.

### Ejercicios

* Leer acerca de [por qué me moví de Angular a React](https://www.robinwieruch.de/reasons-why-i-moved-from-angular-to-react/)

## Requerimientos

Antes de empezar a leer el libro, debe familiarizarse con HTML, CSS y JavaScript (ES5). El libro enseñará JavaScript ES6 y más allá. Si vienes de un marco o biblioteca de SPA diferente, ya deberías estar familiarizado con los conceptos básicos. Si acaba de comenzar en el desarrollo web, debería sentirse cómodo con HTML, CSS y JavaScript ES5 para aprender React. Les animo a que se unan al canal oficial [Slack ](https://slack-the-road-to-learn-react.wieruch.com/) para obtener el libro o ayudar a otros .

Cada desarrollador necesita herramientas para crear aplicaciones. Necesitaras un editor (IDE) y una herramienta de terminal (línea de comandos). Puedes leer mi configuración de desarrollador para organizar tus herramientas: [Configuración del desarrollador](https://www.robinwieruch.de/developer-setup/). Se ajusta para los usuarios de Mac, pero puedes sustituir la mayoría de las herramientas para otro sistema operativo.

El editor se utiliza para organizar y escribir su código. El terminal se utiliza para ejecutar comandos. Un comando puede ser iniciar su aplicación, ejecutar pruebas o instalar otras bibliotecas para su proyecto.

Por último, pero no menos importante, necesitará instalar [node and npm](https://nodejs.org/es/). Ambos se utilizan para administrar las bibliotecas que necesitará en el camino para aprender React. Se instalarán paquetes de node externos a través de npm (gestor de paquetes de node). Estos paquetes de node pueden ser bibliotecas o entornos completos.

Puedes verificar tus versiones de node y npm en la línea de comandos. Si no obtiene ninguna salida en la terminal, primero debe instalar node y npm. Estas son mis versiones:

~~~~~~~~
node --version
*v8.1.3
npm --version
*v5.0.4
~~~~~~~~

## node y npm

Este capítulo le dara un pequeño curso intensivo en nodo y npm. No es exhaustivo, pero obtendrá todas las herramientas necesarias. Si está familiarizado con ambos, puede omitir el capítulo.

El **manejador de paquetes de node** (npm) Permite instalar **paquetes externos **desde la linea de comandos. Estos paquetes pueden ser un conjunto de funciones de utilidad, bibliotecas o entornos completos. Son las dependencias de su aplicación. Puede instalar estos paquetes en su carpeta de paquetes de node global o en su carpeta de proyecto local.

Los paquetes de nodos globales son accesibles desde cualquier lugar del terminal y solo hay que instalarlos una vez. Puede instalar un paquete global escribiendo su terminal:

~~~~~~~~
npm install -g <paquete>
~~~~~~~~

La `-g` bandera indica a npm que debe instalar el paquete globalmente. Los paquetes locales se utilizan en su aplicación. Por ejemplo, React como una biblioteca será un paquete local que puede ser requerido en su aplicación para su uso.Puede instalarlo a través de la terminal escribiendo:

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

Sin embargo no todas las carpetas del proyecto vienen con un archivo package.json. Hay un comando npm para inicializar un proyecto npm y asi un  archivo *package.json*. Solo cuando tienes ese archivo, puedes instalar un nuevo paquete localmente via npm.

~~~~~~~~
npm init -y
~~~~~~~~

La bandera `-y` es un acceso directo para inicializar todos los valores predeterminados en tu *package.json*. Si no lo usas, tienes que decidir como configurar el archivo.

Algo mas sobre el archivo *package.json*. El archivo permite que compartas tu proyecto con otros desarrolladores sin compartir todos los paquetes node. El archivo contiene todas las referencias de los paquetes node utilzados en tu proyecto. Estos paquetes son llamados dependencias. Cualquiera puede copiar tu proyecto sin las depencias. Las dependencias son referenciadas en el archivo *package.json*. Alguien que copie tu proyecto puede instalar todos los paquetes usando `npm install` en la linea de comandos.

Quiero cubrir un comando npm mas para prevenir confusiones:

~~~~~~~~
npm install --save-dev <package>
~~~~~~~~

La bandera `--save-dev` indica que el paquete node es solo usado en el entorno de desarollo. No sera usado en producción cuando deployes tu aplicacion en un servidor. Que tipo de paquete seria ese? Imagina que quieres testear tu aplicacion con la ayuda de un paquete node. Necesitas instalar ese paquete a traves npm, pero quieres excluirlo de tu entorno de producción. Alli ya no desearas testear tu aplicación. Ya debería estar probada y funcionar para todos los usuarios. That's only one use case where you would want to use the `--save-dev` flag. Este es solo un caso de uso donde querras usar la bandera `--save-dev`. 

Encontraras mas comandos npm en el camino. Pero estos seran sufientes por ahora.

### Ejercicios:

* Configurar un proyecto npm inicial 
  * crear una nueva carpeta con `mkdir <nombre_de_la_carpeta>`
  * navegue a la carpeta con `cd <nombre_de_la_carpeta>`
  * ejecute `npm init -y`
  * instale un paquete local como React con `npm install --save react`
  * echale un vistazo al archivo *package.json* y a la carpeta *node_modules/*
  * descubre como desinstalar el paquete node *react*
* leer mas sobre [npm](https://docs.npmjs.com/)

## Instalación

Hay varios enfoques para comenzar con una aplicación React.

La primera es usar un CDN. Eso puede sonar más complicado de lo que es. Un CDN es una [red de entrega de contenidos](https://es.wikipedia.org/wiki/Red_de_entrega_de_contenidos). Muchas compañias tienen CDNs que almacenan publicamente archivos para los usuarios. Estos archivos pueden ser librerias como React. Despues de todo una libreria puede ser solo un archivo JavaScript. Se pueden alojar en algún lugar y se pueden requerir en tu aplicación.

Como usar un CDN para comenzar con React? Puedes insertar la etiqueta `<script>` en su código HTML que apunta a una url de CDN. Para empezar en React necesitas dos archivos (librerias): *react* y *react-dom*.

~~~~~~~~
<script src="https://unpkg.com/react@15/dist/react.js"></script>
<script src="https://unpkg.com/react-dom@15/dist/react-dom.js"></script>
~~~~~~~~

Pero por que deberias usar un CDN cuando tienes npm para instalar paquetes node (librerias)?

Cuando tu aplicacion tien un archivo *package.json*, puedes instalar *react* y *react-dom* desde la linea de comandos. El requisito es que la carpeta se inicialice como proyecto npm con un archivo *package.json*. Puedes instalar multiples paquetes en una linea con npm.

~~~~~~~~
npm install --save react react-dom
~~~~~~~~

Ese enfonque se utiliza a menudo para añadir React a una aplicación existente.

Desafortunadamente eso no es todo. Tendrias que lidear con [Babel](http://babeljs.io/) para hacer tua aplicacion compatible con JSX - la sintaxis de React - y JavaScript ES6. Babel transpiles your code that browsers can interpret ES6 and JSX. No todos los navegadores son capaces de interpretar la sintanxis. La configuración incluye una gran cantidad de configuración y herramientas. Puede ser abrumador para los principientes molestarse con toda la configuración de React.

Por esta razon, Facebook introdujo *create-react-app* como una solucion de configuración cero. El siguiente capítulo te mostrará cómo configurar su aplicación.

### Ejercicios:

* leer mas sobre [React installations](https://facebook.github.io/react/docs/installation.html)

## Configuración de configuración-cero

En el camino de aprender React usaras [create-react-app](https://github.com/facebookincubator/create-react-app) tpara arrancar tu aplicación. It's an opinionated yet zero-configuration starter kit for React introduced by Facebook in 2016. La gente [lo recomenda a los principiantes en un 96%](https://twitter.com/dan_abramov/status/806985854099062785). En *create-react-app* las herramientas y la configuración evolucionan en segundo plano mientras que el foco está en la implementación de la aplicación

Para empezar, necesitaras instalar el paquete a tus paquetes globales node. Despues de eso siempre los tendras disponibles en la linea de comandos para inicializar nuevas aplicaciones React.

~~~~~~~~
npm install -g create-react-app
~~~~~~~~

Puedes comprobar la versión de *create-react-app* para verificar una instalación correcta en la linea de comandos:

~~~~~~~~
create-react-app --version
~~~~~~~~

Debe darte la version. La mia es la: 1.3.3.

Ahora puedes iniciar tu primera aplicación React. La llamamos *hackernews*, pero puedes elegir otro nombre. Despues simplemente navega hacia la carpeta:

~~~~~~~~
create-react-app hackernews
cd hackernews
~~~~~~~~

Ahora puedes abrir la aplcación en tu editor. La siguiente estructura de carpetas, o variacion de esta depente de la version de create-react-app, deberia mostrarte:

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

El foco principal se encuentra en el archivo *src/App.js* para implementar componentes React. Se utilizara para implementar tu aplicación, pero mas adelante desees dividir tus componentes en varios archivos.

Adicionalmente encontras un archivo *src/App.test.js* para pruebas y un *src/index.js* como punto de entrada al mundo de React. Conoceras ambos archivos en un capitulo posterior.Ademas, hay un archivo *src/index.css* y un archivo *src/App.css* para darle estilos a tu aplicación y componentes. Todos vienen con estilo por defecto cuando se abren.

Al lado de la carpeta *src/* encontrarás el archivo *package.json*  y la carpeta  *node_modules/* para administrar tus paquetes node. La aplicación *create-react-app* es un proyecto npm. Puede usar npm para instalar y desinstalar paquetes node en tu proyecto.

El proyecto  *create-react-app* viene con los siguientes scripts npm para su línea de comandos:

~~~~~~~~
// Ejecuta la aplicacion en http://localhost:3000
npm start

// Ejecuta las pruebas
npm test

// Crea la aplicación para la producción
npm run build
~~~~~~~~

Los scripts también se definen en el *package.json*. Tu aplicacion React esta inicializada.

### Ejercicios:

* `npm start` inicia tu aplicacion y visita la pagina en tu navegador 
* ejecuta el comando interactivo `npm test`
* familiarizate con la estrutura de carpetas
* familiarizate con el contenido de los archivos
* leer mas sobre [los comandos y create-react-app](https://github.com/facebookincubator/create-react-app)

## Introducción a JSX

Ahora conocerás a JSX. Es la sintaxis de React. Como he mencionado antes, *create-react-app* ya ha iniciado una aplicación estándar.Todos los archivos vienen con implementaciones predeterminadas. Vamos a sumergirnos en el código fuente.

El único archivo que tocará al principio será el archivo *src/App.js*.

~~~~~~~~
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
~~~~~~~~

No te dejes confundir por las declaraciones de import/export y declaracion de clases. Estas características son JavaScript ES6. Volveremos a verlas en un capítulo posterior.

En el archivo tienes un ** componente ES6 class ** con el nombre App. Es una declaración de componente. Básicamente después de haber declarado un componente, puedes utilizarlo como elemento en cualquier parte de tu aplicación. Producirá una **instancia** de su **componente** o en otras palabras: El componente se instancia.

El **elemento** que devuelve se especifica en el método `render()`. Los elementos son de lo que estan hechos los componentes. Es útil comprender las diferencias entre componente, instancia y elemento.

Muy pronto veras donde se utiliza el componente App. De lo contrario, no verá la salida renderizada en el navegador, verdad? El componente App es sólo la declaración, pero no el uso. Se podría instanciar el componente en algún lugar de su JSX con `<App />`.

El contenido en el bloque render se parece bastante a HTML, pero es JSX. JSX le permite mezclar HTML y JavaScript. Es potente pero confuso cuando estás acostumbrado a HTML simple. Es por eso que un buen punto de partida es utilizar HTML básico en su JSX. A continuación, puedes empezar a incrustar expresiones JavaScript entre llaves.

Primero vamos a eliminar todo el desorden en el archivo.

~~~~~~~~
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
~~~~~~~~

Ahora sólo devuelve HTML sin JavaScript. Hagamos una variable "Bienvenido al camino para aprender React". Una variable puede utilizarse en su JSX.

~~~~~~~~
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
~~~~~~~~

Debería funcionar cuando inicie su aplicación en la línea de comandos..

Además, es posible que hayas notado el atributo `className`. Refleja el atributo estándar `class` en HTML. Debido a razones técnicas, JSX tuvo que reemplazar un puñado de atributos HTML internos. Puede encontrar todos los [atributos HTML compatibles en la documentación de React](https://facebook.github.io/react/docs/dom-elements.html). En tu camino para aprender React e encontrarás con más atributos JSX.

### Ejercicios:

* Definir más variables y renderizarlas en tu JSX
  * Utilizar un objeto complejo para representar a un usuario con nombre y apellido
* leer mas sobre [JSX](https://facebook.github.io/react/docs/introducing-jsx.html)
* leer mas sobre [React componentes, elementos e instancias](https://facebook.github.io/react/blog/2015/12/18/react-components-elements-and-instances.html)

## ES6 const y let

Supongo que notaste que declaramos la variable `helloWorld` con `var`. JavaScript ES6 viene con dos opciones más para declarar sus variables: `const` y `let`. En JavaScript ES6 rara vez encontrarás `var`. Daremos una explicación para `const` y `let`:

Una variable declarada con `const` no se puede volver a asignar o volver a declarar. No puede ser mutada (cambiada, modificada). Adoptas estructuras de datos inmutables al usarlo. Una vez que se define la estructura de datos, no se puede cambiar.

~~~~~~~~
// No permitido
const helloWorld = 'Welcome to the Road to learn React';
helloWorld = 'Bye Bye React';
~~~~~~~~

Una variable declarada con `let` puede mutar.

~~~~~~~~
// Permitido
let helloWorld = 'Welcome to the Road to learn React';
helloWorld = 'Bye Bye React';
~~~~~~~~

Lo usarías cuando necesitaras volver a asignar una variable.

Sin embargo, hay que tener cuidado con `const`. Una variable declarada con `const` no se puede modificar. Pero cuando la variable es un array o un objeto, el valor que tiene puede ser alterado. El valor que tiene no es inmutable.

~~~~~~~~
// allowed
const helloWorld = {
  text: 'Welcome to the Road to learn React'
};
helloWorld.text = 'Bye Bye React';
~~~~~~~~

Pero cuando usar cada una? Hay diferentes opiniones sobre su uso. Sugiero usar `const` cada que puedas. Indica que desea mantener su estructura de datos inmutable aunque los valores en objetos y arreglos se pueden modificar. Si desea modificar la variable, puede utilizar `let`.

La inmutabilidad es adoptada en React y su ecosistema. Es por eso que `const` debe ser tu opción por defecto cuando se define una variable. Sin embargo, en objetos complejos los valores internos pueden ser modificados. Tenga cuidado con este comportamiento.

En su aplicación debe utilizar `const` sobre `var`.

~~~~~~~~
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
~~~~~~~~

### Exercises:

* read more about ES6 [const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
* read more about ES6 [let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
* research more about immutable data structures
  * why do they make sense in programming in general
  * why are they used in React and its ecosystem

## ReactDOM

Before you continue with the App component, you might want to see where it is used. It is located in your entry point to the React world: the *src/index.js* file.

{title="src/index.js",lang=javascript}
~~~~~~~~
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import './index.css';

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
~~~~~~~~

Basically `ReactDOM.render()` uses a DOM node in your HTML to replace it with your JSX. That's how you can easily integrate React in every foreign application. It is not forbidden to use `ReactDOM.render()` multiple times across your application. You can use it at multiple places to bootstrap simple JSX syntax, a React component, multiple React components or a whole application.

`ReactDOM.render()` expects two arguments.

The first argument is JSX that gets rendered. The second argument specifies the place where the React application hooks into your HTML. It expects an element with an `id='root'`. You can open your *public/index.html* file to find the id attribute.

In the implementation `ReactDOM.render()` already takes your App component. However, it would be fine to pass simpler JSX as long as it is JSX. It doesn't have to be an instantiation of a component.

{title="Code Playground",lang=javascript}
~~~~~~~~
ReactDOM.render(
  <h1>Hello React World</h1>,
  document.getElementById('root')
);
~~~~~~~~

### Exercises:

* open the *public/index.html* to see where the React applications hooks into your HTML
* read more about [rendering elements in React](https://facebook.github.io/react/docs/rendering-elements.html)

## Hot Module Reloading

There is one thing that you can do in the *src/index.js* file to improve your experience as a developer.

In *create-react-app* it is already an advantage that the browser automatically refreshes the page when you change your source code. Try it by changing the `helloWorld` variable in your *src/App.js* file. The browser should refresh the page. But you can do better.

Hot Module Reloading (HMR) is a tool to reload your application in the browser. The browser doesn't perform a page refresh. You can easily activate it in *create-react-app*. In your *src/index.js* - your entry point to React - you have to add one little configuration.

{title="src/index.js",lang=javascript}
~~~~~~~~
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import './index.css';

ReactDOM.render(
  <App />,
  document.getElementById('root')
);

# leanpub-start-insert
if (module.hot) {
  module.hot.accept()
}
# leanpub-end-insert
~~~~~~~~

That's it. Try again to change the `hellowWorld` variable in your *src/App.js* file. The browser shouldn't perform a page refresh, but the application reloads and shows the correct output. HMR comes with multiple advantages:

Imagine you are debugging your code with `console.log()` statements. These statements will stay in your developer console, even though you change your code, because the browser doesn't refresh the page anymore. That can be convenient for debugging purposes.

In a growing application a page refresh delays your productivity. You have to wait until the page loads. A page reload can take several seconds in a large application. HMR takes away this disadvantage.

The biggest benefit is that you can keep the application state with HMR. Imagine you have a dialog in your application with multiple steps and you are at step 3. Basically it is a wizard. Without HMR you would change the source code and your browser refreshes the page. You would have to open the dialog again and would have to navigate from step 1 to step 3. With HMR your dialog stays open at step 3. It keeps the application state even though the source code changes. The application itself reloads, but not the page.

### Exercises:

* change your *src/App.js* source code a few times to see HMR in action
* watch the first 10 minutes of [Live React: Hot Reloading with Time Travel](https://www.youtube.com/watch?v=xsSnOQynTHs) by Dan Abramov

## Complex JavaScript in JSX

Let's get back to your App component. So far you rendered some primitive variables in your JSX. Now you will start to render a list of items. The list will be artificial data in the beginning, but later you will fetch the data from an external API. That will be far more exciting.

First you have to define the list of items.

{title="src/App.js",lang=javascript}
~~~~~~~~
import React, { Component } from 'react';
import './App.css';

# leanpub-start-insert
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
# leanpub-end-insert

class App extends Component {
  ...
}
~~~~~~~~

The artifical data will reflect the data we will fetch later on from the API. An item in the list has a title, an url and a author. Additionally it comes with an identifier, points (which indicate how popular an article is) and a count of comments.

Now you can use the built-in JavaScript `map` functionality in your JSX. It enables you to iterate over your list of items to display them. As mentioned, you will use curly braces to encapsulate the JavaScript expression in your JSX.

{title="src/App.js",lang=javascript}
~~~~~~~~
class App extends Component {

  render() {
    return (
      <div className="App">
# leanpub-start-insert
        { list.map(function(item) {
          return <div>{item.title}</div>;
        })}
# leanpub-end-insert
      </div>
    );
  }
}

export default App;
~~~~~~~~

That's pretty powerful in JSX. Usually you might have used `map` to convert one list of items to another list of items. This time you use `map` to convert a list of items to HTML elements.

So far, only the `title` will be displayed for each item. But let's display some more of the item properties.

{title="src/App.js",lang=javascript}
~~~~~~~~
class App extends Component {

  render() {
    return (
      <div className="App">
# leanpub-start-insert
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
# leanpub-end-insert
      </div>
    );
  }
}

export default App;
~~~~~~~~

You can see how the map function is simply inlined in your JSX. Each item property is displayed in a `<span>` tag. Moreover the url property of the item is used in the `href` attribute of the anchor tag.

React will do all the work for you and display each item. But you should add one helper for React to embrace its full potential and improve its performance. You have to assign a key attribute to each list element. That way React is able to identify added, changed and removed items when the list changes. The artificial list items come with an identifier already.

{title="src/App.js",lang=javascript}
~~~~~~~~
{ list.map(function(item) {
  return (
# leanpub-start-insert
    <div key={item.objectID}>
# leanpub-end-insert
      <span>
        <a href={item.url}>{item.title}</a>
      </span>
      <span>{item.author}</span>
      <span>{item.num_comments}</span>
      <span>{item.points}</span>
    </div>
  );
})}
~~~~~~~~

You should make sure that the key attribute is a stable identifier. Don't make the mistake of using the item index in the array. The array index isn't stable at all. For instance, when the list changes its order, React will have a hard time identifying the items properly.

{title="src/App.js",lang=javascript}
~~~~~~~~
// don't do this
{ list.map(function(item, key) {
  return (
    <div key={key}>
      ...
    </div>
  );
})}
~~~~~~~~

You are displaying both list items now. You can start your app, open your browser and see both items of the list displayed.

### Exercises:

* read more about [React lists and keys](https://facebook.github.io/react/docs/lists-and-keys.html)
* recap the [standard built-in Array functionalities in JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
* use more JavaScript expressions on your own in JSX

## ES6 Arrow Functions

JavaScript ES6 introduced arrow functions. An arrow function expression is shorter than a function expression.

{title="Code Playground",lang="javascript"}
~~~~~~~~
// function expression
function () { ... }

// arrow function expression
() => { ... }
~~~~~~~~

But you have to be aware of its functionalities. One of them is a different behavior with the `this` object. A function expression always defines its own `this` object. Arrow function expressions still have the `this` object of the enclosing context. Don't get confused when using `this` in an arrow function.

There is another valuable fact about arrow functions regarding the parenthesis. You can remove the parenthesis when the function gets only one argument, but have to keep them when it gets multiple arguments.

{title="Code Playground",lang="javascript"}
~~~~~~~~
// allowed
item => { ... }

// allowed
(item) => { ... }

// not allowed
item, key => { ... }

// allowed
(item, key) => { ... }
~~~~~~~~

However, let's have a look at the `map` function. You can write it more concisely with an ES6 arrow function.

{title="src/App.js",lang=javascript}
~~~~~~~~
# leanpub-start-insert
{ list.map(item => {
# leanpub-end-insert
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
~~~~~~~~

Additionally you can remove the *block body* of the ES6 arrow function. In a *concise body* an implicit return is attached thus you can remove the return statement. That will happen more often in the book, so be sure to understand the difference between a block body and a concise body.

{title="src/App.js",lang=javascript}
~~~~~~~~
# leanpub-start-insert
{ list.map(item =>
# leanpub-end-insert
  <div key={item.objectID}>
    <span>
      <a href={item.url}>{item.title}</a>
    </span>
    <span>{item.author}</span>
    <span>{item.num_comments}</span>
    <span>{item.points}</span>
  </div>
# leanpub-start-insert
)}
# leanpub-end-insert
~~~~~~~~

Your JSX looks more concise and readable now. It omits the function statement, the curly braces and the return statement.

### Exercises:

* read more about [ES6 arrow functions](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

## ES6 Classes

JavaScript ES6 introduced classes. A class is commonly used in object-oriented programming languages. JavaScript was and is very flexible in its programming paradigms. You can do functional programming and object-oriented programming side by side for their particular use cases.

Even though React embraces functional programming, for instance with immutable data structures, classes are used to declare components. They are called ES6 class components. React mixes the good parts of both programming paradigms.

Let's consider the following Developer class to examine a JavaScript ES6 class without thinking about a component.

{title="Code Playground",lang="javascript"}
~~~~~~~~
class Developer {
  constructor(firstname, lastname) {
    this.firstname = firstname;
    this.lastname = lastname;
  }

  getName() {
    return this.firstname + ' ' + this.lastname;
  }
}
~~~~~~~~

A class has a constructor to make it instantiable. The constructor can take arguments to assign it to the class instance. Additionally a class can define functions. Because the function is associated with a class, it is called a method. Sometimes it is referenced as a class method.

The Developer class is only the class declaration. You can create multiple instances of the class by invoking it. It is similar to the ES6 class component, that has a declaration, but you have to use it somewhere else to instantiate it.

Let's see how you can instantiate the class and how you can use its methods.

{title="Code Playground",lang="javascript"}
~~~~~~~~
const robin = new Developer('Robin', 'Wieruch');
console.log(robin.getName());
// output: Robin Wieruch
~~~~~~~~

React uses JavaScript ES6 classes for ES6 class components. You already used one ES6 class component.

{title="src/App.js",lang=javascript}
~~~~~~~~
import React, { Component } from 'react';

...

class App extends Component {
  render() {
    ...
  }
}
~~~~~~~~

The App class extends from `Component`. Basically you declare the App component, but it extends from another component. What does extend mean? In object-oriented programming you have the principle of inheritance. It is used to pass over functionalities from one class to another class.

The App class extends functionality from the Component class. To be more specific, it inherits functionalities from the Component class. The Component is used to extend a basic ES6 class to a ES6 component class. It has all the functionalities a component needs to have. One of these functionalities, a method, you have already used: the `render()` method. But you will learn about more functionalities.

The `Component` class encapsulates all the React functionalities that a developer doesn't need to see. It enables developers to use classes as components in React.

The methods a React `Component` exposes is the public interface. One of these methods has to be overwritten, the others don't need to be overwritten. You will learn about the latter ones when the book arrives at lifecycle methods in a later chapter. The `render()` method has to be overwritten, because it defines the output of a React `Component`.

Now you know the basics around JavaScript ES6 classes and how they are used in React to extend them to components. As I said, you will learn more about the Component methods when the book describes React lifecycle methods.

### Exercises:

* read more about [ES6 classes](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes)

{pagebreak}

You have learned to bootstrap your own React application! Let's recap the last chapters:

* React
  * create-react-app bootstraps a React application
  * JSX mixes up HTML and JavaScript to define React components
  * components, instances and elements are different things
  * `ReactDOM.render()` is an entry point for a React application
  * built-in JavaScript functionalities can be used in JSX
    * map can be used to render a list of items as HTML elements
* ES6
  * variable declarations with `const` and `let` for particular use cases
  * arrow functions can be used to shorten your function declarations
  * classes are used to define components in React

It makes sense to take a break at this point. Internalize the learnings and apply them on your own. You can experiment with the source code you have written so far.

You can find the source code in the [official repository](https://github.com/rwieruch/hackernews-client/tree/0c5a701170dcc72fe68bdd594df3a6522f58fbb3).

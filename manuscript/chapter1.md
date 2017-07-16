# Introducción a React

El capitulo te da una introducción a React. Podrias preguntarte: ¿Por que debo aprender React en primer lugar? El capitulo podria darte la respuesta a esa pregunta. Despues te sumergiras en el ecosistema iniciando tu primera aplicación React. En el camino se te dara una introducción a JSX y ReactDOM. Preparate para tu primer componente React.

## Hola, mi nombre es React.

**¿Por qué deberías molestarte en aprender React?** En los ultimos años las single page aplications ([SPA](https://en.wikipedia.org/wiki/Single-page_application)) se han vuelto popular. Frameworks como Angular, Ember y Backbone Ayudó a los desarrolladores de JavaScript a construir aplicaciones web modernas más allá del uso de jQuery. La lista no es exhaustiva. Existe una amplia gama de  SPA frameworks. Cuando consideras las fechas de lanzamiento, La mayoría de ellos están entre la primera generación de SPAs: Angular 2010, Backbone 2010, Ember 2011.

La versión inicial de React fue en 2013 por Facebook. React no es un SPA framework pero si una libreria para la vista. Es la V en [MVC](https://de.wikipedia.org/wiki/Model_View_Controller) (modelo vista controlador). Sólo le permite renderizar componentes como elementos visibles en un navegador. Sin embargo, todo el ecosistema alrededor de React hace posible crear aplicaciones de una sola página(SPA).

Pero por que deberias considerar usar React sobre la primera generacion de Frameworks SPA? Mientras que la primera generación de frameworks trató de resolver muchas cosas a la vez, React solo te ayuda a construir tu capa de vista. Es una biblioteca y no un Framework. La idea detrás de ella: Su vista es una jerarquía de componentes componibles.

En React, puedes centrarte en tu vista antes de introducir más aspectos en su aplicación. Cada otro aspecto es otro componente de su SPA. Estos bloques de construcción son esenciales para construir una aplicación madura. Vienen con dos ventajas.

Primero puedes aprender los bloques de construcción paso a paso. No tienes que preocuparte de entenderlos por completo. Es diferente de un marco que le da cada bloque de construcción desde el principio. Este libro se centra en React como el primer bloque de construcción. Más bloques de construcción siguen con el tiempo.

En segundo lugar todos los bloques de construcción son intercambiables. Hace que el ecosistema alrededor de React sea un lugar tan innovador. Múltiples soluciones están compitiendo entre sí. Puede elegir la solución más atractiva para usted y su caso de uso.

La primera generación de Frameworks de SPA llegó a nivel empresarial. Son más rígidos. Reac permanece innovador y se adopto por varias empresas líderes de pensamiento tecnológico como [Airbnb, Netflix y por supuesto Facebook](https://github.com/facebook/react/wiki/Sites-Using-React). Todos ellos invierten en el futuro de React y se conforman con React y su propio ecosistema.

React es probablemente una de las mejores opciones para la construcción de aplicaciones de una sola página hoy en día. Sólo ofrece la capa de vista, pero el ecosistema de React es un framework completo, flexible e intercambiable . React tiene una API simple, un ecosistema impresionante y una gran comunidad. Puedes leer acerca de mis experiencias del por qué me mudé de Angular a React. Recomiendo encarecidamente tener una comprensión de por qué elegiría React sobre otro Framework o biblioteca. Después de todo, todo el mundo está interesado en experimentar a donde nos guiará React en 2017 y más allá.

### Ejercicios

* Leer acerca [por qué me moví de Angular a React](https://www.robinwieruch.de/reasons-why-i-moved-from-angular-to-react/)

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

Sin embargo no todas las carpetas del proyecto vienen con un archivo package.json. There is a npm command to initialize a npm project and thus a *package.json* file. Only when you have that file, you can install new local packages via npm.

~~~~~~~~
npm init -y
~~~~~~~~

The `-y` flag is a shortcut to initialize all the defaults in your *package.json*. If you don't use it, you have to decide how to configure the file.

One more word about the *package.json*. The file enables you to share your project with other developers without sharing all the node packages. The file has all the references of node packages used in your project. These packages are called dependencies. Everyone can copy your project without the dependencies. The dependencies are references in the *package.json*. Someone who copies your project can install all packages by using `npm install` on the command line.

I want to cover one more npm command to prevent confusion:

{title="Command Line",lang="text"}
~~~~~~~~
npm install --save-dev <package>
~~~~~~~~

The `--save-dev` flag indicates that the node package is only used in the development environment. It will not be used in production when you deploy your application on a server. What kind of node package could that be? Imagine you want to test your application with the help of a node package. You need to install that package via npm, but want to exclude it from your production environment. There you don't want to test your application anymore. It should be tested already and work out of the box for users. That's only one use case where you would want to use the `--save-dev` flag.

You will encounter more npm commands on your way. But these will be sufficient for now.

### Exercises:

* setup a throw away npm project
  * create a new folder with `mkdir <folder_name>`
  * navigate into the folder with `cd <folder_name>`
  * execute `npm init -y`
  * install a local package like React with `npm install --save react`
  * have a look into the *package.json* file and the *node_modules/* folder
  * find out how to uninstall the *react* node package
* read more about [npm](https://docs.npmjs.com/)

## Installation

There are multiple approaches to get started with a React application.

The first one is to use a CDN. That may sound more complicated than it is. A CDN is a [content delivery network](https://en.wikipedia.org/wiki/Content_delivery_network). Several companies have CDNs that host files publicly for users. These files can be libraries like React. After all a library can be only one JavaScript file. It can be hosted somewhere and you can require it in your application.

How to use a CDN to get started in React? You can inline the `<script>` tag in your HTML that points to a CDN url. To get started in React you need two files (libraries): *react* and *react-dom*.

{title="Code Playground",lang="javascript"}
~~~~~~~~
<script src="https://unpkg.com/react@15/dist/react.js"></script>
<script src="https://unpkg.com/react-dom@15/dist/react-dom.js"></script>
~~~~~~~~

But why should you use a CDN when you have npm to install node packages (libraries)?

When your application has a *package.json* file, you can install *react* and *react-dom* from the command line. The requirement is that the folder is initialized as npm project with a *package.json* file. You can install multiple node packages in one line with npm.

{title="Command Line",lang="text"}
~~~~~~~~
npm install --save react react-dom
~~~~~~~~

That approach is often used to add React to an existing application.

Unfortunately that's not everything. You would have to deal with [Babel](http://babeljs.io/) to make your application aware of JSX - the React syntax - and JavaScript ES6. Babel transpiles your code that browsers can interpret ES6 and JSX. Not all browsers are capable of interpreting the syntax. The setup includes a lot of configuration and tooling. It can be overwhelming for React beginners to bother with all the configuration.

Because of this reason, Facebook introduced *create-react-app* as a zero-configuration React solution. The next chapter will show you how to setup your application.

### Exercises:

* read more about [React installations](https://facebook.github.io/react/docs/installation.html)

## Zero-Configuration Setup

In the Road to learn React you will use [create-react-app](https://github.com/facebookincubator/create-react-app) to bootstrap your application. It's an opinionated yet zero-configuration starter kit for React introduced by Facebook in 2016. People would [recommend it to beginners by 96%](https://twitter.com/dan_abramov/status/806985854099062785). In *create-react-app* the tooling and configuration evolve in the background while the focus is on the application implementation.

To get started, you will have to install the package to your global node packages. After that you always have it available on the command line to bootstrap new React applications.

{title="Command Line",lang="text"}
~~~~~~~~
npm install -g create-react-app
~~~~~~~~

You can check the version of *create-react-app* to verify a successful installation on your command line:

{title="Command Line",lang="text"}
~~~~~~~~
create-react-app --version
~~~~~~~~

It should give you an output about the version. Mine is: 1.3.3.

Now you can bootstrap your first React application. We call it *hackernews*, but you can choose a different name. Afterward simply navigate into the folder:

{title="Command Line",lang="text"}
~~~~~~~~
create-react-app hackernews
cd hackernews
~~~~~~~~

Now you can open the application in your editor. The following folder structure, or a variaton of it depending on the create-react-app version, should be presented to you:

{title="Folder Structure",lang="text"}
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

In the beginning everything you need is located in the *src/* folder.

The main focus lies on the *src/App.js* file to implement React components. It will be used to implement your application, but later you might want to split up your components into multiple files.

Additionally you will find a *src/App.test.js* file for tests and a *src/index.js* as entry point to the React world. You will get to know both files in a later chapter. In addition, there is a *src/index.css* and a *src/App.css* file to style your application and components. They all come with default style when you open them.

Next to to the *src/* folder you will find the *package.json* file and *node_modules/* folder to manage your node packages. The *create-react-app* application is a npm project. You can use npm to install and uninstall node packages to your project.

The *create-react-app* project comes with the following npm scripts for your command line:

{title="Command Line",lang="text"}
~~~~~~~~
// Runs the application in http://localhost:3000
npm start

// Runs the tests
npm test

// Builds the application for production
npm run build
~~~~~~~~

The scripts are defined in your *package.json* too. Your boilerplate React application is bootstrapped now.

### Exercises:

* `npm start` your application and visit the page in your browser
* run the interactive `npm test` script
* make yourself familiar with the folder structure
* make yourself familiar with the content of the files
* read more about [the scripts and create-react-app](https://github.com/facebookincubator/create-react-app)

## Introduction to JSX

Now you will get to know JSX. It is the syntax in React. As I mentioned before, *create-react-app* has already bootstrapped a boilerplate application. All files come with default implementations. Let's dive into the source code.

The only file you will touch in the beginning will be the *src/App.js* file.

{title="src/App.js",lang=javascript}
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

Don't let yourself get confused by the import/export statements and class declaration. These features are already JavaScript ES6. We will revisit those in a later chapter.

In the file you have an **ES6 class component** with the name App. It is a component declaration. Basically after you have declared a component, you can use it as element everywhere in your application. It will produce an **instance** of your **component** or in other words: the component gets instantiated.

The **element** it returns is specified in the `render()` method. Elements are what components are made of. It is useful to understand the differences between component, instance and element.

Pretty soon you will see where the App component is used. Otherwise you wouldn't see the rendered output in the browser, would you? The App component is only the declaration, but not the usage. You would instantiate the component somewhere in your JSX with `<App />`.

The content in the render block looks pretty similar to HTML, but it's JSX. JSX allows you to mix HTML and JavaScript. It's powerful yet confusing when you are used to plain HTML. That's why a good starting point is to use basic HTML in your JSX. Next you can start to embed JavaScript expressions in between by using curly braces.

First let's remove all the clutter in the file.

{title="src/App.js",lang=javascript}
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

Now you only return HTML without JavaScript. Let's make the "Welcome to the Road to learn React" a variable. A variable can be used in your JSX.

{title="src/App.js",lang=javascript}
~~~~~~~~
import React, { Component } from 'react';
import './App.css';

class App extends Component {
  render() {
# leanpub-start-insert
    var helloWorld = 'Welcome to the Road to learn React';
# leanpub-end-insert
    return (
      <div className="App">
# leanpub-start-insert
        <h2>{helloWorld}</h2>
# leanpub-end-insert
      </div>
    );
  }
}

export default App;
~~~~~~~~

It should work when you start your application on the command line.

Additionally you might have noticed the `className` attribute. It reflects the standard `class` attribute in HTML. Because of technical reasons, JSX had to replace a handful of internal HTML attributes. You can find all of the [supported HTML attributes in the React documentation](https://facebook.github.io/react/docs/dom-elements.html). On your way to learn React you will come across some more JSX attributes.

### Exercises:

* define more variables and render them in your JSX
  * use a complex object to represent an user with a first name and last name
* read more about [JSX](https://facebook.github.io/react/docs/introducing-jsx.html)
* read more about [React components, elements and instances](https://facebook.github.io/react/blog/2015/12/18/react-components-elements-and-instances.html)

## ES6 const and let

I guess you noticed that we declared the variable `helloWorld` with `var`. JavaScript ES6 comes with two more options to declare your variables: `const` and `let`. In JavaScript ES6 you will rarely find `var` anymore. Let's get some explanation for `const` and `let`:

A variable declared with `const` cannot be re-assigned or re-declared. It cannot get mutated (changed, modified). You embrace immutable data structures by using it. Once the data structure is defined, you cannot change it.

{title="Code Playground",lang="javascript"}
~~~~~~~~
// not allowed
const helloWorld = 'Welcome to the Road to learn React';
helloWorld = 'Bye Bye React';
~~~~~~~~

A variable declared with `let` can get mutated.

{title="Code Playground",lang="javascript"}
~~~~~~~~
// allowed
let helloWorld = 'Welcome to the Road to learn React';
helloWorld = 'Bye Bye React';
~~~~~~~~

You would use it when you would need to re-assign a variable.

However, you have to be careful with `const`. A variable declared with `const` cannot get modified. But when the variable is an array or object, the value it holds can get altered. The value it holds is not immutable.

{title="Code Playground",lang="javascript"}
~~~~~~~~
// allowed
const helloWorld = {
  text: 'Welcome to the Road to learn React'
};
helloWorld.text = 'Bye Bye React';
~~~~~~~~

But when to use each declaration? There are different opinions about the usage. I suggest using `const` whenever you can. It indicates that you want to keep your data structure immutable even though values in objects and arrays can get modified. If you want to modify your variable, you can use `let`.

Immutability is embraced in React and its ecosystem. That's why `const` should be your default choice when you define a variable. Still, in complex objects the values within can get modified. Be careful about this behavior.

In your application you should use `const` over `var`.

{title="src/App.js",lang=javascript}
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

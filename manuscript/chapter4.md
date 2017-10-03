# Organización de Código y Pruebas

El capítulo se centrará en temas importantes para mantener tu código mantenible en una aplicación escalable. Aprenderás sobre la organización del código para adoptar las mejores prácticas al estructurar tus carpetas y archivos. Otro aspecto que aprenderás son las pruebas, lo cual es importante para mantener su código robusto.

## Módulos ES6: Importación y Exportación

En JavaScript ES6 puedes importar y exportar funcionalidades desde módulos. Estas funcionalidades pueden ser funciones, clases, componentes, constantes, etc. Básicamente todo lo que puede asignar a una variable. Los módulos pueden ser archivos individuales o carpetas enteras con un archivo de índice como punto de entrada.

Al principio del libro, después de haber iniciado la aplicación con *create-react-app* , ya tenías varios `import` y `export` a través de sus archivos iniciales. Ahora es el momento apropiado para explicar esto.

Las sentencias `import` y `export` te ayudan a compartir código en varios archivos. Antes ya había varias soluciones para esto en el entorno JavaScript. Fue un desastre, porque querrías seguir una manera estandarizada en lugar de tener varios enfoques para la misma cosa. Ahora es un comportamiento nativo en JavaScript ES6.

Además, estas declaraciones adoptan la división de código. Distribuyes el código a través de varios archivos para mantenerlo reutilizable y mantenible. Lo primero es cierto porque puede importar el fragmento de código en varios archivos. Esto último es cierto porque usted tiene una sola fuente donde usted mantiene el pedazo de código.

Por último, pero no menos importante, le ayuda a pensar en encapsulación de código. No es necesario que todas las funcionalidades se exporten desde un archivo. Algunas de estas funcionalidades sólo deben utilizarse en el archivo donde se han definido. Las exportaciones de un archivo son básicamente la API pública del archivo. Sólo las funcionalidades exportadas están disponibles para ser reutilizadas en otro lugar. Sigue la mejor práctica de encapsulación.

Pero seamos prácticos. Como funcionan las declaraciones `import` y `export`? Los ejemplos siguientes muestran las declaraciones compartiendo una o varias variables entre dos archivos. Al final, el enfoque puede escalar a varios archivos y podría compartir más que simples variables.

Puede exportar una o varias variables. Se llama una exportación con nombre.

```js
const firstname = 'robin';
const lastname = 'wieruch';

export { firstname, lastname };
```

Y los importa en otro archivo con una ruta de acceso relativa al primer archivo.

```js
import { firstname, lastname } from './file1.js';

console.log(firstname);
// output: robin
```

También puede importar todas las variables exportadas de otro archivo como un objeto.

```js
import * as person from './file1.js';

console.log(person.firstname);
// output: robin
```

Las importaciones pueden tener un alias. Puede ocurrir que importe funcionalidades de varios archivos que tengan el mismo nombre de exportación. Es por eso que puedes usar un alias.

```js
import { firstname as foo } from './file1.js';

console.log(foo);
// output: robin
```

Por último pero no menos importante existe la declaración `default`. Se puede utilizar para algunos casos de uso:

* exportar e importar una sola funcionalidad
* para resaltar la funcionalidad principal de la API exportada de un módulo
* tener una funcionalidad de importación alternativa


```js
const robin = {
  firstname: 'robin',
  lastname: 'wieruch',
};

export default robin;
```

```js
import developer from './file1.js';

console.log(developer);
// output: { firstname: 'robin', lastname: 'wieruch' }
```

El nombre de importación puede diferir del nombre predeterminado exportado. También puede utilizarlo junto con las instrucciones de exportación e importación nombradas.

```js
const firstname = 'robin';
const lastname = 'wieruch';

const person = {
  firstname,
  lastname,
};

export {
  firstname,
  lastname,
};

export default person;
```

```js
import developer, { firstname, lastname } from './file1.js';

console.log(developer);
// output: { firstname: 'robin', lastname: 'wieruch' }
console.log(firstname, lastname);
// output: robin wieruch
```

En las exportaciones nombradas puede ahorrar líneas adicionales y exportar las variables directamente.

```js
export const firstname = 'robin';
export const lastname = 'wieruch';
```

Estas son las principales funcionalidades de los módulos ES6. Le ayudan a organizar su código, a mantener su código ya diseñar API de módulos reutilizables. También puede exportar e importar funcionalidades para probarlas. Lo harás en uno de los siguientes capítulos.

### Ejercicios:

* leer mas sobre [ES6 import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)
* leer mas sobre [ES6 export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export)

## Organización de código con módulos ES6

Usted podría preguntarse: ¿Por qué no seguimos las mejores prácticas de división de código para el archivo *src/App.js*? En el fichero ya tenemos múltiples componentes que podrían definirse en sus propios ficheros/carpetas(módulos). For the sake of learning React, it is practical to keep these things at one place. But once your React application grows, you should consider to split up these components into multiple modules. Only that way your application scales.

In the following I will propose several module structures you *could* apply. I would recommend to apply them as an exercise at the end of the book. To keep the book itself simple, I will not perform the code splitting and will continue the following chapters with the *src/App.js* file.

One possible module structure could be:

{title="Folder Structure",lang="text"}
~~~~~~~~
src/
  index.js
  index.css
  App.js
  App.test.js
  App.css
  Button.js
  Button.test.js
  Button.css
  Table.js
  Table.test.js
  Table.css
  Search.js
  Search.test.js
  Search.css
~~~~~~~~

It doesn't look too promising. You can see a lot of naming duplications and only the file extension differs. Another module structure could be:

{title="Folder Structure",lang="text"}
~~~~~~~~
src/
  index.js
  index.css
  App/
    index.js
    test.js
    index.css
  Button/
    index.js
    test.js
    index.css
  Table/
    index.js
    test.js
    index.css
  Search/
    index.js
    test.js
    index.css
~~~~~~~~

It looks cleaner than before. A component is defined by its component declaration in the JavasScript file, but also by its style and tests.

Another step could be extracting the constant variables from the App component. These constants were used to compose the Hacker News API url.

{title="Folder Structure",lang="text"}
~~~~~~~~
src/
  index.js
  index.css
# leanpub-start-insert
  constants/
    index.js
  components/
# leanpub-end-insert
    App/
      index.js
      test.js
      index..css
    Button/
      index.js
      test.js
      index..css
    ...
~~~~~~~~

Naturally the modules would split up into *src/constants/* and *src/components/*.

Now the *src/constants/index.js* file could look like the following:

{title="Code Playground: src/constants/index.js",lang="javascript"}
~~~~~~~~
export const DEFAULT_QUERY = 'redux';
export const DEFAULT_PAGE = 0;
export const DEFAULT_HPP = '100';

export const PATH_BASE = 'https://hn.algolia.com/api/v1';
export const PATH_SEARCH = '/search';
export const PARAM_SEARCH = 'query=';
export const PARAM_PAGE = 'page=';
export const PARAM_HPP = 'hitsPerPage=';
~~~~~~~~

The *App/index.js* file could import these variables in order to use them.

{title="Code Playground: src/components/App/index.js",lang=javascript}
~~~~~~~~
import {
  DEFAULT_QUERY,
  DEFAULT_PAGE,
  DEFAULT_HPP,

  PATH_BASE,
  PATH_SEARCH,
  PARAM_SEARCH,
  PARAM_PAGE,
  PARAM_HPP,
} from '../constants/index.js';

...
~~~~~~~~

When you use the *index.js* naming convention, you can omit the filename from the relative path.

{title="Code Playground: src/components/App/index.js",lang=javascript}
~~~~~~~~
import {
  DEFAULT_QUERY,
  DEFAULT_PAGE,
  DEFAULT_HPP,

  PATH_BASE,
  PATH_SEARCH,
  PARAM_SEARCH,
  PARAM_PAGE,
  PARAM_HPP,
# leanpub-start-insert
} from '../constants';
# leanpub-end-insert

...
~~~~~~~~

But what's behind the *index.js* file naming? The convention was introduced in the node.js world. The index file is the entry point to a module. It describes the public API to the module. External modules are only allowed to use the *index.js* file to import shared code from the module. Consider the following made up module structure to demonstrate it:

{title="Folder Structure",lang="text"}
~~~~~~~~
src/
  index.js
  App/
    index.js
  Buttons/
    index.js
    SubmitButton.js
    SaveButton.js
    CancelButton.js
~~~~~~~~

The *Buttons/* folder has multiple button components defined in its distinct files. Each file can `export default` the specific component making it available to *Buttons/index.js*. The *Buttons/index.js* file imports all different button representations and exports them as public module API.

{title="Code Playground: src/Buttons/index.js",lang="javascript"}
~~~~~~~~
import SubmitButton from './SubmitButton';
import SaveButton from './SaveButton';
import CancelButton from './CancelButton';

export {
  SubmitButton,
  SaveButton,
  CancelButton,
};
~~~~~~~~

Now the *src/App/index.js* can import the buttons from the public module API located in the *index.js* file.

{title="Code Playground: src/App/index.js",lang=javascript}
~~~~~~~~
import {
  SubmitButton,
  SaveButton,
  CancelButton
} from '../Buttons';
~~~~~~~~

By going with this constraint, it would be a bad practice to reach into other files than the *index.js* in the module. It would break the rules of encapsulation.

{title="Code Playground: src/App/index.js",lang=javascript}
~~~~~~~~
// bad practice, don't do it
import SubmitButton from '../Buttons/SubmitButton';
~~~~~~~~

Now you know how you could refactor your source code in modules with the constraints of encapsulation. As I said, for the sake of keeping the tutorial simple I will not apply these changes. But you should do the refactoring at the end of the book.

### Exercises:

* refactor your *src/App.js* file into multiple component modules when you finished the book

## Component Interface with PropTypes

You may know [TypeScript](https://www.typescriptlang.org/) or [Flow](https://flowtype.org/) to introduce a type interface to JavaScript. A typed language is less error prone, because the code gets validated based on its program text. Editors and other utilities can catch these errors before the program runs. It makes your program more robust.

React comes with a built-in type checker to prevent bugs. You can use PropTypes to describe your component interface. All the props that get passed from a parent component to a child component get validated based on the PropTypes interface assigned to the child component.

The chapter will show you how you can make all your components type safe with PropTypes. I will omit the changes for the following chapters, because they add unnecessary code refactorings. But you should keep and update them along the way to keep your components interface type safe.

Initially you can import PropTypes. You have to be aware of your React version, because in React version 15.5 the import changed. Check your *package.json* for your React version.

If it is 15.5 or above, you have to install an independent package.

{title="Command Line",lang="text"}
~~~~~~~~
npm install --save prop-types
~~~~~~~~

If your version is 15.4 or below, you can use the already installed React package.

Now, depending on your version, you can import the PropTypes.

{title="src/App.js",lang=javascript}
~~~~~~~~
# leanpub-start-insert
// React 15.5 and above
import PropTypes from 'prop-types';

// React 15.4 and below
import React, { Component, PropTypes } from 'react';
# leanpub-end-insert
~~~~~~~~

Let's start to assign a props interface to the components:

{title="src/App.js",lang=javascript}
~~~~~~~~
const Button = ({ onClick, className = '', children }) =>
  <button
    onClick={onClick}
    className={className}
    type="button"
  >
    {children}
  </button>

# leanpub-start-insert
Button.propTypes = {
  onClick: PropTypes.func,
  className: PropTypes.string,
  children: PropTypes.node,
};
# leanpub-end-insert
~~~~~~~~

That's it. You take every argument from the function signature and assign a PropType to it. The basic PropTypes for primitives and complex objects are:

{title="Code Playground",lang="javascript"}
~~~~~~~~
* PropTypes.array
* PropTypes.bool
* PropTypes.func
* PropTypes.number
* PropTypes.object
* PropTypes.string
~~~~~~~~

Additionally you have two more PropTypes to define a renderable fragment (node), e.g. a string, and a React element.

{title="Code Playground",lang="javascript"}
~~~~~~~~
* PropTypes.node
* PropTypes.element
~~~~~~~~

You already used the `node` PropType for the Button component. Overall there are more PropType definitions that you can read up in the official React documentation.

At the moment all of the defined PropTypes for the Button are optional. The parameters can be null or undefined. But for several props you want to enforce that they are defined. You can make it a requirement that these props are passed to the component.

{title="src/App.js",lang=javascript}
~~~~~~~~
Button.propTypes = {
# leanpub-start-insert
  onClick: PropTypes.func.isRequired,
# leanpub-end-insert
  className: PropTypes.string,
# leanpub-start-insert
  children: PropTypes.node.isRequired,
# leanpub-end-insert
};
~~~~~~~~

The `className` is not required, because it can default to an empty string. Next you will define a PropType interface for the Table component:

{title="src/App.js",lang=javascript}
~~~~~~~~
# leanpub-start-insert
Table.propTypes = {
  list: PropTypes.array.isRequired,
  onDismiss: PropTypes.func.isRequired,
};
# leanpub-end-insert
~~~~~~~~

You can define the content of an array PropType more explicit:

{title="src/App.js",lang=javascript}
~~~~~~~~
Table.propTypes = {
  list: PropTypes.arrayOf(
    PropTypes.shape({
      objectID: PropTypes.string.isRequired,
      author: PropTypes.string,
      url: PropTypes.string,
      num_comments: PropTypes.number,
      points: PropTypes.number,
    })
  ).isRequired,
  onDismiss: PropTypes.func.isRequired,
};
~~~~~~~~

Only the `objectID` is required, because you know that some of your code depends on it. The other properties are only displayed, thus they are not necessarily required. Moreover you cannot be sure that the Hacker News API has always a defined property for each object in the array.

That's it for PropTypes. But there is one more aspect. You can define default props in your component. Let's take again the Button component. The `className` property has an ES6 default parameter in the component signature.

{title="src/App.js",lang=javascript}
~~~~~~~~
const Button = ({ onClick, className = '', children }) =>
  ...
~~~~~~~~

You could replace it with the internal React default prop:

{title="src/App.js",lang=javascript}
~~~~~~~~
# leanpub-start-insert
const Button = ({ onClick, className, children }) =>
# leanpub-end-insert
  <button
    onClick={onClick}
    className={className}
    type="button"
  >
    {children}
  </button>

# leanpub-start-insert
Button.defaultProps = {
  className: '',
};
# leanpub-end-insert
~~~~~~~~

Same as the ES6 default parameter, the default prop ensures that the property is set to a default value when the parent component didn't specify it. The PropType type check happens after the default prop is evaluated.

### Exercises:

* answer yourself the following question
  * does the App component have a PropType interface?
* define the PropType interface for the Search component
* add and update the PropType interfaces when you add and update components in the next chapters
* read more about [React PropTypes](https://facebook.github.io/react/docs/typechecking-with-proptypes.html)

## Snapshot Tests with Jest

[Jest](https://facebook.github.io/jest/) is a JavaScript testing framework. At Facebook it is used to validate the JavaScript code. In the React community it is used for React components test coverage. Fortunately *create-react-app* already comes with Jest.

Let's start to test your first components. Before you can do that, you have to export the components from your *src/App.js* file to test them in a different file.

{title="src/App.js",lang=javascript}
~~~~~~~~
...

class App extends Component {
  ...
}

...

export default App;

# leanpub-start-insert
export {
  Button,
  Search,
  Table,
};
# leanpub-end-insert
~~~~~~~~

In your *App.test.js* file you will find a first test. It verifies that the App component renders without any errors.

{title="src/App.test.js",lang=javascript}
~~~~~~~~
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

it('renders without crashing', () => {
  const div = document.createElement('div');
  ReactDOM.render(<App />, div);
});
~~~~~~~~

You can run it by using the interactive *create-react-app* scripts on the command line.

{title="Command Line",lang="text"}
~~~~~~~~
npm run test
~~~~~~~~

Now Jest enables you to write Snapshot tests. These tests make a snapshot of your rendered component and run this snapshot against future snapshots. When a future snapshot changes you will get notified during the test. You can either accept the snapshot change, because you changed the component implementation on purpose, or deny the change and investigate for an error.

Jest stores the snapshots in a folder. Only that way it can show the diff to future snapshots. Additionally the snapshots can be shared across teams.

You have to install an utility library before you can write your first Snapshot test.

{title="Command Line",lang="text"}
~~~~~~~~
npm install --save-dev react-test-renderer
~~~~~~~~

Now you can extend the App component test with your first Snapshot test.

{title="src/App.test.js",lang=javascript}
~~~~~~~~
import React from 'react';
import ReactDOM from 'react-dom';
# leanpub-start-insert
import renderer from 'react-test-renderer';
# leanpub-end-insert
import App from './App';

# leanpub-start-insert
describe('App', () => {
# leanpub-end-insert

  it('renders', () => {
    const div = document.createElement('div');
    ReactDOM.render(<App />, div);
  });

# leanpub-start-insert
  test('snapshots', () => {
    const component = renderer.create(
      <App />
    );
    let tree = component.toJSON();
    expect(tree).toMatchSnapshot();
  });
# leanpub-end-insert

# leanpub-start-insert
});
# leanpub-end-insert
~~~~~~~~

Run your tests again and see how the tests either succeed or fail. They should succeed. Once you change the output of the render block in your App component, the Snapshot test should fail. Then you can decide to update the snapshot or investigate in your App component.

Let's add more tests for our independent components. First, the Search component:

{title="src/App.test.js",lang=javascript}
~~~~~~~~
import React from 'react';
import ReactDOM from 'react-dom';
import renderer from 'react-test-renderer';
# leanpub-start-insert
import App, { Search } from './App';
# leanpub-end-insert

...

# leanpub-start-insert
describe('Search', () => {

  it('renders', () => {
    const div = document.createElement('div');
    ReactDOM.render(<Search>Search</Search>, div);
  });

  test('snapshots', () => {
    const component = renderer.create(
      <Search>Search</Search>
    );
    let tree = component.toJSON();
    expect(tree).toMatchSnapshot();
  });

});
# leanpub-end-insert
~~~~~~~~

Second, the Button component:

{title="src/App.test.js",lang=javascript}
~~~~~~~~
...
# leanpub-start-insert
import App, { Search, Button } from './App';
# leanpub-end-insert

...

# leanpub-start-insert
describe('Button', () => {

  it('renders', () => {
    const div = document.createElement('div');
    ReactDOM.render(<Button>Give Me More</Button>, div);
  });

  test('snapshots', () => {
    const component = renderer.create(
      <Button>Give Me More</Button>
    );
    let tree = component.toJSON();
    expect(tree).toMatchSnapshot();
  });

});
# leanpub-end-insert
~~~~~~~~

Last but not least, the Table component:

{title="src/App.test.js",lang=javascript}
~~~~~~~~
...
# leanpub-start-insert
import App, { Search, Button, Table } from './App';
# leanpub-end-insert

...

# leanpub-start-insert
describe('Table', () => {

  const props = {
    list: [
      { title: '1', author: '1', num_comments: 1, points: 2, objectID: 'y' },
      { title: '2', author: '2', num_comments: 1, points: 2, objectID: 'z' },
    ],
  };

  it('renders', () => {
    const div = document.createElement('div');
    ReactDOM.render(<Table { ...props } />, div);
  });

  test('snapshots', () => {
    const component = renderer.create(
      <Table { ...props } />
    );
    let tree = component.toJSON();
    expect(tree).toMatchSnapshot();
  });

});
# leanpub-end-insert
~~~~~~~~

Snapshot tests usually stay pretty basic. You only want to cover that the component doesn't change its output. Once its changes the output, you have to decide if you accept the changes. Otherwise you have to fix the component when the output is not the desired output.

### Exercises:

* see how the Snapshot tests fail once you change your component implementation
  * either accept or deny the snapshot change
* keep your snapshots tests up to date when the implementation changes in next chapters
* read more about [Jest in React](https://facebook.github.io/jest/docs/tutorial-react.html)

## Unit Tests with Enzyme

[Enzyme](https://github.com/airbnb/enzyme) is a testing utility by Airbnb to assert, manipulate and traverse your React components. You can use it to conduct unit tests to complement your snapshot tests.

Let's see how you can use enzyme. First you have to install it since it doesn't come with *create-react-app*.

{title="Command Line",lang="text"}
~~~~~~~~
npm install --save-dev enzyme react-addons-test-utils
~~~~~~~~

Now you can write your first unit test in the Table describe block. You will use `shallow()` to render your component and assert that the Table has two items.

{title="src/App.test.js",lang=javascript}
~~~~~~~~
import React from 'react';
import ReactDOM from 'react-dom';
import renderer from 'react-test-renderer';
# leanpub-start-insert
import { shallow } from 'enzyme';
# leanpub-end-insert
import App, { Search, Button, Table } from './App';

describe('Table', () => {

  const props = {
    list: [
      { title: '1', author: '1', num_comments: 1, points: 2, objectID: 'y' },
      { title: '2', author: '2', num_comments: 1, points: 2, objectID: 'z' },
    ],
  };

  ...

# leanpub-start-insert
  it('shows two items in list', () => {
    const element = shallow(
      <Table { ...props } />
    );

    expect(element.find('.table-row').length).toBe(2);
  });
# leanpub-end-insert

});
~~~~~~~~

Shallow renders the component without child components. You can make the test very dedicated to one component.

Enzyme has overall three rendering mechanisms in its API. You already know `shallow()`, but there also exist `mount()` and `render()`. Both instantiate instances of the parent component and all child components. Additionally `mount()` gives you more access to the component lifecycle methods. But when to use which render mechanism? Here some rules of thumb:

* Always begin with a shallow test
* If `componentDidMount()` or `componentDidUpdate()` should be tested, use `mount()`
* If you want to test component lifecycle and children behavior, use `mount()`
* If you want to test children rendering with less overhead than `mount()` and you are not interested in lifecycle methods, use `render()`

You could continue to unit test your components. But make sure to keep the tests simple and maintainable. Otherwise you will have to refactor them once you change your components. That's why Facebook introduced Snapshot tests with Jest in the first place.

### Exercises:

* keep your unit tests up to date during the following chapters
* read more about [enzyme and its rendering API](https://github.com/airbnb/enzyme)

{pagebreak}

You have learned how to organize your code and how to test it! Let's recap the last chapters:

* React
  * PropTypes let you define type checks for components
  * Jest allows you to write snapshot tests for your components
  * Enzyme allows you to write unit tests for your components
* ES6
  * import and export statements help you to organize your code
* General
  * code organization allows you to scale your application with best practices

You can find the source code in the [official repository](https://github.com/rwieruch/hackernews-client/tree/393ce5a350aa34b1c7ae056333f7bb7b0807caef).
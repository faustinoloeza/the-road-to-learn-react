# Conceptos básicos en React

El capítulo les guiará a través de los fundamentos de React. Cubre el estado y las interacciones en los componentes, porque los componentes estáticos son un poco aburridos, ¿no? Además, aprenderá sobre las diferentes maneras de declarar un componente y cómo mantener componentes ensamblables y reutilizables. Esté preparado para dar vida a sus componentes.

## Estado interno del componente

El estado interno del componente te permite almacenar, modificar y eliminar propiedades de tu componente. El componente de clase ES6 puede utilizar un constructor para inicializar el estado interno del componente. El constructor se llama una sola vez cuando el componente se inicializa.

Vamos a introducir un constructor de clase donde se puede establecer el estado interno inicial del componente.

~~~~~~~~
class App extends Component {

  constructor(props) {
    super(props);

    this.state = {
      list: list,
    };
  }

  ...

}
~~~~~~~~

En tu caso, el estado inicial es la lista artificial de elementos.
Tenga en cuenta que tiene que llamar `super(props);` para llamar al constructor de la clase de extendida componente. Es obligatorio, ya que establece `this.props` en tu constructor. Debes seguir la mejor práctica, de lo contrario podrías encontrarte con errores en el futuro.

El estado está ligado a la clase con el objeto `this`. Puedes acceder al estado en tu componente. Por ejemplo, se puede utilizar en el método  `render()`. Anteriormente, se asignó una lista estática de elementos. Ahora está a punto de usar la lista de su estado interno del componente.

~~~~~~~~
class App extends Component {

  ...

  render() {
    return (
      <div className="App">
        { this.state.list.map(item =>
          <div key={item.objectID}>
            <span>
              <a href={item.url}>{item.title}</a>
            </span>
            <span>{item.author}</span>
            <span>{item.num_comments}</span>
            <span>{item.points}</span>
          </div>
        )}
      </div>
    );
  }
}
~~~~~~~~

La lista es parte del componente ahora. Reside en el estado interno del componente.  Podría agregar artículos, cambiar artículos o quitar artículos en y de su lista. Cada vez que cambies el estado del componente, el metodo `render()` de tu componente se ejecutará de nuevo. Así es como puede simplemente cambiar el estado del componente interno y asegurarse de que el componente se vuelva a renderizar.

Pero ten cuidado. No cambies el estado directamente. Tienes que usar un método llamado `setState()` para modificar su estado. Lo conoceras en un capítulo siguiente.

### Ejercicios:

* experimenta con el estado interno
  * define mas estados uniciales en el contructor
  * usa el estado en tu metodo `render()`
* leer mas sobre [the ES6 class constructor](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes#Constructor)

## Inicializador de objetos ES6

En JavaScript ES6 puedes utilizar una sintaxis de propiedad abreviada para inicializar tus objetos más concisos. Imagine la siguiente inicialización de objeto:

~~~~~~~~
const name = 'Robin';

const user = {
  name: name,
};
~~~~~~~~

Cuando el nombre de la propiedad en su objeto sea el mismo que su nombre de variable, puede hacer lo siguiente:

~~~~~~~~
const name = 'Robin';

const user = {
  name,
};
~~~~~~~~

En su aplicación puede hacer lo mismo. El nombre de la variable de lista y el nombre de la propiedad de estado comparten el mismo nombre.

~~~~~~~~
// ES5
this.state = {
  list: list,
};

// ES6
this.state = {
  list,
};
~~~~~~~~

Otro buen ayudante son los nombres abreviados de métodos. En ES6 puedes inicializar métodos en un objeto más conciso.

~~~~~~~~
// ES5
var userService = {
  getUserName: function (user) {
    return user.firstname + ' ' + user.lastname;
  },
};

// ES6
const userService = {
  getUserName(user) {
    return user.firstname + ' ' + user.lastname;
  },
};
~~~~~~~~

Por último, pero no menos importante, se le permite usar nombres de propiedad calculados en ES6.

~~~~~~~~
// ES5
var user = {
  name: 'Robin',
};

// ES6
const key = 'name';
const user = {
  [key]: 'Robin',
};
~~~~~~~~

Los nombres de propiedad calculadas podrían no tener sentido aún. ¿Por qué las necesitarias? En un capítulo futuro del libro llegarás a un punto en el que puedras usarlo.

### Ejercicios:

* experimenta con el inicializador de objetos ES6
* leer más sobre [ES6 object initializer](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Object_initializer)

## Flujo de datos unidireccional

Ahora tienes un estado interno en tu componente App. Sin embargo, no has manipulado el estado interno todavía. El estado es estático y por lo tanto tambien lo es el componente. Una buena manera de experimentar la manipulación del estado es tener alguna interacción de componentes.

Vamos a agregar un botón para cada elemento en la lista mostrada. El botón dice "Dismiss" y eliminará el elemento de la lista. Podría ser útil eventualmente cuando sólo desea mantener una lista de elementos no leídos.

~~~~~~~~
class App extends Component {

  ...

  render() {
    return (
      <div className="App">
        { this.state.list.map(item =>
          <div key={item.objectID}>
            <span>
              <a href={item.url}>{item.title}</a>
            </span>
            <span>{item.author}</span>
            <span>{item.num_comments}</span>
            <span>{item.points}</span>
            <span>
              <button
                onClick={() => this.onDismiss(item.objectID)}
                type="button"
              >
                Dismiss
              </button>
            </span>
          </div>
        )}
      </div>
    );
  }
}
~~~~~~~~

Como puedes ver el metodo `onDismiss()` en la funcion `onClick` queda cerrada por otra función. Sólo de esa manera usted puede colarse en la propiedad `objectID`. De lo contrario, tendría que definir la función fuera. Sin embargo, utilizando una arrow fuction ES6, puedes hacerlo en línea.

Tenga en cuenta que los elementos con múltiples atributos se desordenan en una línea en algún momento. Es por eso que el elemento de botón se utiliza con multilineas e identado para mantenerlo legible. Pero no es obligatorio. Es sólo un estilo de código recomendable.

Ahora tienes que implementar la funcionalidad `onDismiss()`. Se necesita un id del item para identificar el elemento a descartar. La función está vinculada a la clase y se convierte así en un método de clase. Tienes que enlazar métodos de clase en el constructor. Además tienes que definir su funcionalidad en tu clase.

~~~~~~~~
class App extends Component {

  constructor(props) {
    super(props);

    this.state = {
      list,
    };

    this.onDismiss = this.onDismiss.bind(this);
  }

  onDismiss(id) {
    ...
  }

  render() {
    ...
  }
}
~~~~~~~~

Ahora puede definir lo que sucede dentro del método de clase. Puesto que usted desea quitar el artículo clicado de su lista, puedes hacerlo con la funcionalidad de filtro de array incorporada. La función de filtro toma una función para evaluar cada elemento de la lista. Si la evaluación de un item es true, el elemento se queda en la lista. De lo contrario se eliminará. Además, la función devuelve una nueva lista y no altera la lista antigua. Mantiene la estructura de datos inmutables.

~~~~~~~~
onDismiss(id) {

  function isNotId(item) {
    return item.objectID !== id;
  }

  const updatedList = this.state.list.filter(isNotId);
}
~~~~~~~~

Puede hacerlo de forma más concisa utilizando nuevamente una función ES6 arrow function.

~~~~~~~~
onDismiss(id) {
  const isNotId = item => item.objectID !== id;
  const updatedList = this.state.list.filter(isNotId);
}
~~~~~~~~

Podrías incluso hacerlo en una línea, como lo hicimos en el controlador `onClick()` del botón - pero puede ser menos legible.

~~~~~~~~
onDismiss(id) {
  const updatedList = this.state.list.filter(item => item.objectID !== id);
}
~~~~~~~~

La lista elimina ahora el elemento seleccionado. Sin embargo, el estado aún no se actualiza. Por lo tanto, finalmente puede utilizar el metodo de clase `setState()` para actualizar la lista en el estado interno del componente.

~~~~~~~~
onDismiss(id) {
  const isNotId = item => item.objectID !== id;
  const updatedList = this.state.list.filter(isNotId);
  this.setState({ list: updatedList });
}
~~~~~~~~

Ahora vuelve a ejecutar tu aplicación y prueba el boton "Dismiss". Deberia de funcionar. Lo que acabas de experimentar es el **Flujo de datos unidireccional** en React. Usted activa una acción en su vista - con `onClick()` - una funcion o método de clase modifica el estado del componente interno y el metodo `render()` del componente se ejecuta de nuevo para actualizar la vista.

![Internal state update with unidirectional data flow](images/set-state-to-render-unidirectional.png)

### Ejercicios:

* leer mas sobre [El estado y el ciclo de vida de React](https://facebook.github.io/react/docs/state-and-lifecycle.html)

## Interacciones con Formularios y Eventos

Añadamos otra interacción para experimentar formularios y eventos en React. La interacción es una funcionalidad de búsqueda. La entrada del campo de búsqueda se debe utilizar para filtrar la lista basada en la propiedad de título de un elemento.

Primero defina su campo de entrada en su JSX.

~~~~~~~~
class App extends Component {

  ...

  render() {
    return (
      <div className="App">
        <form>
          <input type="text" />
        </form>
        { this.state.list.map(item =>
          ...
        )}
      </div>
    );
  }
}
~~~~~~~~

En el escenario siguiente, se escribirá en el campo y se filtrará la lista temporalmente por el término de búsqueda. Para poder filtrar la lista, necesitas el valor del campo de entrada para actualizar el estado. Pero, ¿cómo acceder al valor? Puede utilizar **eventos sintéticos** en  React para acceder a la carga útil del evento.

Vamos a definir una funcion callbakc `onChange()` para el campo de entrada.

~~~~~~~~
class App extends Component {

  ...

  render() {
    return (
      <div className="App">
        <form>
          <input
            type="text"
            onChange={this.onSearchChange}
          />
        </form>
        ...
      </div>
    );
  }
}
~~~~~~~~

La función está vinculada al componente y, por tanto, un método de clase de nuevo. Tienes que vincular y definir el métodos.

~~~~~~~~
class App extends Component {

  constructor(props) {
    super(props);

    this.state = {
      list,
    };

    this.onSearchChange = this.onSearchChange.bind(this);
    this.onDismiss = this.onDismiss.bind(this);
  }

  onSearchChange() {
    ...
  }

  ...
}
~~~~~~~~

El argumento del método le da acceso al evento React sintético. El evento tiene el valor del campo de entrada en su objeto de destino. Ahora puedes manipular el estado para el término de búsqueda:

~~~~~~~~
class App extends Component {

  ...

  onSearchChange(event) {
    this.setState({ searchTerm: event.target.value });
  }

  ...
}
~~~~~~~~

Además hay que definir el estado inicial para el `searchTerm` en el constructor

~~~~~~~~
class App extends Component {

  constructor(props) {
    super(props);

    this.state = {
      list,
      searchTerm: '',
    };

    this.onSearchChange = this.onSearchChange.bind(this);
    this.onDismiss = this.onDismiss.bind(this);
  }

  ...
}
~~~~~~~~

Ahora almacena el valor de entrada en su estado de componente interno cada vez que el valor en el campo de entrada cambia. Sin embargo, la lista no se actualiza todavía. Deberá filtrar la lista temporalmente en función del `searchTerm`. Eso es bastante simple. Antes de asignar la lista puede aplicar un filtro en ella. Ya ha utilizado la funcionalidad de filtro JavaScript incorporada.

~~~~~~~~
class App extends Component {

  ...

  render() {
    return (
      <div className="App">
        <form>
          <input
            type="text"
            onChange={this.onSearchChange}
          />
        </form>
        { this.state.list.filter(...).map(item =>
          ...
        )}
      </div>
    );
  }
}
~~~~~~~~

Aproximemos la función de filtro de una manera diferente esta vez. Queremos definir el argumento del filtro - la funcion - fuera de nuestro componente de clase ES6. Allí no tenemos acceso al estado del componente - por lo tanto no tenemos acceso a la propiedad `searchTerm` para evaluar la condición del filtro. Tenemos que pasar el `searchTerm` a la función de filtro y tienen que devolver una nueva función para evaluar la condición. Eso se llama una función de orden superior.

Normalmente no mencionaría las funciones de orden superior, pero en un libro de React tiene total sentido. Tiene sentido conocer las funciones de orden superior, Porque React trata con un concepto llamado componentes de orden superior. Conocerás el concepto más adelante en el libro. Ahora de nuevo, vamos a enfocarnos en la funcionalidad del filtro.

Primero tienes que definir la función de orden superior fuera de tu clase.

~~~~~~~~
function isSearched(searchTerm) {
  return function(item) {
    // some condition which returns true or false
  }
}

class App extends Component {

  ...

}
~~~~~~~~

La función toma el `searchTerm` y devuelve otra función que toma un elemento. La función devuelta se utilizará para filtrar la lista en función de la condición definida en la función.

Let's define the condition.

~~~~~~~~
function isSearched(searchTerm) {
  return function(item) {
    return !searchTerm ||
      item.title.toLowerCase().includes(searchTerm.toLowerCase());
  }
}

class App extends Component {

  ...

}
~~~~~~~~

La condición dice varias cosas. Filtrar la lista sólo cuando esta establecido `searchTerm`. Cuando se establece un `searchTerm`, Usted coincide con el patrón `searchTerm` entrante con el título del elemento. Puedes hacerlo con la funcionalidad incorporada  en JavaScript `includes`. Sólo cuando el patrón coincide, devuelve true y el elemento permanece en la lista. Pero tenga cuidado con la coincidencia de patrones: No debes olvidar las minúsculas de ambas cadenas. De lo contrario, habrá desajustes entre un término de búsqueda 'redux' y un título de artículo 'Redux'.

Una cosa queda por mencionar: Hemos engañado un poco utilizando la funcionalidad incluida en JavaScript. Ya es una característica ES6. ¿Cómo se vería eso en JavaScript ES5? Usted usaría la funcion `indexOf()` para obtener el índice del elemento en la lista. Cuando el elemento está en la lista, `indexOf()` devolverá un índice positivo.

~~~~~~~~
// ES5
string.indexOf(pattern) !== -1

// ES6
string.includes(pattern)
~~~~~~~~

Otra impecable refactorización se puede hacer de nuevo con una ES6 arrow function. Hace que la función sea más concisa:

~~~~~~~~
// ES5
function isSearched(searchTerm) {
  return function(item) {
    return !searchTerm || item.title.toLowerCase().includes(searchTerm.toLowerCase());
  }
}

// ES6
const isSearched = (searchTerm) => (item) =>
  !searchTerm || item.title.toLowerCase().includes(searchTerm.toLowerCase());
~~~~~~~~

Uno podría discutir qué función es más legible. Personalmente prefiero la segundo. El ecosistema de React utiliza una gran cantidad de conceptos de programación funcional. Sucede a menudo que usted utilizará una función que devuelve una función (funciones de orden superior). En ES6 puedes expresarlas de forma más concisa con arrow functions.

Por último, pero no menos importante, tienes que usar la funcion definida `isSearched()` para filtrar tu lista.

~~~~~~~~
class App extends Component {

  ...

  render() {
    return (
      <div className="App">
        <form>
          <input
            type="text"
            onChange={this.onSearchChange}
          />
        </form>
        { this.state.list.filter(isSearched(this.state.searchTerm)).map(item =>
          ...
        )}
      </div>
    );
  }
}
~~~~~~~~

Ahora la funcionalidad de búsqueda debería funcionar ahora. Pruebala.

### Ejercicios:

* leer mas sobre [eventos React](https://facebook.github.io/react/docs/handling-events.html)
* leer mas sobre [funciones de orden](https://en.wikipedia.org/wiki/Higher-order_function)

## Desestructuración ES6

Hay una manera en ES6 para acceder a las propiedades en objetos y arrays fácilmente. Se llama desestructuración. Comparar el fragmento siguiente en JavaScript ES5 y ES6.

~~~~~~~~
const user = {
  firstname: 'Robin',
  lastname: 'Wieruch',
};

// ES5
var firstname = user.firstname;
var lastname = user.lastname;

// ES6
const { firstname, lastname } = user;

console.log(firstname + ' ' + lastname);
// output: Robin Wieruch
~~~~~~~~

Mientras tiene que agregar una línea extra cada vez que desee acceder a una propiedad de objeto en ES5, puedes hacerlo en una línea en ES6. Además, no es necesario tener nombres de propiedad duplicados. Una mejor práctica para la legibilidad es utilizar multilíneas cuando desestructuras un objeto en múltiples propiedades.

~~~~~~~~
const {
  firstname,
  lastname
} = user;
~~~~~~~~

Lo mismo ocurre con los arrays. También puede desestructurarlos, pero manténgalos más legibles con multilines..

~~~~~~~~
const users = ['Robin', 'Andrew', 'Dan'];
const [
  userOne,
  userTwo,
  userThree
] = users;

console.log(userOne, userTwo, userThree);
// output: Robin Andrew Dan
~~~~~~~~

Quizás notaste que el estado en el componente App puede destructurarse de la misma manera.Puede acortar el filtro y la línea map del código
~~~~~~~~
  render() {
    const { searchTerm, list } = this.state;
    return (
      <div className="App">
        ...
        { list.filter(isSearched(searchTerm)).map(item =>
          ...
        )}
      </div>
    );
~~~~~~~~

Puede hacerlo de la manera ES5 o ES6:

~~~~~~~~
// ES5
var searchTerm = this.state.searchTerm;
var list = this.state.list;

// ES6
const { searchTerm, list } = this.state;
~~~~~~~~

Pero como el libro utiliza JavaScript ES6 la mayor parte del tiempo, debes atenerse a ES6.

### Ejercicios:

* leer mas sobre [ES6 destructuring](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

## Componentes Controlados

Ya has aprendido sobre el flujo de datos unidireccional en React. La misma ley se aplica al campo de entrada, que actualiza el estado que a su vez filtra la lista. El estado fue cambiado, el metodo `render()` e ejecuta de nuevo y utiliza el estado reciente `searchTerm` para aplicar la condición de filtro.

¿Pero no nos olvidamos de algo en el elemento de entrada? Una etiqueta de entrada HTML viene con un atributo `value`. El atributo valor normalmente tiene el valor que se muestra en el campo de entrada - en nuestro caso la propiedad `searchTerm`. Sin embargo, parece que no lo necesitamos en React.

Eso está mal. Elemnetos de formulario como `<input>`, `<textarea>` y `<select>` mantiene su propio estado. Modifican el valor internamente una vez que alguien lo cambia desde el exterior. En React se les llama **componente no controlado**, porque maneja su propio estado. En React, debe asegurarse de que estos elementos son **componentes controlados**.

¿Cómo debes hacer eso? Sólo tiene que establecer el atributo de valor del campo de entrada. El valor ya está guardado en la propiedad de estado `searchTerm`.

~~~~~~~~
class App extends Component {

  ...

  render() {
    const { searchTerm, list } = this.state;
    return (
      <div className="App">
        <form>
          <input
            type="text"
            value={searchTerm}
            onChange={this.onSearchChange}
          />
        </form>
        ...
      </div>
    );
  }
}
~~~~~~~~

Eso es todo. El ciclo de flujo de datos unidireccional para el campo de entrada es autónomo ahora. El estado componente interno es la única fuente de verdad para el campo de entrada.

Toda la gestión interna del estado y el flujo de datos unidireccional podría ser nuevo para usted. Pero una vez que esté acostumbrado a él, será su flujo natural para implementar las cosas en React. En general, React trajo un nuevo patrón con el flujo de datos unidireccional al mundo de las aplicaciones de una sola página. Es adoptado por varios frameworks y librerias.

### Ejercicios:

* leer mas sobre [React forms](https://facebook.github.io/react/docs/forms.html)

## Dividir Componentes

Ahora tienes un componente de App grande. Sigue creciendo y sera confuso eventualmente. Puede comenzar a dividirlo en pedazos - componentes más pequeños.

Comencemos a utilizar un componente para la entrada de búsqueda y un componente para la lista de elementos.

~~~~~~~~
class App extends Component {

  ...

  render() {
    const { searchTerm, list } = this.state;
    return (
      <div className="App">
        <Search />
        <Table />
      </div>
    );
  }
}
~~~~~~~~

Puede pasar las propiedades de los componentes que pueden utilizar ellos mismos.

~~~~~~~~
class App extends Component {

  ...

  render() {
    const { searchTerm, list } = this.state;
    return (
      <div className="App">
        <Search
          value={searchTerm}
          onChange={this.onSearchChange}
        />
        <Table
          list={list}
          pattern={searchTerm}
          onDismiss={this.onDismiss}
        />
      </div>
    );
  }
}
~~~~~~~~

Ahora puede definir los componentes junto a su componente App. Estos componentes serán también componentes de la clase ES6. Renderizan los mismos elementos como antes
.

El primero es el componente de búsqueda.

~~~~~~~~
class App extends Component {
  ...
}

class Search extends Component {
  render() {
    const { value, onChange } = this.props;
    return (
      <form>
        <input
          type="text"
          value={value}
          onChange={onChange}
        />
      </form>
    );
  }
}
~~~~~~~~

El segundo es el componente Tabla.

~~~~~~~~
...

class Table extends Component {
  render() {
    const { list, pattern, onDismiss } = this.props;
    return (
      <div>
        { list.filter(isSearched(pattern)).map(item =>
          <div key={item.objectID}>
            <span>
              <a href={item.url}>{item.title}</a>
            </span>
            <span>{item.author}</span>
            <span>{item.num_comments}</span>
            <span>{item.points}</span>
            <span>
              <button
                onClick={() => onDismiss(item.objectID)}
                type="button"
                >
                Dismiss
              </button>
            </span>
          </div>
        )}
      </div>
    );
  }
}
~~~~~~~~

Ahora tiene tres componentes de clase ES6. PTal vez usted ha notado el objeto `this.props`. Las props - abrevitura para las propiedades - tienen todos los valores que han pasado a los componentes cuando los utiliza en su componente App. Usted podría reutilizar estos componentes en otro lugar, pero pasarles diferentes valores. Son reutilizables.

### Ejercicios:

* averiguar qué componentes podría dividir
  * pero no lo haga ahora, de lo contrario se encontrará con conflictos en los próximos capítulos

## Componentes Ensamblables

There is one more little property which is accessible in the props object: the `children` prop. You can use it to pass elements to your components from above - which are unknown to the component itself - but make it possible to compose components into each other. Let's see how this looks like when you only pass a text (string) as a child to the Search component.

~~~~~~~~
class App extends Component {

  ...

  render() {
    const { searchTerm, list } = this.state;
    return (
      <div className="App">
        <Search
          value={searchTerm}
          onChange={this.onSearchChange}
        >
          Search
        </Search>
        <Table
          list={list}
          pattern={searchTerm}
          onDismiss={this.onDismiss}
        />
      </div>
    );
  }
}
~~~~~~~~

Now the Search component can destructure the children property from props. Then it can specify where the children should be displayed.

~~~~~~~~
class Search extends Component {
  render() {
    const { value, onChange, children } = this.props;
    return (
      <form>
        {children} <input
          type="text"
          value={value}
          onChange={onChange}
        />
      </form>
    );
  }
}
~~~~~~~~

The "Search" text should be visible next to your input field now. When you use the Search component somewhere else, you can choose a different text if you like. After all it is not only text that you can pass as children. You can pass an element and element trees (which can be encapsulated by components again) as children. The children property makes it possible to weave components into each other.

### Exercises:

* read more about [the composition model of React](https://facebook.github.io/react/docs/composition-vs-inheritance.html)

## Reusable Components

Reusable and composable components empower you to come up with capable component hierarchies. They are the foundation of your view layer. The last chapters mentioned often the term reusability. You can reuse the Table and Search components already. Not to forget the App component.

Let's define one more reusable component - a Button component - which gets reused more often eventually.

~~~~~~~~
class Button extends Component {
  render() {
    const {
      onClick,
      className,
      children,
    } = this.props;

    return (
      <button
        onClick={onClick}
        className={className}
        type="button"
      >
        {children}
      </button>
    );
  }
}
~~~~~~~~

It might seem redundant to declare such a component. You will use a `Button` instead of a `button`. It only spares the `type="button"`. Except for the type attribute you have to define everything else when you want to use the Button component. But you have to think about the long term investment here. Imagine you have several buttons in your application, but want to change an attribute, style or behavior for the button. Without the component you would have to refactor every button. Instead the Button component ensures to have only one single source of truth. One Button to refactor all buttons at once.

Since you already have a button element, you can use the Button component instead. It omits the type attribute.

~~~~~~~~
class Table extends Component {
  render() {
    const { list, pattern, onDismiss } = this.props;
    return (
      <div>
        { list.filter(isSearched(pattern)).map(item =>
          <div key={item.objectID}>
            <span>
              <a href={item.url}>{item.title}</a>
            </span>
            <span>{item.author}</span>
            <span>{item.num_comments}</span>
            <span>{item.points}</span>
            <span>
              <Button onClick={() => onDismiss(item.objectID)}>
                Dismiss
              </Button>
            </span>
          </div>
        )}
      </div>
    );
  }
}
~~~~~~~~

The Button component expects a `className` property in the props. But we didn't pass any `className` when the Button was used. It should be more explicit in the Button component that the `className` is optional.

You can use a JavaScript ES6 feature: the default parameter.

~~~~~~~~
class Button extends Component {
  render() {
    const {
      onClick,
      className = '',
      children,
    } = this.props;

    ...
  }
}
~~~~~~~~

Now, whenever there is no `className` property, the value will be an empty string.

### Exercises:

* read more about [ES6 default parameters](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Default_parameters)

## Component Declarations

By now you have four ES6 class components. But you can do better. Let me introduce functional stateless components as alternative for ES6 class components. Before you will refactor your components, let's introduce the different types of components.

* **Functional Stateless Components:** These components are functions which get an input and return an output. The input is the props object. The output is a component instance. So far it is quite similar to an ES6 class component. However, functional stateless components are functions (functional) and they have no internal state (stateless). You cannot access the state with `this.state` because there is no `this` object. Additionally they have no lifecycle methods. You didn't learn about lifecycle methods yet, but you already used two: `constructor()` and `render()`. Keep this fact about functional stateless components in mind, when you arrive at the lifecycle methods chapter later on.

* **ES6 Class Components:** You already used this type of component declaration. In the class definition they extend from the React component. The `extend` hooks all the lifecycle methods - available in the React component API - to the component. As I mentioned, you already used two of them. Additionally you can store and manipulate state in ES6 class components.

* **React.createClass:** The component declaration was used in older versions of React and still in JavaScript ES5 React applications. But [Facebook declared it as deprecated](https://facebook.github.io/react/blog/2015/03/10/react-v0.13.html) in favor of ES6. They even added a [deprecation warning in version 15.5](https://facebook.github.io/react/blog/2017/04/07/react-v15.5.0.html). You will not use it in the book.

But when to use functional stateless components over ES6 class components? A rule of thumb is to use functional stateless components when you don't need internal component state or component lifecycle methods. Usually you start to implement your components as functional stateless components. Once you need access to the state or lifecycle methods, you have to refactor it to an ES6 class component.

Let's get back to your application. The App component uses internal state. That's why it has to stay as an ES6 class component. But the other three of your ES6 class components are stateless without lifecycle methods. Let's refactor together the Search component to a stateless functional component. The Table and Button component refactoring will remain as your exercise.

~~~~~~~~
function Search(props) {
  const { value, onChange, children } = props;
  return (
    <form>
      {children} <input
        type="text"
        value={value}
        onChange={onChange}
      />
    </form>
  );
}
~~~~~~~~

That's basically it. But you can do more code wise in a functional stateless component. You already know the ES6 destructuring. The best practice is to use it in the function signature to destructure the props.

~~~~~~~~
function Search({ value, onChange, children }) {
  return (
    <form>
      {children} <input
        type="text"
        value={value}
        onChange={onChange}
      />
    </form>
  );
}
~~~~~~~~

But it can get better. You know already that ES6 arrow functions allow you to keep your functions concise. You can remove the block body of the function. In a concise body an implicit return is attached thus you can remove the return statement. Since your functional stateless component is a function, you can keep it concise as well.

~~~~~~~~
const Search = ({ value, onChange, children }) =>
  <form>
    {children} <input
      type="text"
      value={value}
      onChange={onChange}
    />
  </form>
~~~~~~~~

The last step was especially useful to enforce only to have props as input and an element as output. Nothing in between. Still, you could *do something* in between by using a block body in your ES6 arrow function.

{title="Code Playground",lang=javascript}
~~~~~~~~
const Search = ({ value, onChange, children }) => {

  // do something

  return (
    <form>
      {children} <input
        type="text"
        value={value}
        onChange={onChange}
      />
    </form>
  );
}
~~~~~~~~

But you don't need it for now. That's why you can keep the previous version without the block body.

Now you have one lightweight functional stateless component. Once you would need access to its internal component state or lifecycle methods, you would refactor it to an ES6 class component. In addition you saw how JavaScript ES6 can be used in React components to make them more elegant.

### Exercises:

* refactor the Table and Button component to stateless functional components
* read more about [ES6 class components and functional stateless components](https://facebook.github.io/react/docs/components-and-props.html)

## Styling Components

Let's add some basic styling to your application and components. You can reuse the *src/App.css* and *src/index.css* files. These files should be already in your project since you bootstapped it with create-react-app. They should be imported in your *src/App.js* and *src/index.js* files too. I prepared some CSS which you can simply copy and paste to these files, but feel free to use your own style.

{title="src/index.css",lang="css"}
~~~~~~~~
body {
  color: #222;
  background: #f4f4f4;
  font: 400 14px CoreSans, Arial,sans-serif;
}

a {
  color: #222;
}

a:hover {
  text-decoration: underline;
}

ul, li {
  list-style: none;
  padding: 0;
  margin: 0;
}

input {
  padding: 10px;
  border-radius: 5px;
  outline: none;
  margin-right: 10px;
  border: 1px solid #dddddd;
}

button {
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #dddddd;
  background: transparent;
  color: #808080;
  cursor: pointer;
}

button:hover {
  color: #222;
}

*:focus {
  outline: none;
}
~~~~~~~~

{title="src/App.css",lang="css"}
~~~~~~~~
.page {
  margin: 20px;
}

.interactions {
  text-align: center;
}

.table {
  margin: 20px 0;
}

.table-header {
  display: flex;
  line-height: 24px;
  font-size: 16px;
  padding: 0 10px;
  justify-content: space-between;
}

.table-empty {
  margin: 200px;
  text-align: center;
  font-size: 16px;
}

.table-row {
  display: flex;
  line-height: 24px;
  white-space: nowrap;
  margin: 10px 0;
  padding: 10px;
  background: #ffffff;
  border: 1px solid #e3e3e3;
}

.table-header > span {
  overflow: hidden;
  text-overflow: ellipsis;
  padding: 0 5px;
}

.table-row > span {
  overflow: hidden;
  text-overflow: ellipsis;
  padding: 0 5px;
}

.button-inline {
  border-width: 0;
  background: transparent;
  color: inherit;
  text-align: inherit;
  -webkit-font-smoothing: inherit;
  padding: 0;
  font-size: inherit;
  cursor: pointer;
}

.button-active {
  border-radius: 0;
  border-bottom: 1px solid #38BB6C;
}
~~~~~~~~

Now you can use the style in some of your components. Don't forget to use React `className` instead of `class` as HTML attribute.

First, apply it in your App ES6 class component.

~~~~~~~~
class App extends Component {

  ...

  render() {
    const { searchTerm, list } = this.state;
    return (
      <div className="page">
        <div className="interactions">
          <Search
            value={searchTerm}
            onChange={this.onSearchChange}
          >
            Search
          </Search>
        </div>
        <Table
          list={list}
          pattern={searchTerm}
          onDismiss={this.onDismiss}
        />
      </div>
    );
  }
}
~~~~~~~~

Second, apply it in your Table functional stateless component.

~~~~~~~~
const Table = ({ list, pattern, onDismiss }) =>
  <div className="table">
    { list.filter(isSearched(pattern)).map(item =>
      <div key={item.objectID} className="table-row">
        <span>
          <a href={item.url}>{item.title}</a>
        </span>
        <span>{item.author}</span>
        <span>{item.num_comments}</span>
        <span>{item.points}</span>
        <span>
          <Button
            onClick={() => onDismiss(item.objectID)}
            className="button-inline"
          >
            Dismiss
          </Button>
        </span>
      </div>
    )}
  </div>
~~~~~~~~

Now you have styled your application and components with basic CSS. It should look decent. As you know, JSX mixes up HTML and JavaScript. One could argue to add CSS in the mix as well. That's called inline style. You can define JavaScript objects and pass them to the style attribute of an element.

Let's keep the Table column width flexible by using inline style.

~~~~~~~~
const Table = ({ list, pattern, onDismiss }) =>
  <div className="table">
    { list.filter(isSearched(pattern)).map(item =>
      <div key={item.objectID} className="table-row">
        <span style={{ width: '40%' }}>
          <a href={item.url}>{item.title}</a>
        </span>
        <span style={{ width: '30%' }}>
          {item.author}
        </span>
        <span style={{ width: '10%' }}>
          {item.num_comments}
        </span>
        <span style={{ width: '10%' }}>
          {item.points}
        </span>
        <span style={{ width: '10%' }}>
          <Button
            onClick={() => onDismiss(item.objectID)}
            className="button-inline"
          >
            Dismiss
          </Button>
        </span>
      </div>
    )}
  </div>
~~~~~~~~

It is really inlined now. You could define the style objects outside of your elements to make it cleaner.

~~~~~~~~
const largeColumn = {
  width: '40%',
};

const midColumn = {
  width: '30%',
};

const smallColumn = {
  width: '10%',
};
~~~~~~~~

After that you could use it in your columns: `<span style={smallColumn}>`.

In general, you will find different opinions and solutions for style in React. You used pure CSS and inline style now. It is sufficient to get started.

I don't want to be opinionated here, but I want to leave you some more options. You can read about them and apply them on your own. But if you are new to React, I would recommend to stick to pure CSS and inline style for now.

* [radium](https://github.com/FormidableLabs/radium)
* [aphrodite](https://github.com/khan/aphrodite)
* [styled-components](https://github.com/styled-components/styled-components)
* [CSS Modules](https://github.com/css-modules/css-modules)

{pagebreak}

You have learned the basics to write your own React application! Let's recap the last chapters:

* React
  * use `this.state` and `setState()` to manage your internal component state
  * use forms and events in React to add interactions
  * unidirectional data flow is an important concept in React
  * compose components with children and reusable components
  * usage and implementation of ES6 class components and functional stateless components
  * approaches to style your components
* ES6
  * arrow functions with block and concise bodies to shorten your function declarations
  * functions that are bound to a class are class methods
  * destructuring of objects and arrays
  * default parameters
* General
  * higher order functions

Again it makes sense to take a break. Internalize the learnings and apply them on your own. You can experiment with the source code you have written so far. Additionally you can read more in the official [documentation](https://facebook.github.io/react/docs/installation.html).

You can find the source code in the [official repository](https://github.com/rwieruch/hackernews-client/tree/2705dcd1a2027c4a6ecb8132428b399785afdfa5).

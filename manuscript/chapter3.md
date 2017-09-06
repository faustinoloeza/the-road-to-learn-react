# Volverse real con una API

Ahora es el momento de ponerse real con una API, ya que puede ser aburrido tratar con datos artificiales.

Si no está familiarizado con APIs, Te animo [a leer mi viaje donde llegué a conocer APIs](https://www.robinwieruch.de/what-is-an-api-javascript/).

¿Conoces la plataforma [Hacker News](https://news.ycombinator.com/)? Es un gran agregador de noticias sobre temas tecnológicos. En este libro, utilizará la API de Hacker News para obtener historias de tendencias de la plataforma. Hay una API [basica](https://github.com/HackerNews/API) de [busqueda](https://hn.algolia.com/api) para obtener datos de la plataforma. Este último tiene sentido en tu caso para buscar historias en Hacker News. Puedes visitar la especificación de la API para obtener un vistazo de la estructura de datos.

## Métodos del ciclo de vida

Necesitará el conocimiento sobre los métodos de ciclo de vida de React antes de poder empezar a buscar datos. Estos métodos son un gancho en el ciclo de vida de un componente React. Pueden utilizarse en componentes de clase ES6, pero no en componentes funcionales sin estado.

¿Recuerdas cuando un capítulo anterior te enseñe sobre las clases de JavaScript ES6 y cómo se utilizan en React? Aparte del método `render()`, mencioné varios métodos que se pueden sobrescribir en un componente de clase React ES6. Todos estos son los métodos del ciclo de vida. Vamos a sumergirnos en ellos:

Ya conoces dos métodos de ciclo de vida en un componente de clase ES6: `constructor()` y `render()`.

El constructor sólo se llama cuando se crea una instancia del componente y se inserta en el DOM. El componente se instancia. Ese proceso se llama montaje del componente.

El método `render()` también se llama durante el proceso de montaje, pero también cuando el componente actualiza. Cada vez que el estado o las props de un componente cambian, se llama al metodo `render()`.

Ahora ya sabes más acerca de los dos métodos del ciclo de vida y cuándo se llaman. Ya los has utilizado. Pero hay más de ellos.

El montaje de un componente tiene dos métodos de ciclo de vida más: `componentWillMount()` y `componentDidMount()`. El constructor se llama primero, `componentWillMount()` se llama antes del metodo `render()` y `componentDidMount()` se llama después del metodo `render()`.

En general, el proceso de montaje tiene 4 métodos de ciclo de vida. Se invocan en el siguiente orden:

* constructor()
* componentWillMount()
* render()
* componentDidMount()

Pero ¿que pasa con la actualización del ciclo de vida de un camponente que sucede cuando el estado o las propiedades cambian? En general, tiene 5 métodos de ciclo de vida en el siguiente orden:

* componentWillReceiveProps()
* shouldComponentUpdate()
* componentWillUpdate()
* render()
* componentDidUpdate()

Por último, pero no menos importante, está el desmontaje del ciclo de vida. Sólo tiene un método de ciclo de vida: `componentWillUnmount()`.

Después de todo, no es necesario conocer todos estos métodos de ciclo de vida desde el principio. Puede ser intimidante pero no usarás todos - incluso en una aplicación React madura. Sin embargo, es bueno saber que cada método del ciclo de vida se puede utilizar para casos de uso específicos:

* **constructor(props)** - Se llama cuando el componente se inicializa. Puedes establecer un estado inicial del componente y vincular métodos de clase útiles durante ese método de ciclo de vida.

* **componentWillMount()** - Se llama antes del metodo del `render()`. Es por eso que podría ser utilizado para establecer el estado del componente interno, Porque no activará una segunda renderización del componente. Generalmente se recomienda utilizar el `constructor()` para establecer el estado inicial.

* **render()** - Este método del ciclo de vida es obligatorio y devuelve los elementos como una salida del componente. El método debe ser puro y por lo tanto no debe modificar el estado del componente. Recibe como entrada propiedades (props) y estados (state) y regresa un elemento.

* **componentDidMount()** - Se llama una sola vez cuando el componente fue montado. Ese es el momento perfecto para realizar una solicitud asincrónica para obtener datos de una API. Los datos obtenidos se almacenan en el estado interno del componente para mostrarlos en el metodo `render()`.

* **componentWillReceiveProps(nextProps)** - Se llama durante la actualización de un ciclo de vida. Como entrada recibirá las siguientes props . Puedes comparar las props siguientes con las anteriores (`this.props`) para aplicar un comportamiento diferente basado en la diferencia. Además, puede establecer el estado en función de las siguientes props.

* **shouldComponentUpdate(nextProps, nextState)** - Siempre se llama cuando el componente se actualiza debido a cambios de estado o props. Lo usarás en aplicaciones de React maduras para optimizaciones de rendimiento. Dependiendo de un booleano que regrese de este método de ciclo de vida, el componente y todos sus hijos se renderizaran o no en la actualización de un ciclo de vida. Puedes evitar que se ejecute el método de ciclo de vida render de un componente.

* **componentWillUpdate(nextProps, nextState)** - El método del ciclo de vida se invoca inmediatamente antes del método `render()`. Usted ya tiene las siguientes props y el próximo estado a su disposición. Puede utilizar el método como última oportunidad para realizar las preparaciones antes de ejecutar el método render. Tenga en cuenta que ya no puedes activar  `setState()`. Si deseas calcular el estado basado en las siguientes props, tienes que usar `componentWillReceiveProps()`.

* **componentDidUpdate(prevProps, prevState)** - El método del ciclo de vida se invoca inmediatamente después del método `render()`. Puedes usarlo como oportunidad para realizar operaciones DOM o para realizar más solicitudes asíncronas.

* **componentWillUnmount()** - Se llama antes de destruir tu componente. Puedes utilizar el método del ciclo de vida para realizar tareas de limpieza.

Los métodos de ciclo de vida `constructor()` y `render()` ya están siendo utilizados por ti. Estos son los métodos de ciclo de vida comúnmente utilizados para componentes de clase ES6. En realidad, el método `render()` es necesario, de lo contrario no devolveria una instancia de componente.

### Ejercicios:

* leer mas sobre [lifecycle methods in React](https://facebook.github.io/react/docs/react-component.html)
* leer mas sobre [the state related to lifecycle methods in React](https://facebook.github.io/react/docs/state-and-lifecycle.html)

## Obteniendo Datos

Ahora estás preparado para obtener datos de la API de Hacker News. He mencionado un método de ciclo de vida que se puede utilizar para obtener datos: `componentDidMount()`. Utilizará la API nativa para realizar la solicitud.

Antes de poder usarlo, vamos a configurar las constantes de url y los parámetros por defecto para dividir la solicitud de API en partes.

~~~~~~~~
import React, { Component } from 'react';
import './App.css';

const DEFAULT_QUERY = 'redux';

const PATH_BASE = 'https://hn.algolia.com/api/v1';
const PATH_SEARCH = '/search';
const PARAM_SEARCH = 'query=';

...
~~~~~~~~

En JavaScript ES6 puedes usar [plantillas de cadena de texto](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/template_strings) para concatenar cadenas. Lo usará para concatenar tu url para el punto final de la API.


~~~~~~~~
// ES6
const url = `${PATH_BASE}${PATH_SEARCH}?${PARAM_SEARCH}${DEFAULT_QUERY}`;

// ES5
var url = PATH_BASE + PATH_SEARCH + '?' + PARAM_SEARCH + DEFAULT_QUERY;

console.log(url);
// output: https://hn.algolia.com/api/v1/search?query=redux
~~~~~~~~

Eso mantendrá su composición url flexible en el futuro.

Pero vayamos a la solicitud de API donde usarás la url. TEl proceso completo de búsqueda de datos se presentará de una vez, Pero cada paso se explicará después.

~~~~~~~~
...

class App extends Component {

  constructor(props) {
    super(props);

    this.state = {
      result: null,
      searchTerm: DEFAULT_QUERY,
    };

    this.setSearchTopstories = this.setSearchTopstories.bind(this);
    this.fetchSearchTopstories = this.fetchSearchTopstories.bind(this);
    this.onSearchChange = this.onSearchChange.bind(this);
    this.onDismiss = this.onDismiss.bind(this);
  }

  setSearchTopstories(result) {
    this.setState({ result });
  }

  fetchSearchTopstories(searchTerm) {
    fetch(`${PATH_BASE}${PATH_SEARCH}?${PARAM_SEARCH}${searchTerm}`)
      .then(response => response.json())
      .then(result => this.setSearchTopstories(result))
      .catch(e => e);
  }

  componentDidMount() {
    const { searchTerm } = this.state;
    this.fetchSearchTopstories(searchTerm);
  }

  ...
}
~~~~~~~~

Muchas cosas suceden en el código. Pensé en romperlo en pedazos más pequeños. Por otra parte, sería difícil comprender las relaciones de cada pieza entre sí. Permítanme explicar cada paso en detalle.

En primer lugar, puedes eliminar la lista artificial de elementos, porque regresas un resultado de la API de Hacker News. El estado inicial de su componente tiene un resultado vacío y un término de búsqueda predeterminado. El mismo término de búsqueda predeterminado se utiliza en el campo de búsqueda y en su primera solicitud.

En segundo lugar, utilizas el metodo `componentDidMount()` para obtener los datos después de que el componente se montó. En la primera búsqueda, el término de búsqueda predeterminado del estado del componente se utiliza. Obtendrá historias relacionadas con "redux", porque ese es el parámetro predeterminado.

En tercer lugar, la búsqueda nativa se utiliza. Las cadenas de plantilla de JavaScript ES6 le permiten componer la url con el `searchTerm`. TLa url es el argumento de la función API de búsqueda nativa. La respuesta necesita ser transformada en json, es un paso obligatorio en una búsqueda nativa, y finalmente se puede establecer en el estado del componente interno.

Por último, pero no menos importante, no olvide vincular sus nuevos métodos de componentes.

Ahora puede utilizar los datos obtenidos en lugar de la lista artificial de elementos.Sin embargo, tienes que tener cuidado otra vez. El resultado no es sólo una lista de datos. [Es un objeto complejo con meta información y una lista de éxitos (historias).](https://hn.algolia.com/api) Puede emitir el estado interno con `console.log(this.state);` ent tu metodo `render()` para visualizarlo.

Utilizemos el resultado para mostrarlo. Pero lo preveeremos de renderizar cualquier cosa - return null - cuando no hay resultado. Una vez que la solicitud a la API tuvo éxito, el resultado se guarda en el estado y el componente App se volverá a renderizar con el estado actualizado.

~~~~~~~~
class App extends Component {

  ...

  render() {
    const { searchTerm, result } = this.state;

    if (!result) { return null; }

    return (
      <div className="page">
        ...
        <Table
          list={result.hits}
          pattern={searchTerm}
          onDismiss={this.onDismiss}
        />
      </div>
    );
  }
}
~~~~~~~~

Repasemos lo que sucede durante el ciclo de vida del componente. El componente es inicializa por el constructor. Después de que se renderiza por primera vez. Pero evitas que muestre, porque el resultado está vacío. Entonces se ejecuta el metodo `componentDidMount()`. En ese método, obtienes los datos de la API de Hacker News de forma asincrónica. Una vez que los datos llegan, cambia el estado interno del componente. Después de eso, el ciclo de vida de la actualización entra en juego. El componente ejecuta de nuevo el método  `render()`, pero esta vez con datos poblados en su estado interno del componente. El componente y, por tanto, el componente Tabla con su contenido se vuelve a renderizar.

Utilizó la API de recuperación nativa que es compatible con la mayoría de los navegadores para realizar una solicitud asincrónica a una API. La configuración de *create-react-app* garantiza su compatibilidad con todos los navegadores. Hay paquetes de terceros de node que puedes usar para sustituir la API de búsqueda nativa: [superagent](https://github.com/visionmedia/superagent) y [axios](https://github.com/mzabriskie/axios).

Regresa a tu aplicación: La lista de hits debe ser visible ahor. Pero el boton "Dismiss" no funciona. Lo arreglaremos en el siguiente capitulo.

### Ejercicios:

* leer mas sobre [ES6 plantilas de cadena de texto](https://developer.mozilla.org/es/docs/Web/JavaScript/Referencia/template_strings)
* leer mas sobre [the native fetch API](https://developer.mozilla.org/en/docs/Web/API/Fetch_API)
* experimenta con [Hacker News API](https://hn.algolia.com/api)

## ES6 Operadores de propagación

El botón "Dismiss" no funciona porque el metodo `onDismiss()` no tiene conocimiento del objeto complejo resultante. Cambiemos eso:

~~~~~~~~
onDismiss(id) {
  const isNotId = item => item.objectID !== id;
  const updatedHits = this.state.result.hits.filter(isNotId);
  this.setState({
    ...
  });
}
~~~~~~~~

Pero, ¿qué pasa en `setState()` ahora? Desafortunadamente el resultado es un objeto complejo. La lista de hits es sólo una de las múltiples propiedades del objeto. Sin embargo, sólo la lista se actualiza, cuando un elemento se quita en el objeto resultante, mientras que las otras propiedades permanecen igual.

Un enfoque podría ser mutar los hits en el objeto resultante. Lo demostraré, pero no lo haremos de esa manera.

~~~~~~~~
this.state.result.hits = updatedHits;
~~~~~~~~

React abarca la programación funcional. Por lo tanto, no debes mutar un objeto (o mutar el estado directamente). Un mejor enfoque es generar un nuevo objeto basado en la información que tienes. De este modo, ninguno de los objetos se altera. Mantendrás las estructuras de datos inmutables. Siempre devolverás un objeto nuevo y nunca alterarás un objeto.

Vamos a hacerlo en JavaScript ES5. `Object.assign()` toma como primer argumento un objeto destino. Todos los argumentos siguientes son objetos de origen. Estos objetos se combinan en el objeto de destino. El objeto de destino puede ser un objeto vacío. Abarca inmutabilidad, porque ningún objeto fuente se muta. Sería similar a lo siguiente:

~~~~~~~~
const updatedHits = { hits: updatedHits };
const updatedResult = Object.assign({}, this.state.result, updatedHits);
~~~~~~~~

Ahora vamos a hacerlo en el método  `onDismiss()`:

~~~~~~~~
onDismiss(id) {
  const isNotId = item => item.objectID !== id;
  const updatedHits = this.state.result.hits.filter(isNotId);
  this.setState({
    result: Object.assign({}, this.state.result, { hits: updatedHits })
  });
}
~~~~~~~~

Eso es en JavaScript ES5. Existe una solución más sencilla en ES6 y futuras versiones de JavaScript. ¿Puedo presentarles el operador de propagación? Sólo consta de tres puntos: `...` Cuando se utiliza, cada valor de una matriz u objeto se copia a otra matriz u objeto.

Examinemos el operador de propagación de arreglos de ES6, aunque aún no lo necesites.

~~~~~~~~
const userList = ['Robin', 'Andrew', 'Dan'];
const additionalUser = 'Jordan';
const allUsers = [ ...userList, additionalUser ];

console.log(allUsers);
// output: ['Robin', 'Andrew', 'Dan', 'Jordan']
~~~~~~~~

La variables `allUsers`  es un arreglo completamente nuevo. Las otras variables `userList` y `additionalUser` siguen igual. Incluso puedes combinar dos arreglos de esa manera en un nuevo arreglo.

~~~~~~~~
const oldUsers = ['Robin', 'Andrew'];
const newUsers = ['Dan', 'Jordan'];
const allUsers = [ ...oldUsers, ...newUsers ];

console.log(allUsers);
// output: ['Robin', 'Andrew', 'Dan', 'Jordan']
~~~~~~~~

Ahora echemos un vistazo al operador de propagación de objetos. ¡No es ES6! Es una [propuesta para una futura versión de ES](https://github.com/sebmarkbage/ecmascript-rest-spread) ya utilizada por la comunidad React. Es por eso que *create-react-app* incorporó la característica en la configuración.

Básicamente es el mismo que el operador de ES6 de dispersión de array de JavaScript pero con objetos. Copia cada par de valores clave en un nuevo objeto.

~~~~~~~~
const userNames = { firstname: 'Robin', lastname: 'Wieruch' };
const age = 28;
const user = { ...userNames, age };

console.log(user);
// output: { firstname: 'Robin', lastname: 'Wieruch', age: 28 }
~~~~~~~~

Multiples objetos pueden dispersarse como en el ejemplo de dispersion de arreglos.

~~~~~~~~
const userNames = { firstname: 'Robin', lastname: 'Wieruch' };
const userAge = { age: 28 };
const user = { ...userNames, ...userAge };

console.log(user);
// output: { firstname: 'Robin', lastname: 'Wieruch', age: 28 }
~~~~~~~~

Después de todo se puede utilizar para reemplazar ES5 `Object.assign()`.

~~~~~~~~
onDismiss(id) {
  const isNotId = item => item.objectID !== id;
  const updatedHits = this.state.result.hits.filter(isNotId);
  this.setState({
    result: { ...this.state.result, hits: updatedHits }
  });
}
~~~~~~~~

El boton "Dismiss" debería funcionar de nuevo.

### Ejercicios:

* leer más sobre [Object.assign()](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
* leer más sobre the [ES6 array spread operator](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Spread_operator)
  * the object spread operator is briefly mentioned

## Renderizado Condicional

The conditional rendering is introduced pretty early in React applications. It happens when you want to make a decision to render either one or another element. Sometimes it means to render an element or nothing. After all, a conditional rendering simplest usage can be expressed by an if-else statement in JSX.

The `result` object in the internal component state is null in the beginning. So far, the App component returned no elements when the `result` hasn't arrived from the API. That's already a conditional rendering, because you return earlier from the `render()` lifecycle method for a certain condition. The App component either renders nothing or its elements.

But let's go one step further. It makes more sense to wrap the Table component, which is the only component that depends on the `result`, in an independent conditional rendering. Everything else should be displayed, even though there is no `result` yet. You can simply use a ternary expression in your JSX.

~~~~~~~~
class App extends Component {

  ...

  render() {t
    const { searchTerm, result } = this.state;
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
        { result
          ? <Table
            list={result.hits}
            pattern={searchTerm}
            onDismiss={this.onDismiss}
          />
          : null
        }
      </div>
    );
  }
}
~~~~~~~~

That's your second option to express a conditional rendering. A third option is the logical `&&` operator. In JavaScript a `true && 'Hello World'` always evaluates to 'Hello World'. A `false && 'Hello World'` always evaluates to false.

~~~~~~~~
const result = true && 'Hello World';
console.log(result);
// output: Hello World

const result = false && 'Hello World';
console.log(result);
// output: false
~~~~~~~~

In React you can make use of that behavior. If the condition is true, the expression after the logical `&&` operator will be the output. If the condition is false, React ignores and skips the expression. It is applicable in the Table conditional rendering case, because it should return a Table or nothing.

~~~~~~~~
{ result &&
  <Table
    list={result.hits}
    pattern={searchTerm}
    onDismiss={this.onDismiss}
  />
}
~~~~~~~~

These were a few approaches to use conditional rendering in React. You can read about [more alternatives on my website](https://www.robinwieruch.de/conditional-rendering-react/) where I keep an exhaustive list of conditional renderings. Moreover you will get to know their different use cases and when to apply them.

After all, you should be able to see the fetched data in your application. Everything except the Table is displayed when the data fetching is pending. Once the request resolves the result, the Table is displayed.

### Exercises:

* read more about [React conditional rendering](https://facebook.github.io/react/docs/conditional-rendering.html)
* read more about [different ways for conditional renderings](https://www.robinwieruch.de/conditional-rendering-react/)

## Client- or Server-side Search

When you use the search input field now, you will filter the list. That's happening on the client-side though. Now you are going to use the Hacker News API to search on the server-side. Otherwise you would deal only with the first API response which you got on `componentDidMount()` with the default search term parameter.

You can define an `onSubmit()` method in your ES6 class component, which fetches results from the Hacker News API. It will be the same fetch like in your `componentDidMount()` lifecycle method. But it fetches it with the modified search term from the search field input.

~~~~~~~~
class App extends Component {

  constructor(props) {
    super(props);

    this.state = {
      result: null,
      searchTerm: DEFAULT_QUERY,
    };

    this.setSearchTopstories = this.setSearchTopstories.bind(this);
    this.fetchSearchTopstories = this.fetchSearchTopstories.bind(this);
    this.onSearchChange = this.onSearchChange.bind(this);
    this.onSearchSubmit = this.onSearchSubmit.bind(this);
    this.onDismiss = this.onDismiss.bind(this);
  }

  ...

  onSearchSubmit() {
    const { searchTerm } = this.state;
    this.fetchSearchTopstories(searchTerm);
  }

  ...
}
~~~~~~~~

The Search component gets an additional button. The button has to explicitly trigger the search. Otherwise you would fetch data every time from the Hacker News API when your input changes.

As alternative you could debounce (delay) the `onChange()` function and spare the button, but it would add more complexity at this time. Let's keep it simple without a debounce.

First, pass the `onSearchSubmit()` method to your Search component.

~~~~~~~~
class App extends Component {

  ...

  render() {
    const { searchTerm, result } = this.state;
    return (
      <div className="page">
        <div className="interactions">
          <Search
            value={searchTerm}
            onChange={this.onSearchChange}
            onSubmit={this.onSearchSubmit}
          >
            Search
          </Search>
        </div>
        { result &&
          <Table
            list={result.hits}
            pattern={searchTerm}
            onDismiss={this.onDismiss}
          />
        }
      </div>
    );
  }
}
~~~~~~~~

Second, introduce a button in your Search component. The button has the `type="submit"` and the form uses its `onSubmit()` attribute to pass the `onSubmit()` method. You can reuse the children property, but this time it will be used as the content of the button.

~~~~~~~~
const Search = ({
  value,
  onChange,
  onSubmit,
  children
}) =>
  <form onSubmit={onSubmit}>
    <input
      type="text"
      value={value}
      onChange={onChange}
    />
    <button type="submit">
      {children}
    </button>
  </form>
~~~~~~~~

In the Table you can remove the filter functionality, because there will be no client-side filter (search) anymore. The result comes directly from the Hacker News API after you have clicked the "Search" button.

~~~~~~~~
class App extends Component {

  ...

  render() {
    const { searchTerm, result } = this.state;
    return (
      <div className="page">
        ...
        { result &&
          <Table
            list={result.hits}
            onDismiss={this.onDismiss}
          />
        }
      </div>
    );
  }
}

...

const Table = ({ list, onDismiss }) =>
  <div className="table">
    { list.map(item =>
      ...
    )}
  </div>
~~~~~~~~

When you try to search now, you will notice that the browser reloads. That's a native browser behavior for a submit callback in a form. In React you will often come across the `preventDefault()` event method to suppress the native browser behavior.

~~~~~~~~
onSearchSubmit(event) {
  const { searchTerm } = this.state;
  this.fetchSearchTopstories(searchTerm);
  event.preventDefault();
}
~~~~~~~~

Now you should be able to search different Hacker News stories. You interact with a real world API. There should be no client-side search anymore.

### Exercises:

* read more about [synthetic events in React](https://facebook.github.io/react/docs/events.html)

## Paginated Fetch

Did you have a closer look at the returned data structure yet? The [Hacker News API](https://hn.algolia.com/api) returns more than a list of hits. The page property, which is 0 in the first response, can be used to fetch more paginated data. You only need to pass the next page with the same search term to the API.

Let's extend the composable API constants that so it can deal with paginated data.

~~~~~~~~
const DEFAULT_QUERY = 'redux';
const DEFAULT_PAGE = 0;

const PATH_BASE = 'https://hn.algolia.com/api/v1';
const PATH_SEARCH = '/search';
const PARAM_SEARCH = 'query=';
const PARAM_PAGE = 'page=';
~~~~~~~~

Now you can use these constants to add the page parameter to your API request.

~~~~~~~~
const url = `${PATH_BASE}${PATH_SEARCH}?${PARAM_SEARCH}${searchTerm}&${PARAM_PAGE}`;

console.log(url);
// output: https://hn.algolia.com/api/v1/search?query=redux&page=
~~~~~~~~

The `fetchSearchTopstories()` method will take the page as second argument. The `componentDidMount()` and `onSearchSubmit()` methods take the `DEFAULT_PAGE` for the initial API calls. They should fetch the first page on the first request. Every additional fetch should fetch the next page.

~~~~~~~~
class App extends Component {

  ...

  componentDidMount() {
    const { searchTerm } = this.state;
    this.fetchSearchTopstories(searchTerm, DEFAULT_PAGE);
  }

  fetchSearchTopstories(searchTerm, page) {
    fetch(`${PATH_BASE}${PATH_SEARCH}?${PARAM_SEARCH}${searchTerm}&${PARAM_PAGE}${page}`)
      .then(response => response.json())
      .then(result => this.setSearchTopstories(result))
      .catch(e => e);
  }

  onSearchSubmit(event) {
    const { searchTerm } = this.state;
    this.fetchSearchTopstories(searchTerm, DEFAULT_PAGE);
    event.preventDefault();
  }

  ...

}
~~~~~~~~

Now you can use the current page from the API response in `fetchSearchTopstories()`. You can use this method in a button to fetch more stories on a button click. Let's use the Button to fetch more paginated data from the Hacker News API. You only need to define the `onClick()` function which takes the current search term and the next page (current page + 1).

~~~~~~~~
class App extends Component {

  ...

  render() {
    const { searchTerm, result } = this.state;
    const page = (result && result.page) || 0;
    return (
      <div className="page">
        <div className="interactions">
        ...
        { result &&
          <Table
            list={result.hits}
            onDismiss={this.onDismiss}
          />
        }
        <div className="interactions">
          <Button onClick={() => this.fetchSearchTopstories(searchTerm, page + 1)}>
            More
          </Button>
        </div>
      </div>
    );
  }
}
~~~~~~~~

You should make sure to default to page 0 when there is no result.

There is one step missing. You fetch the next page of data, but it will overwrite your previous page of data. You want to concatenate the old and new data. Let's adjust the functionality to add the new data rather than to overwrite it.

~~~~~~~~
setSearchTopstories(result) {
  const { hits, page } = result;

  const oldHits = page !== 0
    ? this.state.result.hits
    : [];

  const updatedHits = [
    ...oldHits,
    ...hits
  ];

  this.setState({
    result: { hits: updatedHits, page }
  });
}
~~~~~~~~

First, you get the hits and page from the result.

Second, you have to check if there are already old hits. When the page is 0, it is a new search request from `componentDidMount()` or `onSearchSubmit()`. The hits are empty. But when you click the "More" button to fetch paginated data the page isn't 0. It is the next page. The old hits are already stored in your state and thus can be used.

Third, you don't want to overwrite the old hits. You can merge old and new hits from the recent API request. The merge of both lists can be done with the JavaScript ES6 array spread operator.

Fourth, you set the merged hits and page in the internal component state.

You can make one last adjustment. When you try the "More" button it only fetches a few list items. The API url can be extended to fetch more list items with each request. Again you can add more composable path constants.

~~~~~~~~
const DEFAULT_QUERY = 'redux';
const DEFAULT_PAGE = 0;
const DEFAULT_HPP = '100';

const PATH_BASE = 'https://hn.algolia.com/api/v1';
const PATH_SEARCH = '/search';
const PARAM_SEARCH = 'query=';
const PARAM_PAGE = 'page=';
const PARAM_HPP = 'hitsPerPage=';
~~~~~~~~

Now you can use the constants to extend the API url.

~~~~~~~~
fetchSearchTopstories(searchTerm, page) {
  fetch(`${PATH_BASE}${PATH_SEARCH}?${PARAM_SEARCH}${searchTerm}&${PARAM_PAGE}${page}&${PARAM_HPP}${DEFAULT_HPP}`)
    .then(response => response.json())
    .then(result => this.setSearchTopstories(result))
    .catch(e => e);
}
~~~~~~~~

Afterward the request to the Hacker News API fetches more list items in one request than before.

### Exercises:

* experiment with the [Hacker News API parameters](https://hn.algolia.com/api)

## Client Cache

Each search submit makes a request to the Hacker News API. You might search for "redux", followed by "react" and eventually "redux" again. In total it makes 3 requests. But you searched for "redux" twice and both times it took a whole asynchronous roundtrip to fetch the data. In a client-sided cache you would store each result. When a request to the API is made, it checks if a result is already there. If it is there, the cache is used. Otherwise an API request is made to fetch the data.

In order to have a client cache for each result, you have to store multiple `results` rather than one `result` in your internal component state. The results object will be a map with the search term as key and the result as value. Each result from the API will be saved by search term (key).

At the moment your result in the component state looks similar to the following:

~~~~~~~~
result: {
  hits: [ ... ],
  page: 2,
}
~~~~~~~~

Imagine you have made two API requests. One for the search term "redux" and another one for "react". The results map should look like the following:

{title="Code Playground",lang="javascript"}
~~~~~~~~
results: {
  redux: {
    hits: [ ... ],
    page: 2,
  },
  react: {
    hits: [ ... ],
    page: 1,
  },
  ...
}
~~~~~~~~

Let's implement a client-side cache with React `setState()`. First, rename the `result` object to `results` in the initial component state. Second, define a temporary `searchKey` which is used to store each `result`.

~~~~~~~~
class App extends Component {

  constructor(props) {
    super(props);

    this.state = {
      results: null,
      searchKey: '',
      searchTerm: DEFAULT_QUERY,
    };

    ...

  }

  ...

}
~~~~~~~~

The `searchKey` has to be set before each request is made. It reflects the `searchTerm`. You might wonder: Why don't we use the `searchTerm` in the first place? The `searchTerm` is a fluctuant variable, because it gets changed every time you type into the Search input field. However, in the end you will need a non fluctuant variable. It determines the recent submitted search term to the API and can be used to retrieve the correct result from the map of results. It is a pointer to your current result in the cache.

~~~~~~~~
componentDidMount() {
  const { searchTerm } = this.state;
  this.setState({ searchKey: searchTerm });
  this.fetchSearchTopstories(searchTerm, DEFAULT_PAGE);
}

onSearchSubmit(event) {
  const { searchTerm } = this.state;
  this.setState({ searchKey: searchTerm });
  this.fetchSearchTopstories(searchTerm, DEFAULT_PAGE);
  event.preventDefault();
}
~~~~~~~~

Now you have to adjust the functionality where the result is stored to the internal component state. It should store each result by `searchKey`.

~~~~~~~~
class App extends Component {

  ...

  setSearchTopstories(result) {
    const { hits, page } = result;
    const { searchKey, results } = this.state;

    const oldHits = results && results[searchKey]
      ? results[searchKey].hits
      : [];

    const updatedHits = [
      ...oldHits,
      ...hits
    ];

    this.setState({
      results: {
        ...results,
        [searchKey]: { hits: updatedHits, page }
      }
    });
  }

  ...

}
~~~~~~~~

The `searchKey` will be used as the key to save the updated hits and page in a `results` map.

First, you have to retrieve the `searchKey` from the component state. Remember that the `searchKey` gets set on `componentDidMount()` and `onSearchSubmit()`.

Second, the old hits have to get merged with the new hits as before. But this time the old hits get retrieved from the `results` map with the `searchKey` as key.

Third, a new result can be set in the `results` map in the state. Let's examine the `results` object in `setState()`.

~~~~~~~~
results: {
  ...results,
  [searchKey]: { hits: updatedHits, page }
}
~~~~~~~~

The bottom part makes sure to store the updated result by `searchKey` in the results map. The value is an object with a hits and page property. The `searchKey` is the search term. You already learned the `[searchKey]` syntax. It is an ES6 computed property name. It helps you to allocate values dynamically in an object.

The upper part needs to object spread all other results by `searchKey` in the state. Otherwise you would lose all results you stored before.

Now you store all results by search term. That's the first step to enable your cache. In the next step you can retrieve the result depending on the search term from your map of results.

~~~~~~~~
class App extends Component {

  ...

  render() {
    const {
      searchTerm,
      results,
      searchKey
    } = this.state;

    const page = (
      results &&
      results[searchKey] &&
      results[searchKey].page
    ) || 0;

    const list = (
      results &&
      results[searchKey] &&
      results[searchKey].hits
    ) || [];

    return (
      <div className="page">
        <div className="interactions">
          ...
        </div>
        <Table
          list={list}
          onDismiss={this.onDismiss}
        />
        <div className="interactions">
          <Button onClick={() => this.fetchSearchTopstories(searchKey, page + 1)}>
            More
          </Button>
        </div>
      </div>
    );
  }
}
~~~~~~~~

Since you default to an empty list when there is no result by `searchKey`, you can spare the conditional rendering for the Table component now. Additionally you will need to pass the `searchKey` rather than the `searchTerm` to the "More" button. Otherwise your paginated fetch depends on the `searchTerm` value which is fluctuant. Moreover make sure to keep the fluctuant `searchTerm` property for the input field in the "Search" component.

The search functionality should work again. It stores all results from the Hacker News API.

Additionally the `onDismiss()` method needs to get improved. It still deals with the `result` object. Now it has to deal with multiple `results`.

~~~~~~~~
  onDismiss(id) {
    const { searchKey, results } = this.state;
    const { hits, page } = results[searchKey];

    const isNotId = item => item.objectID !== id;
    const updatedHits = hits.filter(isNotId);

    this.setState({
      results: {
        ...results,
        [searchKey]: { hits: updatedHits, page }
      }
    });
  }
~~~~~~~~

The "Dismiss" button should work again.

However, nothing stops the application from sending an API request on each search submit. Even though there might be already a result, there is no check that prevents the request. The cache functionality is not complete yet. The last step would be to prevent the request when a result is available in the cache.

~~~~~~~~
class App extends Component {

  constructor(props) {

    ...

    this.needsToSearchTopstories = this.needsToSearchTopstories.bind(this);
    this.setSearchTopstories = this.setSearchTopstories.bind(this);
    this.fetchSearchTopstories = this.fetchSearchTopstories.bind(this);
    this.onSearchChange = this.onSearchChange.bind(this);
    this.onSearchSubmit = this.onSearchSubmit.bind(this);
    this.onDismiss = this.onDismiss.bind(this);
  }

  needsToSearchTopstories(searchTerm) {
    return !this.state.results[searchTerm];
  }

  ...

  onSearchSubmit(event) {
    const { searchTerm } = this.state;
    this.setState({ searchKey: searchTerm });

    if (this.needsToSearchTopstories(searchTerm)) {
      this.fetchSearchTopstories(searchTerm, DEFAULT_PAGE);
    }

    event.preventDefault();
  }

  ...

}
~~~~~~~~

Now your client makes a request to the API only once although you search for a search term twice. Even paginated data with several pages gets cached that way, because you always save the last page for each result in the `results` map.

You have learned to interact with an API in React! Let's recap the last chapters:

* React
  * ES6 class component lifecycle methods for different use cases
  * componentDidMount() for API interactions
  * conditional renderings
  * synthetic events on forms
* ES6
  * template strings to compose strings
  * spread operator for immutable data structures
  * computed property names
* General
  * Hacker News API interaction
  * native fetch browser API
  * client- and server-side search
  * pagination of data
  * client-side caching

Again it makes sense to take a break. Internalize the learnings and apply them on your own. You can experiment with the source code you have written so far.

You can find the source code in the [official repository](https://github.com/rwieruch/hackernews-client/tree/e60436a9d6c449e76a362aef44dd5667357b7994).

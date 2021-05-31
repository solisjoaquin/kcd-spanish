# Lo que necesitas de JavaScript para aprender React

_Con qué características de JavaScript debe estar familiarizado al aprender y usar React_ 

![Benjamin Voros](https://kentcdodds.com/static/3d283a7e351a639fbc71b810eee15eab/c6969/banner.webp)

Una de las cosas que más me gustan de React en comparación con otros frameworks que he usado es lo expuesto que estás a JavaScript cuando lo estás usando. No hay plantilla DSL (JSX se compila en JavaScript), la API del componente solo se ha vuelto más simple con la adición de [React Hooks](https://reactjs.org/hooks), y el framework le ofrece muy poca abstracción fuera de las preocupaciones centrales de la interfaz de usuario que pretende resolver.

Debido a esto, aprender las funciones de JavaScript es realmente recomendable para que seas efectivo en la construcción de aplicaciones con React. Entonces, aquí hay algunas características de JavaScript que le recomiendo que dedique un tiempo a aprender para que pueda ser lo más efectivo posible trabajando con React.

Antes de entrar en algunas cosas de sintaxis, otra cosa que es realmente útil de entender para React, es el concepto de "closure" de una función. Aquí hay una gran descripción de este concepto: [whatthefork.is/closure](https://whatthefork.is/closure).

Ok, vayamos a las funciones de JS que querrás saber para React.

## Template Literals

Los template literals son como strings con superpoderes:

```js
const greeting = 'Hello'
const subject = 'World'
console.log(`${greeting} ${subject}!`) // Hello World!

// this is the same as:
console.log(greeting + ' ' + subject + '!')

// in React:
function Box({className, ...props}) {
  return <div className={`box ${className}`} {...props} />
}
```

[MDN: Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)

## Shorthand property names

Esto es tan común y útil que lo hago sin pensar ahora.

```js
const a = 'hello'
const b = 42
const c = {d: [true, false]}
console.log({a, b, c})

// this is the same as:
console.log({a: a, b: b, c: c})

// in React:
function Counter({initialCount, step}) {
  const [count, setCount] = useCounter({initialCount, step})
  return <button onClick={setCount}>{count}</button>
}
```
[MDN: Object initializer New notations in ECMAScript 2015](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#New_notations_in_ECMAScript_2015)


## Arrow functions

Las arrow functions son otra forma de escribir funciones en JavaScript, pero tienen algunas diferencias semánticas. Afortunadamente para nosotros en React, no tenemos que preocuparnos tanto por esto si usamos hooks en nuestro proyecto (en lugar de clases), pero la arrow function permite funciones anónimas más breves y retornos implícitos, por lo que ver y querer utilizar muchas arrow functions.

```js
const getFive = () => 5
const addFive = a => a + 5
const divide = (a, b) => a / b

// this is the same as:
function getFive() {
  return 5
}

function addFive(a) {
  return a + 5
}
function divide(a, b) {
  return a / b
}

// in React:
function TeddyBearList({teddyBears}) {
  return (
    <ul>
      {teddyBears.map(teddyBear => (
        <li key={teddyBear.id}>
          <span>{teddyBear.name}</span>
        </li>
      ))}
    </ul>
  )
}
```
>Una cosa a tener en cuenta sobre el ejemplo anterior son los paréntesis de apertura y cierre `(`. Esta es una forma común de aprovechar las capacidades de retorno implícitas de la arrow function cuando se trabaja con JSX.

[MDN: Arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

## Destructuring

La desestructuración es probablemente mi característica favorita de JavaScript. Uso esta caracteristica sobre objetos y arrays todo el tiempo (y si estás usando `useState` probablemente también lo estés usando, [así](https://kentcdodds.com/blog/react-hooks-array-destructuring-fundamentals)). Me encanta lo declarativo que es.

```js
// const obj = {x: 3.6, y: 7.8}
// makeCalculation(obj)

function makeCalculation({x, y: d, z = 4}) {
  return Math.floor((x + d + z) / 3)
}

// this is the same as
function makeCalculation(obj) {
  const {x, y: d, z = 4} = obj
  return Math.floor((x + d + z) / 3)
}

// which is the same as
function makeCalculation(obj) {
  const x = obj.x
  const d = obj.y
  const z = obj.z === undefined ? 4 : obj.z
  return Math.floor((x + d + z) / 3)
}

// in React:
function UserGitHubImg({username = 'ghost', ...props}) {
  return <img src={`https://github.com/${username}.png`} {...props} />
}
```
[MDN: Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

> Definitivamente lea ese artículo de MDN. Seguro que aprenderá algo nuevo. Cuando haya terminado, intente refactorizar esto para usar una sola línea de desestructuración:

```js
function nestedArrayAndObject() {
  // refactor this to a single line of destructuring...
  const info = {
    title: 'Once Upon a Time',
    protagonist: {
      name: 'Emma Swan',
      enemies: [
        {name: 'Regina Mills', title: 'Evil Queen'},
        {name: 'Cora Mills', title: 'Queen of Hearts'},
        {name: 'Peter Pan', title: `The boy who wouldn't grow up`},
        {name: 'Zelena', title: 'The Wicked Witch'},
      ],
    },
  }

  // const {} = info // <-- replace the next few `const` lines with this
  const title = info.title
  const protagonistName = info.protagonist.name
  const enemy = info.protagonist.enemies[3]
  const enemyTitle = enemy.title
  const enemyName = enemy.name
  return `${enemyName} (${enemyTitle}) is an enemy to ${protagonistName} in "${title}"`
}
```
## Parametros por default

Esta es otra característica que uso todo el tiempo. Es una forma realmente poderosa de expresar de forma declarativa valores predeterminados para sus funciones.

```js
// add(1)
// add(1, 2)
function add(a, b = 0) {
  return a + b
}

// is the same as
const add = (a, b = 0) => a + b

// is the same as
function add(a, b) {
  b = b === undefined ? 0 : b
  return a + b
}

// in React:
function useLocalStorageState({
  key,
  initialValue,
  serialize = v => v,
  deserialize = v => v,
}) {

  const [state, setState] = React.useState(
    () => deserialize(window.localStorage.getItem(key)) || initialValue,
  )

  const serializedState = serialize(state)
  React.useEffect(() => {
    window.localStorage.setItem(key, serializedState)
  }, [key, serializedState])

  return [state, setState]
}
```
[MDN: Default parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)

## Operador Rest/Spread

La sintaxis `...` se puede considerar como una especie de sintaxis de "colección" en la que opera sobre una colección de valores. Lo uso todo el tiempo y le recomiendo encarecidamente que aprenda cómo y dónde se puede usar también. En realidad, toma diferentes significados en diferentes contextos, por lo que aprender los matices lo ayudará.

```js
const arr = [5, 6, 8, 4, 9]
Math.max(...arr)
// is the same as
Math.max.apply(null, arr)

const obj1 = {
  a: 'a from obj1',
  b: 'b from obj1',
  c: 'c from obj1',
  d: {
    e: 'e from obj1',
    f: 'f from obj1',
  },
}

const obj2 = {
  b: 'b from obj2',
  c: 'c from obj2',
  d: {
    g: 'g from obj2',
    h: 'g from obj2',
  },
}
console.log({...obj1, ...obj2})
// is the same as
console.log(Object.assign({}, obj1, obj2))

function add(first, ...rest) {
  return rest.reduce((sum, next) => sum + next, first)

}

// is the same as
function add() {
  const first = arguments[0]
  const rest = Array.from(arguments).slice(1)
  return rest.reduce((sum, next) => sum + next, first)
}

// in React:
function Box({className, ...restOfTheProps}) {
  const defaultProps = {
    className: `box ${className}`,
    children: 'Empty box',
  }
  return <div {...defaultProps} {...restOfTheProps} />
}
```
[MDN: Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

[MDN: Rest parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)

## ESModules

Si está creando una aplicación con herramientas modernas, lo más probable es que admita módulos, es una buena idea aprender cómo funciona la sintaxis porque cualquier aplicación de tamaño trivial probablemente necesitará hacer uso de módulos para la reutilización y organización del código.

```js
export default function add(a, b) {
  return a + b
}

/*
 * import add from './add'
 * console.assert(add(3, 2) === 5)
 */

export const foo = 'bar'

/*
 * import {foo} from './foo'
 * console.assert(foo === 'bar')
 */

export function subtract(a, b) {
  return a - b
}

export const now = new Date()

/*
 * import {subtract, now} from './stuff'
 * console.assert(subtract(4, 2) === 2)
 * console.assert(now instanceof Date)
 */

// dynamic imports
import('./some-module').then(
  allModuleExports => {
    // the allModuleExports object will be the same object you get if you had
    // used: import * as allModuleExports from './some-module'
    // the only difference is this will be loaded asynchronously which can
    // have performance benefits in some cases
  },
  error => {

    // handle the error
    // this will happen if there's an error loading or running the module
  },
)

// in React:
import React, {Suspense, Fragment} from 'react'

// dynamic import of a React component
const BigComponent = React.lazy(() => import('./big-component'))
// big-component.js would need to "export default BigComponent" for this to work
```

[MDN: import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)

[MDN: export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export)

Como otro recurso, di una charla completa sobre esta sintaxis y [puedes verla aquí](https://www.youtube.com/watch?v=kTlcu16rSLc&list=PLV5CVI1eNcJgNqzNwcs4UKrlJdhfDjshf).

## Ternarios

Amo los ternarios. Son maravillosamente declarativos. Especialmente en JSX.

```js
const message = bottle.fullOfSoda
  ? 'The bottle has soda!'
  : 'The bottle may not have soda :-('

// is the same as
let message
if (bottle.fullOfSoda) {
  message = 'The bottle has soda!'
} else {
  message = 'The bottle may not have soda :-('
}

// in React:
function TeddyBearList({teddyBears}) {
  return (
    <React.Fragment>
      {teddyBears.length ? (
        <ul>
          {teddyBears.map(teddyBear => (
            <li key={teddyBear.id}>
              <span>{teddyBear.name}</span>
            </li>
          ))}
        </ul>
      ) : (
        <div>There are no teddy bears. The sadness.</div>
      )}
    </React.Fragment>
  )
}
```

> Me doy cuenta de que los ternarios pueden tener una reacción instintiva de disgusto por parte de algunas personas que tuvieron que soportar el tratar de dar sentido a los ternarios antes de que aparecieran más bonitos y limpiaran nuestro código. Si aún no está usando [prettier](https://prettier.io/), le recomiendo encarecidamente que lo haga. Prettier hará que tus ternarios sean mucho más fáciles de leer.



[MDN: Conditional (ternary) operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)

## Metodos con arrays

¡Los arrays son fantásticos y yo uso métodos de arrays todo el tiempo! Probablemente utilice los siguientes métodos con más frecuencia:

*   find
*    some
*    every
*    includes
*    map
*    filter
*    reduce

Aqui hay algunos ejemplos:

```js
const dogs = [
  {
    id: 'dog-1',
    name: 'Poodle',
    temperament: [
      'Intelligent',
      'Active',
      'Alert',
      'Faithful',
      'Trainable',
      'Instinctual',
    ],
  },
  {
    id: 'dog-2',
    name: 'Bernese Mountain Dog',
    temperament: ['Affectionate', 'Intelligent', 'Loyal', 'Faithful'],
  },
  {
    id: 'dog-3',
    name: 'Labrador Retriever',
    temperament: [
      'Intelligent',
      'Even Tempered',
      'Kind',
      'Agile',
      'Outgoing',
      'Trusting',
      'Gentle',
    ],
  },
]

dogs.find(dog => dog.name === 'Bernese Mountain Dog')
// {id: 'dog-2', name: 'Bernese Mountain Dog', ...etc}

dogs.some(dog => dog.temperament.includes('Aggressive'))
// false

dogs.some(dog => dog.temperament.includes('Trusting'))
// true

dogs.every(dog => dog.temperament.includes('Trusting'))
// false

dogs.every(dog => dog.temperament.includes('Intelligent'))
// true

dogs.map(dog => dog.name)
// ['Poodle', 'Bernese Mountain Dog', 'Labrador Retriever']

dogs.filter(dog => dog.temperament.includes('Faithful'))
// [{id: 'dog-1', ..etc}, {id: 'dog-2', ...etc}]

dogs.reduce((allTemperaments, dog) => {
  return [...allTemperaments, ...dog.temperament]
}, [])
// [ 'Intelligent', 'Active', 'Alert', ...etc ]

// in React:
function RepositoryList({repositories, owner}) {
  return (
    <ul>
      {repositories
        .filter(repo => repo.owner === owner)
        .map(repo => (
          <li key={repo.id}>{repo.name}</li>
        ))}
    </ul>
  )
}
```

[MDN: Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)

## Nullish coalescing operator
Si un valor es `null` o `undefined`, es posible que desee volver a algún valor predeterminado:
```js
// here's what we often did for this:
x = x || 'some default'

// but this was problematic for numbers or booleans where "0" or "false" are valid values

// So, if we wanted to support this:
add(null, 3)

// here's what we had to do before:
function add(a, b) {
  a = a == null ? 0 : a
  b = b == null ? 0 : b
  return a + b
}

// here's what we can do now
function add(a, b) {
  a = a ?? 0
  b = b ?? 0
  return a + b
}

// in React:
function DisplayContactName({contact}) {
  return <div>{contact.name ?? 'Unknown'}</div>
}
```

[MDN: Nullish coalescing operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)

## Optional chaining

También conocido como el "Operador de Elvis", esto le permite acceder de forma segura a propiedades y call functions que pueden existir o no. Antes del opcional chaining, usabamos una solución que se basaba en falsy/truthy-ness.
```js
// what we did before optional chaining:
const streetName = user && user.address && user.address.street.name

// what we can do now:
const streetName = user?.address?.street?.name

// this will run even if options is undefined (in which case, onSuccess would be undefined as well)
// however, it will still fail if options was never declared,
// since optional chaining cannot be used on a non-existent root object.
// optional chaining does not replace checks like if (typeof options == "undefined")

const onSuccess = options?.onSuccess

// this will run without error even if onSuccess is undefined (in which case, no function will be called)
onSuccess?.({data: 'yay'})

// and we can combine those things into a single line:
options?.onSuccess?.({data: 'yay'})

// and if you are 100% certain that onSuccess is a function if options exists
// then you don't need the extra ?. before calling it. Only use ?. in situations
// where the thing on the left might not exist.

options?.onSuccess({data: 'yay'})

// in React:
function UserProfile({user}) {
  return (
    <div>
      <h1>{user.name}</h1>
      <strong>{user.bio?.slice(0, 50)}...</strong>
    </div>
  )
}
```
Una advertencia sobre esto es que si te encuentras haciendo `?.` mucho en su código, es posible que desee considerar el lugar donde se originan esos valores y asegurarse de que devuelvan constantemente los valores que deberían.

[MDN: Optional chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)

## Promesas y async/await
Este es un tema muy importante y puede tomar un poco de práctica y tiempo trabajar con ellos para ser buenos en ellos. Las promesas están en todas partes en el ecosistema de JavaScript y gracias a lo arraigado que está React en ese ecosistema, también están en todas partes (de hecho, React usa promesas internamente).

Las promesas lo ayudan a administrar el código asincrónico y se devuelven desde muchas API DOM y librerias de terceros. La sintaxis `async/await` es una sintaxis especial para tratar con promesas. Los dos van de la mano.

```js
function promises() {
  const successfulPromise = timeout(100).then(result => `success: ${result}`)

  const failingPromise = timeout(200, true).then(null, error =>
    Promise.reject(`failure: ${error}`),
  )

  const recoveredPromise = timeout(300, true).then(null, error =>
    Promise.resolve(`failed and recovered: ${error}`),
  )
  successfulPromise.then(log, logError)
  failingPromise.then(log, logError)
  recoveredPromise.then(log, logError)
}

function asyncAwaits() {
  async function successfulAsyncAwait() {
    const result = await timeout(100)
    return `success: ${result}`
  }

  async function failedAsyncAwait() {
    const result = await timeout(200, true)
    return `failed: ${result}`
  }

  async function recoveredAsyncAwait() {
    let result
    try {
      result = await timeout(300, true)
      return `failed: ${result}` // this would not be executed
    } catch (error) {
      return `failed and recovered: ${error}`
    }
  }

  successfulAsyncAwait().then(log, logError)
  failedAsyncAwait().then(log, logError)
  recoveredAsyncAwait().then(log, logError)
}

function log(...args) {
  console.log(...args)
}

function logError(...args) {
  console.error(...args)
}

// This is the mothership of all things asynchronous
function timeout(duration = 0, shouldReject = false) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (shouldReject) {
        reject(`rejected after ${duration}ms`)
      } else {
        resolve(`resolved after ${duration}ms`)
      }
    }, duration)
  })
}

// in React:
function GetGreetingForSubject({subject}) {
  const [isLoading, setIsLoading] = React.useState(false)
  const [error, setError] = React.useState(null)
  const [greeting, setGreeting] = React.useState(null)
  
  React.useEffect(() => {
    async function fetchGreeting() {
      try {
        const response = await window.fetch('https://example.com/api/greeting')
        const data = await response.json()
        setGreeting(data.greeting)
      } catch (error) {
        setError(error)
      } finally {
        setIsLoading(false)
      }
    }
    setIsLoading(true)
    fetchGreeting()
  }, [])

  return isLoading ? (
    'loading...'
  ) : error ? (
    'ERROR!'
  ) : greeting ? (
    <div>
      {greeting} {subject}
    </div>
  ) : null
}
```

[MDN: Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

[MDN: async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)

[MDN: await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await)

## Conclusion

Por supuesto, hay muchas funciones que son útiles al crear aplicaciones React, pero estas son algunas de mis favoritas que me encuentro usando una y otra vez. Espero que encuentres esto útil.

Si desea profundizar más en alguno de estos, tengo un taller de JavaScript que di y grabé mientras trabajaba en PayPal, que puede resultarle útil: [ES6 and Beyond Workshop at PayPal](https://www.youtube.com/playlist?list=PLV5CVI1eNcJgUA2ziIML3-7sMbS7utie5)

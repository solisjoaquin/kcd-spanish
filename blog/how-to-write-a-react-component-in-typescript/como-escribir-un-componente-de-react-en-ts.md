# Como escribir un componente de React en TypeScript

_Hay muchas formas de hacerlo, así es como recomiendo escribir componentes en React_

![Photo by Jonny Gios](https://kentcdodds.com/static/ad48b5f3e263a552955b2c9e98e98749/c6969/banner.webp)

Aquí está nuestro componente sin tipos:

```ts
const operations = {
  '+': (left, right) => left + right,
  '-': (left, right) => left - right,
  '*': (left, right) => left * right,
  '/': (left, right) => left / right,
}

function Calculator({left, operator, right}) {
  const result = operations[operator](left, right)

  return (
    <div>
      <code>
        {left} {operator} {right} = <output>{result}</output>
      </code>
    </div>
  )
}

const examples = (
  <>
    <Calculator left={1} operator="+" right={2} />
    <Calculator left={1} operator="-" right={2} />
    <Calculator left={1} operator="*" right={2} />
    <Calculator left={1} operator="/" right={2} />
  </>
)
``` 
Allí mismo puede notar que hacemos las cosas de manera un poco diferente. Quizás prefieras esto en su lugar:

```ts
const Calculator = ({left, operator, right}) => (
  <div>
    <code>
      {left} {operator} {right} ={' '}
      <output>{operations[operator](left, right)}</output>
    </code>
  </div>
)
``` 
No me gusta el retorno implícito allí. Significa que no puede declarar variables o usar hooks de manera razonable. Entonces, incluso para componentes simples, nunca sigo este enfoque.

Ok, tal vez hagas esto:

```ts
const Calculator = ({left, operator, right}) => {
  const result = operations[operator](left, right)
  return (
    <div>
      <code>
        {left} {operator} {right} = <output>{result}</output>
      </code>
    </div>
  )
}
``` 
Honestamente, eso está bien la mayor parte del tiempo. Personalmente, me gustan las características de hoisting de las declaraciones de función en lugar de expresiones de función como esa ([más información](https://kentcdodds.com/blog/function-forms)).

Muy bien, agreguemos algunos tipos a esto. Para las funciones, debe considerar los tipos que entran y los que salen. Comencemos con la entrada: props. Para comenzar, vayamos con props de tipo simple (lo mejoraremos más adelante):

```ts
type CalculatorProps = {
  left: number
  operator: string
  right: number
}
``` 
Con eso, probemos algunas opciones para aplicar ese tipo al objeto props en nuestro componente React.

Un método común para escribir un componente de React es usar uno de los genéricos que están integrados en `@types/react` (quiero decir, está integrado, ¿verdad? Entonces, ¿qué podría salir mal?). Curiosamente, no puede escribir una declaración de función de esta manera, por lo que tendremos que usar una expresión de función:

```ts
const Calculator: React.FC<CalculatorProps> = ({left, right, operator}) => {
  // La implementacion esta omitida por el momento
}
``` 
Esto funciona bastante bien, pero hay tres problemas principales con esto:

1. Nuestra función `Calculator` ahora acepta una `children` prop, aunque no hacemos nada con él 🙃 (Entonces, esto compila: `<Calculator left = {1} operator = "+" right = {2}> What? </Calculator>` ).

2. No puedes usar genéricos. No es muy común, pero definitivamente es una desventaja.

3. Tenemos que usar una expresión de función y no podemos usar una declaración de función.

De acuerdo, quizás el número 3 no sea un problema importante, pero el número 1 es bastante significativo. Hay algunos otros problemas menores establecidos en [este excelente GitHub issue](https://github.com/facebook/create-react-app/pull/8177) si desea profundizar (también consulte [la React TypeScript Cheatsheet](https://github.com/typescript-cheatsheets/react#function-components)). Basta decir que no use `React.FC` (o su alias más largo `React.FunctionComponent`).

Una de las cosas que me encantan de los componentes de React es que no son tan especiales. Aquí está la definición de un componente de React:

> Un componente de React es una función que devuelve algo que React puede representar.

Ahora, de acuerdo con `@types/react`, estamos limitados a `null` y `JSX.Elements`, pero React también puede representar cadenas, números y booleanos. En cualquier caso, debido a que un componente de React es simplemente una función que devuelve algo que React puede representar, escribirlo puede ser tan sencillo como escribir funciones. No tienes que hacer nada especial solo porque es React.

Así que así es como escribiría los accesorios para este componente:

```ts
function Calculator({left, operator, right}: CalculatorProps) {
  // La implementacion esta omitida por el momento
}
``` 

Esto no tiene ninguna de las deficiencias de `React.FC` y no es más complicado que escribir los argumentos en una función normal.

Ok, entonces ¿qué pasa con el valor de retorno? Bueno, podríamos escribirlo como `React.ReactElement` o incluso más ancho como `JSX.Element`. Pero, honestamente, me pongo del lado de mi amigo [Nick McCurdy](https://twitter.com/nickemccurdy) cuando [dice](https://twitter.com/nickemccurdy/status/1365384372908621833) que se pueden cometer errores fácilmente, lo que hace que el tipo de devolución sea demasiado amplio. Entonces, incluso fuera de un contexto de reacción, por defecto no especifico el tipo de retorno (confío en la inferencia) a menos que sea necesario. Y ese es el caso aquí.

## Mejorando el tipo `CalculatorProps` 

Bien, lo siguiente ahora no tiene mucho que ver con escribir componentes de React, pero pensé que lo encontraría interesante de todos modos, así que salte adelante si no lo hace. Mejoremos el tipo CalculatorProps. Como recordatorio, esto es lo que tenemos hasta ahora:

```ts
// I took the liberty of typing each of these functions as well:
const operations = {
  '+': (left: number, right: number): number => left + right,
  '-': (left: number, right: number): number => left - right,
  '*': (left: number, right: number): number => left * right,
  '/': (left: number, right: number): number => left / right,
}

type CalculatorProps = {
  left: number
  operator: string
  right: number
}

function Calculator({left, operator, right}: CalculatorProps) {
  const result = operations[operator](left, right)

  return (
    <div>
      <code>
        {left} {operator} {right} = <output>{result}</output>
      </code>
    </div>
  )
}
``` 

Creo que los tipos `left`  y `right` están bien. Es el operador con el que no estoy satisfecho. El uso de una `string` es demasiado ancho. Hay operaciones específicas que están permitidas. Por ejemplo, qué pasaría si intentáramos:

```ts
const element = <Calculator left={1} operator="wut" right={2} />
``` 

Eso es lo que llamamos un runtime exception, amigos. Es decir ... a menos que tenga el modo estricto activado, en cuyo caso tendrá un error de compilación en las `operations[operator]`. En modo estricto, TypeScript sabrá correctamente que acceder a cualquier cadena desde el objeto de `operations` no _necesariamente_ devolverá una función invocable.

Hay muchas formas de resolver este problema. Básicamente, queremos limitar el operador a solo los operadores admitidos. Podemos hacer eso con un tipo de unión simple:

```ts
type CalculatorProps = {
  left: number
  operator: '+' | '-' | '*' | '/'
  right: number
}
``` 
Pero si decidimos agregar el [Operador de exponenciación](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Exponentiation) (**), entonces tendríamos que actualizar no solo el objeto de operaciones, sino también el tipo de operador, lo cual sería molesto. ¿Quizás haya una forma de derivar el tipo para el operador en función del objeto de operaciones? ¡Sí, la hay!

```ts
type CalculatorProps = {
  left: number
  operator: keyof typeof operations
  right: number
}
``` 

`typeof operatios` nos va a dar un tipo que describe el objeto de `operations`, que es aproximadamente igual a:

```ts
type operations = {
  '+': (left: number, right: number) => number
  '-': (left: number, right: number) => number
  '*': (left: number, right: number) => number
  '/': (left: number, right: number) => number
}
``` 
La parte `keyof` tomará todas las claves de ese tipo, resultando en '+' | '-' | '*' | '/' 🎉

## Conclusión

Aquí está la versión terminada (también escribí las funciones de operaciones):
```ts
const operations = {
  '+': (left: number, right: number): number => left + right,
  '-': (left: number, right: number): number => left - right,
  '*': (left: number, right: number): number => left * right,
  '/': (left: number, right: number): number => left / right,
}

type CalculatorProps = {
  left: number
  operator: keyof typeof operations
  right: number
}

function Calculator({left, operator, right}: CalculatorProps) {
  const result = operations[operator](left, right)
  return (
    <div>
      <code>
        {left} {operator} {right} = <output>{result}</output>
      </code>
    </div>
  )
}

const examples = (
  <>
    <Calculator left={1} operator="+" right={2} />
    <Calculator left={1} operator="-" right={2} />
    <Calculator left={1} operator="*" right={2} />
    <Calculator left={1} operator="/" right={2} />
  </>
)
``` 

Espero que eso le dé una idea de una buena manera de escribir sus componentes de React. ¡Buena suerte y cuidate!

PD Una cosa que no me gusta en absoluto de nuestra solución es que tenemos que escribir cada una de las funciones de operaciones. Curiosamente, esto es un poco como una madriguera de conejo, pero en el otro extremo, los tipos son definitivamente mejores y aprendes algunos trucos en el camino. Originalmente, eso era parte de esta publicación de blog, pero decidí moverlo a su propia publicación. Lea todo sobre esto aquí: [How to write a Constrained Identity Function (CIF) in TypeScript](https://kentcdodds.com/blog/how-to-write-a-constrained-identity-function-in-typescript).

# Sintaxis de funciones en Typescript

### La sintaxis de varias funciones y tipos de funciones en TypeScript con ejemplos simples.

En JavaScript en sí, hay muchas formas de escribir funciones. Agrega TypeScript a la mezcla y, de repente, hay mucho en qué pensar. Entonces, con la ayuda de algunos amigos, he reunido esta lista de varias formas de funciones que normalmente necesitarás / encontrarás con ejemplos simples.

Tenga en cuenta que hay TONELADAS de combinaciones de diferentes sintaxis. Solo incluyo aquellas que son combinaciones menos obvias o únicas de alguna manera.

Primero, la mayor confusión que siempre tengo con la sintaxis de las cosas es dónde poner el tipo de retorno. ¿Cuándo uso `:` y cuándo `=>`?. Aquí hay algunos ejemplos rápidos que pueden ayudarlo a acelerar si está usando esta publicación como referencia rápida:

```tsx
// Simple type for a function, use =>
type FnType = (arg: ArgType) => ReturnType

// Every other time, use :
type FnAsObjType = {
  (arg: ArgType): ReturnType
}
interface InterfaceWithFn {
  fn(arg: ArgType): ReturnType
}

const fnImplementation = (arg: ArgType): ReturnType => {
  /* implementation */
}
```

Creo que esa fue la mayor fuente de confusión para mí. Habiendo escrito esto, ahora sé que la única vez que uso `=> ​​ReturnType` es cuando estoy definiendo un tipo de función como un tipo en sí mismo. En cualquier otro momento, uso `: ReturnType`.

Continua leyendo para ver un montón de ejemplos de cómo se desarrolla esto en ejemplos de código típicos.

## Declaracion de funciones

```tsx
// inferred return type
function sum(a: number, b: number) {
  return a + b
}
```

```tsx
// defined return type
function sum(a: number, b: number): number {
  return a + b
}
```

En los ejemplos siguientes, usaremos tipos de retorno explícitos, pero técnicamente no es necesario que lo especifiques.

## Expresion de una funcion

```ts
// named function expression
const sum = function sum(a: number, b: number): number {
  return a + b
}
```

```ts
// annonymous function expression
const sum = function (a: number, b: number): number {
  return a + b
}
```

```ts
// annonymous function expression
const sum = function (a: number, b: number): number {
  return a + b
}
```

```ts
// arrow function
const sum = (a: number, b: number): number => {
  return a + b
}
```

```ts
// implicit return
const sum = (a: number, b: number): number => a + b
```

```ts
// implicit return of an object requires parentheses to disambiguate the curly braces
const sum = (a: number, b: number): {result: number} => ({result: a + b})
```
También puede agregar una anotación del tipo junto a la variable, y luego la función misma asumirá esos tipos:

```ts
const sum: (a: number, b: number) => number = (a, b) => a + b
```
Y puedes tambien extraer ese tipo

```ts
type MathFn = (a: number, b: number) => number
const sum: MathFn = (a, b) => a + b
```

O tambien puedes usar la sintaxis de tipo objeto

```ts
type MathFn = {
  (a: number, b: number): number
}
const sum: MathFn = (a, b) => a + b
```
Lo cual puede ser útil si desea agregar una propiedad escrita a la función:

```ts
type MathFn = {
  (a: number, b: number): number
  operator: string
}
const sum: MathFn = (a, b) => a + b
sum.operator = '+'
```
Esto tambien puede hacerce con una interfaz

```ts
interface MathFn {
  (a: number, b: number): number
  operator: string
}
const sum: MathFn = (a, b) => a + b
sum.operator = '+'
```
Y luego está `declare function` y `declare namespace` que pretenden decir: "Oye, existe una variable con este nombre y tipo". Podemos usar eso para crear el tipo y luego usar `typeof` para asignar ese tipo a nuestra función. A menudo encontrará que `declare` se usa en archivos `.d.ts` para declarar tipos para libreria.

```ts
declare function MathFn(a: number, b: number): number
declare namespace MathFn {
  let operator: '+'
}
const sum: typeof MathFn = (a, b) => a + b
sum.operator = '+'
```
Dada la opción entre `type`, `interface` y `declare funcion`, creo que prefiero `type` personalmente, a menos que necesite la extensibilidad que ofrece `interface`. Realmente solo usaría `declare` si realmente quisiera decirle al compilador sobre algo que aún no conoce (como una libreria).

## Parametros opcionales/por default

### Parametro opcional

```ts
const sum = (a: number, b?: number): number => a + (b ?? 0)
```

Tenga en cuenta que el orden importa aquí. Si hace que un parámetro sea opcional, todos los parámetros siguientes también deben ser opcionales. Esto se debe a que es posible llamar a sum (1) pero no es posible llamar a sum (, 2). Sin embargo, es posible llamar a sum (undefined, 2) y si eso es lo que desea habilitar, también puede hacerlo:

```ts
const sum = (a: number | undefined, b: number): number => (a ?? 0) + b
```
### Parametros por default

Cuando estaba escribiendo esto, pensé que sería inútil usar parámetros predeterminados sin hacer que ese parámetro fuera opcional, pero resulta que cuando tienes un valor predeterminado, TypeScript lo trata como un parámetro opcional. Entonces esto funciona:

```ts
const sum = (a: number, b: number = 0): number => a + b
sum(1) // results in 1
sum(2, undefined) // results in 2
```
Por lo que ese ejemplo es funcionalmente equivalente a:

```ts
const sum = (a: number, b: number | undefined = 0): number => a + b
```

Curiosamente, esto también significa que si desea que el primer argumento sea opcional pero que el segundo sea obligatorio, puede hacerlo sin usar `| undefined`:

```ts
const sum = (a: number = 0, b: number): number => a + b
sum(undefined, 3) // results in 3
```
Sin embargo, cuando extraiga el tipo, deberá agregar el `| undefined` manualmente, porque = 0 es una expresión de JavaScript, no un tipo.

```ts
type MathFn = (a: number | undefined, b: number) => number
const sum: MathFn = (a = 0, b) => a + b
```

### Parametros rest
Rest params es una característica de JavaScript que le permite recopilar el "resto" de los argumentos de una llamada de función en una matriz. Puede utilizarlos en cualquier posición de parámetro (primero, segundo, tercero, etc.). El único requisito es que sea el último parámetro
```ts
const sum = (a: number = 0, ...rest: Array<number>): number => {
  return rest.reduce((acc, n) => acc + n, a)
}
```
Y puedes extraer el tipo:

```ts
type MathFn = (a?: number, ...rest: Array<number>) => number
const sum: MathFn = (a = 0, ...rest) => rest.reduce((acc, n) => acc + n, a)
```
### Propiedades de los objetos y Metodos

Metodo objeto:

```ts
const math = {
  sum(a: number, b: number): number {
    return a + b
  },
}
```

Propiedad como expresión de función: 

```ts
const math = {
  sum: function sum(a: number, b: number): number {
    return a + b
  },
}
```
Propiedad como expresión de función flecha (con retorno implícito):

```ts
const math = {
  sum: (a: number, b: number): number => a + b,
}
```
Desafortunadamente, para extraer el tipo no puede escribir la función en sí, debe escribir el objeto adjunto. No puede anotar la función con un tipo por sí mismo cuando está definido dentro del objeto literal:

```ts
type MathFn = (a: number, b: number) => number

const math: {sum: MathFn} = {
  sum: (a, b) => a + b,
}
```

Además, si desea agregar una propiedad como algunos de los ejemplos anteriores, es imposible hacerlo dentro del objeto literal. Tienes que extraer la definición de la función por completo:

```ts
type MathFn = {
  (a: number, b: number): number
  operator: string
}

const sum: MathFn = (a, b) => a + b
sum.operator = '+'

const math = {sum}
```

Es posible que haya notado que este ejemplo es idéntico al ejemplo anterior con solo la adición de la `const math = {sum}`. Así que sí, no hay forma de hacer todo esto en línea con la declaración del objeto.

## Clases
Las clases en sí mismas son funciones, pero son especiales (deben invocarse con `new`), pero esta sección hablará sobre cómo se definen las funciones dentro del cuerpo de la clase.

Aquí hay un método normal, la forma más común de una función en el cuerpo de una clase:
```ts
class MathUtils {
  sum(a: number, b: number): number {
    return a + b
  }
}

const math = new MathUtils()
math.sum(1, 2)
```

También puede usar un campo de clase si desea que la función esté vinculada a la instancia específica de la clase:

```ts
class MathUtils {
  sum = (a: number, b: number): number => {
    return a + b
  }
}

// doing things this way this allows you to do this:
const math = new MathUtils()
const sum = math.sum
sum(1, 2)

// but it also comes at a cost that offsets any perf gains you get
// by going with a class over a regular object factor so...
```

Y luego, puede extraer estos tipos. Así es como se ve para la versión del método en el primer ejemplo:

```ts
interface MathUtilsInterface {
  sum(a: number, b: number): number
}

class MathUtils implements MathUtilsInterface {
  sum(a: number, b: number): number {
    return a + b
  }
}
```
Curiosamente, parece que todavía tiene que definir los tipos para la función, aunque son parte de la interfaz que se supone que debe implementar 🤔 🤷‍♂️

Una nota final. En TypeScript, también obtiene público, privado y protegido. Personalmente, no uso clases con tanta frecuencia y no me gusta usar esas características particulares de TypeScript. JavaScript pronto obtendrá una sintaxis especial para miembros privados que es genial ([más información](https://github.com/tc39/proposal-class-fields))

## Modulos
La importación y exportación de definiciones de funciones funciona de la misma manera que con cualquier otra cosa. Donde las cosas se vuelven únicas para TypeScript es si desea escribir un archivo `.d.ts` con una declaración de módulo. Tomemos nuestra función `sum`, por ejemplo:
```ts
const sum = (a: number, b: number): number => a + b
sum.operator = '+'
```
Esto es lo que haríamos asumiendo que lo exportamos como predeterminado:

```ts
declare const sum: {
  (a: number, b: number): number
  operator: string
}
export default sum
```
Y si queremos que sea una funcion llamada:

```ts
declare const sum: {
  (a: number, b: number): number
  operator: string
}
export {sum}
```
## Overloads
He escrito sobre esto especialmente y puede leer eso: [Define function overload types with TypeScript](https://kentcdodds.com/blog/define-function-overload-types-with-type-script). Aquí está el ejemplo de esa publicación:
```ts
type asyncSumCb = (result: number) => void
// define all valid function signatures
function asyncSum(a: number, b: number): Promise<number>
function asyncSum(a: number, b: number, cb: asyncSumCb): void

// define the actual implementation
// notice cb is optional
// also notice that the return type is inferred, but it could be specified
// as `void | Promise<number>`

function asyncSum(a: number, b: number, cb?: asyncSumCb) {
  const result = a + b
  if (cb) return cb(result)
  else return Promise.resolve(result)
}
```
Básicamente, lo que hace es definir la función varias veces y solo implementarla realmente la última vez. Es importante que los tipos para la implementación sean compatibles con todos los tipos de anulación, por lo que `cb` es opcional arriba`.

## Generators
Ni una sola vez he usado un generador en el código de producción ... Pero cuando jugué un poco con él en el campo de juego de TypeScript, no había mucho para el caso simple:
```ts
function* generator(start: number) {
  yield start + 1
  yield start + 2
}

var iterator = generator(0)
console.log(iterator.next()) // { value: 1, done: false }
console.log(iterator.next()) // { value: 2, done: false }
console.log(iterator.next()) // { value: undefined, done: true }
```
TypeScript infiere correctamente que `iterator.next()` devuelve un objeto con el siguiente tipo:

```ts
type IteratorNextType = {
  value: number | void
  done: boolean
}
```

Si desea seguridad de tipo para el valor de finalización de la expresión de rendimiento, agregue una anotación de tipo a la variable a la que lo asigna:

```ts
function* generator(start: number) {
  const newStart: number = yield start + 1
  yield newStart + 2
}

var iterator = generator(0)
console.log(iterator.next()) // { value: 1, done: false }
console.log(iterator.next(3)) // { value: 5, done: false }
console.log(iterator.next()) // { value: undefined, done: true }
```
Y ahora, si intentas llamar a `iterator.next('3')` en lugar de a `iterator.next(3)` obtendrás un error de compilación 🎉

## Async

Las funciones `async / await` en TypeScript funcionan exactamente igual que en JavaScript y la _única_ diferencia al escribirlas es que el tipo de retorno siempre será un `Promise` genérico.

```ts
const sum = async (a: number, b: number): Promise<number> => a + b
```
```ts
async function sum(a: number, b: number): Promise<number> {
  return a + b
}
```

## Generics

Con una declaracion de funcion:

```ts
function arrayify2<Type>(a: Type): Array<Type> {
  return [a]
}
```
Desafortunadamente, con una función flecha (cuando TypeScript está configurado para JSX), la apertura `<` de la función es ambigua para el compilador. "¿Es eso una sintaxis genérica? ¿O es JSX?" Entonces tienes que agregar algo para ayudarlo a eliminar la ambigüedad. Creo que lo más sencillo es hacer `extends unknown`:

```ts
const arrayify = <Type extends unknown>(a: Type): Array<Type> => [a]
```
Lo que nos muestra convenientemente la sintaxis de extensiones en genéricos, así que ahí lo tienes.

## Type Guards
Un protector de tipo (type guard) es un mecanismo para restringir el tipo (type narrowing). Por ejemplo, le permite restringir algo que sea `cadena | número` hasta una cadena o un número. Hay mecanismos incorporados para esto (como `typeof x === 'string'`), pero también puedes crear el tuyo propio. Aquí está uno de mis favoritos (aplauso para mi amigo Peter que originalmente me lo mostró):

```ts
// Array<number | undefined>
const arrayWithFalsyValues = [1, undefined, 0, 2]
```
En Javascript regular lo puedes asi:

```ts
// Array<number | undefined>
const arrayWithoutFalsyValues = arrayWithFalsyValues.filter(Boolean)
```

Desafortunadamente, TypeScript no considera que este sea un type narrowing guard, por lo que el tipo sigue siendo Array `<número | indefinido>` (no se aplica ninguna restricción).

Entonces podemos escribir nuestra propia función y decirle al compilador que devuelve `true / false` por si el argumento dado es de un tipo específico. Para nosotros, diremos que nuestra función devuelve `true` si el tipo de argumento dado no está incluido en uno de los tipos de valor falso (falsy value types).

```ts
type FalsyType = false | null | undefined | '' | 0
function typedBoolean<ValueType>(
  value: ValueType,
): value is Exclude<ValueType, FalsyType> {
  return Boolean(value)
}
```

Y con eso podemos hacer:
```ts
// Array<number>
const arrayWithoutFalsyValues = arrayWithFalsyValues.filter(typedBoolean)
```

Woo! 

## Assertion functions
¿Sabes que a veces verificas el tiempo de ejecución para estar más seguro de algo? Por ejemplo, cuando un objeto puede tener una propiedad con un valor o nulo, desea verificar si es nulo y tal vez arrojar un error si es nulo. Así es como puede hacer algo así:
```ts
type User = {
  name: string
  displayName: string | null
}

function logUserDisplayNameUpper(user: User) {
  if (!user.displayName) throw new Error('Oh no, user has no displayName')
  console.log(user.displayName.toUpperCase())
}
```

TypeScript está bien con `user.displayName.toUpperCase ()` porque la declaración if es un tipo de protección que comprende. Ahora, digamos que quiere tomar eso if check y ponerlo en una función:
```ts
type User = {
  name: string
  displayName: string | null
}

function assertDisplayName(user: User) {
  if (!user.displayName) throw new Error('Oh no, user has no displayName')
}

function logUserDisplayName(user: User) {
  assertDisplayName(user)
  console.log(user.displayName.toUpperCase())
}
```

Ahora, TypeScript ya no está contento porque la llamada a assertDisplayName no es una protección de tipo suficiente. Yo diría que esta es una limitación por parte de TypeScript. Oye, ninguna tecnología es perfecta. De todos modos, podemos ayudar un poco a TypeScript diciéndole que nuestra función hace una afirmación:

```ts
type User = {
  name: string
  displayName: string | null
}

function assertDisplayName(
  user: User,
): asserts user is User & {displayName: string} {
  if (!user.displayName) throw new Error('Oh no, user has no displayName')
}

function logUserDisplayName(user: User) {
  assertDisplayName(user)
  console.log(user.displayName.toUpperCase())
}
```

¡Y esa es otra forma de convertir nuestra función en una función de reducción de tipos!


## Conclusión

Eso definitivamente no es todo, pero esa es gran parte de la sintaxis común que me encuentro escribiendo cuando trato con funciones en TypeScript. ¡Espero que te haya sido de ayuda! Marque esto y compártalo con sus amigos
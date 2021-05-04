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


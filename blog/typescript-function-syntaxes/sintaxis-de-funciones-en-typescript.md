# Sintaxis de funciones en Typescript

### La sintaxis de varias funciones y tipos de funciones en TypeScript con ejemplos simples.

En JavaScript en sí, hay muchas formas de escribir funciones. Agrega TypeScript a la mezcla y, de repente, hay mucho en qué pensar. Entonces, con la ayuda de algunos amigos, he reunido esta lista de varias formas de funciones que normalmente necesitarás / encontrarás con ejemplos simples.

Tenga en cuenta que hay TONELADAS de combinaciones de diferentes sintaxis. Solo incluyo aquellas que son combinaciones menos obvias o únicas de alguna manera.

Primero, la mayor confusión que siempre tengo con la sintaxis de las cosas es dónde poner el tipo de retorno. ¿Cuándo uso ":" y cuándo "=>"?. Aquí hay algunos ejemplos rápidos que pueden ayudarlo a acelerar si está usando esta publicación como referencia rápida:

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

Creo que esa fue la mayor fuente de confusión para mí. Habiendo escrito esto, ahora sé que la única vez que uso **=> ​​ReturnType** es cuando estoy definiendo un tipo de función como un tipo en sí mismo. En cualquier otro momento, uso **: ReturnType**.

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


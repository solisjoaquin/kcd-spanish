# Errores comunes en testing
_Hoy hablemos de algunos errores comunes que la gente comete al testear aplicaciones JavaScript._
[link al post original](https://kentcdodds.com/blog/common-testing-mistakes)

![Photo by Jeremy Bishop on Unsplash](https://kentcdodds.com/static/d6c0c04e06b7423b8f70aad624ec2318/c6969/banner.webp)

## Error numero 0

Uno de los mayores errores que podría cometer sería perderse mi [curso completo de Testing JS](https://testingjavascript.com/). (¿Ves lo que hice ahí?)

## Error numero 1: Testing de detalles de implementacion (Testing Implementation Details)

Insisto mucho en esto ([leer más](https://kentcdodds.com/blog/testing-implementation-details)). Es porque es un gran problema en las pruebas y conduce a pruebas que no brindan tanta confianza como podrían. Aquí hay un ejemplo muy simple de una prueba que está testeando detalles de implementación:

```js
// counter.js
import * as React from 'react'

export class Counter extends React.Component {
  state = {count: 0}
  increment = () => this.setState(({count}) => ({count: count + 1}))
  render() {
    const {count} = this.state
    return <button onClick={this.increment}>{count}</button>
  }
}

// __tests__/counter.js
import * as React from 'react'
// (es dificil hacer tests de detalles de implementacion con React Testing Library
//  asi que usaré Enzyme en este ejemplo 😅)
import {mount} from 'enzyme'
import {Counter} from '../counter'

test('the increment method increments count', () => {
  const wrapper = mount(<Counter />)
  // no hagas esto:
  expect(wrapper.instance().state.count).toBe(0)
  wrapper.instance().increment()
  expect(wrapper.instance().state.count).toBe(1)
})
```

Entonces, ¿por qué esto es testing de implementación de detalles? ¿Por qué es tan malo testear los detalles de la implementación? Aquí hay dos verdades sobre las pruebas que se enfocan en detalles de implementación como la prueba mencionada arriba:

1.    Puedo romper el código y no el test (por ejemplo: podría cometer un error tipográfico en la asignación onClick de mi botón)

2.  Puedo refactorizar el código y romper el test (por ejemplo: podría cambiar el nombre del incremento a updateCount)

Este tipo de pruebas son las peores de mantener porque las actualizan constantemente (debido al punto # 2), y ni siquiera le dan una confianza sólida (debido al punto # 1).

En [mi curso](https://testingjavascript.com/) te mostraré la forma correcta de escribir pruebas y evitar este error común.

## Error numero 2: cubrir el 100% del codigo

Tratar de obtener una cobertura del 100% del código  para una aplicación es un error total y veo esto todo el tiempo. Curiosamente, normalmente he visto esto como un mandato de la administración, pero venga de donde venga, proviene de un malentendido de lo que un informe de cobertura de código puede y no puede decirle sobre la confianza que puede tener en su código base.

Qué le dice la cobertura del código:

* Este código se ejecutó cuando se ejecutaron sus tests.

Qué NO le dice la cobertura del código:

* Este código funcionará de acuerdo con los requisitos comerciales.

* Este código funciona con todos los demás códigos de la aplicación.

* La aplicación no puede entrar en mal estado.

Otro problema con los informes de cobertura de código es que cada línea de código cubierto agrega tanto al informe de cobertura general como cualquier otra línea. Lo que esto significa es que puede aumentar la cobertura de su código tanto agregando pruebas a su página "Acerca de nosotros" como agregando pruebas a su página "Checkout". Una de esas cosas es más importante que la otra, y la cobertura del código no puede brindarle información sobre eso para su base de código...

No existe una solución única para todos para obtener un buen número de cobertura de código. Las necesidades de cada aplicación son diferentes. Me preocupo menos por el número de cobertura del código y más por la confianza que tengo en que las partes importantes de mi solicitud están cubiertas. Utilizo el informe de cobertura de código para ayudarme después de haber identificado qué partes del código de mi aplicación son críticas. Me ayuda a saber si me faltan algunos casos extremos que cubre el código, pero mis pruebas no.

> Debo señalar que para los módulos de código abierto, optar por una cobertura de código del 100% es totalmente apropiado porque generalmente son mucho más fáciles de mantener al 100% (porque son más pequeños y más aislados) y son códigos realmente importantes debido a el hecho de que se comparten en varios proyectos.

Hablé un poco sobre esto en mi [livestream](https://youtu.be/O2tsvUJT09U?index=9&list=PLV5CVI1eNcJgCrPH_e6d57KRUTiDZgs0u&t=0s) el otro día, ¡compruébalo!

## Error numero 3: Repetir tests

Una de las mayores quejas que tiene la gente sobre las pruebas de extremo a extremo (E2E) es lo lentas y frágiles que son en comparación con las pruebas unitarias o de integración. No hay forma de que obtenga una sola prueba E2E tan rápida o confiable como una prueba unitaria. Simplemente nunca sucederá. Dicho esto, una sola prueba E2E le dará MUCHO más confianza que una sola prueba unitaria. De hecho, hay algunos rincones de confianza que son imposibles de sacar de las pruebas unitarias en las que las pruebas E2E son excelentes, por lo que definitivamente vale la pena tenerlas cerca.

Pero esto no significa que no podamos hacer que nuestras pruebas E2E sean más rápidas y confiables de lo que probablemente haya experimentado en el pasado. La repetición de pruebas es un error común que cometen las personas al escribir pruebas E2E que contribuyen al bajo rendimiento y confiabilidad.

[Las pruebas siempre deben funcionar de forma aislada](https://kentcdodds.com/blog/test-isolation-with-react). Eso significa que cada prueba debe ejecutarse como un usuario diferente. Entonces, cada prueba deberá registrarse e iniciar sesión como un nuevo usuario, ¿Correcto? Correcto. Por lo tanto, debe tener algunos objetos de página para las páginas de registro y de inicio de sesión porque estará revisando esas páginas en cada prueba, ¿verdad? ¡EQUIVOCADO! ¡Ese es el error!

Demos un paso atrás. ¿Por qué estás escribiendo tests? ¡Así puede enviar su aplicación con la confianza de que las cosas no se romperán! Digamos que tiene 100 pruebas que necesitan un usuario autenticado. ¿Cuántas veces necesita ejecutar el flujo de registro de "ruta feliz" para estar seguro de que el flujo funciona? ¿100 veces o 1 vez? Creo que es seguro decir que si funcionó una vez, debería funcionar siempre. Por eso, esas 99 carreras extra no te dan más confianza. **Eso es un esfuerzo inútil**.

Entonces, ¿qué haces en su lugar? Quiero decir, ya establecimos que sus pruebas deberían funcionar de forma aislada, por lo que no debería compartir un usuario entre ellas. Esto es lo que debe hacer: realice las mismas llamadas HTTP en sus pruebas que hace su aplicación cuando se registra e inicia sesión como un nuevo usuario. Esas solicitudes serán MUCHO más rápidas que hacer clic y escribir en la página y hay menos posibilidades de fallas de falsos negativos. Y mientras mantenga una prueba que realmente pruebe el flujo de registro / inicio de sesión, no ha perdido la confianza de que este flujo funciona.

## Conclusion

Recuerde siempre que la razón por la que está probando es la confianza. Si algo de lo que está haciendo su prueba no le brinda más confianza, entonces considere si puede dejar de hacerlo.

Buena suerte
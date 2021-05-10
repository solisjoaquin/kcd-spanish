---
slug: 'when-i-follow-tdd'
title: 'When I follow TDD'
date: '2020-06-29'
author: 'Kent C. Dodds'
description:
  "_Test-Driven Development doesn't always make sense, here's when it does for
  me._"
categories:
  - 'testing'
keywords:
  - 'testing'
  - 'javascript'
  - 'tdd'
  - 'test driven development'
banner: './images/banner.jpg'
bannerCredit: 'Photo by [Robin Vet](https://unsplash.com/photos/VU4y5JRD-zo)'
---


El desarrollo guiado por tests (TDD) es un proceso de tres pasos. A menudo se refiere a él como "ciclo rojo, verde, refactorización"

![TDD Cycle](./images/0.jpg)

Así es como funciona:

- 🚨 **Rojo**: Escribe un test para una función/módulo antes de que exista la función que estás añadiendo. Esto te proporciona un test que falla (obtienes un mensaje "rojo" de error). 
- ✅ **Green**: Implementa únicamente el código necesario para conseguir pasar el test (obtienes un mensaje "verde" de éxito).
- 🌀 **Refactor**: Revisa el código que has escrito y refactorízalo para asegurarte de que está bien escrito, así como legible, y bien diseñado. (Lo interesante de este paso es que ahora tendrás un test que te dirá si has roto algo durante la refactorización).
- 🔁 **Repite**: Es un ciclo, despues de todo continúa hasta que hayas implementado todo lo que necesites.

Hay un montón de matices sobre este enfoque y algunas personas pueden llegar a ser francamente estrictas sobre todo este asunto. Yo trato de seguir un enfoque práctico de TDD y sólo aplicarlo en situaciones donde siento que podría ser realmente beneficioso.

https://twitter.com/kentcdodds/status/1276673772251017216

Pero esta es la gran pregunta: "¿Cuándo tiene sentido usar TDD?" Es realmente una intuición que desarrollas y francamente tiene mucho que ver con tu comodidad y experiencia con TDD, pero aquí hay unos pocos ejemplos de situaciones donde yo sigo el ciclo rojo-verde-refactor de TDD.

## Arreglando un bug

Cuando tengo que arreglar un bug, _amo_ reproducir este bug con un test antes de arreglarlo. Haciendo esto me da una enorme cantidad de confianza para entender la causa del bug en primer lugar y cuando consigo que el test sea verde. Realmente he solucionado el bug y no solo he probado el problema.

Diría que sigo este enfoque el 90% del tiempo en el software sobre el que me importa (y por lo tanto para tener pruebas en él). Especialmente en mis librerías de código abierto.

[Aqui hay un ejemplo de un test de este tipo](https://github.com/testing-library/user-event/blob/e5db332c3f0ed3f6743d400f25b3cbf91a697f32/src/__tests__/type.js#L595-L601).

¿Arreglando un bug? Prueba TDD

## Funciones puras

No pruebo todas mis funciones de utilidad [puras](https://en.wikipedia.org/wiki/Pure_function) ([Cubro la mayoría con test de integración](/blog/write-tests)), pero si tengo una función de utilidad lo suficientemente complicada para necesitar pruebas unitarias aisladas, entonces esta es otra gran situación para la que es adecuada el TDD. Con este tipo de funciones, a menudo tu tienes un buena cantidad de entradas y salidas basadas en los requisitos que tienes para el código.

Creo que la mayoría de nosotros hemos experimentado situaciones como estas (y pronto lo harás si no lo has hecho aún). Cuando estuve en PayPal, necesitaba formatear la cantidad de un campo de entrada mientras el usuario escribía la cantidad de dinero que ellos querían enviar. La lógica para esto era asombrosamente más complicada de la que podrías imaginar gracias a la precisión de la moneda (algunas monedas no tienen un concepto de cantidad decimal). Formatear la cantidad de una moneda así fue la situación perfecta para TDD porque las posibles entradas y las salidas requeridas eran faciles de obtener.

Otro buen conjunto de ejemplos de esto (esto también es de código abierto), son [los tests para mi proyecto rtl-css-js](https://github.com/kentcdodds/rtl-css-js/blob/master/src/__tests__/index.js).

¿Escribir una función de utilidad pura? Prueba TDD

## Interfaces de usuario bien definidas

Solo desde que creé [Testing Library](https://testing-library.com) pensé que el TDD de las interfaces de usuario eran relamente viables en la web. Esto es porque:

**No tiene sentido hacer TDD cuando se hacen pruebas [implementation details](/blog/testing-implementation-details).**

Honestamente, no tiene sentido probar todo si estás probando detalles de implementación (sólo te retrasarán). Parte del objetivo de usar TDD es para ayudarte a pensar sobre lo que estás construyendo desde fuera, sin pensar en la implementación, de modo que cuando estes implementando las cosas no te pierdas en los detalles del código y puedas mantener el objetivo de alto nivel en mente. Te ayuda cuando solo sabes _qué_ estás construyendo, pero no _cómo_ lo vas a construir.

Las herramientas más populares antes de Testing Library (en todas sus vertientes), te permitían (y alentaban) a probar los detalles de implementación. Entonces, para usar TDD, requería que supieses (por ejemplo) que ibas a implementar un metodo privado llamado `makeDonation` y sería llamado con `amount` y `currency` (y no de cualquier otra forma). Por lo que el TDD siempre parecía una perdida de tiempo sin sentido. Sólo se trataba de una rutina.

Sin embargo, desde Testing Library te permite centrarte en la [experiencia de usuario](/blog/avoid-the-test-user), en lugar de en la implementación, y puedes seguir TDD cuando construyas interfaces de usuario que tengan un diseño y una experiencia de usuario bien definidas.

Por ejemplo,
[Aquí un vídeo que hice hace unos pocos años](https://www.youtube.com/watch?v=kCR3JAR7CHE) para demostrar esto con un componente de inicio de sesión. Tiene unos cuantos años, por lo que hay cosas que son mas fáciles hoy en día. Si estas buscando algo como esto, solo que más en profundida, entonces adquiere una licencia a [TestingJavaScript.com](https://testingjavascript.com) y puedes verme enseñarte TDD en vídeos de 8 minutos de alto valor por minuto (además de un montón de cosas más).

¿Construyendo una interfaz de usuario bien definida? Prueba TDD

## Conclusiones

Eso es todo por mi. Estoy seguro de que otras personas tienen situaciones válidas donde aplican las prácticas de TDD y eso está bien.

Si estoy simplemente haciendo algun exploración mientras codifico (algo que hago mucho) o estoy trasteando, entonces no me molestaré en seguir TDD y solo añadiré pruebas cuando esté satisfecho con la dirección que están cogiendo las cosas. Por cierto, este es el mismo enfoque que sigo cada vez que he usado un sistema de tipos (como Flow o TypeScript). Este es también el enfoque que sigo con [haciendo abstracciones](/blog/aha-programming).

Escribiendo tests, añadiendo tipos, y haciendo abstracciones para tu código son inversiones en lo que has construido. Hacer esas inversiones no tienen sentido si no estas convencido de que lo que estás construyendo va a existir a largo plazo. Esas inversiones pueden tambien ser desaconsejadas si no sabes con certeza que forma tendrá lo que estás construyendo para cuando hayas acabado. Y para ir más lejos, la falacia de los costes irrecuperables de esas inversiones puede influenciarte de manera que resulte en una solución subóptima.

¡Buena suerte!
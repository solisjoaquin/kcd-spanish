Desarrollar o comprar: Edición librerías de componentes
=========================================

[](https://kentcdodds.com/static/7ada1615181833135eadad3efd73ff3e/3e561/banner.jpg)
![](https://kentcdodds.com/static/7ada1615181833135eadad3efd73ff3e/d6099/banner.webp)
Foto por [George Bakos](https://unsplash.com/photos/VDAzcZyjun8)

*Algunas cosas que pensar antes de decidir crear tu propia librería de componentes.*

La última vez que iniciaste un nuevo proyecto de software, ¿escribiste primero tu propio lenguaje de programación? ¿Construiste tu computadora desde cero? Por supuesto que no. Eso sería ridículo. Sería una pérdida de tiempo (y en un negocio sostenible eso significa dinero). No es tu competencia principal. No es tu propuesta de valor. Te quedarías sin dinero antes de siquiera terminar.

Cuando comenzaste a trabajar en la página de preferencias de usuario de tu aplicación (o cualquiera que fuera la última característica que decidiste implementar), ¿usaste algo que ya existía? Es muy probable que tu base de datos de elección tenga una interfaz de usuario prediseñada para acciones CRUD simples. ¿Por qué no lo usaste? Probablemente porque tus clientes esperan un diseño y una experiencia profesional, moderna y consistentes en toda la aplicación; Y esa interfaz de usuario prediseñada quizás no podría hacer eso por tus clientes.


Estos son ejemplos de los extremos entre desarrollar en comparación a comprar en el mundo del software. Habrá un término medio entre esas dos líneas de pensamiento que es óptimo para el éxito de tu proyecto (y tu carrera/negocio).

El mundo de código abierto está lleno de librerías y frameworks increíbles que pueden ayudarnos a crear nuestro software y despacharlo a los usuarios de manera rápida. librerías como [ReachUI](https://reach.tech/), [MaterialUI](https://material-ui.com/),
e incluso algunas librerías de componentes creadas por corporaciones, como por ejemplo: [Adobe's React Spectrum](https://react-spectrum.adobe.com/) la cual no solo es madura, sino que ha sido testeada extensamente (e incluso también, ha sido probada en temas de accesibilidad). Es alentador que en el espacio de la UI, incluso hay opciones de pago que están disponibles (por ejemplo, [TailwindUI](https://tailwindui.com/) y [Remix](https://remix.run/)). 


Para muchas de las cosas en las que te verás involucrado como desarrollador de UI, ya existen soluciones para varios de los problemas que enfrentarás.

Lo que me encanta de esto es que significa que hay menos cosas en las que tengo que dedicar mi tiempo y que no son mi competencia principal como desarrollador. Así como sería ridículo para mí desarrollar mi propio lenguaje de programación, sería igual de tonto para mí desarrollar mi propia implementación de ventana modal cuando ya existen unas implementaciones bastante buenas.

Ya puedo imaginarme a algunos de ustedes quejándose, así que permítanme tocar el tema más difícil. A veces, encontrarás que simplemente no te gusta la forma en que se implementó un componente y en ese caso estarás haciendo todo lo posible para adaptar el caso de uso de ese componente a tu API. Sugeriría que cuando estés tratando con una solución madura y establecida para el tipo de UI que estás tratando de desarrollar, hagas una pausa por un momento y consideres si lo que te molesta de la implementación es realmente un problema legítimo (como por ejemplo problemas de rendimiento y/o accesibilidad), o si es solo una cuestión de falta de familiaridad. A menudo, podemos tener reacciones "instintivas" a las API que son diferentes a las que estamos acostumbrados y sería un error dejar que esas primeras impresiones controlen nuestra decisión de si adoptamos lo nuevo o no...(se me viene a la mente React + JSX).

Ten en cuenta que no estoy diciendo que nunca debas crear una libreria de componentes para tu empresa. La mayoría de las empresas *deberían* hacerlo (¿de dónde crees que provienen la mayoría de las soluciones existentes?). Pero, por el amor de Dios, si estás pensando en desarrollar tu propio acordeón de pestañas o tu propio "combobox", *por favor* reconsidera. Quizás no es trivial que estos componentes queden *perfectos*. Personalmente, culpo a la plataforma web por este problema (las versiones "estilizables" de estos componentes comunes deberían venir integradas en la plataforma), pero eso es irrelevante para esta discusión. Encuentra una versión madura y extensamente testeada de este tipo de componentes y utilízala. Tu empresa no es tan única como crees.

Los tipos de componentes que *deberían* incluirse en la libreria de componentes de tu empresa, son los que envuelven los componentes de un nivel inferior para los casos de uso comunes en tu aplicación. Y no, no estoy diciendo: "haz un *wraper*, y luego puedes cambiar la implementación" (esto rara vez funciona en la práctica). Lo que estoy diciendo es que tomes las capacidades de los componentes que has elegido y limita lo que las personas pueden hacer para promover la coherencia en tú UI y tú base de código tanto como sea práctico. Además, probablemente hay elementos de la interfaz de usuario en tu aplicación que son bastante exclusivos de tu aplicación, pero son una composición de varios otros componentes de nivel inferior. Estos también son buenos candidatos para una libreria de componentes propia.


Así que, por supuesto que puedes tener una libreria de componentes que incluya cosas como botones, diseño, tipografía, elementos de formulario, etc. Pero no tienes que desarrollar cada una de estas cosas desde cero. El otro día, vi un componente de botón con *miles* de líneas de código. A lo que me refiero es que, estas cosas pueden volverse sorprendentemente complejas si las dejas, pero por el amor de Dios, concéntrate en tu negocio.

Sé que puede ser muy divertido desarrollar todo ti mismo. Cuando estaba en PayPal, trabajé en una libreria de componentes de React y construí un botón desde cero (pero también use algunas cosas open source para otros componentes). Así que he estado ahí. Pero no todas las empresas tienen los recursos para dedicar uno o dos ingenieros únicamente a la creación de componentes UI. En algún momento, debes poner esos componentes en algo útil para las personas que pagan las facturas. Y esas personas no pagan por el sitio de documentación de la libreria de componentes de uso interno (incluso si *tiene* ejemplos de código ejecutables en el navegador).

Realmente no quiero que parezca que tener una libreria de componentes de algún tipo es una pérdida de tiempo porque no lo es. Solo tienes que equilibrar tu entusiasmo por desarrollar la abstracción perfecta para un `<Divider />` con la practicidad y la sostenibilidad de tu negocio. Ten en cuenta la competencia central de tu negocio y no optes por la opción de "desarrollar" solo porque es un desafío técnico divertido, sino porque es realmente necesario para que tu negocio tenga éxito.

Cualquiera que sea la combinación entre desarrollar y comprar que elijas, te deseo la mejor suerte. 👍

[2021-02-04](https://github.com/kentcdodds/kentcdodds.com/commits/main/content/blog/build-vs-buy-component-libraries-edition/index.mdx)

traducido por: @dani1995ar
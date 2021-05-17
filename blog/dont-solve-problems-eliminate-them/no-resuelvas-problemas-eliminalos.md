No resuelvas problemas, elimínalos
====================================

![Software Engineer, React Training, Testing JavaScript Training](https://res.cloudinary.com/kentcdodds-com/image/upload/v1620771700/kentcdodds.com/blog/don-t-solve-problems-eliminate-them/banner_qzwcgj.jpg)

Foto por [Jordan Whitt](https://unsplash.com/photos/EerxztHCjM8)

*Como eliminar problemas puede simplificar drásticamente tus bases de código y tu vida*

Los seres humanos somos solucionadores de problemas por naturaleza. El hecho de que hayamos sobrevivido tanto tiempo como especie lo comprueba.

Los seres humanos también somos buscadores de problemas naturales. piénsalo por un momento...Y no estoy hablando de *"los otros"*. Estoy hablando de ti y de mí también. Es difícil y se necesita hacer un esfuerzo consciente para evitarlo. Pasamos tanto tiempo resolviendo problemas, que naturalmente buscamos problemas para resolver, incluso si no tenemos problemas en este momento. 

![Photo of a Violin by Providence Doucet](https://res.cloudinary.com/kentcdodds-com/image/upload/f_auto,q_auto,dpr_2.0/v1620774892/kentcdodds.com/blog/don-t-solve-problems-eliminate-them/violin_pdtl8b.jpg)

Por ejemplo, una de mis hermanas me pregunto si podía ayudarla a crear una aplicación que combinara las capacidades de Zoom, Tito y Google Calendar para permitir que los músicos sin trabajo (debido a la pandemia) pudieran enseñar sus habilidades de manera remota. Ella estaba buscando problemas para resolver antes de siquiera tener problemas.

En lugar de ayudarla a crear soluciones a problemas que aún no tenía, la animé a que simplemente *usara* Zoom, Tito y Google Calendar para hacer que esta idea despegara, y luego, en el momento que estas herramientas se quedaran cortas, esto sería un problema para el cual estaría mejor preparada para resolver, ya que tendría experiencia real con el problema y, por lo tanto, tendría más contexto para resolverlo.

Al final, mi hermana decidió no seguir con su idea. Es bueno que no haya decidido resolver los problemas que no tenía antes de decidirse a dejar la idea. Ojalá pudiera decir que nunca he cometido ese error. ¿Cuántas veces he escrito una prueba para una pieza de código que al final terminé eliminando si quiera antes de hacerle *"commit"*? 🤦‍♂️

**Evitar problemas es mejor que resolverlos.** No intentes resolver problemas que aún no tienes.Y con eseto no estoy diciendo que no deberias de planear con anticipación. Puedes evitar resolver problemas que no tienes sin tener que arrinconarte a ti mismo en una esquina.


Problemas inevitables
------------------------------------------------------------------------------------------------------------
Aunque evitar un problema es lo mejor, a veces esto no es posible. ¿Y entonces que hacemos en este caso?

Los humanos **deberían** ser eliminadores de problemas. Esto no es natural y requiere un esfuerzo adicional. Cuando nos enfrentamos a un problema, los humanos naturalmente comienzamos a pensar en soluciones al problema. Y cuando lo resolvemos, nos sentimos bien con nosotros mismos, pero sin darnos cuenta nos hemos hecho **cautivos del mantenimiento de nuestra solución** ⛓

Sin embargo, si alguien puede dar un paso hacia atrás y eliminar el problema en lugar de resolverlo, se encontrará en una excelente posición, liberado para entonces concentrarse en tareas distintas de mantener las soluciones. Y, a menudo, los problemas también se eliminan para las personas que utilizan lo estos eliminadores de problemas producen.

A continuación consideremos algunos ejemplos:

Eliminación de problemas en la vida real
------------------------------------------------------------------------------------------------------------------------------

[![Tesla Model S driving fast with mountains in the background](https://res.cloudinary.com/kentcdodds-com/image/upload/f_auto,q_auto,dpr_2.0/v1620774548/kentcdodds.com/blog/don-t-solve-problems-eliminate-them/tesla_model_s_mbupt9.jpg)](https://tesla.com/s)

Tesla es un buen ejemplo de esto. Al ser 100% electricos han logrado eliminar un sinfin de partes y procesos que habian sido standard en la industria durante decadas. Esto los ha liberado para ellos entonces poder concentrarse en su enfoque alternativo.

Como dueño de un carro eléctrico, haber cambiado de motor de combustión interna a un motor eléctrico me ha permitido eliminar problemas como "¿dónde le realizo el cambio de aceite a mi motor?", o preocupaciones de que quizás la trasmisión se va a estropear, las pastas de freno requieren cambio, y un largo etcétera. (Esto se debe a que los carros eléctricos requieren menos mantenimiento debido a que tienen una cantidad inferior de partes comparados con los carros tradicionales de combustión interna)

[![Screenshot of a tesla livestream showing the model y giga casting machine with the words "40% rear underbody cost savings" and "-79 parts per car"](https://res.cloudinary.com/kentcdodds-com/image/upload/f_auto,q_auto,dpr_2.0/v1620835374/kentcdodds.com/blog/don-t-solve-problems-eliminate-them/giga_casting_dymoig.png)](https://youtu.be/l6T9xIeZTds?t=4767) 
(40% de ahorro en costos en el cuerpo inferior) | (79 partes menos por carro)

Una de las innovaciones más recientes de Tesla es el uso de la "Gigapress (la gigantoprensa)" la cual les permite forjar enteramente la parte trasera o delantera del vehículo a partir de una sola pieza 
(en los carros tradicionales esto se hace en diferentes secciones y requiere muchas piezas). Este proceso elimina la necesidad de tener docenas de robots que estén atornillando y soldando las piezas unas a otras.

Tesla es un fantástico ejemplo de eliminación de problemas. Un caso para estudiar para cualquier persona que esté interesada en la manufactura a gran escala. La eliminación de problemas es un factor decisivo de gran éxito.

Programando eliminación de problemas
------------------------------------------------------------------------------------------------------------------------

La mayoría de los que están leyendo esto probablemente no manufacturamos a gran escala. Probablemente tú desarrolles aplicaciones. Entonces ¿cuáles son algunos de los ejemplos de eliminación de problemas relacionados con la programación? 

[![React logo](https://res.cloudinary.com/kentcdodds-com/image/upload/f_auto,q_auto,dpr_2.0/v1620775101/kentcdodds.com/blog/don-t-solve-problems-eliminate-them/react_nlj9aq.png)](https://reactjs.org/)

Hace algunos años, para poder crear un componente en React, necesitábamos crear una clase que `"extiende React.Component"`. Agregaríamos métodos para diferentes eventos del ciclo de vida que quisiéramos manejar.Esto funcionó bien durante algunos años, pero un gran problema con esto era la reutilización del código. Una "preocupacion" (o característica) podia tener codigo distribuido en cualquiera o todos los `constructores`, `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`, y `render`. Crear abstracciones reutilizables en cada uno de estos "ciclos de vida" era todo un reto.

El equipo y la comunidad de React propusieron ideas como "Componentes de orden superior" y "Accesorios de renderizado" para resolver estos problemas. Durante mucho tiempo, esto pareció una solución bastante buena. Hubo algunas "asperezas" (problemas de "nesting" y jerarquías falsas con accesorios de renderizado o soporte de escritura terrible y direccionamiento indirecto / choques de accesorios para los HOCs), pero, como comunidad nos habíamos acostumbrado a estos problemas y la solución funcionaba bastante bien.

Luego, el equipo de React cambió el juego por completo e introdujo "hooks" (ganchos). Con los "hooks", la reutilización del código es trivial y obvia. Compartes código con los hooks de React de la misma manera que compartes código en JavaScript vainilla: crea una función. Eliminaron por completo el problema, ya no sentimos la frustración que nos llevó a los HOCs o los accesorios de renderizado, excepto en escenarios muy específicos.

Otro pequeño ejemplo: al principio de React, la única forma oficialmente admitida de obtener "estado" y las funciones de un lugar a otro en React era pasar accesorios. Esto llevó a una "perforación de accesorios" en la que tienes que canalizar accesorios a través de componentes en toda tu aplicación. Esto era un gran dolor. Había una nota en los documentos sobre una API de "contexto" que existía, pero se desaconsejaba directamente en los documentos.

Luego, redux entró en escena y resolvió la perforación de accesorios (entre otras cosas) y la gente se cambio a redux rápidamente. Redux en realidad *usó* la API de "contexto", pero debido a que estaba oculta detrás de una biblioteca, a la gente no le preocupaba la advertencia en los documentos (la mayoría ni siquiera sabía que estaban usando la API de "contexto" indirectamente).

Sin embargo, cuando el "contexto" se volvió oficial, y cuando los "hooks" lo hicieron mucho más fácil de usar, muchas personas descubrieron que el problema principal para el cual estaban usando redux (obtener el "estado" en diferentes partes de su aplicación) se había eliminado con un enfoque integrado, y eliminó redux a favor del nuevo enfoque.

(Para ser claros, hay otras razones por las que las personas usan redux, pero antes de que el "contexto" fuera oficial, esta fue la principal razon que llevó a las personas a usar redux).

[![Remix logo](https://res.cloudinary.com/kentcdodds-com/image/upload/f_auto,q_auto,dpr_2.0/v1620776599/kentcdodds.com/blog/don-t-solve-problems-eliminate-them/remix-on-light_har5s6.png)](https://remix.run/)

Remix es otro gran ejemplo de una eliminación de problemas. Han adoptado un enfoque completamente diferente para crear aplicaciones con React y han eliminado un montón de problemas en el proceso.

Las personas que vienen de otros metaframeworks se enamoran rápidamente del soporte integrado para el enrutamiento "anidado" (nested). Entre otras cosas, esto elimina el problema de los componentes de diseño compartidos. Si conoces la frustración, entiendes lo que quiero decir. Si no lo haces ... que suerte la que tienes.

Debido a que Remix expone una API directa a los encabezados de la caché de respuesta, puede tener todos los beneficios principales de los generadores de sitios estáticos sin necesidad de realizar reconstrucciones incrementales "inteligentes" (que es una solución enormemente compleja para un problema real que enfrenta el enfoque SSG).

Debido a la forma en que Remix te permite cargar sus datos en una función `loader` en el mismo archivo que tu componente, se elimina el problema de la obtención de datos en exceso (simplemente filtras lo que no necesita en el` loader` así que solo envías lo que se necesita por cable) y se elimina un gran problema que lleva a las personas a clientes graphql (para ser claros, Remix funciona con graphql, simplemente no tiene que usar un cliente graphql complejo del lado del cliente con Remix para evitar más de buscar). Remix también solo recupera los datos de los * diseños cambiados * en una transición de página (algo que realmente solo puede hacer con el enrutamiento anidado), lo que elimina aún más el problema de búsqueda excesiva.


Because of the way Remix allows you to load your data in a `loader` function in the same file as your component, the problem of data over fetching is eliminated (you just filter out what you don't need in the `loader` so you only send what's needed over the wire) and a big problem that drives people to graphql clients is eliminated (to be clear, Remix works with graphql, you just don't have to use a complex client-side graphql client with Remix to avoid over fetching). Remix also only fetches the data for the *changed layouts* on a page transition (something you can only really do with nested routing), further eliminating the over fetching problem.

Because Remix supports `<form>` directly, you don't have to worry about the song-and-dance of form state management and submission. And to get the same benefits with client-side routing, it exposes a `<Form>` component that emulates the same experience without a full-page refresh.

Because Remix automatically re-calls your loaders on mutations, you don't need to worry about cache invalidation.

Because Remix allows you to specify the `link` tags included on a route-by-route basis, you don't need to worry about changes of CSS on one page impacting those on another page. That problem has been completely eliminated and now maybe you'll think twice before reaching to a CSS-in-JS library to solve that problem. Because it just doesn't exist when using Remix.

Because Remix is a progressive-enhancement focused framework, you don't need to worry about whether your app will work on an unreliable network where the JS fails to load for some reason.

Because Remix is built on top of web-based APIs primarily, they've eliminated over half of the documentation they would otherwise need to write because they can just point you to [MDN](https://developer.mozilla.org/). And they've eliminated the problem of transferrable skills for us as users because the better we get at Remix, the better we get at building websites without it too.

[](https://kentcdodds.com/blog/don-t-solve-problems-eliminate-them#trade-offs)Trade-offs
----------------------------------------------------------------------------------------

By now you've probably had this thought at least once: "But Kent... They may have eliminated some problems, but they introduced some new ones!" Yes, this is what we call trade-offs and they're impossible to avoid. Even inaction (the most efficient problem elimination technique) has trade-offs.

EVs may not have the maintenance headaches of traditional ICE vehicles, but they also don't charge as quickly as you can gas up a traditional car and you can't just carry a gas can around with you just in case.

React hooks drastically simplified code reuse, but now you've got to learn about value identity and memoization is when building those abstractions (though, often [by putting things inside the `useEffect`](https://epicreact.dev/memoization-and-react/), we can eliminate that problem).

The ultimate goal is that the new problems you have to face are easier/cheaper to solve than the ones you had before.

**Eliminate big problems in exchange for smaller problems.**

[](https://kentcdodds.com/blog/don-t-solve-problems-eliminate-them#conclusion)Conclusion
----------------------------------------------------------------------------------------

There are countless examples of problem elimination throughout history and in every industry that have taken our world to new heights.

I want to encourage us all to embrace the problem solving of humanity. I also want us to be mindful, take a step back, and ask ourselves whether we're solving the right problems. Are we just solving problems we created from the solution to other problems? Is it possible to eliminate those first problems so we don't have to solve the problems our solution created?

**Start by not seeking problems. If you really do have a problem, first try to eliminate it if you can, and only solve it if you're sure you can't.**

The biggest challenge is making sure that our elimination of problems don't create bigger problems. But when you can do that, you can drastically improve things for yourself and everyone who enjoys what you've created as well. Take chances, make mistakes, and eliminate problems!

[2021-05-11](https://github.com/kentcdodds/kentcdodds.com/commits/main/content/blog/don-t-solve-problems-eliminate-them/index.mdx)
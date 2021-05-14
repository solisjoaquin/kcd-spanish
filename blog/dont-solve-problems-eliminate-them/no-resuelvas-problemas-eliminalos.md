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

And as an EV owner, switching from gas to electric allows me to eliminate problems like "where do I get an oil change" or worries that the transmission will blow or that I'll need new break pads, etc etc etc. (EVs require very little maintenance because there are just so fewer parts that can wear out and break).

[![Screenshot of a tesla livestream showing the model y giga casting machine with the words "40% rear underbody cost savings" and "-79 parts per car"](https://res.cloudinary.com/kentcdodds-com/image/upload/f_auto,q_auto,dpr_2.0/v1620835374/kentcdodds.com/blog/don-t-solve-problems-eliminate-them/giga_casting_dymoig.png)](https://youtu.be/l6T9xIeZTds?t=4767)

A more recent innovation of Tesla is the use of the "Gigapress" which allows them to make a single-piece casting of the entire back and front of the vehicle. This eliminates the need for dozens of robots to bolt and weld dozens of parts together.

Tesla is a fantastic example of problem elimination. Very interesting case study for anyone interested in manufacturing at a huge scale. Problem elimination is key to their success.

[](https://kentcdodds.com/blog/don-t-solve-problems-eliminate-them#coding-problem-elimination)Coding problem elimination
------------------------------------------------------------------------------------------------------------------------

Most of you reading probably don't manufacture at scale. You're building apps. So what are some code-related examples of problem elimination?

[![React logo](https://res.cloudinary.com/kentcdodds-com/image/upload/f_auto,q_auto,dpr_2.0/v1620775101/kentcdodds.com/blog/don-t-solve-problems-eliminate-them/react_nlj9aq.png)](https://reactjs.org/)

Years ago, to create a React component, we created a class that `extends React.Component`. We would add methods for different lifecycle events we wanted to handle. This worked well for years, but a big sticking point was code reuse. A given "concern" (or feature) could have code spread across any or all of `constructor`, `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`, and `render`. Creating reusable abstractions that required code in each of those lifecycles was a challenge.

The React team and community came up with ideas like "Higher Order Components" and "Render Props" to solve these problems. For a long time this seemed like a pretty good solution. There were rough edges (nesting and false hierarchy issues with render props or terrible typing support and prop indirection/clashes for HOCs), but we'd pretty much gotten used to these problems as a community and the solution worked pretty well.

Then the React team changed the game entirely and introduced hooks. With hooks, code reuse is trivial and obvious. You share code with React hooks the same way you share regular JavaScript code: make a function. They completely eliminated the problem and we no longer feel the pain that led us to HOCs or render props except for very specific scenarios.

As another quick example: early in the React world, the only officially supported way to get state and functions from one place to another in React is to pass props. This led to "prop drilling" where you have to pipe props through components all over your app. This was a huge pain. There was a note in the docs about a "context" API that existed, but its use was strongly discouraged directly in the docs.

Then redux came on the scene and solved prop drilling (among other things) and people jumped on it quick. Redux actually *used* the context API, but because it was hidden behind a library people weren't worried about the warning in the docs (most didn't even know they were indirectly using context).

However, when context became official, and when hooks made it much easier to use, many people found that the primary problem for which they were using redux (getting state around their app) had been eliminated with a built-in approach, and dropped redux in favor of the new approach.

(To be clear, there are other reasons people use redux, but in days before official context, this was the primary pain that drove people to redux).

[![Remix logo](https://res.cloudinary.com/kentcdodds-com/image/upload/f_auto,q_auto,dpr_2.0/v1620776599/kentcdodds.com/blog/don-t-solve-problems-eliminate-them/remix-on-light_har5s6.png)](https://remix.run/)

Remix is another great example of a problem eliminator. They've taken a completely different approach to building applications with React and eliminated a bunch of problems in the process.

People coming from other metaframeworks very quickly fall in love with the built-in support for nested routing. Among other things, this eliminates the problem of shared layout components. If you know the frustration, you understand what I mean. If you don't... lucky you.

Because Remix exposes a direct API to the response cache headers, you can have all the primary benefits of static site generators with no need to do "intelligent" incremental rebuilds (which is an enormously complex solution to a real problem faced by the SSG approach).

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
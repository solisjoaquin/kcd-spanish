# introduccion super simple a React

La implementacion mas simple imaginable de React

```
<html>
  <body>
    <div id="root"></div>
    <script src="https://unpkg.com/react@16.13.1/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@16.13.1/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/@babel/standalone@7.8.3/babel.js"></script>
    <script type="text/babel">
      ReactDOM.render(<div>Hello World</div>, document.getElementById('root'))
    </script>
  </body>
</html>
```

Cuando estas aprendiendo algo nuevo (o quiere reforzar tu comprensión de algo con lo que ya está familiarizado), una de las cosas más valiosas que puede hacer es eliminar todo lo que sabe, hasta que todo lo que le quede sea lo único que estás tratando de aprender.

Cuando hablamos de crear aplicaciones, estamos juntando muchas abstracciones diferentes (herramientas y bibliotecas) para hacerlo. Cuando todo lo que quieres hacer es entregar el producto terminado, es natural ver todas esas cosas como una gran bola de gomas elásticas donde no sabes cuándo comienza una abstracción y termina la otra y, honestamente, no importa tanto porque todo lo que le importa es enviarlo terminado.

Pero si realmente desea obtener una base sólida y utilizar las abstracciones en su mayor potencial, entonces descubrirá que es mucho más eficaz si separa esas gomas elásticas y las explora de forma aislada. Conocerá sus capacidades y qué papel desempeñan en la aplicación general. De esa manera, cuando los use en el futuro, no intentará juntar dos piezas de una manera que no fue la intención, porque comprenderá cuáles son los casos de uso previstos.

Así que sigamos adelante e intentemos esto con React. Cuando creamos una aplicación en React, usamos un montón de herramientas juntas (tanto herramientas de desarrollo como bibliotecas que enviamos a producción). Si no sabes dónde React termina y dónde comienza Webpack, tampoco serás tan efectivo de como usarlos. Entonces, eliminemos todo y hagámoslo lo más simple posible: un archivo **index.html**.

El siguiente parrafo será básicamente una versión simple de lo que puedes ver en mi curso gratuito "Beginner's Guide to React" en Egghead. Para esta próxima parte, puede ver el video en este [link](https://egghead.io/lessons/react-create-a-user-interface-with-vanilla-javascript-and-dom?af=5236ad).

Comenzemos con este archivo HTML

```
<html>
  <body></body>
</html>
```

(Técnicamente, ni siquiera necesitas tanto porque el navegador es muy indulgente cuando se trata de este tipo de cosas y agregará las etiquetas html y body automáticamente. Pero mantengamos esas etiquetas).

Muy bien, crearemos nodos en el DOM usando JavaScript y los colocaremos en un contenedor o nodo llamado "root". Así que agreguemos eso:

```
<html>
  <body>
    <div id="root"></div>
  </body>
</html>
```

Le damos el ID al root para que sea más fácil encontrar ese nodo del DOM en nuestro JavaScript. Agreguemos eso a continuación:

```
<html>
  <body>
    <div id="root"></div>
    <script type="module">
      const rootElement = document.getElementById('root')
    </script>
  </body>
</html>
```

Genial, ahora que tenemos rootElement, creemos un elemento DOM para ponerlo dentro:

```
<html>
  <body>
    <div id="root"></div>
    <script type="module">
      const rootElement = document.getElementById('root')
      const element = document.createElement('div')
      element.textContent = 'Hello World'
      element.className = 'container'
      rootElement.append(element)
    </script>
  </body>
</html>
```

Ahora lo que verá en la página es "Hello World" que se renderizará dentro de un div dentro de root.


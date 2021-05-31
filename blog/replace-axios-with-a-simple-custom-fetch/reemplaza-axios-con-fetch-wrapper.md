# Reemplaza axios con un fetch wrapper

*Axios puede hacer un montón de cosas, pero aquí hay una solución más simple que puede manejar la mayoría de los casos de uso.*

![image](https://kentcdodds.com/static/8c6b5cbd59a615259e4f6e93151a7972/c6969/banner.webp)

Recuerdo estar con [Matt Zabriskie](https://twitter.com/mzabriskie) cuando se le ocurrió la idea de una versión de JavaScript vanila del servicio `$http` de AngularJS. Parecía una idea brillante y esa noche en su habitación de hotel en MidwestJS, armó la primera iteración.

Fue increíble porque trabajar con [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) sin procesar para realizar solicitudes HTTP no fue muy divertido. Su biblioteca, que más tarde llamó [`axios`](https://github.com/axios/axios), es un trabajo brillante y funcionaba tanto en NodeJS como en el navegador, por lo que recuerdo que estaba muy emocionado (y yo también).

Han pasado casi seis años y si está leyendo esto, es probable que al menos haya oído hablar de él y es muy probable que lo haya usado en el pasado o lo esté usando ahora. Tiene un número enorme y creciente de [descargas en npm](https://www.npmtrends.com/axios). Y aunque Matt dejó el proyecto hace mucho tiempo, todavía se mantiene activamente.

Desde su lanzamiento, el estándar del navegador ha evolucionado para agregar una nueva API basada en promesas para realizar solicitudes HTTP que brindan una experiencia de desarrollador mucho mejor. Esta API se llama [fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) y si aún no la ha utilizado, debería comprobarla. Es ampliamente compatible y se puede rellenar fácilmente (mi favorito es [unfetch](https://github.com/developit/unfetch) porque la mascota del perro es linda 🐶).

Aquí hay algunas razones por las que podría considerar cambiar axios por un contenedor personalizado simple en torno a la recuperación:

* Menos API para aprender
* Tamaño más pequeño del bundle
* Problemas reducidos al actualizar paquetes / administrar cambios importantes
* Lanzamientos / correcciones de errores inmediatos
* Conceptualmente más simple

Tengo un fetch wrapper para mi [bookshelf app](https://github.com/kentcdodds/bookshelf) que me ha funcionado bien. Construyémoslo juntos:

```js
function client(endpoint, customConfig) {
  const config = {
    method: 'GET',
    ...customConfig,
  }

  return window
    .fetch(`${process.env.REACT_APP_API_URL}/${endpoint}`, config)
    .then(response => response.json())
}
```

Esta función de `client` me permite hacer llamadas a la API de mi aplicación así:

```js
client(`books?query=${encodeURIComponent(query)}`).then(
  data => {
    console.log('here are the books', data.books)
  },

  error => {
    console.error('oh no, an error happened', error)
  },
)
```

Sin embargo, la API `window.fetch` incorporada no maneja los errores de la misma manera que lo hace `axios`. De forma predeterminada, `window.fetch` solo rechazará una promesa si la solicitud real falló (error de red), no si devolvió una "Respuesta de error del cliente". Afortunadamente, el objeto `Response` tiene una propiedad [ok](https://developer.mozilla.org/en-US/docs/Web/API/Response/ok) que podemos usar para rechazar la promesa en nuestro contenedor:

```js
function client(endpoint, customConfig = {}) {
  const config = {
    method: 'GET',
    ...customConfig,
  }

  return window
    .fetch(`${process.env.REACT_APP_API_URL}/${endpoint}`, config)
    .then(async response => {
      if (response.ok) {
        return await response.json()
      } else {
        const errorMessage = await response.text()
        return Promise.reject(new Error(errorMessage))
      }
    })
}
```

Genial, ahora nuestra cadena de promesas se rechazará si la respuesta no es correcta.

Lo siguiente que queremos hacer es poder enviar datos al backend. Podemos hacer esto con nuestra API actual, pero hagámoslo más fácil:

```js
function client(endpoint, {body, ...customConfig} = {}) {
  const headers = {'Content-Type': 'application/json'}
  const config = {
    method: body ? 'POST' : 'GET',
    ...customConfig,
    headers: {
      ...headers,
      ...customConfig.headers,
    },
  }

  if (body) {
    config.body = JSON.stringify(body)
  }

  return window
    .fetch(`${process.env.REACT_APP_API_URL}/${endpoint}`, config)
    .then(async response => {
      if (response.ok) {
        return await response.json()
      } else {
        const errorMessage = await response.text()
        return Promise.reject(new Error(errorMessage))
      }
    })
}
```

Ahora podemos hacer cosas como esta:

```js
client('login', {body: {username, password}}).then(
  data => {
    console.log('here the logged in user data', data)
  },

  error => {
    console.error('oh no, login failed', error)
  },
)
```
A continuación, queremos poder realizar solicitudes autenticadas. Hay varios enfoques para hacer esto, pero así es como lo hago en la aplicación de estantería:

```js
const localStorageKey = '__bookshelf_token__'
function client(endpoint, {body, ...customConfig} = {}) {
  const token = window.localStorage.getItem(localStorageKey)
  const headers = {'Content-Type': 'application/json'}
  if (token) {
    headers.Authorization = `Bearer ${token}`
  }

  const config = {
    method: body ? 'POST' : 'GET',
    ...customConfig,
    headers: {
      ...headers,
      ...customConfig.headers,
    },
  }

  if (body) {
    config.body = JSON.stringify(body)
  }

  return window
    .fetch(`${process.env.REACT_APP_API_URL}/${endpoint}`, config)
    .then(async response => {
      if (response.ok) {
        return await response.json()
      } else {
        const errorMessage = await response.text()
        return Promise.reject(new Error(errorMessage))
      }
    })
}
```
Entonces, básicamente, si tenemos un token en localStorage con esa clave, agregamos el encabezado de Autorización (según la especificación [JWT](https://jwt.io/)) que nuestro servidor puede usar para determinar si el usuario está autorizado. Práctica muy común allí.

Otra cosa útil que podemos hacer es si el `response.status` es 401, eso significa que el token del usuario no es válido (tal vez expiró o algo así) para que podamos cerrar la sesión del usuario automáticamente y actualizar la página para ellos:

```js
const localStorageKey = '__bookshelf_token__'

function client(endpoint, {body, ...customConfig} = {}) {
  const token = window.localStorage.getItem(localStorageKey)
  const headers = {'content-type': 'application/json'}
  if (token) {
    headers.Authorization = `Bearer ${token}`
  }

  const config = {
    method: body ? 'POST' : 'GET',
    ...customConfig,
    headers: {
      ...headers,
      ...customConfig.headers,
    },
  }

  if (body) {
    config.body = JSON.stringify(body)
  }

  return window
    .fetch(`${process.env.REACT_APP_API_URL}/${endpoint}`, config)
    .then(async response => {
      if (response.status === 401) {
        logout()
        window.location.assign(window.location)
        return
      }

      if (response.ok) {
        return await response.json()
      } else {
        const errorMessage = await response.text()
        return Promise.reject(new Error(errorMessage))
      }
    })
}

function logout() {
  window.localStorage.removeItem(localStorageKey)
}
```

Dependiendo de su situación, tal vez los redireccione a la pantalla de inicio de sesión.

Además de esto, la aplicación de estantería tiene algunos otros envoltorios para realizar solicitudes. Como `list-items-client.js`:

```js
import {client} from './api-client'

function create(listItemData) {
  return client('list-items', {body: listItemData})
}

function read() {
  return client('list-items')
}

function update(listItemId, updates) {
  return client(`list-items/${listItemId}`, {
    method: 'PUT',
    body: updates,
  })
}

function remove(listItemId) {
  return client(`list-items/${listItemId}`, {method: 'DELETE'})
}

export {create, read, remove, update}
```

## Conclusion

Axios hace MUCHO por usted y si está satisfecho con él, no dude en seguir usándolo (lo uso para proyectos de Node porque es genial y no me ha motivado a investigar las alternativas que estoy seguro de que te mueres por contarme todo sobre eso ahora). Pero para el navegador, creo que a menudo será mejor que cree su propio wrapper simple alrededor de la búsqueda que haga exactamente lo que necesita que haga y nada más. Cualquier cosa que se le ocurra para un interceptor o transformación  con axios, puede hacer que su wrapper lo haga. Si no desea que se aplique a todas las solicitudes, puede crear un contenedor para su contenedor.

[Kent's tweet](https://twitter.com/kentcdodds/status/1244820744564965376?ref_src=twsrc%5Etfw%7Ctwcamp%5Etweetembed%7Ctwterm%5E1244820744564965376%7Ctwgr%5E%7Ctwcon%5Es1_&ref_url=https%3A%2F%2Fkentcdodds.com%2Fblog%2Freplace-axios-with-a-simple-custom-fetch-wrapper)

Buena suerte!
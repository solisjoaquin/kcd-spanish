# ¿A que proyecto open source debo contribuir?

[link al post original](https://kentcdodds.com/blog/what-open-source-project-should-i-contribute-to)

_Mi respuesta mágica a esta pregunta que se plantea con frecuencia y cómo empezar_

Esta es una pregunta que he tenido innumerables veces:

https://twitter.com/sarna_pranu/status/672438850724175872

_[El primer pull request de Pranu se produjo poco después de tuitear esto](https://github.com/Automattic/mongoose/pull/3644)_

https://twitter.com/geraldchecka/status/670445392706736128

Y en mensajes directos, correos electrónicos, etc. La esencia general es: "¿En qué proyecto de código abierto puedes recomendarme que empiece a contribuir?" Muchas de estas personas leen mi publicación [First Timers Only](https://kentcdodds.com/blog/first-timers-only) y esperan encontrar un proyecto que sea amigable para los que recién empiezan a hacer [pull requests](https://help.github.com/articles/using-pull-requests).


## La respuesta

Mi respuesta mágica proviene de mi publicación [Open Source Stamina](https://kentcdodds.com/blog/open-source-stamina):


> Contribuyes mejor a algo que usas regularmente

Donde he encontrado la mayor satisfacción de contribuir al código abierto es en proyectos que me importan a mí y (posiblemente) a otros. Y luego contribuir a ese proyecto con regularidad. Para hacer eso, debe comprender los casos de uso y los problemas asociados con una herramienta o biblioteca en particular. Por eso digo que es mejor _contribuir a algo que usas con regularidad_.

¿Qué librerias/frameworks/herramientas de código abierto utiliza regularmente? Quizás estes trabajando con Webpack y sientas que una opción en la configuración podría mejorarse o documentarse mejor. O tal vez estes trabajando con una biblioteca de React o Vue que podría necesitar un pequeño arreglo. Una cosa es segura: sea lo que sea que esté creando, probablemente esté utilizando un proyecto o herramienta de código abierto en el que podrías beneficiarte personalmente al contribuir.

Paso 1: Abra su `package.json` y lea las dependencias que tiene. Piensa en tu experiencia de aprendizaje y uso de ese módulo. ¿Recuerdas haber luchado con uno de ellos? Elige ese.

## Contribución
Una vez que haya encontrado el proyecto al que desea contribuir, ¿cómo sabe qué contribuir? Muchos proyectos tienen un archivo [CONTRIBUTING](https://github.com/blog/1184-contributing-guidelines). Busque eso primero para encontrar instrucciones para contribuir al proyecto. Si no hay uno, puede haber instrucciones en el archivo `README` (que normalmente se muestra en la página de inicio del proyecto). Si no existen tales instrucciones, puedes enviar un pull request para agregar solo un archivo esqueleto de `CONTRIBUTING.md` para iniciar una conversación sobre cómo agregar uno.

Familiarízate con el proyecto. Leer documentación es bueno, pero mi forma favorita de aprender cómo funciona un proyecto es leyendo el código. Mi forma favorita de hacer esto es agregar un `debugger` antes de llamar a una función de la libreria o cuando una libreria llama a mi función y salta por la call stack, así:


https://twitter.com/kentcdodds/status/1135687475110670341

Revise el código y aprenderá mucho sobre cómo funciona el framework/library. No te preocupes si no comprendes lo que está sucediendo de inmediato. Eso vendrá con el tiempo. Síguelo. ¡Puedes hacerlo! Puedes hacer lo mismo con herramientas no basadas en navegador con su [node debugger](https://code.visualstudio.com/docs/editor/debugging) favorito (o agregar console.logs).

Una vez que hayas descubierto los estándares y procesos para contribuir al proyecto y te hayas familiarizado un poco con su funcionamiento interno, deberá identificar los cambios que el proyecto necesita. Te recomiendo que analices los problemas existentes y comentes los que consideres interesantes. ¡Trabaje con el (los) encargado (s) para identificar una buena implementación y [haz tu pull request](https://help.github.com/articles/creating-a-pull-request)!

Si tienes tu idea propia de como corregir un bug o una función que desees implementar, te recomiendo encarecidamente que la ejecute el encargado del proyecto en un [GitHub issue](https://guides.github.com/features/issues) primero. Quizás dirán que está fuera del alcance del proyecto o que están trabajando en él, o podrían darle alguna dirección. Perderás menos tiempo asegurándote de que tu solicitud de extracción sea aceptada antes de hacerlo (al igual que estaba seguro de que mi esposa respondería "sí" cuando le pedí que se casara conmigo antes de pedírselo 😃).


_Tambien, mira [esta pagina](http://24pullrequests.com/contributing) para mas tips de como contribuir._

## Tu primer Pull Request

Para tu primer [pull request](https://help.github.com/articles/using-pull-requests), siéntete libre de encontrar un proyecto aleatorio con un bug/feature e intenta contribuir. Hágale saber al encargado del proyecto que usted es nuevo y que necesita una guía para aprender cómo entrar en él. Tal vez estén demasiado ocupados para ayudar, si es así, siga adelante y busque otro proyecto. Esa primera contribución es la más difícil, es posible que desee un poco de ayuda y entrenamiento. La contribución real del código importa menos que aprender el proceso. Así que busque un proyecto o alguien que tenga tiempo y paciencia para guiarlo.


Quizas estes interesado en mi curso **gratis** en egghead.io 
[How to Contribute to an Open Source Project on GitHub](https://egghead.io/courses/how-to-contribute-to-an-open-source-project-on-github):


## Recursos

Echa un vistazo a los GitHub issues etiquetados como 
[first-timers-only](https://github.com/issues?utf8=%E2%9C%93&q=is%3Aopen+is%3Aissue+label%3Afirst-timers-only),
[good for beginners](https://github.com/issues?utf8=%E2%9C%93&q=is%3Aopen+is%3Aissue+label%3A%22good+for+beginners%22+),
[good first bug](https://github.com/issues?utf8=%E2%9C%93&q=is%3Aopen+is%3Aissue+label%3A%22good+first+bug%22+)
(o
[good-first-bug](https://github.com/issues?utf8=%E2%9C%93&q=is%3Aopen+is%3Aissue+label%3Agood-first-bug)),
o
[help wanted](https://github.com/issues?utf8=%E2%9C%93&q=is%3Aopen+is%3Aissue+label%3A%22help+wanted%22+)
(mas [aqui](https://twitter.com/kentcdodds/status/672873736974897152)... _necesitamos_ estandarizar en esto).

Además, aquí hay buenos recursos para encontrar formas sencillas de contribuir:


[**Your First PR (@yourfirstpr)**](https://twitter.com/yourfirstpr)

[**first-timers-only (@first_tmrs_only)**](https://twitter.com/first_tmrs_only)

[**24 Pull Requests**](http://24pullrequests.com)

[**Up For Grabs**](http://up-for-grabs.net/#)

[**MunGell/awesome-for-beginners**](https://github.com/MunGell/awesome-for-beginners)

[Mi primer pull request](http://firstpr.me/#kentcdodds) fue corregir un error tipográfico en un comentario ([encuentra el tuyo](http://firstpr.me)). Era muy pequeño y era para un proyecto que realmente no usé tanto (descubrí el error tipográfico al revisar su código en un depurador). Fue una gran primera contribución, aunque realmente no tuve un impacto duradero en el proyecto y no estaba motivado para seguir contribuyendo, me ayudó a superar el problema de contribuir por primera vez, que es la parte más difícil.

## Conclusion
Contribuir al código abierto [ha sido fantástico para mí ](https://kentcdodds.com/blog/how-getting-into-open-source-has-been-awesome-for-me) y recomiendo encarecidamente a otros que se adentren en él. Es muy difícil comenzar, pero una vez que superas la primera contribución, hacer contribuciones futuras es mucho más fácil. No todo son rosas. La comunidad de código abierto tiene sus fallas aquí y allá. Sigue trabajando en ello. ¡Lo harás genial! ¡Buena suerte!

Por cierto, si estás interesado en crear tu propio proyecto, asegúrate de revisar mi serie en egghead.io:

[**How to Write an Open Source JavaScript Library**](https://egghead.io/series/how-to-write-an-open-source-javascript-library)

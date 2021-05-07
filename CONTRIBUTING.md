# Como contribuir

Gracias por estar dispuesto a ayudar!

**Estas haciendo tu primer pull request?** Puedes hacer el curso de Kent en egghead.io [How to Contribute to an Open Source Project on GitHub](https://egghead.io/courses/how-to-contribute-to-an-open-source-project-on-github)

 1. Clonar el proyecto
 2. crear la rama, moverte hacia ella y hacer los cambios alli. Puedes usar el siguiente comando que crea una rama y te mueve hacia ella:
 
 ```git 
 git checkout -b "nombre-de-la-rama"
 ```

 3. Guardar los cambios con add . y commit 
 ```
 git add .
 git commit -m "descripcion del commit"
 ``` 

 4. hacer `git push`. Cuando hagas esto estaras mandando la rama al repositorio en Github pero como todavia no existe la rama en el repositorio de Github se te mostrará un comando que deberás copiar en la consola para mandar los cambios y crear la rama.

 5. Ve al repositorio en Github y busca la opcion de pull request. Esto es basicamente una solicitud de que quieres agregar cambios al repo original. El paso anterior solo subió la rama pero todavia no se unió a la rama principal. El pull request basicamente de indica desde donde hacia donde quieres mandar esos cambios. En este caso:

 ###  'rama-creada-con-cambios' ---> 'rama-main'

 6. Si no eres encargado del proyecto, esos cambios que mandaste todavia no estan en el repositorio original. Tienes que esperar que los apruebe alguien encargado del repo.
# Rutas dinámicas en Nuxt 3

Puesto que, como es lógico, vamos a querer tener más de una lección, le vamos a tener que añadir secciones dinámicas a la ruta. Es decir, esa parte de la ruta se podrá extraer como una variable que podremos usar en la lógica de nuestra app.

Para ello, lo único que hay que hacer es introducir *square brackets* (`[]`) en el nombre del archivo y luego definir los *route parameters*.

La estructura de carpetas sería así: dentro de `pages/course` creamos la carpeta `chapter`, dentro de `chapter` un archivo o carpeta llamado `[chapterSlug]`, dentro de esta carpeta `lesson` y dentro de `lesson` el archivo `[lessonSlug].vue`.

Ahora la ruta que teníamos antes ya no funciona, tenemos que adaptarla a lo que tenemos: por ejemplo `/course/chapter/chapter-1/lesson/lesson1`.

Para poder usar ambos slugs, podemos usar la variable universal `$route`, a la que se puede acceder desde cualquier template en nuestra app. Por ejemplo, podemos poner en el template estas líneas (aquí representado en texto, sin usar bloque de código para evitar cortes):

`<p>Chapter Slug: {{ $route.params.chapterSlug }}</p>` (Ejemplo: chapter-1)  
`<p>Lesson Slug: {{ $route.params.lessonSlug }}</p>` (Ejemplo: lesson1)

En la siguiente lección usarás estos parámetros para mostrar la información correcta según la ruta.

El docente prefiere mostrarnos todo lo que se puede hacer con las rutas dinámicas:

- Se pueden mezclar partes dinámicas y estáticas dentro de cada segmento de la ruta.

   Por ejemplo, con esta estructura y archivo:  
   `pages/course/chapter-[chapterSlug]/lesson-[lessonSlug].vue`  

   La ruta resultante sería:  
   `/course/chapter-one/lesson-two`

- Se pueden combinar distintos *route parameters* dentro del mismo segmento (cuidando qué caracteres los separan):

   Por ejemplo, con esta estructura:  
   `pages/course/[chapterSlug]-[lessonSlug].vue`  

   Y la ruta:  
   `/course/one-two`

Pero lo ideal es tener un *route parameter* por segmento para mayor claridad.

- Se pueden tener segmentos opcionales usando doble *square brackets* (`[[ ]]`):

   Por ejemplo, esta estructura:  
   `pages/course/[chapterSlug]/[[lessonSlug]].vue`  

   Matcheará ambas rutas:  
   `/course/chapterSlug`  
   `/course/chapterSlug/lesson`

---

Con esto queda claro cómo funcionan las rutas dinámicas en Nuxt 3 y cómo sacar partido a los parámetros de ruta para construir rutas flexibles y anidadas.


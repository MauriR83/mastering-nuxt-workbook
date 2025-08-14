# Nested Routes en Nuxt 3

El formador quiere que las rutas a las distintas lecciones se vean así, anidadas:

`/course/chapter/first-chapter/lesson/second-lesson`

## ¿Cómo hacerlo?

- Dentro de la carpeta `pages`, se crea una carpeta llamada `course`.
- Dentro de `course`, se crea un archivo `lesson.vue`.

## Uso del componente `<NuxtPage/>`

- En el archivo `course.vue` (creado en la lección anterior) se añade el componente `<NuxtPage/>`.
- Esto permite que Nuxt renderice la página anidada que corresponda según la ruta.

## ¿Qué pasa con las rutas?

- Si navegamos a `/course`, Nuxt muestra el contenido de `course.vue`.
- Si navegamos a `/course/lesson`, Nuxt primero encuentra `/course`, y luego gracias al `<NuxtPage/>` anidado dentro de `course.vue`, sigue buscando y renderiza el componente `lesson.vue`.
- Esto permite que Nuxt haga matching de las rutas **de izquierda a derecha** y renderice anidadamente las páginas según la ruta.
- Sin el `<NuxtPage/>` en `course.vue`, Nuxt no puede continuar el matching y no renderizará las páginas anidadas.

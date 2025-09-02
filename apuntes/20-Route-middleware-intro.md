El Route Middleware se ejecuta cada vez antes de navegar a una ruta específica. De hecho será lo primero en ejecutarse cada vez que clickamos un link (por ejemplo). Este hecho nos dará la oportunidad de checkear algunas cosas sobre la app o la ruta e impedir la navegación, redirigir a otro sitio o simplemente dejar que sí suceda. 

El route middleware es distinto del server middleware (que se ejecuta dentro de Nitro). 
Server middleware se ejecuta en cada una de las request. Y su propósito es más añadir cosas al objeto de la request. En la opinión del docente, route middleware es más útil y seguramente se termine usando más que el server middleware. 
Puesto que se ejecuta cada vez que cambiamos de ruta, se ejecuta en el cliente y en el servidor. 

En el capítulo anterior, habíamos definido un método que checkeaba si la ruta introducida era una ruta válida. Pero como habíamos indicado, si usamos eso, no podemos usar otro middleware. Y qué pasa si queremos, por ejemplo usar authentication? 
El docente empieza el refactor. Existe la key middleware (dentro del definePageMeta) que puede ser un string, un navigation guard (method) o un array de string o navigatinon guards. 

El docente realiza el refactor, importante la parte donde se lanza el error se envuelve en un tag de abortNavigation. Otra diferencia con respecto a lo que teníamos, es que ya no necesitamos el return true. 

Vamos de esto: 
```js
definePageMeta({
  validate({ params }) {
    const course = useCourse();

    const chapter = course.chapters.find(
      (chapter) => chapter.slug === params.chapterSlug
    );

    if (!chapter) {
      return createError({
        statusCode: 404,
        message: 'Chapter not found',
      });
    }

    const lesson = chapter.lessons.find(
      (lesson) => lesson.slug === params.lessonSlug
    );

    if (!lesson) {
      return createError({
        statusCode: 404,
        message: 'Lesson not found',
      });
    }

    return true;
  },
});
```

A esto: 

```js
definePageMeta({
  middleware: function ({ params }, from) {
    const course = useCourse();

    const chapter = course.chapters.find(
      (chapter) => chapter.slug === params.chapterSlug
    );

    if (!chapter) {
      return abortNavigation(
        createError({
          statusCode: 404,
          message: 'Chapter not found',
        })
      );
    }

    const lesson = chapter.lessons.find(
      (lesson) => lesson.slug === params.lessonSlug
    );

    if (!lesson) {
      return abortNavigation(
        createError({
          statusCode: 404,
          message: 'Lesson not found',
        })
      );
    }
  },
})
```

# Cómo funciona exactamente Route Middleware?


Se debe seguir un formato específico, debemos tener una ruta a la que vamos y una desde la que venimos, y necesitamos devolver una de tres cosas:
- No hacer nada, y dejar que la navegación transcurra con normalidad. 
- Devolver un navigate to pero haciendo un navigate. 
- Devolver el abort navigation con un error que detendrá la navegación. 

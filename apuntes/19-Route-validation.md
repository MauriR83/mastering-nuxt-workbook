En el ejercicio anterior vimos cómo recogíamos el error. Pero puesto que el ejemplo usado, tiene que ver mayormente con rutas que no funcionan, hay un mejor modo de hacerlo: usando el route validation. 

Ahora en el **definePageMeta**, saca un **validate()** y aquí envuelve todo lo que teníamos de manejo de errores. Con ésto lo que hacemos es no esperar a que se renderice, el validate parece que lo hace de antemano. 
Hay que considerar que el definePageMeta no es una función normal y corriente. 
POr lo tanto, si fuera de ella se había declarado el useCourse (const course = useCourse()), dentro de ella el scope no llega y se tiene que volver a declarar. Y no hay que olvidar retornar un boolean al final. Si no devolvemos true, la página no renderizará. 

```js
const course = useCourse();
const route = useRoute();

definePageMeta({
  validate({ params }) {
    const course = useCourse();

    const chapter = course.chapters.find(
      (chapter) => chapter.slug === params.chapterSlug
    )

    if (!chapter) {
      return createError({
        statusCode: 404,
        message: 'Chapter not found',
      })
    }

    const lesson = chapter.lessons.find(
      (lesson) => lesson.slug === params.lessonSlug
    )

    if (!lesson) {
      return createError({
        statusCode: 404,
        message: 'Lesson not found',
      })
    }

    return true;
  },
})
```

Este validate hay que verlo como algo así como un middleware => Ejecuta un route middleware antes de que la página sea ejecutada para ver si se puede. Si se añade la función validate, no se podrá usar ningún otro middleware en esta página (de momento no nos afecta, pero hay que tenerlo presente). 
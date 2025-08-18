Es momento de añadir todos los chapters y lessons en la navegación. Para ello nos valdremos del composable useCourse. 

Empieza metiendo dentro de divs con la directiva v-if los chapters y luego los lessons de cada chapter. 

Construye, con los slugs interpolados las rutas dinámicas para cada lesson. 
(`/course/chapter/${chapter.slug}/lesson/${lesson.slug}`)

Al hace click ahora, el vídeo cambia, es rápido, pero no es instantáneo. Esto es porque se tira del server en cada click. 
No se está disfrutando de las ventajas del universal rendering. 

Para ello necesitamos NuxtLink (es un componente built-in), que sustituirá los tags 'a'. 
Es necesario también cambiar el atributo 'href' por la prop 'to'. 


```js
 <NuxtLink
            v-for="(lesson, index) in chapter.lessons"
            :key="lesson.slug"
            class="flex flex-row space-x-1 no-underline prose-sm font-normal py-1 px-4 -mx-4"
            :to="`/course/chapter/${chapter.slug}/lesson/${lesson.slug}`"
          >
            <span class="text-gray-500"
              >{{ index + 1 }}.</span
            >
            <span>{{ lesson.title }}</span>
          </NuxtLink>

```

Ahora vemos que es instantáneo (tarda sólo lo que tarde a cargar el vídeo, que ahí ya poco se puede hacer).

Nuxtlink nos permite navegar por completo en el lado del clliente, sin tirar de server. Además hace prefetch de los links. Es una de las armas de nuxt para ser increíblemente rápido. 

PERSONALMENTE A MÍ me está dando un error de VIMEO y los nuxtlinks no funcionan. Si los cambio por anchors sí funcionan. 

Los nuxtlink (cuando funcionan xD) no son unicamente para links internos, también funcionan para links externos. 

Le añadirá el noopener y noreferrer para asegurarse que los links son seguros. 

La idea ahora es, en vez de tener los paths a cada vídeo pre-computed, añadirlos a la propia data. 

Para ello vamos a tener que mapearlos. Esto es últi porque nos ayuda a sacar lógica fuera del template. 

EN vez de devolver courseData, lo que hacemos es: 

```js
  return {
    ...courseData,
    chapters: courseData.chapters.map((chapter) => ({
      ...chapter,
      lessons: chapter.lessons.map((lesson) => ({
        ...lesson,
        path: `/course/chapter/${chapter.slug}/lesson/${lesson.slug}`,
      })),
    })),
  };
```

Y ahora, en el nuxtlink nuestra prop 'to' ya puede ser tan simple como : 

 `:to="lesson.path`

Se añade un pequeño highlight de en qué lección estamos actualmente. 
Existe la .router-lin-active de vue router. Pero usa el docente cosas de tailwind.

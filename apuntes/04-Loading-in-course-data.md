# Crear un composable para reutilizar en múltiples componentes

Podemos crear el composable usando nuxi con el comando:  
`nuxi add composable useCourse`

Nosotros lo hacemos a mano: creamos la carpeta `composables/` (si no existe) y dentro el archivo `useCourse.ts`.

En ese archivo devolvemos directamente el contenido de `courseData.js`, que el docente ya tiene hecho de otros cursos, solo copiamos y pegamos.

Ahora, para usar el composable en `[lessonSlug].vue`, en el `<script setup>` hacemos:

   <script setup lang="ts">
const course = useCourse()
const route = useRoute()

const chapter = computed(() => {
  return course.chapters.find(chapter => chapter.slug === route.params.chapterSlug)
})

const lesson = computed(() => {
  return chapter.value?.lessons.find(lesson => lesson.slug === route.params.lessonSlug)
})
</script>


En la parte del template mostramos:

    <template>
      <p>{{ chapter?.title }}</p>
      <p>{{ lesson?.title }}</p>
    </template>

Por último, la ruta que debemos usar debe apuntar a capítulos y lecciones existentes, por ejemplo:  
`/course/chapter/1-chapter-1/lesson/1-introduction-to-typescript-with-vue-js-3`

Luego en un vídeo de un minuto, añade unos estilos, para poder hacer download del vídeo, y añade título y descripción. 


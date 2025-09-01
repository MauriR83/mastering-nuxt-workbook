Nuxt 3 viene con algo llamado <NuxtErrorBoundary> que captura cualquier error en su slot por defecto. NOs deja capturar un error y mostrar un mensaje de modo más específico. Por lo que podemos aislar errores específicos en vez de tener una página de error genérica. 

Le mete esto en lessonSlug para forzar el error: 

```js
@update:model-value="throw createError('Could not update')"

```

El caso es que al introducir el Error Boundary en la página de Course, ahora cuando da ese fallo, el error no se da en consola y el curso se deja de renderizar, porque da la oportunidad de mostrar el error slot en vez de el default slot. 

Con esto capturamos el error, pero la idea es recuperarse del error para poder continuar con nuestra app. Hace una cosa muy rara, y es que crea un botón dentro del slot de error para resetear el error (ponerlo a null)

Bueno, se dificulta explicar esto, por temas de nuevas versiones, en los comentarios del còdigo cambiado en el video correspondiente, hablan de cómo hacer mejor lo de los errores. : 

Por lo tanto, no podemos hacer lo que hemos puesto antes. 

Se queda así: 

```js
<LessonCompleteButton :model-value="isLessonComplete" @update:model-value="handleUpdate" />

...


const handleUpdate = () => {
  throw createError({ statusCode: 500, statusMessage: 'Could not update' })
}

```

Cuando se cambia el valor, es decir al clickar y decir que se ha completado la lección, lanzamos el error mediante la función de handleUpdate (que sustituye temporalmente a toggleComplete por motivos de aprendizaje).


Y en course, como veremos, ya se puede usar directamente el *clearError* nativo de nuxt:

```js
  <NuxtErrorBoundary>
        <NuxtPage />
        <template #error="{ error, clearError }">
          <div class="text-red-500">
            <h2>Oops, something went wrong!</h2>
            <p><strong>{{ error.statusMessage || error.message }}</strong></p>
            <button class="custom-button mt-4" @click="clearError()">Reset</button>
          </div>
        </template>
      </NuxtErrorBoundary>
    </div>

  ```

  




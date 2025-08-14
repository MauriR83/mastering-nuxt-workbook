1. File Based Routing

- Creamos una carpeta pages en el proyecto.
- Dentro de pages creamos un archivo index.vue.
- El contenido de index.vue es lo que se muestra directamente al ejecutar npm run dev. No fue necesario modificar app.vue ni otros archivos para que esto funcione.

- Creamos un archivo course.vue dentro de la carpeta pages.
- Si accedemos a /course en el navegador, podemos ver el contenido de course.vue.

- Nuxt genera automáticamente las rutas basándose en la estructura de archivos dentro de la carpeta pages.

- Nuxt utiliza internamente vue-router para gestionar las rutas, aunque por ahora no necesitamos preocuparnos mucho por los detalles internos.

- En toda aplicación Nuxt, el componente principal es app.vue. Actualmente es muy simple y se encarga de renderizar la página correspondiente según la ruta activa.

- Por último, copiamos un fragmento de código dentro de course.vue para añadir funcionalidad o contenido a esa ruta.


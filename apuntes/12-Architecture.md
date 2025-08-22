Partimos que smaller is better. Los componentes pequeños son más fáciles de manejar. 
Pero no caigamos en el error de hacer piezas tan diminutas, que sean imposibles de manejar. 

La idea pues, es manejar el código en piezas manejables. 
Y nuxt nos da unas herramientas que nos ayudan a hacer esto (Layouts, pages y composables).

Lo primero que vamos a ver brevemente es **app.vue**. Se trata del componente raíz de nuestra app (se puede ver en las Vue dev tools) y lo que se encarga de cargar el resto de cosas. 
El básico que viene por defecto tiene un NuxtLayout envolviendo un componente NuxtPage (este lo necesitamos si queremos usar el Page's Directory para definir las rutas de la app (lo de la estructura de rutas siguiendo los archivos dentro de la carpeta pages)). 

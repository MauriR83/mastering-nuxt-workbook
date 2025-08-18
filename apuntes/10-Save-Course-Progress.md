PEqueño reminder: Después de lo hecho en el capítulo anterior, sólo pondemos mantener el estado hasta que refrescamos la página. 

Aquí lo lograremos usando el módulo **VueUse** para Nuxt y poder sincronizar nuestro estado con el localStorage. 

El docente habla de las maravillas de VueUse y cómo se integra con Nuxt. 

Necesitamos instalar el módulo. 

Necesitamos instalar el VueUse/nuxt y el VueUse/core. 

Una vez instalado y para poder usarlo, lo tenemos que agregar a nuestra configuración. 
en el archivo nuxt.config, dentro de los módulos, añadimos *@vueuse/nuxt*


El único cambio que habría aque hacer a priori es el de cambiar useState por useLocalStorage (VueUse tiene un built in autoImport ).

```js
//antes
const progress = useState<boolean[][]>('progress', () => [])
//después
const progress = useLocalStorage<boolean[][]>('progress', [])
```

Ahora funciona y guarda el estado, pero sucede una cosa, el botón, pone completed! pero el color se queda el gris si referescamos. 
En la app en las devtools tam bién pone true. Por qué sucede esto? 
Tiene que ver con la hidratación. 

Cuando vamos a una app de nuxt, lo primero que usa es el SSR para servir la app, y luego carga la app para ejecutarla en el lado del cliente.

POdríamos decir que la hidratación es el proceso de pasar de una página HTML estática servida por el servidor, a una completa e interactiva apliación de Javascript. 
Por lo tanto, si hemos iniciado un estado en el server y queremos cargarlo en el cliente, puede que suceda una cosa peculiar, así que debemos prestar atención a cómo se hidrata el estado. 

En nuestra app, siempre inicializamos el state del progreso como una array vacía. Por lo tanto, cada vez que hacemos refresh, es un array vacío. Pero cuando el estado se carga en el cliente, carga el estado de LocalStorage. Ya no usa el valor por defecto. Y esto hace que no coincida el estado del servidor (array vacío) y el del cliente. POr eso al refrescar está esta disparidad. 

Ahora tiene sentido lo que decíamos en el capítulo anterior sobre las ventajas de useState: 

2) maneja la deta del server side mejor de lo que lo hace ref (se profundizará más adelante).


Pero bueno, puesto que esto todavía no va a database, no vamos a resolverlo en el servidor. Vamos a valernos de un truquito que Nuxt nos da para renderizar componentes únicamente en el lado del cliente. 
El componente **ClientOnly**. Ya que nuestro state es, de momento sólo del lado del servidor, tiene sentido que sólo se renderice el checkbox button del lado del cliente. 

Por lo tanto vamos a envolver el botón con los tags de <ClientOnly>
 Y al refrescar ya no existe ese problema. 

 Sin embargo, este ClientOnly tiene aspectos negativos. POr ejemplo no nos aprovechamos de las ventajas de performance  que nos da el server-side rendering. Pero puesto que esto es una pequeñísima parte de la página, apenas impacta. 

 Otra cosa a tener en cuenta sobre el ClientOnly es que sólo se debe usar cuando tienes un componente que a veces está renderizado en el servidor pero a veces no queremos que esté renderizado en el server (Es decir, en una páginas sí y en otra no, al tratarse de un componente reutilizable). 
 Sin embargo, puesto que en nuestro caso, siempre queremos tenerlo renderizado únicamente en el cliente, hay uno modo mejor de hacerlo en Nuxt:

Tan fácil como cambiar el nombre del archivo y añadir el sufijo client. 

`LessonCompleteButton.client.vue`

Aquí debemos tener claro que siempre lo queremos sólo en el cliente. Si no, como hemos dicho, ClientOnly. 

Lo del sufijo client ayuda mucho porque así vemos y entendemos de primera, que eso sólo lo queremos en el cliente. 

Al renombrar un componente, nos toca reiniciar el server. 


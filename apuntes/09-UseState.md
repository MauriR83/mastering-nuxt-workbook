Para saber cómo hemos avanzado en el curso, vamos a poner un checkbox (más adelante se supone que se integrará con el backend).

Creamos un LessonCompleteButton.vue en la carpeta de componentes.  

Y lo añade en  el lessonSlug.vue

De momento el botón no hace nada, vamos a tener que crear una ref para controlar el estado de este botón.


```js

const progress = ref()
```

Y en el tag del botón, le ponemos el v-model a este progress. 

```js

<LessonCompleteButton v-model='progress' />
```

Ahora al clickar, pues ya vemos que cambia a completed, pero esto se pierde al cambiar de vista. Sabemos que esto pasa porque al cambiar de página, la lessonpage se destruye  y se crea de nuevo, incluyendo nuestra ref. 

Otro problema es que estamos almacenando el estado como una única variable (por lo tanto, cada lección es una variable distinta).

Teniendo esto en cuenta, es difícil calcular el progreso. Sería más fácil si se puediese guardar en una única variable. 

Se podría guardar todo en una array, que a su vez tuviese una array por cada capítulo:

```js
[
    [true, true, false],
    [false, false, false ]
]
```

Esta array facilita mucho todo, el guardado en la database y el hacer computaciones para trackear el progreso. 

Nuxt nos aporta el composable useState. 
UseState devuelve un ref, pero, a diferencia del ref normal y corriente, ofrece dos diferencias que lo hacen muy útil. 

1) este estado se puede compartir entre componetes y no se destruye al cambiar de lección. 

2) maneja la deta del server side mejor de lo que lo hace ref (se profundizará más adelante). 


POr lo tanto, progress ya no será una ref, sino un composable use state, al que debemos darle una key única, para que sepa a qué trocito del state queremos acceder, y una función que devuelva el valor por defecto por si no se ha inicializado todavía. 

```js
const progress = useState('progress', ()=>{
    return []
})

```

Lo siguiente, será crear una computed para que pueda acceder al estado (isLessonComplete). 
HAce una mierda infecta llenad de ifs que espero que luego corrija, pero explica el por que. 
Primero de todo, debe ver si ya hay valor o de momento está devolviendo la array vacía. 
Va checkeando chapters y luego lessons. 



A continuación crea el toggleComplete. Si el chapter array no existe, lo crea. Y luego ya setea el valor. 


El último paso es hacer que nuestro lessonCompleteButton sea capaz de actualizar. 
Puesto que ahora es más complejo, el v-model ya no nos sirve. 
Lo que hace es usar el :model-value y el @update:model-value


```js

<LessonCompleteButton 
    :model-value='isLessonComplete'
    @update:model-value='toggleComplete'
 />
```


Ahora ya guarda los estados. Corrijo unos problemas de tipado y ya funciona todo bien. 

Pero hay un problema. Si refrescamos, se pierde todo el estado. No tiene persistencia. 
Esto lo veremos en la siguiente lección. 
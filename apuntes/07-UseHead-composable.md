El título de la webpage en la tab (sigue poniendo localhost bla bla bla) es lo que queda por actualizar. 
Lo que queremos que ponga es la lección y se vaya actualizando conforme vamos cambiando de lección. 

Para esto vamos a usar el composable useHead. Si vemos la documentación, hay un montón de cosas que se pueden hacer con useHead. De momento nos vamos a centrar en actualizar el título de nuestra página.

Vamos a haceerlo dese el lessonSlug.vue, ya que aquí calculamos lesson y chapter y tenemos acceso a dichos títulos. 


Veamos primero cómo funciona useHead. 

Si yo hago desde lessonSlug

```js
useHead({
    title:'Titulaco'
})
```

Esto actualizará el título en la tab (importante ver que el useHead está en un componente random). Sin embargo no es lo que queremos. Vamos a aprovecharnos que cada propiedad que le paseamos a usehead puede ser reactiva. 
Por lo que se calcula una nueva propiedad (una computed) para que saque el título. 


```js
const title = computed(()=>{
    return ´${lesson.value.title}-${course.title}`
})
```

Y ese title es lo que tendrá useheas (sólo hay que quitarle :Titulaco a lo de antes)
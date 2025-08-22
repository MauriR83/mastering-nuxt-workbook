La mayoría de webs comparten código en su mayoría de páginas. 
El ejemplo que pone es amazon, que mantiene header y footer fijos. Da igual en qué vista estés. Aquí entran los layouts en acción. 
Una cosa guay es que no tienes que montar y desmontar los elementos una y otra vez. 
A parte de facilitar a otros developers el saber dónde encontrar las cosas de footers y headers, Nuxt añade otras magias a los Layouts (actualización dinámica, transiciones entre layouts etc.). 

Vamos a crear un layout para nuestra app. De momento, tenemos un background en la página de cursos, pero la homepage no tiene nada. 
La idea es usar un mismo layout. 

Empezmos por crear una carpeta *layouts* que contendrá un archivo llamado *default.vue*. 

Añade el contenido de la template, muy similar al que tenía course, pero con   un slot. Y aprovechamos para quitar el div que había similar en course. 


La vista course se sigue viendo exactamente igual. 
Si ahora vamos a la homepage, veremos que ha añadido el gris del background y que ha centrado el texto en la pantalla. 

Esto funciona porque, si recordamos, nuestro *app.vue* renderizaba el <NuxtLayout> y el homepage que contiene. POr eso hemos podido obtener el style por defecto. 

Se pueden hacer más cosas con layouts a parte de proporcionar estilos por defecto a través de las páginas.  

Se puede usar el composable definePageMeta para cambiar que layout se está usando en cada página. 

Para que no renderice ninguno, se puede poner el layout a false:

```javascript
definePageMeta({
    layout:false
})
```

También se pueden crear layouts customizados. Por ejemplo el docente crea un archivo en la carpeta layouts llamado  custom.vue. Y en el definePageMeta de course.vue, lo especifica (layout:'custom').


El valor del layout no tiene por qué ser estático. Se puede usar una variable reactiva. 

Otra cosa que se puede hacer es hardcodear el nombre de un layout específico en nuestro layout component (el que hay en app.vue)


<NuxtLayout name='custom'>

Si lo hacemos así, no hará falta el definePageMeta y ambos, homepage y course page compartirán background (que es lo que cambia custom layout).


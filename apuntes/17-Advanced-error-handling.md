En la entrada anterior, se 'soluciona' el problema haciendo un re-renderizado del componente. Esto, lógicamente, no va a ser siempre suficiente. 

El colega se hace un if para que falle el código cuando se va  a la tercera lección. 

Ahora si vas a la tercera lección y le das al botón de reset que has hecho antes, el error no se soluciona. 
Puesto que en este caso estamos en un loop, este es un buen ejemplo de cuando hacer una 'retirada estratégica' y navegar a una parte segura de la aplicación que tenga más opciones de funcionar correctamente (en este caso a la primera lección). 

Aquí puede haber un problema, porque lo que hace es editar resetError (que aquí se había cambiado por el clearError) para que primero redirija y luego pase a null el valor del error. 
De todos modos el docente admite que podemos querer hacer mil cosas diferentes con el error y va a ser muy específico. Pero bueno, que nos quedemos con que es importante resolver el error primero. 
Una última cosa sobre el client side error handling es que se pueden escalar estos errores a errores fatales. 

Para el ejemplo vuelve a editar reset error para que cree un error con la propiedad fatal a true. Si ahora navega a la tercer lección (la que había tuneado para que diera el error) y luego, le da a reset, le muestra el pantallazo ese con el 500 fatal error. Esto es para cuando se esté seguro que no es posible recuperarse del error. 

Ahora una cosa interesante, dónde vamos a querer poner estos error boundaries?
Para empezar, no deberíamos envolver cada componente de la app con el errorBoundary, eso sería totalmente exagerado. Lo que hace es envolver child routes*. 
Si tuviésemos un dashboard para admins con muchos widgets (p.ej. google analytics), también puede que quisiéramos envolver cada uno de los widgets individuales con el boundary. 


POr cierto, puesto que nosotros ya no tenemos el resetError, porque usamos el clearError ,podemos hacer esto:
` <button @click="clearError({ redirect: '/course/chapter/1-chapter-1/lesson/1-introduction-to-typescript-with-vue-js-3' })">`
Es decir, poner el redirect dentro del clear error.

* “Envolver child routes” significa poner un <NuxtErrorBoundary> alrededor de <NuxtPage /> dentro de un layout o página padre. Así, si un componente de la ruta hija falla, se maneja localmente y no rompe todo.
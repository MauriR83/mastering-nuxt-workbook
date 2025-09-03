Nuestra página de login estará a nivel de raíz. Pega un código así muy básico con un header y un botón.
La ruta es, por supuesto /login.

OTra cosa que hace es ir a la página de course y envolverlo todo en un div. Para evitar tener múltiples nodos. Así, además de que así se harán las transiciones de rutas de forma correcta, facilitará el añadir cosas más adelante. 
Refactoriza algunas cosas como el título etc.
Y por fin una cosa que se echaba de menos,  un link de home a first lesson! 
Puesto que no es el primer sitio desde el que se quiere volver a la first lesson (había una recuperación de error en el server que nos enviaba ahí también), se decide crear un composable useFirstLesson. Es muy simple, se trae chapters y lessons y devuelve la primera lesson del primer chapter. 

```js
export default () => {
  const { chapters } = useCourse();
  return chapters[0].lessons[0];
}
```

En fin, que quizá el título de la lección lleve a confusión porque sí, ha creado una página de login, pero no está haciendo nada xD


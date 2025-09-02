Empezamos por recordar que nuxt puede renderizar la página tanto en el servidor como en el cliente. Por lo tanto aquí veremos qué sucede cuando los errores suceden en el servidor. 
La metodología será similar a la del cliente, primero se debe capturar el error, luego mostrar un error de mensaje y por último, dar al usuario un modo de recuperarse del error. 

Si ahora vamos al browser y añadimos strings a voleo en la dirección, asegurándonos que el chapter no esxiste, nos mostrará un error 500. Evidentemente esto no es un error del router, porque la dirección matchea (los casos de chapter/lesson/ etc.). Es simplemente que no estamos recogiendo un caso en el que la dirección no exista. Se está asumiendo que la ruta existe. 

Para gestionar esto correctamente, vamos a usar el método createError.  Antes habíamos visto cómo pasarle una string, pero podemos pasarle también un objeto con más datos (los típicos de un error object).

De este modo, con el createError podemos pasar el status code. En el ejemplo que hemos puesto (la ruta que no existe) el que más sentido tiene es el 404. Si ahora vamos a una ruta que no existe, vemos que ya no sale la página por defecto, sale una un poco distinta (con 404 en vez del 500).
En El ejemplo, el if que había puesto el docente era para cuando no existe la lesson, pero se puede hacer lo mismo para el chapter. 

## Custom error page

Lo primero es crear un archivo *error.vue* en la raíz del proyecto.
En cuanto al contenido de la página, se asegura de usar el <NuxtLayout> (para que tenga los estilos por defecto) y luego le pone unos textos random. 
Ahora eso es lo que muestra cuando hay un error. 
Sin embargo la idea es mostrar un poco más acerca del error, por lo que vamos a usar el composable *useError*. 

Con esto podemos jugar, y poner algún if dependiendo del error.status (error=useError()) y displayear el error.message etc. Por ejemplo, dado que el error 404 es el más común tiene sentido que tenga su propia página. 

```js
if (!chapter.value) {
  throw createError({
    statusCode: 404,
    message: 'Chapter not found',
  });
}
```

Lo que necesitamos también es limpiar el error y darle al usuario un modo de recuperarse del error. 

Hacen una cosa parecida, crean un anchor con el texto 'go to the first lesson'. Y para limpiar el error, se puede usar el método clearError, que tiene como una de sus opciones, 'redirect'. Por lo que si se usa, limpiará el error. y luego redigirá a la ruta indicada. Es similar a lo que se hacía del lado del cliente, pero aquí se hace con una solo llamada. 
Una consideración que debe hacerse es tener en cuenta que el objeto de error que estamos usando y el clearError, únicamente existe en el servidor *(Esto es lo que dice, pero nosotros sí lo estamos usando, el clearError como mínimo)*

Lo que sí es cierto, es que 


NOTAS:
- useError() se usa para obtener o establecer errores globales en tu app de Nuxt. Es decir, errores que afectan a toda la página (no solo un componente individual como con NuxtErrorBoundary).

- ❌ ¿Dónde no usar useError()?

❌ Dentro de un NuxtErrorBoundary → Usa el slot con error y clearError.

❌ Para errores menores en UI local (como un modal que no carga) → eso no necesita useError.
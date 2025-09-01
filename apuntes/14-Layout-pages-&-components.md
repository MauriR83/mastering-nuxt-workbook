Parece que tenemos un problema. Como dice el título, tenemos tres formas distintas de introducir código en nuestra aplicación. 

Cómo saber cuándo usar cada una?

Lo primero que hay que tener en cuenta es que a todos los efectos, todos ellos son componentes. 

LUego para decidir cuál usar, nos podemos centrar en las propiedades especiales que da nuxt a cada uno de estos distintos tipos de componentes. 
 
 Por ejemplo hemos visto que las pages se usan para definir el routing.
 A los layouts se les da la propiedad de facilitar el compartir código  entre distintas pages. 
 Los componentes son ligeros y no tienen ninguna mágia extra. 

 El docente hace una propuesta. 

 1) Por defecto, el código va a pages. 
 2) Se mueven las piezas comunes a Layouts. 
 3) Se mueven las pequeñas piezas de funcionalidad a Components.

 Ahora veamos los pasos anteriores un poco más detalladamente.

 1) Por defecto a pages:
 - céntrate en que todo funcione (es la meta inicial)

 2) Piezas comunes en Layouts
 - Cuando veas código en común en las pages (ej. mismo header, mismo footer, mismo estilo...)
 - Regla de tres. Crearemos la abstracción cuando veamos que algo sucede tres veces. 
 - Sabemos cómo va a ser antes de tiempo (porque hemos visto el diseño)

 3) Piezas pequeñas en componentes:
 - Ejemplo: Se han creado varias layouts que usan headers similares. Es el momento de crear un componente header. 

Algunas consideraciones: 

*Decidir entre Layout o Component*

Una pregunta que nos podemos hacer es dónde esperamos encontrar este código. 
Por ejemplo, el vídeo que hemos creado, nos pega más como componente, mientras que el header y footer parece que tendrían más sentido como parte de un layout. 
Los components normalmente hacen una úncia cosa. Los layouts hacen varias. 
Un componente reproduce un vídeo. O crea un botón. 
Un Layer combina Footer y Header, añade estilos etc. 

Un consejo sería empezar metiendo todo en layout y luego ver si tiene sentido moverlo a componente.  


*Bonus track: Composables*

Breve recordatorio, los composoables nos ayudaban a organizar la lógica reactiva. 
Cualquier lógica reactiva puede convertirse en un composable siempre que use cualquiera de las apis de reactividad de vue (refs, computed, watcher...). 

Diferenciamos tres tipos de composables=>
1) Single Use composables. Donde simplemente intentamos extraer un montón de lógica complicada de una página o componente para que sea más fácil de leer.  
2) Reusables. El más común. Un ejemplo es nuestro useCourse. Es un set de funcionalidad que queremos usar en múltiples sitios. Así que lo definimos en un composable y lo usamos por todos los sitios. 
3) Genérico. No son específicos de nuestra lógica de negocio, pero son útiles. Un buen ejemplo sería useLocalStorage ya que cualquier app podría querer usar useLocalStorage, no es algo que sea propio de nuestra app. 

Todos los composables van a la carpeta composables, y todo lo que definamos ahí (sea .js o .ts) estará automimportado en nuestros componentes, páginas y laouts.  



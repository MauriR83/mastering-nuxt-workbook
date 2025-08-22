Lo primero que hay que hacer es setear el repo en github para que pueda ser usado en Netlify. 

Se crea un nuevo repo. Se pushea un existing repo al nuevo repo. 
Luego vamos a Netlify. Te puedes loguear usando credenciales de Github, gitlab etc. 
NO ME QUEDA CLARO si es porque no lo tenía online, y lo acaba de subir por primera vez, o de verdad hay que clonarlo.


- Clickamos *'Add New Site'*
- Seleccionamos *Import an existing project*. 
- Luego en las opciones seleccionamos Github. 
- Luego selecciona la opción 'Configure the Netlify app on Github' (No sés si porque no le aparece en la lista o porque prefiere hacerlo desde github).
- Desde aquí selecciona sólo la opción de que Nelify acceda unicamente a los repos seleccionados (por un tema de limpieza y orden)
- Selecciona el que queremos y le da a save. 
- Ahora va a la vista anterior y ya se ve el repo que queremos (esto contesta una de las dudas en el 4 punto)
- Si lo seleccionamos, nos será posible importarlo desde github y Nuxt detectará automáticamente que se está buildeando en Netlify y se configurará a sí mismo. 
- Lo único que tenemos que hacer es pulsar el botón 'deploy site'
- Una vez deployado, vemos que arriba hay una tab 'deploys'. Vamos a ir ahí a ver cómo ha sido deployado. 

EN la consola podemos ver el log mientras se construye y hace un bundle. En breve ya lo tendríamos. 

Ahora, para ver cómo hacer un nuevo build, debemos volver al tab 'deploys'. 
Ahí vemos que hay un dropdown 'trigger deploy'. 
Esto nos deja hacer un deploy manual si lo necesitamos. 

Evidentemente, se puede setear Netlify para que deploye cada vez que pusheamos a github. 
Para ello vamos a la tab, *Site Overview* y luego dentro de esa tab, la tab *site settings*. 
De ahí seleccionamos *build and deploy* y en la sección *branches*, seleccionamos la opción all en braqnch deploys. 


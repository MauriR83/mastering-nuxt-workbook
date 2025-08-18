

En este capítulo habla de la diferencia entre SPA (single page) y SSR (server side rendering). 

Básicamente las SPA hacen request también al server, pero sólo se traen el raw data, no se traen HTML y Css. 

Alguna diferencia. 

En la **SPA**, la carga inicial es **lenta**. En **SSR** es **muy rápida**. 

En los siguientes clicks, la **SPA** es **muy rápida**, porque no pide nada al server. En **SSR** las interacciones son **lentas**. 

Cada una de las formas, SPA y SSR tiene una fortaleza. Lo que intenta hacer Nuxt es combinar ambas con el **Universal Rendering**.

Tenemos un start up muy rápido y luego minimiza los round trips al server. 

Luego explica cositas más técnicas. Pero bueno. Con esto me sobra de momento. 
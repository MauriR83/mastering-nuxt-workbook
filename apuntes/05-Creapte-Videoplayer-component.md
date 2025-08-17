
El docente crea un componente videoplayer con nuxi, nosotros lo creamos a mano. 

Creamos primero la carpeta (recordar que todo lo que vaya aquí podra ser autoimportado).

Empieza copiando el iframe de viemo (Lo copiamos de su código online). Hace la source dinámica para que seamos capaces de pasarle cualquier vídeo. Por lo tanto necesitamos definir la prop videoId. 

```js
const props = defineProps({
    videoId:{
        type:String,
        required: true
    }
})
```

Usamos el componente en la vista, y arreando! 

```js
 <a
        v-if="lesson?.downloadUrl"
        class="font-normal text-md text-gray-500"
        :href="lesson.downloadUrl"
      >
        Download Video
      </a>
```
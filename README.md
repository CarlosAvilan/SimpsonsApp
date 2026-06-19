2do Parcial - Parte Practica
Que se solicita:

El codigo tiene 10 errores. Recae en usted analizar que es un error dentro del codigo.
Los Alumnos tendran que forkear este repo como propio, hacer un issue desde Github con Comentarios refiriendo en que linea esta el error, y como se debe solucionar.
La respuesta sera con el link a ese Fork, y adentro deben estar los issues. Los profesores tenemos que poder ingresar al mismo. Recae en los alumnos asegurarse de que los profesores puedan ingresar.
Tambien pueden editar el Archivo Readme y poner los resultados dentro de sus propios forks.
https://github.com/ExBattou/SimpsonsApp

Errores encontrados

1 Episode.kt, líneas 13-15
El init no hace nada aquí (no se necesita inicialización), está fuera de las llaves  y podría ocasionar errores de compilación.
Solución: borrar el bloque del init.

2 EpisodeRepository.kt (línea 8) y EpisodeRepositoryImpl.kt (línea 23)
Hay diferencias entre la nomenclatura utilizada en la función get episodes, que aparece como get_episodes() en la interfaz, pero en la implementación está como getEpisodes().
Al no coincidir uno no se aplica, el otro no se implementa.
Solución: se debería cambiar la interfaz a getEpisodes() para que funcione.

3 DataModule.kt (líneas 34-38)
El builder del RetrofitClient no tiene la base Url.
Solución: Agregar  la baseUrl ("https://thesimpsonsapi.com/") antes del .build().

4 EpisodeRemoteMediator.kt (línea 106)
Se copió toda la url completa en el get sin usar la base Url de Retrofit.
Solución: combinado con el error anterior, se debería usar en esta función solo el path relativo a partir de la base url que debería estar en el Retrofit.

5 MainScreenViewModel.kt  (todo el archivo)
No se utiliza este ViewModel, sino que se usa MainViewModel. Tampoco incluye las anotaciones de Hilt ni Inject.
Solución: eliminar el archivo.

6 AppNavigation.kt (líneas 9–10)
Los  import androidx.navigation.* y androidx.compose.* no son necesarios. El primero “vuelve” a importar todo lo que ya estaba importado en las líneas de arriba, y el segundo no es válido.
Solución: eliminar estos dos imports.
7 data/DataRepository.kt (todo el archivo)
Esta clase no se emplea en DataModule.kt y solo es referenciada por MainScreenViewModel, que tampoco es necesario.
Solución: eliminar el archivo.

8  MainScreenTest.kt (línea 18)
MainScreen recibe onNavigateToDetail: (Int) -> Unit como parámetro, no una lista, entonces el test no va a compilar así.
Solución: se puede utilizar composeTestRule.setContent { MainScreen(onNavigateToDetail = { }) } 

9  MainScreenTest.kt (líneas 22-24)
MainScreen no está hecho para mostrar strings de textos como los marcados com “Hello…”
Solución: reescribir el test para que verifique el uso de elementos reales de la pantalla de la aplicación.

10 DataModule.kt (línea 26), EpisodeRemoteMediator (líneas 105-110)
Falta la interfaz SimpsonsApi en DataModule.kt, pero funciona porque está al final de EpisodeRemoteMediator. Pero es un error porque una interfaz debería estar en un archivo aparte.
Solución: crear esta interfaz para que coincida con lo implementado en 





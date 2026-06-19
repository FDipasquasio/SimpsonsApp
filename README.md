2do Parcial - Parte Practica
Que se solicita:

El codigo tiene 10 errores. Recae en usted analizar que es un error dentro del codigo.
Los Alumnos tendran que forkear este repo como propio, hacer un issue desde Github con Comentarios refiriendo en que linea esta el error, y como se debe solucionar.
La respuesta sera con el link a ese Fork, y adentro deben estar los issues. Los profesores tenemos que poder ingresar al mismo. Recae en los alumnos asegurarse de que los profesores puedan ingresar.
Tambien pueden editar el Archivo Readme y poner los resultados dentro de sus propios forks.
https://github.com/ExBattou/SimpsonsApp

Errores
1— Hay 2 viewModels para la misma pantalla MainViewModel.kt y MainScreenViewModel.kt 
sospecho que el MainScreenViewModel es viejo ya que manejo un dataRepository generico
2- En el archivo MainScreen.kt linea 1 hay un composable que evalua si las temporadas estan vacias 
y decide cuando llamar a refreshSeasons(). Esta logica debe estar a cargo del viewmodel sino estaria 
rompiendo con la logica MVM.
4 — En el archivo DataModule.kt línea 27 hay un interceptor que registra header y 
body completos de cualquier entorno. Estos interceptores solo deberian ser usados en entorno de prueba 
y desarrollo
5 — En los archivos episoderemoteMediator.kt y EpisodeRepositoryImpl.kt reciben la Base de datos completa,
haciendo un erro grave el cual le permite acceder a todos los daos cuando deberia tener solo uno
6 - En el archivo DataRepository.kt , la interfaz devuelve Flow<List<String>> que son strings genericos 
sin relacion con los episodios ni las temporadas. pese a que esta para los test este deberia ser sacado
del codigo antes de pasarlo a produccion
7 - en getEpisodesUseCase.kt y el resto de use cases no hace ninguna transformacion,
ni validacion de datos,ni logica de negocio,lo cual rompe un poco con las buenas formas de clean arquitecture.
8 - en DetailViewModel.kt el estado es MutableStateFlow<Episode?>(null) donde el null 
puede significar 3 casos distintos que carga que hubo un error o que no se encontro el episodio. 
Al no poder diferenciar la intefaz de usuario no puede mostrar correctamente el caso.
9 - en el archivo EpisodeRepositoryImpl.kt linea 53 la traformacion de EpisodeEntity a 
Episode que es la clase que se usa no es responsabilidad del repositorio y deberia ser manejada antes.
10 - en el archivo EpisodeRemoteMediator.kt linea 106 la url esta dentro del @GET la url deberia estar 
centralizada en un DataModel y que el endpoint solo conozca la ubicacion relativa
11 - en el Gradle copies gradle.properties línea 32  esta hardcodeado que use el org.gradle.java.home=/opt/homebrew/Cellar/openjdk@17/17.0.15/libexec/openjdk.jdk/Contents/Home esa linea deberia ser eliminada
12 - en el archivo Episode.kt líneas 13-15 hay un bloque init a nivel de archivo que no es válido, con un return que también es inválido estas lineas deberia ser eliminadas

Executable: https://drive.google.com/file/d/1JSllUg7-RnWF4Yth-LJ5EE5pYQsKxIVD/view?usp=sharing

# El proyecto

### De la practica 2:
El juego existe de un mundo virtual, lo cual debería verse como una fabrica de robots. En ese mundo, el jugador tiene que colectar algunos chips que contienen información sobre la fabrica, y llegar al fin para extraer esa información.

Para llegar al fin, el jugador tiene que recoger tarjetas que le dan entrada a diferentes partes de la fabrica, donde tiene que buscar los chips. Pero mientras está navegándose por la fabrica, el jugador va a encontrarse con robots que le quieren parar y matar.  Los robots perseguirán al jugador si lo pueden ver, si no siguen su camino a puntos fijos y a veces aleatorios (depende del tipo de enemigo - en mi juego hay dos tipos, lo que se explica en https://github.com/DEV21-G07/practica2/wiki/Las-pruebas en la parte sobre "Los enemigos").

El jugador puede disparar al robot para defenderse (pero lo mejor es evitarlos) y puede destruir los spawners de los robots para qué dejan de aparecer en el mundo. Disparando va perdiendo balas, por eso hay paquetes de munición que se puede recoger para tener más balas. Los robots también pueden dañar al jugador, quitándose las vidas. Después de un tiempo esas vidas se recuperan.

### De la practica 4:
En esta practica, nos enfocamos en efectos visuales, tal como animaciones, efectos electricos, ... Los robots estarán animados de manera diferente según estén quietos, caminen o corran. También podrán golpear al jugador y a objetos que se encuentran en su camino. Los robots también tendran animación de muerte, y justo antes de morir caminaran como que son heridos, y van mas lento. A hacerle dano a los robots, le saldran chispas, y al matarlo habrá explosiones y -con cierta probabilidad- incendios que pueden propagarse y afectar a otros personajes. Con el generacion de los robots habrá mucha luz, sonido y descargas eléctricas.

----

# Proceso

## Preproducción (Nov 1)

#### Prototipos
Para tener un poco mas claro la idea de los efectos, hicimos en clase un proyecto usando el Niagara system de ue4. Cuando el personaje esta corriendo, queremos que sale una nube de polvo en el suelo, que se desaparece después de un tiempo. Aunque no usarémos este efecto en la practica, es bien entender como funciona.

#### Estética 
Ya que el juego ya estaba hecho, solo tuve que pensar en que herramientas deberia usar para los animaciones y los efectos. Al fin decidi usar Mixamo, ya que parece que tienen muchos animaciones, ya ya habia podido encontrar animaciones para golpes y morirse.

Para la mayoria de los efectos, fui buscando en los content examples que tiene ue4. Los "effect gallery" y "lighting gallery" me han dado mucho inspiracion sobre como hacer los efectos de electricidad y chispes, etc.

#### Planificación
Primero, tendré que mover el proyecto sin quedarme con todos los objetos que no necesito y que me dan los 22GB de la practica 2. Después, me parece importante primero hacer todo - o casi todo - lo que pide la practica 4, antes de ir mejorando las cosas de la practica anterior. Asi que empecaré con los efectos y animaciones, y después iré mejorando todo.


## Produccion

#### Mover la practica 2 (Dec 3)
El emigrar el proyecto o un nuevo proyecto me ha costado mas de lo que pensaba que iba a costar. Hubieron problemas con el jugador que ya no entro en el juego al spawn, y el mapping de los teclados. Al fin todo se ha resuelto y ahora pesa menos el proyecto.

#### Resolver el color del arma (Dec 4)
Ya que era algo muy simple, lo he hecho antes de empezar con la practica de verdad. Querria que no se vuelve muy rojo demasiado temprano, pero no salio muy bien en la practica anterior. Asi que ahora, el arma empieza a ponerse roja cuando solo quedan menos de 10 balas. Empiezas con 20, asi que las primeras balas, el arma se queda el mismo color.

#### Animaciones (Dec 9)

##### El robot se muere
Primero, he buscado en Mixamo para un animacion de alguien muriendo y cayendose al suelo. Como queria seguir usando el robot que ya tenia, que usa un mannequin de ue4, he tenido que hacer un "retarget" de los animaciones. Para eso, he usado el tutorial https://www.youtube.com/watch?v=92rag3qStI4, en donde tuve que cambiar también unas cosas en el mapping del Mannequin. Asi que antes de morirse de verdad, el robot hara esta animacion. Tuve que anadir un notify para que el robot solo se muera antes de acabar con el animacion, porque poner un "Destroy" en el mismo event graph donde llamas al animacion, destruye inmediatamante al robot (tendria que poner un delay, pero no me parecia la mejor solucion).

##### El robot puede dar golpes
Para esto también he encontrado el animacion en Mixamo, tenia que ser una animacion que puede hacer un loop rapido, y que no dura como 4 segundos antes de regresar a su posicion inicial. En el codigo, al darle dano al jugador, el robot tiene que ejecutar esta animacion mientras esta tocando el jugador (o luego el objeto que esta en su camino).

##### Modos del robot: quieto, caminar y correr (herido vs. no herido)
Ya que ue4 ya cambia los animaciones de un personaje cuando va mas rapido o mas lento, solo tenia que cambiar la velocidad cuando el robot ha visto el jugador.

También querria al hacerle dano al robot, que se va moviendo de una manera herida. Por eso, he econtrado en Mixamo 3 animaciones que se pueden seguir el uno al otro: estando quieto, caminando y corriendo, todos de forma herida. Por eso, en el .... TODO

#### Efectos visuales (Dec 10 - Dec 15)

##### Chispas al danar los robots
Para esto fui al "effects gallery" de ue4 de content examples, y encontré algo que se llamaba "random sparks", era exactamente lo que necesitaba, con sonido y todo. Asi que lo movi a mi proyecto, y activo las chispas cuando el robot esta tocado con una bala del jugador. Ya que el event hit tiene un parametro que da la direccion del hit, podria poner las chispas justo en esa direccion y ese lugar donde la bala ha tocado el robot.

##### Una explosion cuando se muere el robot
Para esto anadi un explosion al notify del animicion de morirse, para hacer la explosion al fin del animacion. Usé el explosion que ya estaba en el starter pack de ue4. 

##### Electricidad al generar un robot
Para esto, también usé los "random sparks" del effects gallery. También fui buscando para una luz parpadeante, o por lo menos una inspiracion en el lightning gallery. Ahi encontré algo simular, pero con el logo de ue4. Lo que la luz usaba era un Lightning Function, lo cual he cambiado un poco para mi proyecto, y he agregado luces con ese lightning function al spawner. 

También he buscado en internet un sonido que puede ser el sonido del generador mientras esta generando el robot, lo he importado en el proyecto y ya activo el sonido 4-5 segundos antes de que se aparece un robot.

##### Fuego después de la explosion
- catch on fire
- damage

#### Resolver problemas de la practica anterior (Dec 14 - Dec 16)

##### Usar BehaviorTrees para los AIs

##### Un mecanismo de fysica

##### Juntar los enemy classes


## Postproducción (Dec 17)



----

# Diseño del juego 
## Jugabilidad

### Mecánica
**Salud**
- El jugador tiene 10 vidas 
- Al tocar un robot, el jugador pierde una vida. Después sigue perdiendo vidas cada 1 segundo.
- El jugador recupera vida cada 5 segundos.
- Al estar en llamas, el jugador perdera 4 vidas.

**Combate**
- El jugador pierde balas mientras está disparando.
- Se puede matar a los robots disparándolos 3 veces.
- Se puede destruir los spawners disparándolos 3/4/5 veces (depende del nivel).
- Al destruir los robots, puede ser que habra un fuego que dana al jugador y los robots si estan demasiado cerca.

**Coleccionar**
- El jugador puede recoger munición caminando sobre el objeto o tocándolo.
- El jugador puede recoger tarjetas de entrada caminando sobre el objeto o tocándolo.
- El jugador puede recoger chips caminando sobre el objeto o tocándolo.
- Se puede abrir puertas si tiene una tarjeta de entrada.
- Se puede abrir la puerta final si tiene todos los chips.
- El jugador tiene que disparar a los cubos grande para pasar pasillos, ...

### Dinámica
- El jugador necesita evitar o matar a los robots para que no se muera. Necesita acumular munición para seguir disparando.
- Se necesita coleccionar tarjetas de entradas, para superar a la parte actual del mapa y seguir a una otra parte.
- El jugador se va juntando todos los chips del nivel. Así podrá abrir la ultima puerta y acabar con el juego.
- El jugador podra danar varios robots de una vez, si destruye a un robot y la explosion (que a veces no hay) le afecta a los otros robots.

### Estética
- El mundo debería verse como una fabrica real, para que el jugador se siente realmente adentro de una fabrica de robots.
- El jugador necesita tener miedo de no saber de donde vienen los robots, no debería ser obvio donde está el spawner. Al descubrirlo se sentirá aliviado.
- Dará susto descubrir un robot fuerte detrás de una esquina, la apariencia de esos robots darán más miedo que los robots normales.
- En alguna parte el jugador puede abrir la puerta equivocada si va avanzando demasiado rápido, tendrá que volver lo que le da frustración pero también curiosidad por no haber descubierto algo antes.
- En alguna parte también hay que mirar bien que no se ha perdido un chip que está un poco escondido.  Aquí también tendrá que regresar, para buscarlo. Si ha acabado con todos los spawners se sentirá tranquilo, sin mucho apuro, si no será más miedoso y difícil.
- El acercarse de los robots al jugador tiene que darle miedo, cuando está perdiendo vidas también habrá un efecto de la vista que se da cuenta de que se va a perder su vida.



## Contenido
Todas las siguientes partes se encuentra en el wiki:  https://github.com/DEV21-G07/practica2/wiki/Las-pruebas
### Los enemigos
### Los objetos especiales 
### Los niveles

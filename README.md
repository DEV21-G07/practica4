Executable: https://drive.google.com/file/d/1JSllUg7-RnWF4Yth-LJ5EE5pYQsKxIVD/view?usp=sharing

# El proyecto

### De la practica 2:
El juego existe de un mundo virtual, lo cual debería verse como una fabrica de robots. En ese mundo, el jugador tiene que colectar algunos chips que contienen información sobre la fabrica, y llegar al fin para extraer esa información.

Para llegar al fin, el jugador tiene que recoger tarjetas que le dan entrada a diferentes partes de la fabrica, donde tiene que buscar los chips. Pero mientras está navegándose por la fabrica, el jugador va a encontrarse con robots que le quieren parar y matar.  Los robots perseguirán al jugador si lo pueden ver, si no siguen su camino a puntos fijos y a veces aleatorios (depende del tipo de enemigo - en mi juego hay dos tipos, lo que se explica en https://github.com/DEV21-G07/practica2/wiki/Las-pruebas en la parte sobre "Los enemigos").

El jugador puede disparar al robot para defenderse (pero lo mejor es evitarlos) y puede destruir los spawners de los robots para qué dejan de aparecer en el mundo. Disparando va perdiendo balas, por eso hay paquetes de munición que se puede recoger para tener más balas. Los robots también pueden dañar al jugador, quitándose las vidas. Después de un tiempo esas vidas se recuperan.

### De la practica 4:
En esta práctica, nos enfocamos en efectos visuales, tal como animaciones, efectos eléctricos, ... Los robots estarán animados de manera diferente según estén quietos, caminen o corran. También podrán golpear al jugador y a objetos que se encuentran en su camino. Los robots también tendrán animación de muerte, y justo antes de morir caminarán como que son heridos, y van más lento. A hacerle daño a los robots, le saldrán chispas, y al matarlo habrá explosiones y -con cierta probabilidad- incendios que pueden propagarse y afectar a otros personajes. Con el generación de los robots habrá mucha luz, sonido y descargas eléctricas.

----

# Proceso

## Preproducción (Dec 4)

#### Prototipos
Para tener un poco más claro la idea de los efectos, hicimos en clase un proyecto usando el Niagara system de ue4. Cuando el personaje está corriendo, queremos que sale una nube de polvo en el suelo, que se desaparece después de un tiempo. Aunque no utilizaremos este efecto en la practica, es bien entender como funciona.

También seguí este tutorial https://www.youtube.com/watch?v=92rag3qStI4, para intentar de hacer una animación con Mixamo.

#### Estética 
Ya que el juego ya estaba hecho, solo tuve que pensar en que herramientas debería usar para la animación y los efectos. Al fin decidí utilizar Mixamo, porque parece que tienen muchas animaciones, ya había podido encontrar animaciones para golpes y morirse.

Para la mayoría de los efectos, fui buscando en los content examples que tiene ue4. Los "effect gallery" y "lighting gallery" me han dado mucha inspiración sobre como hacer los efectos de electricidad y chispas, etc.

#### Planificación
Primero, tendré que mover el proyecto sin quedarme con todos los objetos que no necesito y que me dan los 22 GB de la practica 2. Después, me parece importante primero hacer todo - o casi todo - lo que pide la practica 4, antes de ir mejorando las cosas de la practica anterior. Así que empezaré con los efectos y animaciones, y después iré mejorando todo.


## Producción

#### Mover la practica 2 (Dec 3)
El emigrar el proyecto o un nuevo proyecto me ha costado más de lo que pensaba que iba a costar. Hubo problemas con el jugador que ya no entro en el juego al spawn, y el mapping de los teclados. Al fin todo se ha resuelto y ahora pesa menos el proyecto.

#### Resolver el color del arma (Dec 4)
Ya que era algo muy simple, lo he hecho antes de empezar con la practica de verdad. Querría que no se vuelve muy rojo demasiado temprano, pero no salió muy bien en la practica anterior. Así que ahora, el arma empieza a ponerse roja cuando solo quedan menos de 10 balas. Empiezas con 20, así que las primeras balas, el arma se queda el mismo color.

#### Animaciones (Dec 9)

##### El robot se muere
Primero, he buscado en Mixamo para una animación de alguien muriendo y cayéndose al suelo. Como quería seguir usando el robot que ya tenía, que usa un mannequin de ue4, he tenido que hacer un "retarget" de las animaciones. Para eso, he utilizado el tutorial https://www.youtube.com/watch?v=92rag3qStI4, en donde tuve que cambiar también unas cosas en el mapping del Mannequin. Así que antes de morirse de verdad, el robot hará esta animación. Tuve que añadir un notify para que el robot solo se muera antes de acabar con el animación, porque poner un "Destroy" en el mismo event graph donde llamas a la animación, destruye inmediatamente al robot (tendría que poner un delay, pero no me parecía la mejor solución).

##### El robot puede dar golpes
Para esto también he encontrado la animación en Mixamo, tenía que ser una animación que puede hacer un loop rápido, y que no dura como 4 segundos antes de regresar a su posición inicial. En el código, al darle daño al jugador, el robot tiene que ejecutar esta animación mientras está tocando el jugador (o luego el objeto que está en su camino).

##### Modos del robot: quieto, caminar y correr (herido vs. no herido)
Ya que ue4 ya cambia las animaciones de un personaje cuando va más rápido o más lento, solo tenía que cambiar la velocidad cuando el robot ha visto el jugador.

También querría al hacerle daño al robot, que se va moviendo de una manera herida. Por eso, he encontrado en Mixamo 3 animaciones que se pueden seguir el uno al otro: estando quieto, caminando y corriendo, todos de forma herida. Por eso, he creado un nuevo BlendSpace ThirdPerson_IdleRunInjured con las animaciones de los robots heridos y sus transiciones. En la animación ThirdPerson_AnimBP en el eventGraph tengo un variable isInjured que se cambia para ver cuantas vidas tiene el robot. En el animGraph he creado un nuevo stateMachine (injured vs. default) y he usado un BlendPosesByBool que depende del variable isInjured. Los dos estados injured y default están "synced" para tener una transición correcta.

#### Efectos visuales (Dec 10 - Dec 15)

##### Chispas al dañar los robots
Para esto fui al "effects gallery" de ue4 de content examples, y encontré algo que se llamaba "random sparks", era exactamente lo que necesitaba, con sonido y todo. Así que lo moví a mi proyecto, y activo las chispas cuando el robot está tocado con una bala del jugador. Ya que el event hit tiene un parámetro que da la dirección del hit, podría poner las chispas justo en esa dirección y ese lugar donde la bala ha tocado el robot.

##### Una explosión cuando se muere el robot
Para esto añadí una explosión al notify de la animación de morirse, para hacer la explosión al fin de la animación. Usé la explosión que ya estaba en el starter pack de ue4. 

##### Electricidad al generar un robot
Para esto, también usé los "random sparks" del effects gallery. También fui buscando para una luz parpadeante, o por lo menos una inspiración en el lightning gallery. Ahí encontré algo simular, pero con el logo de ue4. Lo que la luz usaba era un Lightning Function, lo cual he cambiado un poco para mi proyecto, y he agregado luces con ese lightning function al spawner. 

También he buscado en internet un sonido que puede ser el sonido del generador mientras está generando el robot, lo he importado en el proyecto y ya activo el sonido 4-5 segundos antes de que se aparece un robot.


##### Fuego después de la explosión
Para esto he encontrado un Particle System en los content examples, tienes que ponerlo en los huesos o socket del esqueleto del personaje. El juego dañará a los robots hasta que se mueren, el jugador solo perderá la mitad de sus vidas. Usando random integers, hay una posibilidad de que si o no coges fuego.

#### Resolver problemas de la practica anterior (Dec 14 - Dec 16)

##### Usar BehaviorTrees para los AIs
Tuve que cambiar la lógica a BehaviorTrees, no fue muy difícil, ya que es mucho más fácil y simple que intentar de hacer todo en Blueprints. Solo había un problema: el MoveTo no estaba funcionado en la parte Patrol del BehaviorTree. Por eso, he escrito mi propio MoveTo que funciona casi igual al MoveTo, solo que elige en el MoveTo mismo a donde ir (así que es más como un RandomMoveTo).

##### Un mecanismo de física
Para esto, elegí bloques que se pueden mover de forma física. Para el jugador era fácil: solo le cambié el PushForce para que ya no puede mover los bloques, solo los puede mover disparándolos porque los disparos tienen mucha fuerza.

Para el enemigo tuve que poner código en los bloques que reaccionan al ser golpeado por los robots.

##### Juntar los enemy classes
Ya que había cambiado mucho en el EnemyCharacter, me di cuenta de que es un poco "tonto" tener que hacerlo en el otro. Así que decidí juntarlos y borrar el StrongEnemyCharacter, porque ahora tienen mucho más código.

##### Personalizar el mundo
He puesto en barriles "Dest: Freya's robot factory" para verse un poco como acaban de llegar de una entrega. También hay un cartel que dice "Engineering departement F.R.E.Y.A" en el pasillo de la sala 2.

##### (Amplificar el escenario)
Al fin, no he llegado a esto, aunque hubiera sido bien para poner más generadores etc.


## Postproducción (Dec 17)

#### Bug durante el robot se muere
En ciertas situaciones el robot no se estaba muriendo y se quedó quieto. Tuve que buscar un poco que fue la razón, después me di cuenta de que eran más cosas que una que estaban causando el problema. Primero, al morirse no querría que había más overlapEvents con el TouchVolume, así que tuve que desactivarlo. Eso ya ayudo un poco, pero aún había algo mal. También cuando estaba golpeando a algo, tuve que pararse y hacer la animación de morir, sin embargo, había código que paraba esta animación y por eso no se moria. Así que he añadido un check para ver si se puede parar la animación o no.

#### Bug durante los golpes del robot
Había otro bug con los golpes del robot: a veces salieron None errors al llamar una función de lo que está golpeando el robot. Así que tuve que verificar si el objeto es válido (si sigue en overlap) o no.

#### Mejorar animación de fuego
Cuando se muere el robot en llamas, el fuego no estaba siguiendo la animación porque le hice el spawn del fuego en el cuerpo y no en un hueso o socket. Así que añadí un socket al esqueleto del robot para poner ahí el fuego.

#### Destruir el spawner
Por alguna razón ya no se podía destruir los spawners, tuve que jugar un poco con los colission settings del FirstPersonProjectile y del collisionBox del spawner.

----

# Diseño del juego 
## Jugabilidad

### Mecánica
**Salud**
- El jugador tiene 10 vidas 
- Al tocar un robot, el jugador pierde una vida. Después sigue perdiendo vidas cada 1 segundo.
- El jugador recupera vida cada 5 segundos.
- Al estar en llamas, el jugador pierde 4 vidas.

**Combate**
- El jugador pierde balas mientras está disparando.
- Se puede matar a los robots disparándolos 3 veces.
- Se puede destruir los spawners disparándolos 3/4/5 veces (depende del nivel).
- Al destruir los robots, puede ser que habrá un fuego que daña al jugador y los robots si están demasiado cerca.
- Los robots mueren después de algunos segundos en llamas, pero pueden seguir atacando.
- El jugador podrá usar los cubos grandes para interrumpir el camino de los robots.

**Coleccionar**
- El jugador puede recoger munición caminando sobre el objeto o tocándolo.
- El jugador puede recoger tarjetas de entrada caminando sobre el objeto o tocándolo.
- El jugador puede recoger chips caminando sobre el objeto o tocándolo.
- Se puede abrir puertas si tiene una tarjeta de entrada.
- Se puede abrir la puerta final si tiene todos los chips.
- El jugador tiene que disparar a los cubos grande para pasar pasillos, ...

### Dinámica
- El jugador necesita evitar o matar a los robots para que no se muera. Necesita acumular munición para seguir disparando.
- Se necesita coleccionar tarjetas de entradas, para superar a la parte actual del mapa y seguir a otra parte.
- El jugador se va juntando todos los chips del nivel. Así podrá abrir la última puerta y acabar con el juego.
- El jugador podrá dañar varios robots de una vez, si destruye a un robot y la explosion (que a veces no hay) le afecta a los otros robots.

### Estética
- El mundo debería verse como una fábrica real, para que el jugador se siente realmente dentro de una fábrica de robots.
  - Ayudan los efectos electrónicos mientras se está generando un robot
  - Ayudan las chispas que le salen del robot al dispararle
  - Ayuda la explosion despues de destruir un robot
  - El fuego después de la explosion puede hacer que el jugador se siente más cuidadoso al destruir un robot
- El jugador necesita tener miedo de no saber de dónde vienen los robots, no debería ser obvio dónde está el spawner. Al descubrirlo se sentirá aliviado.
- Dará susto descubrir un robot fuerte detrás de una esquina, la apariencia de esos robots darán más miedo que los robots normales.
- En alguna parte el jugador puede abrir la puerta equivocada si va avanzando demasiado rápido, tendrá que volver lo que le da frustración pero también curiosidad por no haber descubierto algo antes.
- En alguna parte también hay que mirar bien que no se ha perdido un chip que está un poco escondido.  Aquí también tendrá que regresar, para buscarlo. Si ha acabado con todos los spawners se sentirá tranquilo, sin mucho apuro, si no será más miedoso y difícil.
- El acercarse de los robots al jugador tiene que darle miedo, cuando está perdiendo vidas también habrá un efecto de la vista que se da cuenta de que se va a perder su vida.




## Contenido
Todas las siguientes partes se encuentra en el wiki:  https://github.com/DEV21-G07/practica4/wiki/Las-pruebas
### Los enemigos
### Los objetos especiales 
### Los niveles


# El proyecto

### De la practica 2:
El juego existe de un mundo virtual, lo cual debería verse como una fabrica de robots. En ese mundo, el jugador tiene que colectar algunos chips que contienen información sobre la fabrica, y llegar al fin para extraer esa información.

Para llegar al fin, el jugador tiene que recoger tarjetas que le dan entrada a diferentes partes de la fabrica, donde tiene que buscar los chips. Pero mientras está navegándose por la fabrica, el jugador va a encontrarse con robots que le quieren parar y matar.  Los robots perseguirán al jugador si lo pueden ver, si no siguen su camino a puntos fijos y a veces aleatorios (depende del tipo de enemigo - en mi juego hay dos tipos, lo que se explica en https://github.com/DEV21-G07/practica2/wiki/Las-pruebas en la parte sobre "Los enemigos").

El jugador puede disparar al robot para defenderse (pero lo mejor es evitarlos) y puede destruir los spawners de los robots para qué dejan de aparecer en el mundo. Disparando va perdiendo balas, por eso hay paquetes de munición que se puede recoger para tener más balas. Los robots también pueden dañar al jugador, quitándose las vidas. Después de un tiempo esas vidas se recuperan.

### Esta practica:
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

## Postproducción ()


----

# Diseño del juego 
## Jugabilidad

### Mecánica
**Salud**
- El jugador tiene 10 vidas 
- Al tocar un robot, el jugador pierde una vida. Después sigue perdiendo vidas cada 1 segundo.
- El jugador recupera vida cada 5 segundos.

**Combate**
- El jugador pierde balas mientras está disparando.
- Se puede matar a los robots disparándolos 3 veces.
- Se puede destruir los spawners disparándolos 3/4/5 veces (depende del nivel).

**Coleccionar**
- El jugador puede recoger munición caminando sobre el objeto o tocándolo.
- El jugador puede recoger tarjetas de entrada caminando sobre el objeto o tocándolo.
- El jugador puede recoger chips caminando sobre el objeto o tocándolo.
- Se puede abrir puertas si tiene una tarjeta de entrada.
- Se puede abrir la puerta final si tiene todos los chips.

### Dinámica
- El jugador necesita evitar o matar a los robots para que no se muera. Necesita acumular munición para seguir disparando.
- Se necesita coleccionar tarjetas de entradas, para superar a la parte actual del mapa y seguir a una otra parte.
- El jugador se va juntando todos los chips del nivel. Así podrá abrir la ultima puerta y acabar con el juego.

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

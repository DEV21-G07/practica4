# practica4

# El proyecto

De la practica 2:
El juego existe de un mundo virtual, lo cual debería verse como una fabrica de robots. En ese mundo, el jugador tiene que colectar algunos chips que contienen información sobre la fabrica, y llegar al fin para extraer esa información.

Para llegar al fin, el jugador tiene que recoger tarjetas que le dan entrada a diferentes partes de la fabrica, donde tiene que buscar los chips. Pero mientras está navegándose por la fabrica, el jugador va a encontrarse con robots que le quieren parar y matar.  Los robots perseguirán al jugador si lo pueden ver, si no siguen su camino a puntos fijos y a veces aleatorios (depende del tipo de enemigo - en mi juego hay dos tipos, lo que se explica en https://github.com/DEV21-G07/practica2/wiki/Las-pruebas en la parte sobre "Los enemigos").

El jugador puede disparar al robot para defenderse (pero lo mejor es evitarlos) y puede destruir los spawners de los robots para qué dejan de aparecer en el mundo. Disparando va perdiendo balas, por eso hay paquetes de munición que se puede recoger para tener más balas. Los robots también pueden dañar al jugador, quitándose las vidas. Después de un tiempo esas vidas se recuperan.

----

# Proceso

## Preproducción ()

#### Prototipos

#### Estética 


#### Planificación

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

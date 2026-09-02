# Reporte

## Mi diseño

```
P . . .
. . G P
P . . .
> . . W
```

 Esto representa: > = agente, P = pit, W = wumpus, G = oro.

## Observaciones

En el mapa que diseñé, los agentes que lograron encontrar el oro y salir de la cueva fueron el agente basado en utilidad y el agente de aprendizaje. Los agentes de reflejo simple, basado en modelo y basado en objetivos no lograron completar el recorrido en la configuración original del mapa.

En el caso del agente de reflejo simple, considero que falla principalmente por la forma en que está construido y por la posición del Pit. Como coloqué un Pit en la casilla [1,2], el agente empieza detectando una brisa desde [1,1]. De acuerdo con la lógica del agente, cuando percibe esta condición su acción es girar a la derecha. El problema es que no tiene suficiente información para tomar otra decisión, por lo que termina girando en el mismo lugar y entra en un ciclo hasta que se terminan sus pasos. En este diseño no tuvo suerte, ya que desde la primera casilla quedó prácticamente bloqueado.

El agente basado en modelo se comportó de una manera muy similar en mi mapa. La diferencia es que mantiene un historial de lo que va percibiendo, pero como desde el inicio solamente conoce [1,1] y esa casilla tiene una brisa, no cuenta con una alternativa segura para comenzar a explorar. Por eso tampoco logra avanzar. Algo parecido ocurre con el agente basado en objetivos en esta configuración.

Al mover el Pit, el resultado del agente basado en modelo cambia bastante. Cuando el Pit está en [1,2], la brisa aparece desde la casilla inicial y limita el movimiento del agente. En cambio, cuando moví el primer Pit a [1,3], la casilla [1,2] deja de representar un peligro inmediato y el agente puede avanzar, acumular información y explorar la cueva. Con esta modificación logró encontrar el oro y salir de la cueva en 35 pasos. Esto muestra que, en este tipo de agente, la información disponible al inicio y la posición de los peligros influyen mucho en su capacidad para explorar.

Por otro lado, el agente basado en utilidad tardó 26 pasos. En mi interpretación, hace una especie de escaneo: recorre las filas, detecta riesgos y va regresando cuando encuentra condiciones que no puede resolver directamente. Finalmente encuentra el oro en [3,3] y regresa por el mismo camino. El agente de aprendizaje fue el más eficiente en mi diseño, ya que completó el recorrido en solo 14 pasos. Aprovechó la información obtenida durante el recorrido y tomó prácticamente el camino más óptimo de la cueva.

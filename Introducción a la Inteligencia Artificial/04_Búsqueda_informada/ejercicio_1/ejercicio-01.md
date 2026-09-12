# Ejercicio 1 — Comparar Greedy y A* en el mapa de Rumania

## Contexto

En el proyecto `Búsqueda informada/project` (AIMA cap. 3–4, Figuras 3.2 y 3.22)
se resuelve el problema de **encontrar una ruta** entre dos ciudades del mapa
carretero de Rumania. Dos algoritmos de búsqueda **informada** comparten el
mismo grafo, el mismo `RouteFindingProblem` y la misma heurística `h(n)`:

| Programa | Algoritmo | Qué optimiza (o no) |
|---|---|---|
| `03_greedy_best_first_search.py` | Greedy best-first | Expande el menor `h(n)` (sin garantía de optimalidad) |
| `04_a_star_search.py` | A* | Expande el menor `f(n) = g(n) + h(n)` (óptimo si `h` es admisible) |

El caso por defecto es **Arad → Bucharest**. En este ejercicio **no vas a
programar** los algoritmos: vas a **elegir otra pareja origen–destino**,
ejecutar ambos métodos y **explicar** por qué coinciden o discrepan.

Los vecinos se expanden en **orden alfabético**, así que los resultados son
deterministas si usas la misma pareja de ciudades.

A* (y Greedy) necesitan `h(n)` = estimado desde **cualquier ciudad** hasta el
destino que elegiste. Eso ya está resuelto: no implementas `h`. Al pasar
`--to DESTINO`, `heuristic_for` construye `h(ciudad)` para las 20 ciudades:

- Si el destino es **Bucharest**, usa la **distancia en línea recta** de la
  tabla AIMA (admisible y consistente).
- Si el destino es **cualquier otra ciudad**, usa la **distancia euclidiana**
  entre las coordenadas del mapa (también admisible: nunca sobreestima el
  costo por carretera).

Puedes verificarlo con `python 02_heuristics.py --to DESTINO`: imprime `h`
de cada ciudad hacia ese destino.

## Objetivo

Elegir una ruta distinta de Arad → Bucharest, inspeccionar `h(n)`, correr
Greedy y A*, y analizar diferencias de camino, costo, profundidad y nodos
expandidos a la luz de `g`, `h` y `f`.

## Resultados

La ruta elegida es la misma utilizada en el ejercicio anterior de Zerind a Giurgiu.

- `Zerind` → `Giurgiu`

Desde Zerind existen las siguientes conexiones:

```text
Zerind → Arad       75 km
Zerind → Oradea     71 km
```

Giurgiu está conectado con:

```text
Giurgiu → Bucharest 90 km
```


### Diagrama
```text
                              Zerind
                                 |
                               Arad
                                 |
                               Sibiu
                              /     \
                             /       \
                       Fagaras      Rimnicu Vilcea
                          |                |
                          |              Pitesti
                          |                |
                          |    ←───────────               
                       Bucharest           
                          |                
                       Giurgiu 
```
La ruta encontrada por Greedy fue:

```text
Zerind → Arad → Sibiu → Fagaras → Bucharest → Giurgiu
```

La ruta encontrada por A* fue:

```text
Zerind → Arad → Sibiu → Rimnicu Vilcea → Pitesti → Bucharest → Giurgiu
```

## Heurística

Los valores obtenidos con:

```bash
python 02_heuristics.py --from-city Zerind --to Giurgiu
```

fueron:

| Ciudad         | h(n) |
|----------------|-----:|
| Giurgiu        |    0 |
| Bucharest      |   62 |
| Pitesti        |  112 |
| Urziceni       |  114 |
| Craiova        |  123 |
| Hirsova        |  178 |
| Eforie         |  188 |
| Fagaras        |  192 |
| Rimnicu Vilcea |  199 |
| Drobeta        |  212 |
| Mehadia        |  218 |
| Vaslui         |  220 |
| Lugoj          |  237 |
| Sibiu          |  251 |
| Iasi           |  256 |
| Neamt          |  269 |
| Timisoara      |  314 |
| Arad           |  360 |
| Zerind         |  373 |
| Oradea         |  387 |

Para este ejercicio son especialmente importantes:

```text
Arad             h = 360
Sibiu            h = 251
Fagaras          h = 192
Rimnicu Vilcea   h = 199
Pitesti          h = 112
Bucharest        h = 62
Giurgiu          h = 0
```

#### Greedy - Greedy Best-First Search

El comando utilizado fue:

```bash
python 03_greedy_best_first_search.py --from-city Zerind --to Giurgiu
```

El resultado obtenido fue:

| **Dato**      | **Resultado**                                         |
|---------------|-------------------------------------------------------|
| **Algorithm** | Greedy best-first search                              |
| **Problem**   | Zerind → Giurgiu                                      |
| **Status**    | Success                                               |
| **Path**      | Zerind → Arad → Sibiu → Fagaras → Bucharest → Giurgiu |
| **Depth**     | 5 roads                                               |
| **Cost**      | 615 km                                                |
| **Expanded**  | 5 nodes                                               |
| **Generated** | 16 nodes                                              |
| **Frontier**  | Max size 6                                            |

La información de `g`, `h` y `f` fue:

| City       |   g |   h |   f |
|------------|----:|----:|----:|
| Zerind     |   0 | 373 | 373 |
| Arad       |  75 | 360 | 435 |
| Sibiu      | 215 | 251 | 466 |
| Fagaras    | 314 | 192 | 506 |
| Bucharest  | 525 |  62 | 587 |
| Giurgiu    | 615 |   0 | 615 |

La ruta encontrada fue:

```text
Zerind → Arad → Sibiu → Fagaras → Bucharest → Giurgiu
```

con un costo de 615 km

#### A* - A* Search

El comando utilizado fue:

```bash
python 04_a_star_search.py --from-city Zerind --to Giurgiu
```

El resultado obtenido fue:

| **Dato**      | **Resultado**                                                          |
|---------------|------------------------------------------------------------------------|
| **Algorithm** | A* search                                                              |
| **Problem**   | Zerind → Giurgiu                                                       |
| **Status**    | Success                                                                |
| **Path**      | Zerind → Arad → Sibiu → Rimnicu Vilcea → Pitesti → Bucharest → Giurgiu |
| **Depth**     | 6 roads                                                                |
| **Cost**      | 583 km                                                                 |
| **Expanded**  | 11 nodes                                                               |
| **Generated** | 31 nodes                                                               |
| **Frontier**  | Max size 4                                                             |

La información de `g`, `h` y `f` fue:

| City           | g   | h   | f   |
|----------------|----:|----:|----:|
| Zerind         |   0 | 373 | 373 |
| Arad           |  75 | 360 | 435 |
| Sibiu          | 215 | 251 | 466 |
| Rimnicu Vilcea | 295 | 199 | 494 |
| Pitesti        | 392 | 112 | 504 |
| Bucharest      | 493 |  62 | 555 |
| Giurgiu        | 583 |   0 | 583 |

La ruta encontrada fue:

```text
Zerind → Arad → Sibiu → Rimnicu Vilcea → Pitesti → Bucharest → Giurgiu
```

con un costo de 583 km

#### Tabla comparativa

| Algoritmo  | Status   | Depth   |       Cost | Expanded   | Generated   | Frontier máx.   |
|------------|----------|--------:|-----------:|-----------:|------------:|----------------:|
| **Greedy** | Success  |       5 |     615 km |          5 |          16 |               6 |
| **A***     | Success  |       6 |     583 km |         11 |          31 |               4 |

La diferencia principal es:

```text
Greedy → 5 carreteras → 615 km

A*     → 6 carreteras → 583 km
```

Greedy y A no devolvieron el mismo camino.

#### Resultados de Greedy

Una de las principales diferencias observadas está después de llegar a Sibiu.

Desde Sibiu, dos de las opciones que llevan hacia el destino son:

```text
Sibiu → Fagaras
Sibiu → Rimnicu Vilcea
```

Los valores de la heurística son:

| Ciudad         |   h(n) |
|----------------|-------:|
| Fagaras        |    192 |
| Rimnicu Vilcea |    199 |

Greedy selecciona el nodo con menor `h(n)`.

Por lo tanto:

```text
Fagaras         h = 192
Rimnicu Vilcea  h = 199
```

Como:

```text
192 < 199
```

Greedy selecciona Fagaras

La ruta continúa:

```text
Sibiu → Fagaras → Bucharest → Giurgiu
```

y termina con:

```text
Cost = 615 km
```
#### Análisis de A*
A* utiliza:

```text
f(n) = g(n) + h(n)
```

Por lo tanto, no solamente considera qué tan cerca parece estar una ciudad del destino, sino también cuánto ha costado llegar hasta ella.

Para Fagaras:

```text
g(Fagaras) = 314 km
h(Fagaras) = 192 km

f(Fagaras) = 314 + 192
f(Fagaras) = 506
```

Para Rimnicu Vilcea:

```text
g(Rimnicu Vilcea) = 295 km
h(Rimnicu Vilcea) = 199 km

f(Rimnicu Vilcea) = 295 + 199
f(Rimnicu Vilcea) = 494
```

La comparación queda:

```text
Fagaras
f = 506

Rimnicu Vilcea
f = 494
```

Aunque Rimnicu Vilcea tiene una `h(n)` ligeramente mayor, su `f(n)` es menor.

Por eso A* selecciona:

```text
Rimnicu Vilcea
```

y continúa por:

```text
Rimnicu Vilcea → Pitesti → Bucharest → Giurgiu
```

---

##### Greedy vs A*

Greedy encontró:

```text
Zerind → Arad → Sibiu → Fagaras → Bucharest → Giurgiu
```

con 615 km.

A* encontró:

```text
Zerind → Arad → Sibiu → Rimnicu Vilcea → Pitesti → Bucharest → Giurgiu
```

con 583 km.

La diferencia es:

```text
615 - 583 = 32 km
```

Por lo tanto, A* encontró una ruta 32 km más corta que Greedy.

Aunque A* utiliza una ruta con una carretera adicional:

```text
Greedy → 5 carreteras
A*     → 6 carreteras
```

el costo total es menor:

```text
Greedy → 615 km
A*     → 583 km
```

Esto demuestra que tener menos carreteras no necesariamente significa recorrer menos kilómetros.

##### Heurística es admisible.

La heurística utilizada es la distancia euclidiana desde cada ciudad hasta Giurgiu.

Una heurística admisible no sobreestima el costo real necesario para llegar al objetivo.

En este ejercicio:

```text
h(n) ≤ costo real mínimo hasta Giurgiu
```

Por lo tanto, la heurística puede ser utilizada por A* para encontrar una solución óptima en términos de costo.

Sin embargo, que la heurística sea admisible no significa que Greedy siempre encuentre el camino óptimo.

Esto ocurre porque Greedy solamente utiliza `h(n)` y no utiliza `g(n)`.


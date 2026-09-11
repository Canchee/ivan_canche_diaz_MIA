# Ejercicio 1 — Comparar BFS, UCS, DFS, DLS e IDS en el mapa de Rumania

## Contexto

En el proyecto `Búsqueda no informada/project` (AIMA cap. 3, Figura 3.2) se
resuelve el problema de **encontrar una ruta** entre dos ciudades del mapa
carretero de Rumania. Cinco algoritmos de búsqueda **no informada** comparten
el mismo grafo y el mismo `RouteFindingProblem`:

| Programa | Algoritmo | Qué optimiza (o no) |
|---|---|---|
| `02_breadth_first_search.py` | BFS | Menor número de **carreteras** (hops) |
| `03_uniform_cost_search.py` | UCS | Menor costo en **km** |
| `04_depth_first_search.py` | DFS | Ninguna garantía de optimalidad |
| `05_depth_limited_search.py` | DLS | DFS con límite de profundidad |
| `06_iterative_deepening_search.py` | IDS | Misma optimalidad de hops que BFS |

El caso por defecto es **Arad → Bucharest**. En este ejercicio **no vas a
programar** los algoritmos: vas a **elegir otra pareja origen–destino**,
ejecutar los cinco métodos y **explicar** por qué coinciden o discrepan.

Los vecinos se expanden en **orden alfabético**, así que los resultados son
deterministas si usas la misma pareja de ciudades.

## Objetivo

Elegir una ruta distinta de Arad → Bucharest, correr BFS, UCS, DFS, DLS e IDS,
y analizar diferencias de camino, costo, profundidad y nodos expandidos.

## Resultados

La ruta elegida es de Zerind a Giurgiu.

- `Zerind` → `Giurgiu`

Diagrama
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
Existen otras rutas para llegar a Giurgiu, pero no fueron exploradas por los algoritmos, dichas rutas no son óptimas para llegar al destino..

Los siguientes algoritmos fueron ejecutados

```bash
python 02_breadth_first_search.py --from-city Zerind --to Giurgiu
python 03_uniform_cost_search.py  --from-city Zerind --to Giurgiu
python 04_depth_first_search.py   --from-city Zerind --to Giurgiu
python 05_depth_limited_search.py --from-city Zerind --to Giurgiu --limit 2
python 05_depth_limited_search.py --from-city Zerind --to Giurgiu --limit 4
python 06_iterative_deepening_search.py --from-city Zerind --to Giurgiu
```

Los resultados obtenidos de ejecutar los algoritmos son los siguientes.
### BFS - Breadth-First Search

| **Dato**      | **Resultado**                                         |
|---------------|-------------------------------------------------------|
| **Algorithm** | Breadth-first search                                  |
| **Problem**   | Zerind → Giurgiu                                      |
| **Status**    | Success                                               |
| **Path**      | Zerind → Arad → Sibiu → Fagaras → Bucharest → Giurgiu |
| **Depth**     | 5 roads                                               |
| **Cost**      | 615 km                                                |
| **Expanded**  | 9 nodes                                               |
| **Generated** | 23 nodes                                              |
| **Frontier**  | Max size 4                                            |

### UCS -  Uniform-Cost Search

| **Dato**      | **Resultado**                                                          |
|---------------|------------------------------------------------------------------------|
| **Algorithm** | Uniform-cost search                                                    |
| **Problem**   | Zerind → Giurgiu                                                       |
| **Status**    | Success                                                                |
| **Path**      | Zerind → Arad → Sibiu → Rimnicu Vilcea → Pitesti → Bucharest → Giurgiu |
| **Depth**     | 6 roads                                                                |
| **Cost**      | 583 km                                                                 |
| **Expanded**  | 14 nodes                                                               |
| **Generated** | 38 nodes                                                               |
| **Frontier**  | Max size 4                                                             |

### DFS - Depth-First Search

| **Dato**       | **Resultado**                                         |
|----------------|-------------------------------------------------------|
| **Algorithm**  | Depth-first search                                    |
| **Problem**    | Zerind → Giurgiu                                      |
| **Status**     | Success                                               |
| **Path**       | Zerind → Arad → Sibiu → Fagaras → Bucharest → Giurgiu |
| **Depth**      | 5 roads                                               |
| **Cost**       | 615 km                                                |
| **Expanded**   | 5 nodes                                               |
| **Generated**  | 16 nodes                                              |
| **Frontier**   | Max size 6                                            |

### DLS - Depth-Limited Search - Limit 2

| **Dato**      | **Resultado**        |
|---------------|----------------------|
| **Algorithm** | Depth-limited search |
| **Problem**   | Zerind → Giurgiu     |
| **Status**    | Cutoff               |
| **Path**      | NA                   |
| **Depth**     | NA                   |
| **Cost**      | NA                   |
| **Expanded**  | 3 nodes              |
| **Generated** | 8 nodes              |
| **Frontier**  | Max size 5           |
| **Detail**    | Limit 2              |

### DLS - Depth-Limited Search - Limit 4

| **Dato**      | **Resultado**        |
|---------------|----------------------|
| **Algorithm** | Depth-limited search |
| **Problem**   | Zerind → Giurgiu     |
| **Status**    | Cutoff               |
| **Path**      | NA                   |
| **Depth**     | NA                   |
| **Cost**      | NA                   |
| **Expanded**  | 13 nodes             |
| **Generated** | 35 nodes             |
| **Frontier**  | Max size 7           |
| **Detail**    | Limit 4              |

### DLS - Depth-Limited Search - Limit 5

| **Dato**      | **Resultado**                                         |
|---------------|-------------------------------------------------------|
| **Algorithm** | Depth-limited search                                  |
| **Problem**   | Zerind → Giurgiu                                      |
| **Status**    | Success                                               |
| **Path**      | Zerind → Arad → Sibiu → Fagaras → Bucharest → Giurgiu |
| **Depth**     | 5 roads                                               |
| **Cost**      | 615 km                                                |
| **Expanded**  | 5 nodes                                               |
| **Generated** | 8 nodes                                               |
| **Frontier**  | Max size 9                                            |
| **Detail**    | Limit 5                                               |

### IDS - Iterative Deepening Search

| **Dato**      | **Resultado**                                         |
|---------------|-------------------------------------------------------|
| **Algorithm** | Iterative deepening search                            |
| **Problem**   | Zerind → Giurgiu                                      |
| **Status**    | Success                                               |
| **Path**      | Zerind → Arad → Sibiu → Fagaras → Bucharest → Giurgiu |
| **Depth**     | 5 Roads                                               |
| **Cost**      | 615 km                                                |
| **Expanded**  | 28 nodes                                              |
| **Generated** | 73 nodes                                              |
| **Frontier**  | Max size 9                                            |

## Tabla comparativa

| Algoritmo       | Status  | Depth |   Cost | Expanded | Generated | Frontier máx. |
|-----------------|---------|------:|-------:|---------:|----------:|--------------:|
| **BFS**         | Success |     5 | 615 km |        9 |        23 |             4 |
| **UCS**         | Success |     6 | 583 km |       14 |        38 |             4 |
| **DFS**         | Success |     5 | 615 km |        5 |        16 |             6 |
| **DLS limit 2** | Cutoff  |   N/A |    N/A |        3 |         8 |             5 |
| **DLS limit 4** | Cutoff  |   N/A |    N/A |       13 |        35 |             7 |
| **DLS limit 5** | Success |     5 | 615 km |        5 |         8 |             9 |
| **IDS**         | Success |     5 | 615 km |       28 |        73 |             9 |

## Análisis BFS vs UCS

Una de las principales diferencias observadas está entre BFS y UCS.

### BFS

```text
Zerind → Arad → Sibiu → Fagaras → Bucharest → Giurgiu
```

- 5 carreteras
- 615 km

### UCS

```text
Zerind → Arad → Sibiu → Rimnicu Vilcea → Pitesti → Bucharest → Giurgiu
```

- 6 carreteras
- 583 km

La razón de esta diferencia es que BFS considera principalmente la profundidad, mientras que UCS considera el costo acumulado de cada camino.

En otras palabras
BFS pregunta:
¿Cuál es el camino que llega al objetivo utilizando menos carreteras?

Mientras que
UCS pregunta:
¿Cuál es el camino cuyo costo total en kilómetros es menor?

Por eso es posible que UCS seleccione un camino con más carreteras, siempre que la suma de sus distancias sea menor.

En este ejercicio se observa exactamente ese comportamiento:

```text
BFS - 5 carreteras - 615 km
UCS - 6 carreteras - 583 km
```

Por lo tanto, BFS encontró el camino con menos carreteras, mientras que UCS encontró el camino con menos kilómetros.

## Análisis DFS

DFS explora el espacio de búsqueda siguiendo una rama hasta profundizar lo máximo posible antes de regresar y probar otras alternativas.

A diferencia de BFS, DFS no tiene como objetivo encontrar la solución con menor número de carreteras.

Por ello, si existen más caminos, por ejmplo:

```text
Camino A - 3 carreteras
Camino B - 8 carreteras
```

DFS podría explorar primero el Camino B y encontrar una solución antes de regresar para investigar el Camino A.

En esta ejecución, DFS encontró la misma ruta que BFS:

```text
Zerind → Arad → Sibiu → Fagaras → Bucharest → Giurgiu
```

En total 5 carreteras.

Esto es consecuencia del orden de expansión de los vecinos y de su estructura. No significa que DFS sea óptimo.

## Análisis DLS

DLS permite controlar hasta qué profundidad puede buscar el algoritmo.

En este ejercicio se probaron tres límites:

```text
Limit 2 - Cutoff
Limit 4 - Cutoff
Limit 5 - Success
```

La relación con BFS e IDS es directa.
BFS e IDS encontraron una solución con:

```text
Depth = 5
```

Por lo tanto:

- Un límite menor que 5 no permite alcanzar esa solución.
- Un límite igual a 5 permite alcanzar la solución.
- El experimento confirmó esto directamente con DLS.

El comportamiento observado puede representarse como:

```text
Profundidad

0
│
├── 1
│
├── 2  ← DLS limit 2: CUTOFF
│
├── 3
│
├── 4  ← DLS limit 4: CUTOFF
│
└── 5  ← DLS limit 5: SUCCESS
             │
             └── Giurgiu
```

# Ejercicio 1 — Separar los blobs y volver a elegir \(k\)

## Contexto

La notebook `Clustering K-medias/Notebooks/01 K-medias.ipynb` (capítulo de
Géron / Hands-On ML) entrena **k-means** de scikit-learn sobre nubes
gaussianas y termina con segmentación de color de una foto.

La parte central genera **5** blobs, ajusta `KMeans(n_clusters=5, ...)` y
después busca el \(k\) “bueno” con dos herramientas:

| Herramienta | Qué grafica | Lectura en la notebook original |
|---|---|---|
| **Codo** (inercia \(J\) vs \(k\)) | `inertias` para \(k = 1,\ldots,9\) | El codo está en **\(k = 4\)**, no en 5 |
| **Silueta** | `silhouette_score` para \(k = 2,\ldots,9\) | \(k = 4\) se ve muy bien; **\(k = 5\)** también |

Eso no es un bug: tres blobs de la izquierda están **casi pegados**
(`std = 0.1` y centros en \(x = -2.8\)). K-means (y el codo) los trata como
un solo grupo.

En este ejercicio **sí vas a modificar código**, pero un cambio pequeño y
local: **alejar esos blobs**. No toques `Clustering K-medias/project/`.
Trabajas en **Colab**, sobre una **copia** de la notebook.

## Objetivo

Correr la notebook en Colab **tal como está**, anotar el \(k\) que sugieren
codo y silueta, **separar los 5 blobs** en el arreglo `blob_centers` (y, si
hace falta, `blob_std`) y volver a graficar. Debes ver si el codo y la
silueta se mueven hacia **\(k = 5\)**.

## Resultados

### Notebook en Google Colab

[Ver notebook en Google Colab](https://colab.research.google.com/drive/1a0BgOEj0ePjGWh1ofJPisLpSvq4pUc05?usp=sharing)


### Primera corrida - datos originales

Primero ejecuté la notebook original completa (`Run all`) sin modificar los datos.

Los resultados de esta corrida se guardaron en la carpeta:

```text
First run/
```

#### Resultados de inercia

```text
Inercia k=3: 653.2167190021554
Inercia k=5: 224.0743312251571
Inercia k=8: 127.13141880461835
```

#### Codo

Al observar la gráfica de inercia, el codo se encuentra en:

```text
k = 4
```

#### Silueta

El valor máximo de la silueta también se encuentra en:

```text
k = 4
```

con un valor aproximado de:

```text
0.6885
```

### Centros originales

Los centros originales utilizados por `make_blobs` son:

```python
blob_centers = np.array([
    [ 0.2,  2.3],
    [-1.5,  2.3],
    [-2.8,  1.8],
    [-2.8,  2.8],
    [-2.8,  1.3]
])
```

Los valores de `blob_std` originales son:

```python
blob_std = np.array([0.4, 0.3, 0.1, 0.1, 0.1])
```

#### Representación aproximada de los centros originales

```text
x₂
 ↑
3.0 |
2.8 |   ● C4 (-2.8, 2.8)
    |
2.3 |          ● C2 (-1.5, 2.3)        ● C1 (0.2, 2.3)
    |
1.8 |   ● C3 (-2.8, 1.8)
    |
1.3 |   ● C5 (-2.8, 1.3)
    |
    +------------------------------------------------→ x₁
       -3       -2       -1        0        1
```

Se puede observar que los tres centros de la izquierda tienen la misma coordenada:

```text
x = -2.8
```

Además, sus desviaciones estándar son pequeñas:

```text
std = 0.1
```

Esto hace que los tres blobs estén muy cerca entre sí.

### Problema observado en los datos originales

Aunque `make_blobs` genera 5 centros, los tres blobs de la izquierda están muy agrupados.

Al aumentar `k`:

```text
k = 3 → k = 4
```

se obtiene una reducción importante de la inercia.

Pero al pasar de:

```text
k = 4 → k = 5
```

la mejora es mucho menor.

Por esta razón, el método del codo identifica:

```text
k = 4
```

y la silueta también tiene su máximo en:

```text
k = 4
```

K-Means sí calcula las distancias correctamente, pero la distribución de los datos hace que separar los tres blobs de la izquierda no produzca una mejora suficientemente grande como para que el algoritmo los identifique como tres grupos independientes.

### Segunda corrida - Custom blobs

Para la segunda corrida conservé:

```text
n_samples = 2000
random_state = 7
```

y los mismos parámetros de K-Means.

Solamente cambié los centros y la dispersión de los blobs.

Los resultados de esta corrida se guardaron en:

```text
Custom run/
```

#### Centros propuestos

Utilicé los siguientes centros:

```python
my_centers = np.array([
    [-2.8, 1.8],
    [-2.0, 2.8],
    [-1.3, 1.5],
    [ 0.0, 2.6],
    [ 0.9, 1.3]
])
```

#### Desviaciones estándar

```python
my_std = np.array([
    0.45,
    0.25,
    0.25,
    0.35,
    0.25
])
```

#### Representación aproximada de los centros propuestos

```text
x₂
 ↑
3.0 |
2.8 |          ● C2 (-2.0, 2.8)
    |
2.6 |                              ● C4 (0.0, 2.6)
    |
1.8 |   ● C1 (-2.8, 1.8)
    |
1.5 |                 ● C3 (-1.3, 1.5)
    |
1.3 |                                      ● C5 (0.9, 1.3)
    |
    +------------------------------------------------------→ x₁
       -3       -2       -1        0        1
```

La intención fue aumentar la separación entre los centros para que los cinco blobs pudieran distinguirse visualmente.

### Resultados de los datos modificados

Después de generar los nuevos datos, obtuve:

```text
Inercia k=3: 1276.719641956485

Inercia k=5: 373.088701688521

Inercia k=8: 265.91419828971215
```

#### Codo

La gráfica de inercia muestra un cambio importante alrededor de:

```text
k = 5
```

Después de `k=5`, las reducciones de la inercia son mucho menores.

#### Silueta

El resultado de la silueta fue:

```text
Max silhouette: k = 5
Score: 0.612047570819947
```

Por lo tanto:

```text
Máxima silueta → k = 5
```

Después de `k=5`, el valor de la silueta comienza a disminuir.

### Comparación de resultados

| Resultado         | First run   | Custom run |
|-------------------|------------:|-----------:|
| Inercia k=3       |    653.2167 |  1276.7196 |
| Inercia k=5       |    224.0743 |   373.0887 |
| Inercia k=8       |    127.1314 |   265.9142 |
| Codo              |         k=4 |        k=5 |
| Máxima silueta    |         k=4 |        k=5 |
| Silhouette máxima |      0.6885 |     0.6120 |

Las inercias de los datos modificados no tienen que ser menores que las originales. Lo importante en este ejercicio es observar cómo cambia la estructura de la curva al modificar la distribución de los datos.

### Comparación visual

En los datos originales, los tres blobs de la izquierda están muy juntos:

```text
Original

        ●
        │
        ●
        │
        ●
```

Esto hace que sea más difícil para K-Means distinguirlos como tres grupos separados.

En los datos modificados:

```text
Custom

       ●                    ●

                 ●

  ●                                      ●
```

los cinco grupos tienen una separación más clara.

Esto permite que K-Means encuentre una solución con 5 clusters que representa mejor la distribución de los datos.


### Conclusiones

#### 1. ¿Por qué los datos originales prefieren k=4?

Los datos originales prefieren `k=4` porque existen tres blobs muy agrupados en la parte izquierda. Al pasar de `k=3` a `k=4` se produce una reducción significativa de la inercia, pero al pasar de `k=4` a `k=5` la mejora es mucho menor. Esto ocurre porque los tres blobs de la izquierda están muy cerca entre sí y K-Means no encuentra suficiente separación entre ellos para considerarlos grupos completamente independientes.

La función de distancia de K-Means funciona correctamente, pero la distribución de los datos hace que separar esos tres blobs no produzca una mejora suficientemente grande.

#### 2. ¿Qué ocurrió al separar los blobs?

Al separar mis blobs, el codo queda más pronunciado alrededor de `k=5`. Al existir una mayor distancia entre los centros, K-Means puede distinguir mejor los cinco grupos y la reducción de la inercia al pasar a `k=5` es más significativa. Después de `k=5`, aumentar el número de clusters produce mejoras mucho menores.

#### 3. ¿Coinciden el codo y la silueta?

Sí. En mis datos ambos métodos coinciden en `k=5`.

El codo se encuentra en:

```text
k = 5
```

y la silueta alcanza su valor máximo en:

```text
k = 5
```

con un score de:

```text
0.6120
```

Después de `k=5`, el valor de la silueta disminuye.

#### 4. ¿Qué importancia tuvieron la distancia entre centros y `blob_std`?

Fue importante mantener una distancia suficiente entre los centros para evitar que las nubes se mezclaran. Cuando dos blobs están demasiado cerca y además tienen una dispersión grande, sus puntos pueden ocupar regiones similares y K-Means puede tener dificultades para distinguirlos como grupos independientes.

Al separar los centros y mantener un `std` relativamente pequeño, las cinco nubes quedan más claramente diferenciadas. Esto se refleja tanto en la gráfica como en los resultados del codo y la silueta.

---

### Resultado final

La primera corrida mostró:

```text
Codo       → k=4
Silueta    → k=4
```

Después de modificar la distribución de los blobs:

```text
Codo       → k=5
Silueta    → k=5
```

Por lo tanto, al modificar la posición de los centros y la dispersión de los blobs, conseguimos que la estructura de los datos sea más compatible con una solución de 5 clusters.

La comparación muestra que el número de clusters sugerido por K-Means depende de la distribución y separación de los datos, y no solamente del número de centros utilizado originalmente para generar los blobs.

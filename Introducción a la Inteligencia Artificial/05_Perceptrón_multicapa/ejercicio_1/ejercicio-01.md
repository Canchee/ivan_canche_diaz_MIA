# Ejercicio 1 — Más capas en el perceptrón multicapa (Iris)

## Contexto

En `Perceptrón multicapa/Notebooks/` hay dos notebooks que resuelven el mismo
problema: clasificar las **3 especies** del conjunto **Iris** (4 atributos:
sépalo/pétalo en largo y ancho). Ambas redes son un MLP con activación
**sigmoide**, error **MSE**, **SGD** con \(\eta = 0.03\) y **500 épocas**.

| Notebook                                        | Cómo está implementada                    | Topología inicial       |
|-------------------------------------------------|-------------------------------------------|-------------------------|
| `01 Multilayer perceptron.ipynb`                | A mano (NumPy): forward, error y backprop | \(4 \times 3 \times 3\) |
| `02 Keras - multilayer perceptron - iris.ipynb` | Keras / TensorFlow (`Sequential`)         | \(4 \times 3 \times 3\) |

En la notebook 01, \(4 \times 3 \times 3\) significa: **4** entradas, **una**
capa oculta de **3** neuronas y **3** neuronas de salida (una por clase). En
Keras es lo mismo: dos `Dense(3)` (la primera con `input_shape=(4,)`).

En este ejercicio **sí vas a modificar código**, pero no el de
`Perceptrón multicapa/project/`. Trabajas **en Colab**, sobre **copias** de las
dos notebooks.

## Objetivo

Correr ambas notebooks en **Google Colab** con la arquitectura original,
**agregar dos capas** a cada red, volver a entrenar y **comparar** qué cambia
(curva de error/pérdida, velocidad, calidad de la clasificación).

## Resultados

Se comparó la red original `4 × 3 × 3` con una red más profunda `4 × 3 × 3 × 3 × 3`, manteniendo sigmoide, MSE, `η = 0.03` y 500 épocas.
Buscamos observar si agregar capas mejora realmente el aprendizaje en el conjunto Iris.

| Implementación | Red original | Red profunda |
|----------------|--------------|--------------|
| **NumPy**      | 0.05976      | 0.15877      |
| **Keras**      | 0.18049      | 0.22031      |


Al agregar las dos capas ocultas, el error no bajó, sino que aumentó en ambas implementaciones. En NumPy pasó de `0.05976` a `0.15877`,
mientras que en Keras pasó de `0.18049` a `0.22031`. Por lo tanto, para esta configuración, la red original obtuvo mejores resultados.

Las curvas de NumPy y Keras con la misma topología tampoco son iguales. En NumPy la red original comienza con un error cercano a `0.9` y termina
en `0.05976`, mientras que Keras comienza alrededor de `0.28` y termina en `0.18049`. En la red profunda también se observa una diferencia:
NumPy presenta periodos donde el error se mantiene casi constante antes de volver a disminuir, mientras que Keras muestra una reducción más continua.

Estas diferencias pueden deberse a la forma en que están implementadas ambas redes, por ejemplo, la inicialización aleatoria de los pesos, 
el orden y procesamiento de los datos. Por esto, aunque ambas redes tienen la misma topología, no necesariamente tienen que producir la misma curva.

Finalmente, considero que el resultado tiene sentido al utilizar varias capas con sigmoide y MSE. 
Al aumentar la profundidad, los gradientes que se propagan hacia las primeras capas pueden hacerse cada vez más pequeños,
provocando algo que aprendí que se llama `vanishing gradient`.
Esto se puede relacionar con lo observado en las gráficas, especialmente con los periodos de poco aprendizaje de la red profunda de NumPy.

Por estas razones, agregar más capas no garantiza un mejor aprendizaje.
Con esta configuración, la red más profunda necesitó más esfuerzo para conseguir un resultado que aun así fue peor que el de la red original.


## Conclusión

La red `4 × 3 × 3` obtuvo menor error tanto en NumPy como en Keras. La red profunda sí logró aprender, pero su entrenamiento fue menos favorable. 
Esto muestra que la profundidad por sí sola no garantiza una mejora, especialmente cuando se utilizan sigmoides apiladas y MSE.

## Evidencias

### Enlaces de las notebooks modificadas

Las dos notebooks contienen las corridas originales y las corridas con la red profunda.

1. [Notebook 1 — Multilayer Perceptron](https://drive.google.com/file/d/1Dhe9ofeJX59o1KsWP1g1Q7uwG7O5_T_A/view?usp=sharing)
2. [Notebook 2 — Keras Multilayer Perceptron](https://drive.google.com/file/d/1xvqVvSKk9KVnzh_bRSiqrnGSuqqjcAGy/view?usp=sharing)

### Capturas de las cuatro corridas

#### 1. NumPy — Red original `4 × 3 × 3`

**Resultado final:**

```text
Error final: 0.05975627061971051
```

#### 2. NumPy — Red profunda `4 × 3 × 3 × 3 × 3`

**Resultado final:**

```text
Error final: 0.1587695986062239
```

#### 3.  Keras — Red original `4 × 3 × 3`

**Resultado final:**

```text
Loss final: 0.18048645555973053
```

### 4 Keras — Red profunda `4 × 3 × 3 × 3 × 3`

**Resultado final:**

```text
Loss final: 0.2203100621700287
```

###  `model.summary()` de Keras

#### Keras - Red original `4 × 3 × 3`

```text
Model: "sequential"

┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━┓
┃ Layer (type)                    ┃ Output Shape           ┃       Param # ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━┩
│ layer1 (Dense)                  │ (None, 3)              │            15 │
├─────────────────────────────────┼────────────────────────┼───────────────┤
│ layer2 (Dense)                  │ (None, 3)              │            12 │
└─────────────────────────────────┴────────────────────────┴───────────────┘

Total params: 27 (108.00 B)
Trainable params: 27 (108.00 B)
Non-trainable params: 0 (0.00 B)
```

#### Keras - Red profunda `4 × 3 × 3 × 3 × 3`

```text
Model: "sequential_1"

┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━┓
┃ Layer (type)                    ┃ Output Shape           ┃       Param # ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━┩
│ layer1 (Dense)                  │ (None, 3)              │            15 │
├─────────────────────────────────┼────────────────────────┼───────────────┤
│ layer2 (Dense)                  │ (None, 3)              │            12 │
├─────────────────────────────────┼────────────────────────┼───────────────┤
│ layer3 (Dense)                  │ (None, 3)              │            12 │
├─────────────────────────────────┼────────────────────────┼───────────────┤
│ layer4 (Dense)                  │ (None, 3)              │            12 │
└─────────────────────────────────┴────────────────────────┴───────────────┘

Total params: 51 (204.00 B)
Trainable params: 51 (204.00 B)
Non-trainable params: 0 (0.00 B)
```

### Resumen de resultados

| Implementación  | Arquitectura        | Error / Loss final  |
|-----------------|---------------------|--------------------:|
| NumPy           | `4 × 3 × 3`         |      **0.05975627** |
| NumPy           | `4 × 3 × 3 × 3 × 3` |      **0.15876960** |
| Keras           | `4 × 3 × 3`         |      **0.18048646** |
| Keras           | `4 × 3 × 3 × 3 × 3` |      **0.22031006** |
 
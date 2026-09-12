# Ejercicio 1 — Cambiar la imagen de predicción en YOLO

## Contexto

La notebook `Visión computacional/Notebooks/13 YOLO ultralytics.ipynb` es un
tutorial corto de **YOLOv8** (paquete Ultralytics) pensado para **Google
Colab**. Hace tres cosas:

1. Instala `ultralytics` y comprueba el entorno.
2. Corre inferencia por CLI sobre la foto de muestra `zidane.jpg`.
3. Carga `yolov8n.pt`, entrena **3 épocas** en `coco128` y predice
   `bus.jpg`.

YOLO detecta objetos de las clases **COCO** (persona, auto, bus, corbata,
etc.) y dibuja cajas. En este ejercicio **sí vas a modificar código**, pero
solo un cambio pequeño y visible: **la imagen sobre la que predice**.

No toques `Visión computacional/project/`. Trabajas en **Colab**, sobre una
**copia** de la notebook.

## Objetivo

Correr la notebook en Colab **tal como está**, sustituir las dos imágenes de
muestra por **una imagen tuya** (la misma en ambas predicciones) y comparar
qué objetos detecta YOLO en la foto original frente a la tuya.

## Resultados - Detección de objetos con YOLO

En este ejercicio se ejecutó YOLO sobre las imágenes originales proporcionadas por Ultralytics y posteriormente sobre una imagen propia. En la imagen de `zidane.jpg`, YOLO detectó `personas`(2) y una `corbata`(1). En la imagen de `bus.jpg`, detectó `personas`(4), un `autobús`(1) y una `señal de stop`(1).

Para la imagen propia utilicé una fotografía de mis perros:

- **Ronin:** perro blanco, mezcla de pitbull, ubicado a la izquierda de la fotografía.
- **Logan:** perro negro, Rottweiler, ubicado a la derecha de la fotografía.

La fotografía se utilizó para realizar las predicciones mediante las dos formas solicitadas: la celda CLI y `model(...)`.

En este caso, YOLO detectó la clase `dog`(2) para los perros y también detectó `skateboard`(1), aunque esta última detección corresponde a un falso positivo ya que en la imagen no hay patinetas. Esto muestra que el modelo puede realizar detecciones incorrectas dependiendo de las características de la imagen.

En la ejecución mediante la celda `CLI`, utilizando la misma fotografía, YOLO detectó 3 perros (`dog`) y 1 `skateboard`. Esto muestra que el modelo puede producir detecciones adicionales o diferentes dependiendo de la forma en que se realiza la inferencia.

También se observa que un objeto evidente de la fotografía, una cruz católica, no fue etiquetado por YOLO. Una posible explicación es que esta clase no se encuentra entre las categorías utilizadas por COCO, por lo que el modelo no tiene una clase específica para identificarla.

Finalmente, las predicciones realizadas mediante la celda `CLI` y mediante `model(...)` no coincidieron exactamente. La ejecución con `model(...)` detectó 2 perros y 1 skateboard, mientras que la ejecución `CLI` detectó 3 perros y 1 skateboard. Por lo tanto, aunque ambas identificaron las mismas clases generales, el número de detecciones fue diferente.

Las evidencias del ejercicio se encuentran en las carpetas correspondientes de este ejercicio.

## Tabla resumen de la imagen propia

| Elemento observado | Resultado                 |
|--------------------|---------------------------|
| Ronin (blanco)     | Detectado como `dog`      |
| Logan (negro)      | Detectado como `dog`      |
| Cruz católica      | No detectada              |
| Skateboard         | Detectada incorrectamente |
| CLI                | 3 `dog` + 1 `skateboard`  |
| `model(...)`       | 2 `dog` + 1 `skateboard`  |
 
## Conclusión

YOLO logró identificar correctamente los objetos principales de las imágenes utilizadas, especialmente las personas, el autobús y los perros. Sin embargo, también presentó un falso positivo al identificar una patineta que no aparece en la fotografía y no identificó la cruz presente en mi imagen. Además, las dos formas de realizar la predicción sobre la imagen propia produjeron resultados ligeramente diferentes. Esto demuestra que la detección depende de las clases conocidas por el modelo y de factores relacionados con la inferencia y el nivel de confianza de las detecciones.

## Notebook utilizado

[Ver notebook en Google Colab](https://colab.research.google.com/drive/1WC7GuRZul1p-pdp59d9-A1RkoDCI8pT8?usp=sharing)

Notebook con la ejecución original de YOLO y las modificaciones realizadas para realizar las predicciones utilizando mi propia imagen.

# Tarea 5 - Diseñar una CNN compacta con Global Average Pooling

Tarea de clasificación de imágenes con redes neuronales convolucionales, el objetivo es diseñar una CNN con Global Average Pooling (GAP) que supere el 95 % de exactitud en validación en MNIST usando menos de 54 330 parámetros entrenables, que es el total de la CNN base con Flatten. Entre las arquitecturas que cumplen ambos requisitos se elige la de menos parámetros. Después se mide qué tan bien reconoce los dígitos cuando cambia su posición.

Se entrenan doce variantes de la CNN con GAP. Cambian el número de filtros, la profundidad, el tamaño del kernel y la ubicación del pooling, e incluyen siete comparaciones en las que se cambia una sola decisión de diseño. Todas usan la misma configuración: Adam con tasa 0.001, lote de 128, 20 épocas y semilla 42. La selección se hace solo con la exactitud de validación. El conjunto de prueba se reserva para comparar Flatten base, GAP base y el GAP seleccionado ante desplazamientos de 0, 2 y 4 píxeles.

Esta práctica usa subconjuntos estratificados, con las mismas particiones del notebook de clase:

Entrenamiento: 8 000 imágenes tomadas del conjunto oficial de entrenamiento.
Validación: 1 500 imágenes tomadas también del conjunto oficial de entrenamiento. Se usan para elegir la arquitectura.
Prueba: 2 000 imágenes tomadas del conjunto oficial de prueba. Se usan solo para la comparación final.

A cada imagen se le añade un margen negro de cuatro píxeles por lado, por lo que la red recibe imágenes de 36 × 36 × 1. Este margen permite desplazar un dígito hasta cuatro píxeles hacia arriba, abajo, izquierda o derecha sin recortar la imagen original.

Las diez clases están prácticamente balanceadas, así que la métrica principal es la exactitud.

El notebook se organiza así:

Datos y modelos de referencia: carga de MNIST, particiones y reentrenamiento de la CNN + Flatten y la CNN + GAP base.
Exploración de arquitecturas con GAP: doce variantes, curvas de validación y comparaciones de una sola decisión.
Selección: la variante con menos parámetros entre las que superan el 95 % en validación.
Efecto del desplazamiento: exactitud en prueba a 0, 2 y 4 píxeles, gráfica con una curva por modelo y caída en puntos porcentuales.

## Requisitos de ejecución

* Python
* numpy
* pandas
* scikit-learn
* matplotlib
* tensorflow 
* Jupyter 

## Instrucciones

No es necesario descargar archivos de datos. La primera vez que se ejecuta, el notebook descarga MNIST automáticamente, por lo que se requiere conexión a internet. Abra el archivo Tarea_5.ipynb en Jupyter Notebook, instale las bibliotecas indicadas en los requisitos y ejecute las celdas en orden, de arriba hacia abajo.

# Declaración de uso de la IA

Para esta práctica se utilizó la inteligencia artificial Anthropic Claude como herramienta de asistencia para la revisión, edición y mejora del formato de texto así como el apoyo en la toma de sugerencias para la parte del código y la corrección de errores.

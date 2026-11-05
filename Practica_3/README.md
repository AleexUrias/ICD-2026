# Práctica 3 - Predicción temprana de deserción estudiantil

Práctica de clasificación supervisada: predecir, al cierre del primer semestre, la situación que tendrá un estudiante al final de la duración normal de su carrera: graduate (graduado), dropout (desertor) o enrolled (todavía inscrito).

Se comparan cinco clasificadores (árbol de decisión, Naive Bayes, k vecinos más cercanos, máquinas de soporte vectorial y regresión logística), cada uno optimizado con validación cruzada estratificada. La métrica principal es el F1 macro.

Descripción del dataset

Los datos provienen del dataset Predict Students' Dropout and Academic Success del repositorio UCI Machine Learning Repository (https://archive.ics.uci.edu/dataset/697). Son datos reales de 4 424 estudiantes de licenciatura del Instituto Politécnico de Portalegre (Portugal), que ingresaron entre los ciclos 2008/09 y 2018/19.

Esta práctica trabaja con dos archivos, ya separados:

desercion-entrenamiento.csv: 3 539 estudiantes con 36 atributos, más la columna id y la variable objetivo Target.
desercion-prueba.csv: 885 estudiantes con la columna id y solo los 30 atributos conocidos al cierre del primer semestre. No incluye Target ni los atributos del segundo semestre.

La variable objetivo está moderadamente desbalanceada en el conjunto de entrenamiento: Graduate representa alrededor del 50 %, Dropout el 32 % y Enrolled el 18 %.

Los atributos se agrupan así:

Demográficos y socioeconómicos: estado civil, nacionalidad, género, edad al ingreso, estudios y ocupación de los padres, becario, deudor, colegiaturas al corriente, desplazado, necesidades educativas especiales, estudiante internacional.
Ingreso: modo de solicitud, orden de solicitud, carrera, turno (diurno o vespertino), calificación previa y su nota, nota de admisión.
Macroeconómicos: tasa de desempleo, inflación y PIB.
Académicos del primer semestre: unidades curriculares acreditadas, inscritas, evaluadas, aprobadas, sin evaluación y nota promedio.
Académicos del segundo semestre: los mismos seis atributos. Solo existen en el conjunto de entrenamiento y se usan únicamente para estimar cuánto mejoraría el clasificador si se esperara un semestre más. El clasificador final no los usa.

Varios atributos nominales vienen codificados como números enteros (por ejemplo, la carrera o la ocupación de los padres). Esos códigos no tienen orden ni distancia, por lo que el notebook los trata como categorías. La descripción completa de cada atributo y de sus códigos está en la ficha del dataset en UCI.

## Requisitos de ejecución

* Python 
* numpy 
* pandas 
* scipy 
* scikit-learn 
* matplotlib
* Jupyter (jupyter, nbconvert e ipykernel) para abrir y ejecutar el notebook

## Intrucciones

Primero descargue los archivos llamados `desercion-prueba` y `desercion-entrenamiento` y adjuntelo en la misma carpeta del notebook, despues abrir el archivo Practica_3.ipynb para ello es necesario ya tener instalado Jupyter Notebook, instalar cualquier archivo complementario que requiera el archivo, y correr las celdas en orden descendente.

Realinho, V., Vieira Martins, M., Machado, J. y Baptista, L. (2021). Predict Students' Dropout and Academic Success [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5MC89

# Práctica 4 - Ensambles para la deserción estudiantil y Bank Marketing
 
Práctica de clasificación supervisada con ensambles. Responde dos preguntas: cuánto ganan los ensambles sobre los cinco clasificadores base de la Práctica 3 cuando estos ya están bien ajustados, y si lo aprendido se transfiere a otro problema, la aceptación de un depósito a plazo en llamadas de telemarketing bancario.
 
En la Parte 1 se recuperan los cinco clasificadores de la Práctica 3 (árbol de decisión, Naive Bayes, k vecinos más cercanos, máquinas de soporte vectorial y regresión logística) con sus mejores hiperparámetros, sin repetir su optimización. Contra ellos se comparan bagging, AdaBoost, votación dura, votación suave, stacking, Random Forest, Extra-Trees, XGBoost y LightGBM. En la Parte 2 se busca el mejor modelo para Bank Marketing combinando preprocesamiento, balanceo de clases, ajuste del umbral, clasificadores, optimización y ensambles. En ambas partes la métrica principal es el F1 macro.
 
Descripción de los datasets
 
**1. Deserción estudiantil (Parte 1)**
 
Los datos provienen del dataset Predict Students' Dropout and Academic Success del repositorio UCI Machine Learning Repository (https://archive.ics.uci.edu/dataset/697). Son datos reales de 4 424 estudiantes de licenciatura del Instituto Politécnico de Portalegre (Portugal), que ingresaron entre los ciclos 2008/09 y 2018/19.
 
Esta práctica trabaja con dos archivos, ya separados:
 
desercion-entrenamiento.csv: 3 539 estudiantes con 36 atributos, más la columna id y la variable objetivo Target.
desercion-prueba.csv: 885 estudiantes con la columna id y solo los 30 atributos conocidos al cierre del primer semestre. No incluye Target ni los atributos del segundo semestre. Se conserva junto al notebook como en la Práctica 3, aunque en esta práctica no se usa.
 
La variable objetivo está moderadamente desbalanceada en el conjunto de entrenamiento: Graduate representa alrededor del 50 %, Dropout el 32 % y Enrolled el 18 %.
 
Los atributos se agrupan así:
 
Demográficos y socioeconómicos: estado civil, nacionalidad, género, edad al ingreso, estudios y ocupación de los padres, becario, deudor, colegiaturas al corriente, desplazado, necesidades educativas especiales, estudiante internacional.
Ingreso: modo de solicitud, orden de solicitud, carrera, turno (diurno o vespertino), calificación previa y su nota, nota de admisión.
Macroeconómicos: tasa de desempleo, inflación y PIB.
Académicos del primer semestre: unidades curriculares acreditadas, inscritas, evaluadas, aprobadas, sin evaluación y nota promedio.
Académicos del segundo semestre: los mismos seis atributos. No se usan, porque al cierre del primer semestre todavía no se conocen.
 
Para que los resultados sean comparables con la Práctica 3, se evalúa con los mismos cinco pliegues estratificados: StratifiedKFold(5, shuffle=True, random_state=42).
 
**2. Bank Marketing (Parte 2)**
 
Los datos provienen del dataset Bank Marketing del repositorio UCI Machine Learning Repository (https://archive.ics.uci.edu/dataset/222). Son llamadas reales de campañas de telemarketing de un banco portugués, realizadas entre mayo de 2008 y noviembre de 2010.
 
Se usa el archivo bank-additional-full.csv: 41 188 llamadas con 20 atributos y la variable objetivo y, separados por punto y coma. La variable objetivo indica si el cliente contrató un depósito a plazo y está fuertemente desbalanceada: yes representa alrededor del 11 % y no el 89 %.
 
Los atributos se agrupan así:
 
Datos del cliente: edad, ocupación, estado civil, escolaridad, crédito en incumplimiento, crédito hipotecario y préstamo personal.
Último contacto de la campaña actual: tipo de contacto (celular o teléfono fijo), mes y día de la semana. La duración de la llamada (duration) se elimina, porque solo se conoce después de la llamada y casi determina el resultado.
Historial de campañas: número de contactos en esta campaña, días desde el último contacto de una campaña anterior (999 significa que nunca se le contactó), contactos previos y resultado de la campaña anterior.
Contexto socioeconómico: tasa de variación del empleo, índice de precios al consumidor, índice de confianza del consumidor, tasa Euribor a 3 meses y número de empleados.
 
Varios atributos categóricos tienen el valor unknown cuando el dato no se registró. El notebook lo conserva como una categoría más.
 
La evaluación usa StratifiedKFold(n_splits=5, shuffle=True, random_state=2026), con y igual a 1 para yes y 0 para no. Todo lo que se ajusta con datos (preprocesamiento, selección de atributos, balanceo y umbral) va dentro del modelo, para que en cada pliegue se ajuste solo con el entrenamiento.
 
## Requisitos de ejecución
 
* Python 
* numpy
* pandas
* scipy
* scikit-learn 
* xgboost
* lightgbm
* imbalanced-learn
* matplotlib
* joblib
* Jupyter 
 
## Instrucciones
 
Primero descargue los archivos `desercion-entrenamiento.csv`, `desercion-prueba.csv` y `bank-additional-full.csv` y colóquelos en la misma carpeta que el notebook. Después abra el archivo `Practica_4.ipynb`; para ello es necesario tener instalado Jupyter Notebook y las librerías de la lista anterior. Por último, ejecute **Kernel → Restart & Run All** para correr todas las celdas en orden.
 
La ejecución completa tarda alrededor de una hora en una computadora de 2 núcleos, por las búsquedas de hiperparámetros. Las semillas están fijas, así que los resultados se reproducen en cada ejecución.
 
Al terminar, el notebook genera estos archivos en la misma carpeta:
 
* `random_forest_optimizado_umbral_modelo.joblib`: el mejor modelo de Bank Marketing. Es un Pipeline completo (preprocesamiento, clasificador y umbral) que recibe directamente las 19 columnas del archivo sin `duration` ni `y`.
* `resultados_desercion.csv` y `resultados_bank.csv`: las tablas de resultados de cada parte.
 
## Referencias
 
Moro, S., Cortez, P. y Rita, P. (2014). A data-driven approach to predict the success of bank telemarketing. Decision Support Systems, 62, 22-31. https://doi.org/10.1016/j.dss.2014.03.001
 
Realinho, V., Vieira Martins, M., Machado, J. y Baptista, L. (2021). Predict Students' Dropout and Academic Success [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5MC89

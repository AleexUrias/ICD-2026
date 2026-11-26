# Proyecto final - Predicción de resultados de juegos de la NFL y del desempeño de los Denver Broncos

Proyecto de ciencia de datos sobre juegos de la NFL. El objetivo es estimar la probabilidad de victoria del equipo local y el marcador final de juegos de temporada regular usando solo información disponible antes de cada juego, y evaluar si eso anticipa el desempeño de los Denver Broncos, que pasaron de 5 victorias en 2022 a 14 en 2025. Se responden tres preguntas: si un modelo con desempeño reciente supera a una línea base en la temporada 2025, qué atributos son los más influyentes y si su orden es estable, y si el modelo anticipa las 14 victorias de Denver en 2025. Como extensión, se predice el marcador final y se revisa el pronóstico de un juego real: Las Vegas en Denver, el 22 de noviembre de 2026.

Los atributos se construyen solo con juegos anteriores para evitar fuga de información: un Elo de puntos, medias móviles de anotación, porcentaje de victorias, descanso, localía, cambios de mariscal y clima. Se comparan una línea base (siempre la tasa de victoria local), el Elo, Naive Bayes, regresión logística L1, random forest y boosting. La selección de atributos usa un filtro de correlación y regresión logística L1. Los hiperparámetros se eligen con validación temporal de ventana creciente, y el modelo final se prueba una sola vez en 2025. Para el marcador se predicen el margen y el total de puntos con regresión (Ridge, random forest y boosting). Las apuestas se usan como referencia externa. Todos los modelos aleatorios y el bootstrap usan la semilla 42.

Los datos son la tabla games.csv de nflverse (licencia CC BY 4.0), con una fila por juego:

Entrenamiento: juegos de temporada regular 2015–2024. Las temporadas 2012–2014 solo se usan para iniciar el Elo y las medias móviles.
Validación: dos pliegues temporales, 2015–2022 → 2023 y 2015–2023 → 2024. Se usan para elegir hiperparámetros y atributos.
Prueba: los 272 juegos de la temporada 2025. Se usan solo para la comparación final.
Temporada 2026: los 158 juegos ya jugados se usan para evaluar el modelo, y los pendientes para el pronóstico.

nflverse actualiza el archivo varias veces al día y corrige datos y líneas de apuestas, así que se usan dos versiones fijas de su historial en GitHub: la del 22 de noviembre de 2026, previa al juego LV @ DEN, para todo el análisis, y la del 24 de noviembre de 2026 solo para revisar ese pronóstico.

La métrica principal es el log-loss, porque evalúa la calidad de la probabilidad y no solo el acierto. También se reportan el Brier, la exactitud y, para el marcador, el error absoluto medio (MAE). La incertidumbre se estima con un bootstrap que remuestrea semanas completas.

El notebook se organiza así:

Datos: carga de games.csv, número de juegos y tipos de las columnas.
Análisis exploratorio: ventaja de local por temporada, distribución del margen, datos faltantes y victorias de Denver por año.
Preprocesamiento: limpieza, ingeniería de atributos (Elo y medias móviles), selección de atributos y tabla del marcador.
Modelado: modelos de probabilidad de victoria con validación temporal y modelos de margen y total para el marcador.
Evaluación: comparación con la base, importancia de atributos, victorias de Denver en 2025, evaluación del marcador en 2025 y 2026, calibración de los rangos del 80 % y revisión del pronóstico del juego LV @ DEN.
Conclusiones: qué significan los resultados, limitaciones y trabajo futuro.

## Requisitos de ejecución

* Python
* numpy
* pandas
* scipy
* scikit-learn
* matplotlib
* Jupyter

## Instrucciones

No es necesario descargar archivos de datos. La primera vez que se ejecuta, el notebook descarga automáticamente las dos versiones fijas de games.csv de nflverse y verifica que sean las correctas, por lo que se requiere conexión a internet. Abra el archivo Proyecto_Final_ICD.ipynb en Jupyter Notebook, instale las bibliotecas indicadas en los requisitos y ejecute las celdas en orden, de arriba hacia abajo. La ejecución completa tarda unos minutos.

# Declaración de uso de la IA

Para este proyecto se utilizó la inteligencia artificial Anthropic Claude como herramienta de asistencia para la revisión, edición y mejora del formato de texto así como el apoyo en la toma de sugerencias para la parte del código y la corrección de errores.

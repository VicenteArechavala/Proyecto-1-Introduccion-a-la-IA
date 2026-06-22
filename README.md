# Proyecto-1-Introduccion-a-la-Inteligencia Artificial
**Integrantes**: Vicente Arechavala Alegría

# Título del proyecto
Predicción de Resultados de partidos de Futbol de la Liga Española.

## Definición del problema
En el fútbol profesional, el análisis de datos pre-partido es una práctica común a la hora de intentar determinar el ganador de un enfrentamiento, en la que regularmente se toman en cuenta duelos previos entre ambos equipos. El problema que se busca resolver consiste en encontrar precisamente esto, es decir, predecir el resultado final de un partido (Victoria Local, Empate o Victoria Visitante) basándose en el historial de partidos previos. Se abordará como un problema de clasificación multiclase, buscando identificar patrones historicos que puedan determinar el resultado final de futuros encuentros.

## Dataset
El dataset fue encontrado en Kaggle, nombrado como *European Football Matches* de Aiden Flynn. Dado que la base de datos estaba dividida en distintas hojas de calculo, cada una de una liga distinta se dió preferencia a la primera liga de España (La Liga). Dicha base corresponde a todos los partidos disputados desde el año 1993 hasta el año 2023, en donde sus variables principales se observa la fecha de ocurrido el encuentro (Date), los equipos involucrados diferenciados del equipo local (HomeTeam) y el equipo visitante (AwayTeam), los goles marcados por cada uno (HomeGoals y AwayGoals), y por último una variable que categoriza el resultado final del partido, que indica si el equipo local ganó (H), si el visitante ganó (A), o si hubo un empate (D).
La última variable descrita será utilizada como la variable objetivo.

## Plan de acción
Para evaluar como se desempeña el modelo en la predicción, se hará una división temporal de los datos, de manera que el modelo utilice las temporadas pasadas como entrenamiento y intente predecir lo que ocurre en las temporadas más recientes. De esta forma, el modelo simula una interacción real, dado que la predicción se basará en la información que se tiene en el momento para predecir un resultado futuro.

El problema observado es de clasificación multiclase (la variable objertivo cuenta con las opciones victoria, derrota, empate), además que dichas clases no están balanceadas (en general los equipos ganan mas de local). Por lo tanto, se implementará la lectura del accuracy, precision, recall, F1-score y matriz de confusion.

## Justificación del modelo
Como se comentó, existe un posible problema de overfitting, por lo qué se prevé el uso de regresión logística y random forest para la aplicación de este modelo. 

La primera será utilizada dado que se puede establecer un rendimiento alto sin correr el riesgo del sobreajuste, aplicando los criterios de regularización (se verá si lasso o ridge es más efectivo) de modo que se penalice los coeficientes excesivamente grandes, como puede ocurrir con los equipos que suelen ganar en general. Sin embargo, al tratarse de un modelo lineal, es posible que no pueda interpretar de buena manera las interacciones más complejas (interacciones no lineales), como por ejemplo un equipo que tiende a perder de local en general gane siempre de local contra un equipo específico.

El segundo modelo a aplicar se elige para la captura de patrones no lineales, 
(como por ejemplo, que un equipo tiende a ganar más específicamente cuando juega de local o cuando juega de visita con cierto equipo), siendo esta la dificultad del modelo anterior. El problema de es que dicha información es menos interpretable (problema de la "caja negra").

Se evaluará el uso de PCA es caso de que existan muchas variables que se correlacionen entre si.

## Análisis Exploratorio de Datos (EDA)
La base cuenta con los datos de todos los partidos de la primera división de España desde el año 1993 hasta 2023, exponiendo resultados de victoria para el equipo local (H), victoria para el visitante (A) y empate (D).

### Chequeo de la base
Como se observa, la base de datos, al registrar resultados de todos los partidos, no cuenta con datos nulos.

### Distribución de los resultados
Se puede observar primeramente que la localía del equipo es un dato relevante para lograr la victoria. Sin embargo, al ser esto una generalidad, sería conveniente determinar si dicha generalidad presenta algún tipo de cambio respecto al tiempo o a un equipo en concreto.

### Distribución de victorias como local según la década
Como se observa, en la primera década existe una mayor diferencia en los resultados, puesto que la capacidad de conseguir la victoria por parte del equipo local empieza a descender ligeramente en las siguientes décadas de la base de datos. Para confirmar la tendencia observada en el gráfico, se calculó el porcentaje de victorias locales sobre el total de partidos de cada periodo, permitiendo ver con mayor precisión si la ventaja de local realmente disminuye con el tiempo, más allá de lo que sugiere la inspección visual del gráfico de barras.

### Tasa de victorias según década
Por medio de este gráfico, se confirma que existe un distinto porcentaje de victorias hacia el equipo local dependiendo de la década que estemos observando.

### Mayor y menor cantidad de victorias por equipo
Como se puede ver en los datos, existen diferentes capacidades de victoria dependiendo del equipo, lo que probablemente tenga relación con el presupuesto del equipo en sí. Más allá de eso, es importante recalcar que las tasas de los equipos más bajos pueden tener relación con equipos que disputaron una menor cantidad de ligas (entiéndase por esto que existe el descenso para los 3 equipos con el menor rendimiento). Por lo tanto, es importante apreciar si esta tendencia también se aplica para equipos que hayan tenido una importante cantidad de temporadas en la primera división de España.

### Comparativa de equipos con una alta participación en la primera liga de España
> Nota: Para la elección de los equipos se buscó por internet cuáles son los equipos que han tenido mayor presencia a lo largo de estos 30 años, dando como resultado los 5 equipos elegidos.
> 
Dado lo visto previamente, se denota que equipos como el Barcelona o Real Madrid tienen un desbalance estadístico masivo a su favor. Este sesgo es algo a tener en cuenta más adelante, cuando se trabaje en la etapa de modelado predictivo, ya que podría influir en que el modelo tienda a favorecer siempre a estos equipos cuando juegan de local.

### Mapa de calor de algunos equipos de la Liga
> Nota: Nuevamente se utilizó la búsqueda en internet para seleccionar estos equipos.
> 
Como se puede analizar, efectivamente existen equipos que pueden presentar una "dominancia" respecto de otros equipos. Esto, como ya se indicó previamente, podría ocurrir por cuestiones más relacionadas al presupuesto o calidad de la plantilla, pero es importante que el modelo predictivo que se pretende crear tenga en cuenta dichas ventajas para no subestimar (o sobreestimar) ciertos equipos.

### Conclusiones iniciales
En esta primera etapa se realizó una exploración general de la base de datos de La Liga, en donde se puede destacar:
- La base de datos no presenta valores nulos, no se necesitó limpieza adicional en esta etapa.
- Existe una ventaja histórica clara para los locales, aunque muestra una leve tendencia a la baja.
- A nivel individual, el rendimiento varía fuertemente, pues equipos como Barcelona y Real Madrid muestran un desbalance estadístico a su favor, lo que es importante considerar para los sesgos.
- El análisis de victorias locales puede mostrar qué enfrentamientos muestran mayor dominancia.

Estos resultados sientan la base exploratoria para la siguiente etapa del proyecto, en la que se buscará construir un modelo predictivo de resultados.

## Modelamiento

### Clasificación Multiclase

Para el caso anterior, se procederá a entrenar los modelos de Regresión Logística y Random Forest utilizando únicamente la identidad de los equipos (HomeTeam, AwayTeam, codificados con One-Hot-Encoding, que vuelve dichos datos a 0 y 1) como las variables predictoras, dando los siguientes resultados:
> Resultados en el código > 

Como se puede observar en los resultados obtenidos, los modelos cuentan con resultados similares en su acuraccy, siendo ligeramente superior la Regresión Logística. Por otro lado, el F1 macro de Random Forest es superior al de Regresión Logistica, lo que se demuestra en su leve mejoría en la clasificación de los empates.

En ambos modelos se presenta una complejidad enorme en clasificar los empates, además de concentrarse la mayor parte de las predicciones (sesgo) hacia la victoria local (H).

Dicha cuestión probablemente ocurra por lo visto previamente en el data set, el cual presenta un desbalance inclinado hacia las victorias del equipo. Por lo mismo, una manera de intentar mejorar los resultados del modelo predictivo es balancear el dataset combinando los resultados de empate y derrota, de forma que el modelo solo tenga que elegir entre dos opciones en vez de dos. Si bien es cierto que dicho cambio deshabilita la opción de clasificar un empate, es posible que el porcentaje de acierto generalizado del modelo mejore considerablemente.

### Prueba con datos balanceados (multiclase a binaria)
Dado lo expresado anteriormente, se decidió simplificar el problema de una clasificación multiclase a una binaria, fusionando los resultados de empate y derrota en una sola categoría (No victoria local), de forma que el modelo elige entre dos opciones en lugar de tres. El cambio de enfoque permitió los siguientes resultados:
> Resultados en el código >

Se observa que, luego de cambiar el problema de uno multiclase a uno binario, la precision de ambos modelos mejora bastante, pues pasa de un 0.471 a un 0.594 en Random Forest, y de un 0.495 a un 0.622 en Regresión Logística, siendo ahora el mejor modelo. Esto ocurre debido a que, al tratarse ahora de solo dos variables, encuentra la linealidad de los resultados, y por ende, mejora considerablemente su capacidad de predicción. 

### Nuevas Variables

Sobre los resultados obtenidos previamente, se construyeron 4 variables nuevas a partir del historial que se muestra para cada equipo, las nuevas variables son las siguientes:
- Racha_Puntos_Local / Racha_Puntos_Visita: Promedio de puntos obtenidos (victoria=3, empate=1, derrota=0) en los ultimos 5 partidos de cada equipo, sin importar si es que jugó de local o de visita.
- Tasa_Victorias_Local / Tasa_Victorias_Visita: Porcentaje histórico de victorias de cada equipo, considerando todos sus partidos previos disponibles.

Los valores nulos se imputaron con la media de cada variable para las rachas, y con 0.5 para las tasas de victoria.

Con estas variables incorporadas, se reentrenaron ambos modelos, dando los siguientes resultados:
> Resultados en el código >

### Comentarios finales
Al incorporar las nuevas variables, ambos modelos mejorar de forma consistente respecto a la versión anterior del modelo. Para el caso de evitar el sobreajuste, se calculó la diferencia del F1 macro tanto del train como del test, donde se observa una diferencia relativamente pequeña (datos en el código), lo que indica que el modelo no está memorizando los datos de entrenamiento (overfitting), sino que los generaliza correctamente.

Al comparar los resultados de los modelos, la regresión logística presenta un mejor F1 macro en comparación al random forest, mientras que random forest presenta un mejor accuracy (aunque muy leve). Esto quiere decir que el random forest intenta maximizar los aciertos del modelo, y por tanto prioriza las "no victorias". En cambio, la regresión logística busca un balance entre los datos, y por ello penaliza el desequilibrio entre las clases.

En resumen
- El problema de clasificación multiclase original es más complicado de modelar que su versión binaria, dado que los modelos presentan problemas importantes en la predicción de los empates, que es posible que ocurran por la falta de datos en la base original, como también porque los equipos que suelen empatar están más "parejos" en rendimiento, cosa que es dificil de predecir en las condiciones actuales del los modelos.
- Simplificar el modelo ayudó considerablemente a tener mejores desempeños en los modelos, a costa de perder la capacidad de predecir los empates, que tal como hemos comentado, presentaba dificultades para hacerlo.
- Las variables introducidas ayudaron a mejorar nuevamente el desempeño de los modelos, encontrando una cualidad para cada uno de estos (random forest más preciso pero conservador; regresion logísitca más balanceado pero ligeramente menos preciso).
  
- El control del overfitting se ve realizado, dado a que las diferencias entre las métricas de entrenamiento y testeo son mínimas en los casos vistos.

- Para terminar, sería importante la inclusión de nuevas variables o nuevos datos a la base de datos para aportar mas complejidad o especificidad, de forma que pueda mejorarse el desempeño de los modelos actuales, como también ver si es que el problema inicial (clasificación multiclase) es abordable.

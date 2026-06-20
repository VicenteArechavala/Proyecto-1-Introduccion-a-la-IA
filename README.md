# Proyecto-1-Introduccion-a-la-Inteligencia Artificial
**Integrantes**: Vicente Arechavala Alegría

# Título del proyecto
Predicción de Resultados de partidos de Futbol de la Liga Española.

## Definición del problema
En el fútbol profesional, el análisis de datos pre-partido es una práctica común a la hora de intentar determinar el ganador de un enfrentamiento, en la que regularmente se toman en cuenta duelos previos entre ambos equipos. El problema que se busca resolver consiste en encontrar precisamente esto, es decir, predecir el resultado final de un partido (Victoria Local, Empate o Victoria Visitante) basándose en el historial de partidos previos. Se abordará como un problema de clasificación multiclase, buscando identificar patrones historicos que puedan determinar el resultado final de futuros encuentros.

## Dataset
El dataset fue encontrado en Kaggle, nombrado como *European Football Matches* de Aiden Flynn. Dado que la base de datos estaba dividida en distintas hojas de calculo, cada una de una liga distinta se dió preferencia a la primera liga de España (La Liga). Dicha base corresponde a todos los partidos disputados desde el año 1993 hasta el año 2023, en donde sus variables principales se observa la fecha de ocurrido el encuentro (Date), los equipos involucrados diferenciados del equipo local (HomeTeam) y el equipo visitante (AwayTeam), los goles marcados por cada uno (HomeGoals y AwayGoals), y por último una variable que categoriza el resultado final del partido, que indica si el equipo local ganó (H), si el visitante ganó (A), o si hubo un empate (D).
La última variable descrita será utilizada como la variable objetivo.

## Justificación del modelo
Se prevé el uso de regresión logística y random forest para la aplicación de este modelo.
La primera será utilizada dado que se puede establecer un rendimiento alto sin correr el riesgo del sobreajuste, además de que permitirá idenificar correctamente si es que existe peso estadístico a la hora de jugar de local o por un equipo en específico. El segundo modelo a aplicar se elige para la captura de patrones específicos en líneas complejas (como por ejemplo, que un equipo tiende a ganar más específicamente cuando juega de local o cuando juega de visita con cierto equipo), por lo demás, también es un buen modelo para evitar el sobreajuste.

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
Dado lo visto previamente, se denota que equipos como el Barcelona o Real Madrid tienen un desbalance estadístico masivo a su favor. Este sesgo es algo a tener en cuenta más adelante, cuando se trabaje en la etapa de modelado predictivo, ya que podría influir en que el modelo tienda a favorecer siempre a estos equipos cuando juegan de local.

### Mapa de calor de algunos equipos de la Liga
> Nota: Nuevamente se utilizó la búsqueda en internet para seleccionar estos equipos.
Como se puede analizar, efectivamente existen equipos que pueden presentar una "dominancia" respecto de otros equipos. Esto, como ya se indicó previamente, podría ocurrir por cuestiones más relacionadas al presupuesto o calidad de la plantilla, pero es importante que el modelo predictivo que se pretende crear tenga en cuenta dichas ventajas para no subestimar (o sobreestimar) ciertos equipos.

### Conclusiones iniciales
En esta primera etapa se realizó una exploración general de la base de datos de La Liga, en donde se puede destacar:
- La base de datos no presenta valores nulos, no se necesitó limpieza adicional en esta etapa.
- Existe una ventaja histórica clara para los locales, aunque muestra una leve tendencia a la baja.
- A nivel individual, el rendimiento varía fuertemente, pues equipos como Barcelona y Real Madrid muestran un desbalance estadístico a su favor, lo que es importante considerar para los sesgos.
- El análisis de victorias locales puede mostrar qué enfrentamientos muestran mayor dominancia.

Estos resultados sientan la base exploratoria para la siguiente etapa del proyecto, en la que se buscará construir un modelo predictivo de resultados.

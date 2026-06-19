# Proyecto-1-Introduccion-a-la-Inteligencia Artificial
**Integrantes**: Vicente Arechavala Alegría

# Título del proyecto
Predicción de Resultados de partidos de Futbol de la Liga Española.

## 1 Definición del problema
En el fútbol profesional, el análisis de datos pre-partido es una práctica común a la hora de intentar determinar el ganador de un enfrentamiento, en la que regularmente se toman en cuenta duelos previos entre ambos equipos. El problema que se busca resolver consiste en encontrar precisamente esto, es decir, predecir el resultado final de un partido (Victoria Local, Empate o Victoria Visitante) basándose en el historial de partidos previos. Se abordará como un problema de clasificación multiclase, buscando identificar patrones historicos que puedan determinar el resultado final de futuros encuentros.

## Dataset
El dataset fue encontrado en Kaggle, nombrado como *European Football Matches* de Aiden Flynn. Dado que la base de datos estaba dividida en distintas hojas de calculo, cada una de una liga distinta se dió preferencia a la primera liga de España (La Liga). Dicha base corresponde a todos los partidos disputados desde el año 1993 hasta el año 2023, en donde sus variables principales se observa la fecha de ocurrido el encuentro (Date), los equipos involucrados diferenciados del equipo local (HomeTeam) y el equipo visitante (AwayTeam), los goles marcados por cada uno (HomeGoals y AwayGoals), y por último una variable que categoriza el resultado final del partido, que indica si el equipo local ganó (H), si el visitante ganó (A), o si hubo un empate (D).
La última variable descrita será utilizada como la variable objetivo.

## Justificación del modelo
Se prevé el uso de regresión logística y random forest para la aplicación de este modelo.
La primera será utilizada dado que se puede establecer un rendimiento alto sin correr el riesgo del sobreajuste, además de que permitirá idenificar correctamente si es que existe peso estadístico a la hora de jugar de local o por un equipo en específico. El segundo modelo a aplicar se elige para la captura de patrones específicos en líneas complejas (como por ejemplo, que un equipo tiende a ganar más específicamente cuando juega de local o cuando juega de visita con cierto equipo), por lo demás, también es un buen modelo para evitar el sobreajuste.

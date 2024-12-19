# bootcamp
Entrega de trabajo final BDA4
ANÁLISIS EXITOS MUSICALES DE LOS ÚLTIMOS AÑOS EN SPOTIFY
En la industria de la música se acostumbra analizar el comportamiento y performance entre los lanzamientos y los usuarios peor no se incluye en el análisis el componente musical, sus características únicas y que en definitiva, al poder establecer tendencias se podría proyectar próximos éxitos y ayudar a los equipos artísticos para que desde la data dura se pueden definir características del producto.

Caso de Estudio
Como dataset se utiliza un conjunto de datos obtenido de Kaggle que muestra las características musicales de más de 1500 canciones que fueron parte del Chart Global de Spotify en los últimos años. Para complementar las tablas y tener toda la información que requería este proyecto, sumé un dataset de álbumes también de Kaggle y apoyado en Copilot completé campos como Idioma y país.

Herramientas
Excel: Para hacer una primera limpieza ya que el dataset tenía muchos problemas de caracteres no tradicionales y se necesitaba tener eso bien para requerir la información de Copilot. También se utilizó para una limpieza en lo que es géneros musicales a través de una matriz de detección de género y asignación a uno pre establecido y evitar tener un listado de 500 géneros. Un gran problema con los géneros musicale ses la localización geog´rafica o idiomática que genera múltiples sub géneros como rock naciona, urbano latino o pop italiano.
BigQuery: Utilizado para almacenar los datos, ejecutar consultas SQL y extraer la información necesaria para realizar el análisis exploratorio.
Power Query: Herramienta empleada para la limpieza y transformación de datos antes de proceder con el análisis en Power BI.
Power BI: Usado para diseñar dashboards interactivos que muestran de manera visual los resultados del análisis.
Photoshop y Midjourney: Aplicados en el diseño de elementos visuales tanto para los dashboards como para la documentación del proyecto.

Objetivos:
Analizar patrones que sirvan para establecer un framework para en un futuro combinar con el análisis de charts pasados y futuros y lograr proyectar tendencias del componente musical que sirvan para orientan la producción de nuevos lanzamientos. 
Comparar el comportaiento de diferentes tipos de contenidos y ver a qué metricas atender para hacer foco en el desarrollo e inversión.
Tambie´n parte del aprendizaje con este trabajo es ver qué variables son las más relevantes para definir el ADN de una canción. Así como se afirma esto también como aprendizaje, trabajar un dataset global hace más complejo entender ciertos comportamientos que si estuvieran en un marco de tiempo y país podrían dar resultados más tangibles. 

Plan de Métricas
Para las pruebas de hipótesis de negocio, se plantean 13 KPIs que permitan examinar el comportamiento de los usuarios entre las distintas transacciones.

A continuación, se detallan las métricas utilizadas, junto con su cálculo y los puntos de vista desde los cuales se pueden analizar. Se puede ver con más detalles en la documentación del Plan de Métricas



EDA

Modelo de Datos 

Data Flow

Métricas de Rendimiento

Análisis de datos

Hipotesis, Aprendizajes y Futuro

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
Analizar patrones de transacciones y comportamientos de usuarios.
Explorar la relación entre cashback, lealtad y montos de transacción.
Comparar el rendimiento en dispositivos móviles vs. computadoras.
Identificar oportunidades de optimización a través de la tasa de conversión y abandono.
Hipótesis de Negocio
Los usuarios que acumulan más puntos de lealtad son más propensos a realizar transacciones de mayor monto.
Los meses con mayores tasas de conversión en general se correlacionan con un aumento en el uso de dispositivos móviles, indicando que la optimización para estos dispositivos es fundamental para maximizar las transacciones.
Las categorías de productos con mayor cashback tienen un ticket promedio más alto.
Los meses en los que se reportan altos márgenes de ganancia en categorías específicas son seguidos por un incremento en las ganancias generales, sugiriendo que la rentabilidad de estas categorías impulsa el crecimiento del negocio.
Plan de Métricas
Para las pruebas de hipótesis de negocio, se plantean 13 KPIs que permitan examinar el comportamiento de los usuarios entre las distintas transacciones.

A continuación, se detallan las métricas utilizadas, junto con su cálculo y los puntos de vista desde los cuales se pueden analizar. Se puede ver con más detalles en la documentación del Plan de Métricas



EDA

Modelo de Datos 

Data Flow

Métricas de Rendimiento

Análisis de datos

Hipotesis, Aprendizajes y Futuro

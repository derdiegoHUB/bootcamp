# bootcamp
Entrega de trabajo final BDA4 INCOMPLETO

![image](https://github.com/user-attachments/assets/bb9b5907-f8c4-46a0-b3e6-a5291570af91)


ANÁLISIS EXITOS MUSICALES DE LOS ÚLTIMOS AÑOS EN SPOTIFY
En la industria de la música se acostumbra analizar el comportamiento y performance entre los lanzamientos y los usuarios peor no se incluye en el análisis el componente musical, sus características únicas y que en definitiva, al poder establecer tendencias se podría proyectar próximos éxitos y ayudar a los equipos artísticos para que desde la data dura se pueden definir características del producto.

![image](https://github.com/user-attachments/assets/500a095a-421e-44ec-a782-e55cedbb3fb4)

Caso de Estudio
Como dataset se utiliza un conjunto de datos obtenido de Kaggle que muestra las características musicales de más de 1500 canciones que fueron parte del Chart Global de Spotify en los últimos años. Para complementar las tablas y tener toda la información que requería este proyecto, sumé un dataset de álbumes también de Kaggle y apoyado en Copilot completé campos como Idioma y país.

Herramientas
Excel: Para hacer una primera limpieza ya que el dataset tenía muchos problemas de caracteres no tradicionales y se necesitaba tener eso bien para requerir la información de Copilot. También se utilizó para una limpieza en lo que es géneros musicales a través de una matriz de detección de género y asignación a uno pre establecido y evitar tener un listado de 500 géneros. Un gran problema con los géneros musicale ses la localización geog´rafica o idiomática que genera múltiples sub géneros como rock naciona, urbano latino o pop italiano.
BigQuery: Utilizado para almacenar los datos, ejecutar consultas SQL y extraer la información necesaria para realizar el análisis exploratorio.
Power Query: Herramienta empleada para la limpieza y transformación de datos antes de proceder con el análisis en Power BI.
Power BI: Usado para diseñar dashboards interactivos que muestran de manera visual los resultados del análisis.
Photoshop: Aplicados en el diseño de elementos visuales tanto para los dashboards como para la documentación del proyecto.

Objetivos:
Analizar patrones que sirvan para establecer un framework para en un futuro combinar con el análisis de charts pasados y futuros y lograr proyectar tendencias del componente musical que sirvan para orientan la producción de nuevos lanzamientos. 
Comparar el comportaiento de diferentes tipos de contenidos y ver a qué metricas atender para hacer foco en el desarrollo e inversión.


Plan de Métricas
Para las pruebas de hipótesis de negocio, se plantean 13 KPIs que permitan examinar el comportamiento de los usuarios entre las distintas transacciones.

A continuación, se detallan las métricas utilizadas, junto con su cálculo y los puntos de vista desde los cuales se pueden analizar. Se puede ver con más detalles en la documentación del Plan de Métricas



EDL
Reemplazo de caracteres rotos
Normalización de decimales
Sumar nacionalidad
Sumar idioma
Generar artista principal a partir de artistas
Buscar reemplazar valores vacíos
Cambio de nombre para ciertos campos para normalizar en un idioma
Simplificación del campo de género musical a traves de una matriz de detección de género principal. El objetivo de esto era simplificar la cantidad de categorías y eliminat de los nombres de categorías cualquier cosa que tenga que ver con idioma o región, por ejemplo, italo pop es POP, rock nacional es ROCK.

Después de la normalización en bronce, ya cargado en big query
Se limpiaron unas columnas redundantes

ALTER TABLE `silver_layer.Spotify_Hits`
DROP COLUMN Index,
DROP COLUMN int64_field_1;

Se limpiaron filas sin campos obligatorios
DELETE FROM `silver_layer.Spotify_Hits`
WHERE `Song ID` IS NULL
   OR `Song Name` IS NULL
   OR `Streams` IS NULL
   OR `Album_ID` IS NULL;

DELETE FROM `silver_layer.Spotify_Hits`
WHERE `Song ID` = '#N/A'
   OR `Song Name` = '#N/A'
   OR `Album_ID` = '#N/A'
   OR `Track N` = '#N/A';

DELETE FROM `silver_layer.Spotify_Hits`
WHERE `Song ID` IS NULL OR `Song ID` = ' '
   OR `Release Date` IS NULL OR `Release Date` = ''
   OR `Artist_Name` IS NULL OR `Artist_Name` = '';



Con esto limpie los de tracks vacíos con un 1 y limpieza de explicit con NA para los vacíos
UPDATE `silver_layer.Spotify_Hits`
SET `Track N` = '1'
WHERE `Track N` IS NULL OR `Track N` = '' OR `Track N` = ' ';



Se agregó un artist id para poder separar la tabla de forma eficiente
CREATE OR REPLACE TABLE `silver_layer.Spotify_Hits` AS
SELECT 
  *,
  DENSE_RANK() OVER (ORDER BY Artist_Name) AS Artist_ID
FROM `silver_layer.Spotify_Hits`;
 

Limpieza de tipos de campos
Release date
ALTER TABLE `silver_layer.Spotify_Hits` ADD COLUMN Release_Date_Formatted DATE;

Y luego
UPDATE `silver_layer.Spotify_Hits` SET Release_Date_Formatted = PARSE_DATE('%m/%d/%Y', `Release Date`) WHERE SAFE.PARSE_DATE('%m/%d/%Y', `Release Date`) IS NOT NULL;


Boolean para explicit (luego fue eliminada, la información de este campo me estaba generando problemas)
UPDATE `silver_layer.Spotify_Hits`
SET Explicit_Lyrics = CASE
  WHEN LOWER(Explicit) = 'true' THEN TRUE
  WHEN LOWER(Explicit) = 'false' THEN FALSE
  ELSE NULL
END
WHERE TRUE;

 

**Modelo de Datos **
![image](https://github.com/user-attachments/assets/25ecba27-ee89-4cac-b34c-c53e5b57ce04)
Hay un problema en la relación entre la tabla de Tracks y de Album que no termino de comprender y me ha limitado en el dashboard que contiene información de album. Aparentemente existe un id repetido pero no logro resolverlo sin afectar la tabla, algo similar ocurre con la tabla de artist.

**Data Flow**

**Métricas de Rendimiento**
Age: es la antiguedad del lanzamiento, calculado a través de fecha hoy() - Album (Releades Date). A más de 180 días sería "Deep Catálogo", más de 120 días sería ¨Catálogo¨ y sino "Recent Release"
Popularidad x Artista:
Popularidad x Género:
Cantidad de tracks x idioma:
Cantidad de tracks por años de release_date (album)

**Group by Genre:**

  Idioma
    
  País
  
  Single Vs Album
  
  Duración Promedio en minutos y segundos
  
  BPM Promedio

**Análisis de datos**

El trabajo pretencía tener 3 instancias luego de una presentación formal, una general mostrando de los éxitos de los últimos años la composicón por:
1. GENERAL
a) Ranking de Streams x Géneros
b) Popularidad x Artistas, Géneros y países
c) Exitos en una linea de tiempo sergún sus fechas de lanzamientos
d) Cantidad de canciones x ioidima y sus porcentajes
e) Composición de Singles Vs Albums
No presenta opciones de filtrado

2. X Género
a) Atributos promedio
b) Share x Antiguedad
c) Share x Idioma
d) Share x Países
e) Share x Single Vs Album
Presenta opciones de filtrado x Género
Muestra un listado de las 10 canciones más populares de ese Género

4. X País
a) Atributos promedio
b) Share x Antiguedad
c) Share x Idioma
d) Share x Países
e) Share x Single Vs Album
Presenta opciones de filtrado x País
Muestra un listado de las 10 canciones más populares de ese País


![image](https://github.com/user-attachments/assets/c5a80e24-9c21-4017-91c3-0a9e9fa8cdc9)

**Hipotesis, Aprendizajes y Futuro**
A partir de analizar una base de más de 1500 resgitros que han sido parte de los charts globales intentar detectar trends o elementos que sirvan para analizar y aplicar estas características en futuras producciones.
Parte del aprendizaje con este trabajo es ver qué variables son las más relevantes para definir el ADN de una canción. Así como se afirma esto también como aprendizaje, trabajar un dataset global hace más complejo entender ciertos comportamientos que si estuvieran en un marco de tiempo y país podrían dar resultados más tangibles. Parte de la idea de este proyecto era incluir una propuesta de 20 títulos en base a la selección de una canción de estas 1500 para poder hacer un análisis detallado de estas.

**ULTIMO UPDATE:** me he encontrado con múltiples complicaciones en el desarrollo de este trabajo que me deja estos aprendizajes:
Comenzar de menor a mayor es fundamental. Tener clara la hipótesis antes de buscar el dataset. Modelar de la forma más clara y simple la estructura de la base de datos.
Por problemas con las conexiones con las tablas de artist y de album muchos de los campos a incorporar en los dashboards no funcionaron, y por la cantidad de datos y registros y limitaciones propias luego de intentarlo múltiples veces, prefiero cortar con esto acá y retomar un proyecto así con un dataset mejor trabajado, una selección de datos más ajustada y decién ahí avanzar. De igual forma, lo hecho en gran parte sirve como un framewor a seguir trabajando y aplicar con futuras tomas de datos frescos.




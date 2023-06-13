# Bienvenido/a al repositorio de mi proyecto MLOps de Henry


***Introducción***

Mi nombre es Romina Prestupa y este es el desarrollo de mi proyecto individual de Machine Learning Operations. A continuación podrás encontrar una breve descripción de los requerimientos, y el paso a paso de la construcción del proyecto.



**Contexto simulado de trabajo:**

En esta ocasión, ocuparé un rol de Data Scientist, trabajando en una start up que brinda servicios a  plataformas de streaming. El primero de los requerimientos es entonces, poner en marcha un sistema de recomendación de películas. 
Para ello, el primer paso lógico será realizar el proceso de ETL, que podrás encontrar aquí.



Proceso de ETL
-------------
**Extracción**
- Ingesta de datos desde los archivos csv provisto a un DataFrame de Pandas;
- Análisis exploratorio de la estructura de los mismos;

**Transformación**
Se ejecutan las transformaciones solicitadas en los requerimientos, mas transformaciones adicionales necesarias para el plan de desarrollo del sistema de recomendación:
- Desanidamiento de los campos que contienen datos dict o list.;
- Identificación y tratamiento de nulos en columnas Revenue y Budget;
- Creación de una columna donde se extraerá el año de estreno de las películas. Además, las fechas fueron trasformadas al formato AAA-mm-dd;
- Creación de una columna Return, calculada a partir de Revenue y Budget;
- Eliminación de columnas: video, imdb_id, adult, original Title, poster_path y homepage ;

Adicionalmente:
- Incorporación del archivo Credits, y unión de ambos dataframes;
- Desanidamiento de las columnas Cast y Crew;

**Carga**
Se exportan los datos limpios a un nuevo archivo csv, y a partir de él, se crean archivos adicionales que serán consumidos por la API.

`Proceso de ETL` : <https://github.com/Rowinelle/Proyecto01_Henry/blob/master/Etl_P1MLOps.ipynb>




Desarrollo de la API
-------------
Se solicitan las siguientes consultas:
- Cantidad de películas por mes de estreno;
- Cantidad de películas por día de estreno;
- Puntuación alcanzada por una película, y el año en que se estrenó;
- Cantidad de votaciones recibidas por una película, y el promedio de las mismas. En caso de que no alcance dos mil votaciones, se devuelve un mensaje explicitando la cantidad insuficiente de votos;
- Exito de un actor, medido a través del retorno total generado por el mismo en todas las películas que ha participado. Además, la consulta arroja la cantidad de películas en las que ha participado y el promedio de retorno;
- Exito obtenido por un director, medido a través del retorno total generado por el mismo en todas las películas que ha dirigido. Además, la consulta arroja el nombre de cada película interpretada, el  año de estreno, el retorno individual, el costo y la recaudación obtenida;

**Procedimiento**
- en el desarrollo de cada función, se usaron archivos específicos, delimitando la cantidad de campos en función de lo requerido por la consulta, con el fin de optimizar el proceso;
- se normalizan los inputs para Día y Mes, inhibiendo el impacto de mayúsculas y tildes. Se traducen los inputs al  idioma inglés;
- el código está compuesto por 8 endpoints, correspondientes a un mensaje de bienvenida, 6 funciones y el modelo de recomendación que consume la API;


`Desarrollo de las funciones` : <https://github.com/Rowinelle/Proyecto01_Henry/blob/master/Funciones_P1MLOps.ipynb>




Desarrollo del análisis exploratorio
-------------
- se llevó a cabo un análisis exploratorio de los datos, utilizando Pandas y Seaborn;
- se visualiza la forma general del dataset provisto;
- se realiza un análisis de contenido de las películas, explorando los conceptos mas frecuentes a través de la construcción de un Wordcloud; 
- para determinados análisis, se decide acotar los datos a las películas estrenadas durante los últimos 40 años; 
- algunos de los análisis efectuados, arrojan un ordenamiento de películas por popularidad, cantidad de películas estrenadas por mes, popularidad total alcanzada por películas de determinado director, etc; 

El desarrollo del EDA propuesto podrás encontrarlo aquí debajo:

`Desarrollo del análisis exploratorio` : <https://github.com/Rowinelle/Proyecto01_Henry/blob/master/EDA_P1MLOps.ipynb>




Modelo de recomendación
-------------
Para la construcción del modelo de recomendación, se utilizó la medida de la similitud del coseno, que se comenta brevemente a continuación. 
Se realiza como primer paso, un pre-procesamiento de los datos, en el cual:
- se decide realizar un modelo de recomendación basado en el contenido;
- se eligen como features para la comparación de compatibilidad de cada película, el género, el director, y los actores;
- los valores nulos fueron reemplazados por strings vacíos, para que puedan ser procesados como un término, por el componente de la biblioteca Sklearn que calcula las frecuencias de los términos, el TfidfVectorizer; 
- se trabajó con un data set reducido, en función de la popularidad de la película y la antigüedad de la misma. Se considera relevante para un sistema de recomendación, sugerir películas que hayan tenido un alto nivel de aceptación por el público, y que puedan resultarle novedosas al usuario;
- se decidió eliminar elementos por su duración, a fin de optimizar los tiempos de procesamiento y teniendo en cuenta que se contaba con recursos de espacio limitados para deployar el modelo; 

En el desarrollo del modelo, se construyó una matriz de similitud de las películas entre sí, y a partir del input ingresado, se arroja como resultado los cinco títulos que tienen mayor puntaje de similitud con el target.
La construcción del modelo la encontrarás en el siguiente link:

`Desarrollo del sistema de recomendación` : <https://github.com/Rowinelle/Proyecto01_Henry/blob/master/Modelo2_ML_P1MLOps.ipynb>



Tecnologías
-------------
Por último, las tecnologías utilizadas en este proyecto fueron:
- IDE: Visual Studio Code;
- API: FastAPI;
- Servidor ASGI: Uvicorn;
- Deploy: Render;
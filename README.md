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

`Proceso de ETL` : <https://github.com>




Desarrollo de la API
-------------
Se solicitan las siguientes consultas:
- Cantidad de películas por mes de estreno;
- Cantidad de películas por día de estreno;
- Puntuación alcanzada por una película, y el año en que se estrenó;
- Cantidad de votaciones recibidas por una película, y el promedio de las mismas. En caso de que no alcance dos mil votaciones, se devuelve un mensaje explicitando la cantidad insuficiente de votos;
-Exito de un actor, medido a través del retorno total generado por el mismo en todas las películas que ha participado. Además, la consulta arroja la cantidad de películas en las que ha participado y el promedio de retorno;
-Exito obtenido por un director, medido a través del retorno total generado por el mismo en todas las películas que ha dirigido. Además, la consulta arroja el nombre de cada película interpretada, el  año de estreno, el retorno individual, el costo y la recaudación obtenida;
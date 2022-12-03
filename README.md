# PySpark (Batch) Test
1. Descargar uno o más archivos grandes (el más grande de mínimo 20MB, independiente del número de registros y columnas). El que usted prefiera, hay muchas fuentes:
    1. https://www.imdb.com/interfaces/
    2. https://www.kaggle.com/ 
    3. https://www.datos.gov.co/ 
    4. Sitios con “Open Data” (Buscar en Google)

IMPORTANTE: Que el dataset tenga una fecha (que servirá más adelante para particionar).

2. Cargarlo a alguna plataforma de Notebooks que permita habilitar PySpark (Google Colab, DataBricks, AWS Glue como Job o como Notebook). También pueden hacerlo en un computador local, con una instalación local de PySpark. 

3. Con PySpark: Leer el o los archivos. Tener en cuenta el separador, también si el archivo viene con títulos de columnas (“header”), y pueden pedirle a Spark que infiera el esquema (estructura de columnas). 

4. Con PySpark: Llevar a cabo alguna operación de limpieza (valor por defecto o borrar vacíos o quitar duplicados).

5. Con PySpark: Llevar a cabo alguna operación de filtrado (condiciones), puede ser descartar una parte de los datos (pero NO descartar más del 70% de los datos).

6. Construir un DataFrame -DF- adicional desde cero (es decir, SIN leer de un archivo), con más de una columna y más de un registro, e involucrar ese DF en el procesamiento con el o los otros DFs construídos a partir de archivos (del punto 3). Puede ser para filtrar o como parámetros de algún tipo. Revisar la posibilidad de usarlo para Broadcasting en el proceso.

7. Con PySpark: Agregar valor a los datos, es decir, llevar a cabo algún tipo de operación en el 
DataFrame (MÍNIMO DOS DE LAS SIGUIENTES OPERACIONES):
    1. Agrupar para contar, sumar o promediar (o máximo o mínimo).
    2. Alguna operación de conjunto (UNION ALL que en Spark es con df1.union(df2), MINUS que en Spark es con df.except, etc) que tenga sentido.
    3. Algún “join”, por lo que probablemente toque manejar uno o varios DataFrames adicionales que pueden armar leyendo otro(s) archivo(s) o armándolo(s) manualmente.
    4. Subtotales (rollup o cube).
    5. Usar ventanas (windows con .partitionBy y .orderBy, para calcular un ranking o un cálculo de ponderación (valor alguna columna del registro dividido entre el total de esa misma columna para la ventana) o una columna adicional con el valor atrasado o adelantado (.lead o .lag).
MUY IMPORTANTE: Explicar la operación u operaciones (ver abajo el punto 2 en la sección “Entregar”). 

8. Guardar los resultados (con valor agregado) particionando por Año, Mes, Día (de la fecha mencionada en el punto 1).

## Entregar:
1. Código fuente (Python)
2. Texto corto con justificación del valor agregado a los datos de entrada (“Se agrupó por estas columnas porque… y se totalizaron o contaron o promediaron por…” o “Se calculó el ranking por cada -”columnas ventana”- porque...). También pueden mencionar por qué filtraron u por qué limpiaron los datos... 
3. Fotos (imágenes) de evidencias de resultados: el resultado de un .show() o una foto de los datos generados (descargados como CSV y cargados a Excel) donde se vean los cambios que hace el programa. 

Script para habilitar Spark en Google Colab:
```
!apt-get update 
!apt-get install openjdk-8-jdk-headless -qq > /dev/null 
!wget -q
http://archive.apache.org/dist/spark/spark-2.3.1/spark-2.3.1-bin-hadoop2.7.tgz !tar xf spark-2.3.1-bin-hadoop2.7.tgz 
!pip install -q findspark 
import os 
os.environ["JAVA_HOME"] = "/usr/lib/jvm/java-8-openjdk-amd64" os.environ["SPARK_HOME"] = "/content/spark-2.3.1-bin-hadoop2.7" 
!ls 
import findspark 
findspark.init() 
import pyspark 
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate() 
spark
```


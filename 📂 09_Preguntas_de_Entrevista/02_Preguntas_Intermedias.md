## 🔥 Preguntas Intermedias sobre Apache Spark

### 📌 General

1. **¿Qué es Apache Spark y para qué se utiliza?**  
   Apache Spark es un motor de procesamiento de datos de código abierto, diseñado para procesar grandes volúmenes de datos en paralelo de manera rápida y eficiente. Se utiliza en tareas de análisis de datos, machine learning, procesamiento en tiempo real y Big Data.

2. **¿Cuáles son los principales módulos de Apache Spark?**  
   - **Spark Core**: Maneja la ejecución y administración de tareas.
   - **Spark SQL**: Permite consultas SQL sobre datos estructurados.
   - **Spark Streaming**: Procesamiento de datos en tiempo real.
   - **MLlib**: Librería de Machine Learning.
   - **GraphX**: Procesamiento de datos en grafos.

3. **¿Cómo se diferencia Spark de MapReduce en términos de rendimiento?**  
   Spark es significativamente más rápido que MapReduce porque procesa los datos en memoria, mientras que MapReduce escribe los resultados intermedios en disco, lo que genera una gran latencia.

4. **¿Qué ventajas ofrece Spark sobre otras tecnologías de procesamiento de datos?**  
   - Procesamiento en memoria para mayor velocidad.
   - API en múltiples lenguajes (Scala, Python, Java, R).
   - Soporte para procesamiento por lotes y en tiempo real.
   - Compatibilidad con Hadoop y otras herramientas de Big Data.

5. **¿Cuáles son las desventajas o limitaciones de Spark?**  
   - Alto consumo de memoria.
   - Puede ser más costoso en la nube debido a la necesidad de hardware más potente.
   - Requiere ajustes para optimizar el rendimiento en grandes clústeres.

6. **¿En qué escenarios es más útil usar Spark en lugar de Hadoop?**  
   - Cuando se requiere procesamiento en tiempo real o análisis en memoria.
   - Para ejecutar cargas de trabajo iterativas como Machine Learning.
   - En entornos donde se necesita flexibilidad con diferentes fuentes de datos.

7. **¿Qué es el SparkContext y por qué es importante?**  
   Es el punto de entrada principal para cualquier aplicación de Spark. Administra la configuración de la aplicación y la distribución de tareas en el clúster.

8. **¿Cómo se inicia una sesión de Spark?**  
   Se inicia creando un `SparkSession` en código o ejecutando `spark-shell` en la línea de comandos.

9. **¿Qué es un SparkSession y cuál es su función?**  
   Es el punto de entrada unificado para trabajar con Spark, reemplazando la necesidad de `SparkContext`, `SQLContext` y `HiveContext`.

10. **¿Cuáles son los principales entornos donde se puede ejecutar Spark?**  
    - Modo local en una sola máquina.
    - Clúster Hadoop YARN.
    - Apache Mesos.
    - Kubernetes.
    - Servicios en la nube como AWS EMR, Databricks, Google Cloud Dataproc.

### ⚡ Arquitectura y Funcionamiento

11. **¿Qué es un RDD y cómo se diferencia de un DataFrame?**  
    - **RDD (Resilient Distributed Dataset)**: Estructura fundamental en Spark, basada en datos distribuidos y procesamiento inmutable.
    - **DataFrame**: Colección de datos organizados en formato tabular, optimizados con Catalyst Optimizer y más fáciles de usar que los RDDs.

12. **¿Cómo se crean y transforman los RDDs en Spark?**  
    - Desde colecciones locales usando `parallelize()`.
    - Desde archivos almacenados en HDFS, S3, etc.
    - Aplicando transformaciones como `map()`, `filter()`, `flatMap()`.

13. **¿Qué operaciones se pueden realizar en un RDD?**  
    - **Transformaciones**: `map()`, `filter()`, `reduceByKey()`.
    - **Acciones**: `count()`, `collect()`, `take()`.

14. **¿Qué es el Lazy Evaluation en Spark y por qué es importante?**  
    Significa que las transformaciones en Spark no se ejecutan inmediatamente, sino que se construye un plan de ejecución que solo se activa cuando se realiza una acción. Esto optimiza el rendimiento y reduce la sobrecarga de cálculo.

15. **¿Qué es el Directed Acyclic Graph (DAG) en Spark?**  
    Es un gráfico que representa la secuencia de operaciones en una tarea de Spark, optimizando la ejecución y eliminando redundancias.

16. **¿Cómo funciona la planificación de tareas en Spark?**  
    - El Driver convierte las operaciones en un DAG.
    - Divide el DAG en Stages.
    - Distribuye tareas entre ejecutores en un clúster.

17. **¿Qué papel juegan los ejecutores en la ejecución de tareas?**  
    Son procesos que ejecutan tareas asignadas por el Driver y administran la memoria para el almacenamiento en caché.

18. **¿Cómo maneja Spark la tolerancia a fallos?**  
    - **Lineage de RDDs**: Permite reconstruir datos a partir de transformaciones previas.
    - **Replicación en memoria y disco**.
    - **Reejecución de tareas fallidas**.

19. **¿Qué es la ejecución especulativa en Spark y cuándo se usa?**  
    Es una función que detecta tareas lentas y las reejecuta en otros nodos para evitar cuellos de botella.

20. **¿Cómo se optimiza el número de particiones en un trabajo de Spark?**  
    - Ajustando `repartition(n)` o `coalesce(n)` según la carga de datos.
    - Configurando `spark.default.parallelism` en base al número de núcleos disponibles.

### 🔄 Transformaciones y Acciones

21. **¿Cuál es la diferencia entre transformaciones y acciones en Spark?**  
    - **Transformaciones**: Devuelven un nuevo RDD/DataFrame sin ejecutarse inmediatamente. Ejemplo: `map()`, `filter()`, `groupByKey()`.
    - **Acciones**: Ejecutan las transformaciones y devuelven un resultado al driver. Ejemplo: `count()`, `collect()`, `take()`.

22. **¿Qué es un narrow transformation y un wide transformation?**  
    - **Narrow Transformation**: Las operaciones afectan solo una partición, sin requerir redistribución de datos. Ejemplo: `map()`, `filter()`.
    - **Wide Transformation**: Requiere redistribuir datos entre múltiples particiones (shuffle). Ejemplo: `groupByKey()`, `reduceByKey()`.

23. **¿Cuáles son ejemplos de transformaciones comunes en Spark?**  
    - `map()`, `flatMap()`, `filter()`, `groupByKey()`, `reduceByKey()`, `repartition()`, `coalesce()`.

24. **¿Cuáles son ejemplos de acciones comunes en Spark?**  
    - `count()`, `collect()`, `take()`, `first()`, `saveAsTextFile()`, `foreach()`.

25. **¿Qué es el proceso de Shuffle en Spark?**  
    Es el proceso de redistribución de datos entre particiones, ocurre en operaciones como `groupByKey()` y `join()`, y puede afectar el rendimiento debido al tráfico de red.

26. **¿Cómo se minimiza el Shuffle en Spark?**  
    - Usar `reduceByKey()` en lugar de `groupByKey()`.
    - Ajustar el número de particiones con `coalesce()` en lugar de `repartition()`.
    - Evitar joins innecesarios y usar `broadcast()` cuando sea posible.

27. **¿Cómo funcionan las transformaciones `map()` y `flatMap()`?**  
    - `map()`: Aplica una función a cada elemento del RDD/DataFrame y devuelve un solo valor por entrada.
    - `flatMap()`: Similar a `map()`, pero permite devolver múltiples valores por entrada, resultando en una estructura aplanada.

28. **¿Cómo se diferencian `groupByKey()` y `reduceByKey()`?**  
    - `groupByKey()`: Agrupa los valores por clave sin reducirlos, lo que puede generar un alto uso de memoria y shuffle.
    - `reduceByKey()`: Aplica una función de reducción directamente en cada clave antes del shuffle, mejorando el rendimiento.

29. **¿Por qué `reduceByKey()` es más eficiente que `groupByKey()`?**  
    `reduceByKey()` realiza la agregación localmente en cada partición antes del shuffle, lo que minimiza la cantidad de datos transferidos a través de la red.

30. **¿Cómo se pueden unir diferentes conjuntos de datos en Spark?**  
    - Usando `join()` para combinar DataFrames/RDDs basados en una clave común.
    - Optimizando joins con `broadcast()` cuando una de las tablas es pequeña.

### 📊 Spark SQL y DataFrames

31. **¿Qué es Spark SQL y para qué se utiliza?**  
    Es un módulo de Spark que permite consultar datos estructurados usando SQL y APIs de DataFrames/Datasets, proporcionando optimizaciones automáticas a través del **Catalyst Optimizer**.

32. **¿Cuál es la diferencia entre un DataFrame y un Dataset en Spark?**  
    - **DataFrame**: Colección de datos estructurados similar a una tabla SQL, sin tipado estricto.
    - **Dataset**: Similar a un DataFrame, pero con tipado fuerte y más seguridad en tiempo de compilación (solo disponible en Scala y Java).

33. **¿Cómo se crean DataFrames en Spark?**  
    - Desde archivos CSV, JSON, Parquet: `spark.read.format("csv").load("archivo.csv")`.
    - A partir de una consulta SQL: `spark.sql("SELECT * FROM tabla")`.
    - Desde RDDs con `spark.createDataFrame(rdd, schema)`.

34. **¿Cómo se puede ejecutar SQL en Spark?**  
    - Usando `spark.sql("SELECT * FROM tabla")`.
    - Creando una vista temporal con `createOrReplaceTempView()` y ejecutando consultas SQL sobre ella.

35. **¿Qué es una vista temporal en Spark SQL?**  
    Es una vista lógica que permite consultar un DataFrame con SQL dentro de una sesión de Spark, sin persistencia en disco.

36. **¿Qué diferencia hay entre `createOrReplaceTempView()` y `createGlobalTempView()`?**  
    - `createOrReplaceTempView()`: Solo está disponible dentro de la sesión de Spark actual.
    - `createGlobalTempView()`: Disponible en todas las sesiones de Spark dentro del clúster.

37. **¿Cómo se pueden leer datos de diferentes formatos en Spark SQL?**  
    - CSV: `spark.read.csv("archivo.csv")`.
    - JSON: `spark.read.json("archivo.json")`.
    - Parquet: `spark.read.parquet("archivo.parquet")`.
    - ORC: `spark.read.orc("archivo.orc")`.

38. **¿Qué es el Catalyst Optimizer en Spark?**  
    Es el optimizador de consultas de Spark SQL, encargado de transformar y mejorar el plan de ejecución de consultas para maximizar el rendimiento.

39. **¿Cómo funciona el Predicate Pushdown en Spark?**  
    Es una técnica de optimización que filtra los datos lo más cerca posible de la fuente, reduciendo la cantidad de datos leídos y mejorando el rendimiento.

40. **¿Cómo se pueden escribir resultados en diferentes formatos en Spark SQL?**  
    - CSV: `df.write.csv("salida.csv")`.
    - JSON: `df.write.json("salida.json")`.
    - Parquet: `df.write.parquet("salida.parquet")`.
    - ORC: `df.write.orc("salida.orc")`.

### 🔀 Spark Streaming

41. **¿Qué es Spark Streaming y en qué se diferencia de Batch Processing?**  
    Spark Streaming permite procesar datos en tiempo real dividiéndolos en pequeños micro-batches, mientras que Batch Processing procesa datos en lotes estáticos sin una entrada continua.

42. **¿Cuál es la diferencia entre Spark Streaming y Structured Streaming?**  
    - **Spark Streaming** usa **DStreams** (RDDs de datos en tiempo real).
    - **Structured Streaming** usa **DataFrames y Datasets**, lo que permite optimizaciones automáticas con el Catalyst Optimizer y una sintaxis SQL más intuitiva.

43. **¿Cómo se procesa un flujo de datos en Spark Streaming?**  
    1. **Recepción** de datos en micro-batches desde una fuente como Kafka o sockets.
    2. **Transformación** aplicando operaciones como `map()`, `filter()`, `groupBy()`.
    3. **Salida** almacenando los resultados en bases de datos, sistemas de archivos o dashboards.

44. **¿Qué son los DStreams en Spark Streaming?**  
    Son estructuras de datos en Spark Streaming que representan una serie de RDDs en tiempo real y permiten procesamiento distribuido de flujos de datos continuos.

45. **¿Cómo se conecta Spark Streaming con Kafka?**  
    - Usando `spark.readStream.format("kafka")` en Structured Streaming.
    - Usando `KafkaUtils.createDirectStream()` en Spark Streaming tradicional.

46. **¿Cómo se gestiona el checkpointing en Spark Streaming?**  
    El checkpointing guarda el estado de la aplicación en HDFS o S3 para recuperación en caso de fallos, asegurando tolerancia a fallos en el procesamiento de flujos.

47. **¿Qué es el concepto de Watermarking en Structured Streaming?**  
    Es una técnica para manejar eventos tardíos en flujos de datos, estableciendo un límite de tiempo hasta el cual Spark considera datos atrasados en una ventana de agregación.

48. **¿Cómo se manejan eventos tardíos en Spark Streaming?**  
    - Con **Watermarking** para establecer un umbral de retención de datos.
    - Con **ventanas de tiempo** (`window()` en Structured Streaming) para agrupar eventos en intervalos.

49. **¿Qué diferencia hay entre Output Modes en Structured Streaming?**  
    - **Append**: Solo muestra nuevas filas.
    - **Complete**: Reemplaza toda la tabla con cada actualización.
    - **Update**: Solo actualiza las filas modificadas.

50. **¿Cómo se pueden almacenar los resultados de un streaming en Spark?**  
    - En sistemas de archivos (`writeStream.format("parquet").start()`).
    - En bases de datos (`writeStream.format("jdbc")`).
    - En Kafka (`writeStream.format("kafka")`).

### 🚀 Optimización en Spark

51. **¿Qué es Adaptive Query Execution (AQE) en Spark?**  
    Es una optimización en tiempo de ejecución que ajusta dinámicamente particiones y estrategias de join según los datos reales procesados.

52. **¿Cómo se puede mejorar el rendimiento de consultas en Spark SQL?**  
    - Usar formatos como Parquet y ORC.
    - Habilitar AQE (`spark.sql.adaptive.enabled = true`).
    - Aplicar filtrado temprano (`WHERE` antes de `JOIN`).

53. **¿Qué son los Broadcast Joins y cuándo se usan?**  
    Son una optimización donde Spark envía una tabla pequeña a todos los ejecutores en lugar de hacer un shuffle masivo, útil cuando una de las tablas es pequeña (`broadcast(df)`).

54. **¿Cómo afecta el número de particiones al rendimiento de Spark?**  
    - **Pocas particiones** pueden causar un uso ineficiente de los recursos.
    - **Demasiadas particiones** pueden aumentar la sobrecarga de administración de tareas.

55. **¿Cómo optimizar un Shuffle en Spark?**  
    - Usar `reduceByKey()` en lugar de `groupByKey()`.
    - Reducir el número de particiones (`coalesce()`).
    - Habilitar AQE (`spark.sql.adaptive.enabled = true`).

56. **¿Qué es `spark.sql.shuffle.partitions` y cuándo ajustarlo?**  
    Es el número de particiones usadas en operaciones de shuffle en Spark SQL. Se recomienda ajustar según la cantidad de datos y núcleos disponibles (`spark.conf.set("spark.sql.shuffle.partitions", 200)`).

57. **¿Cómo mejorar el rendimiento de escrituras en Spark?**  
    - Usar `partitionBy()` al escribir archivos grandes.
    - Aplicar `coalesce()` para reducir archivos pequeños.
    - Preferir formatos binarios eficientes como Parquet.

58. **¿Cuáles son las mejores prácticas para optimizar la memoria en Spark?**  
    - Usar `persist()` y `cache()` sabiamente.
    - Ajustar `spark.memory.fraction` y `spark.memory.storageFraction`.
    - Evitar `collect()` en grandes volúmenes de datos.

59. **¿Cómo funciona el Garbage Collection en Spark?**  
    - Java GC maneja la memoria de Spark, lo que puede causar pausas.
    - Se puede optimizar con `spark.memory.fraction` y evitando objetos innecesarios en caché.

60. **¿Cómo evitar la fragmentación de archivos al escribir datos en Spark?**  
    - Usar `coalesce()` para reducir la cantidad de archivos pequeños.
    - Configurar `spark.sql.files.maxPartitionBytes` para controlar el tamaño de cada partición.




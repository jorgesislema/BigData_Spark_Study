# ❓ 150 Preguntas Básicas sobre Apache Spark

## 🔥 Introducción
Apache Spark es una de las tecnologías más utilizadas en **Big Data** y **procesamiento distribuido**. A continuación, se presentan **150 preguntas básicas** para entrevistas y aprendizaje con sus respectivas respuestas.

---

## 📌 Preguntas Generales
1. **¿Qué es Apache Spark?**  
   Apache Spark es un motor de procesamiento de datos de código abierto diseñado para el procesamiento distribuido y en memoria.

2. **¿Cuáles son las principales características de Spark?**  
   - Procesamiento en memoria
   - API en múltiples lenguajes
   - Compatibilidad con SQL, ML y Streaming
   - Alta escalabilidad

3. **¿En qué se diferencia Spark de Hadoop MapReduce?**  
   Spark es mucho más rápido porque procesa datos en memoria, mientras que Hadoop usa disco para cada operación intermedia.

4. **¿Cuáles son los componentes principales de Apache Spark?**  
   - Spark Core
   - Spark SQL
   - Spark Streaming
   - MLlib (Machine Learning)
   - GraphX (Procesamiento de grafos)

5. **¿Qué lenguajes de programación son compatibles con Spark?**  
   Python, Scala, Java y R.

6. **¿Qué es Spark Core?**  
   Es el motor central de Spark que maneja tareas de procesamiento distribuido y gestión de memoria.

7. **¿Cuáles son las bibliotecas adicionales que ofrece Spark?**  
   Spark SQL, Spark Streaming, MLlib y GraphX.

8. **¿Qué ventajas tiene Spark sobre otras soluciones de procesamiento de datos?**  
   - Procesamiento en memoria
   - Velocidad superior
   - Soporte para múltiples cargas de trabajo
   - Integración con herramientas de Big Data

9. **¿Cuál es la última versión estable de Apache Spark?**  
   Se debe consultar la documentación oficial en [Apache Spark Releases](https://spark.apache.org/downloads.html).

10. **¿Quién desarrolló Apache Spark y cuándo?**  
   Spark fue desarrollado por **AMPLab de UC Berkeley** en 2009 y donado a la Apache Software Foundation en 2013.

---

## ⚡ Arquitectura y Funcionamiento
11. **¿Qué es un RDD en Spark?**  
    Un **RDD (Resilient Distributed Dataset)** es una colección inmutable y distribuida de elementos que se pueden procesar en paralelo en un clúster de Spark.

12. **¿Cuáles son los tipos de RDDs en Spark?**  
    - **RDD por transformación de datos:** Creado a partir de otros RDDs mediante operaciones como `map()` o `filter()`.
    - **RDD por entrada de datos:** Creado a partir de fuentes externas como HDFS, S3 o bases de datos.

13. **¿Cómo se crean los RDDs en Spark?**  
    - A partir de colecciones en el código (`parallelize`).
    - Desde fuentes externas como HDFS, S3 o bases de datos.
    - Mediante transformaciones en otros RDDs.

14. **¿Qué significa la inmutabilidad en RDDs?**  
    Significa que una vez creado un RDD, no se puede modificar. Cualquier cambio genera un nuevo RDD.

15. **¿Cuáles son las operaciones básicas en RDDs?**  
    - **Transformaciones:** `map()`, `flatMap()`, `filter()`, `reduceByKey()`.
    - **Acciones:** `collect()`, `count()`, `take()`, `saveAsTextFile()`.

16. **¿Qué es un DAG en Spark?**  
    Un **DAG (Directed Acyclic Graph)** es una representación gráfica de la secuencia de operaciones que se ejecutarán en un trabajo de Spark.

17. **¿Cómo maneja Spark la tolerancia a fallos?**  
    - Utiliza **RDD Lineage**, lo que permite reconstruir un RDD en caso de fallo.
    - Usa replicación de datos en caso de ejecución en modo distribuido.

18. **¿Qué es un ejecutor en Spark?**  
    Un **ejecutor** es un proceso que ejecuta tareas en un clúster de Spark y almacena datos en caché si es necesario.

19. **¿Cuál es la diferencia entre Spark Driver y Spark Executor?**  
    - **Spark Driver:** Coordina la ejecución de las tareas y transforma el DAG en tareas distribuidas.
    - **Spark Executor:** Ejecuta las tareas asignadas por el Driver y gestiona la memoria en caché.

20. **¿Cómo funciona el paralelismo en Spark?**  
    - Spark divide los datos en **particiones**, que son procesadas en paralelo por múltiples ejecutores.
    - Cada ejecutor ejecuta varias **tareas** en paralelo, optimizando el uso de los recursos del clúster.

...

# ## 🔄 Transformaciones y Acciones

21. **¿Qué son las transformaciones en Spark?**  
    Son operaciones que generan un nuevo RDD o DataFrame sin modificar el original. Son **perezosas**, lo que significa que no se ejecutan hasta que una acción las activa. Ejemplos: `map()`, `filter()`, `flatMap()`.

22. **¿Qué son las acciones en Spark?**  
    Son operaciones que devuelven un resultado al driver o escriben datos en almacenamiento. Activan la ejecución de las transformaciones. Ejemplos: `collect()`, `count()`, `take()`, `saveAsTextFile()`.

23. **¿Cuál es la diferencia entre transformaciones perezosas y acciones?**  
    Las **transformaciones** son perezosas y solo se computan cuando se llama a una **acción**, lo que permite optimizar la ejecución y evitar cálculos innecesarios.

24. **¿Qué es `map()` y `flatMap()` en Spark?**  
    - `map()`: Aplica una función a cada elemento y devuelve un nuevo RDD/DataFrame con los resultados.
    - `flatMap()`: Similar a `map()`, pero aplana los resultados si la función devuelve múltiples valores.

25. **¿Qué hace la función `filter()` en Spark?**  
    Devuelve un nuevo RDD o DataFrame con los elementos que cumplen una condición específica.

26. **¿Cómo funciona `reduceByKey()`?**  
    Agrupa elementos por clave y aplica una función de reducción en cada grupo, minimizando el shuffle.

27. **¿Qué es `groupByKey()` y por qué se debe evitar?**  
    `groupByKey()` agrupa valores por clave, pero **requiere más memoria y puede generar más tráfico de red** que `reduceByKey()`, por lo que se recomienda evitarlo en grandes volúmenes de datos.

28. **¿Qué diferencia hay entre `repartition()` y `coalesce()`?**  
    - `repartition(n)`: Redistribuye los datos en `n` particiones, generando un shuffle.
    - `coalesce(n)`: Reduce el número de particiones **sin shuffle** cuando es posible, por lo que es más eficiente.

29. **¿Qué es `persist()` y cuándo se usa?**  
    Almacena un RDD/DataFrame en memoria o disco para reutilización, evitando recomputaciones innecesarias.

30. **¿Cuál es la diferencia entre `cache()` y `persist()`?**  
    - `cache()`: Equivalente a `persist(StorageLevel.MEMORY_ONLY)`, almacena en memoria.
    - `persist(level)`: Permite definir el nivel de almacenamiento (memoria, disco o ambos).

---

## 📊 Spark SQL

31. **¿Qué es Spark SQL?**  
    Es un módulo de Apache Spark que permite el procesamiento de datos estructurados mediante consultas SQL o la API de DataFrames/Datasets.

32. **¿Qué son los DataFrames en Spark?**  
    Son estructuras tabulares similares a tablas de bases de datos, optimizadas para trabajar con grandes volúmenes de datos.

33. **¿Cómo se diferencian los DataFrames de los RDDs?**  
    - **RDDs:** Más flexibles pero requieren más código para manipulaciones complejas.
    - **DataFrames:** Más optimizados, usan el **Catalyst Optimizer** y almacenan datos en formato de columnas.

34. **¿Qué es un Dataset en Spark?**  
    Es una estructura similar a un DataFrame pero con **tipado fuerte**, permitiendo mayor seguridad en el código.

35. **¿Cómo se crea un DataFrame en Spark?**  
    - A partir de un archivo CSV, JSON o Parquet.
    - Desde una consulta SQL.
    - A partir de un RDD con `spark.createDataFrame()`.

36. **¿Cómo se puede ejecutar SQL en Spark?**  
    Mediante `spark.sql("SELECT * FROM tabla")` o registrando un DataFrame como tabla temporal.

37. **¿Qué es un `TempView` en Spark?**  
    Una vista temporal que permite ejecutar SQL sobre un DataFrame dentro de una sesión de Spark.

38. **¿Qué diferencia hay entre `createOrReplaceTempView()` y `createGlobalTempView()`?**  
    - `createOrReplaceTempView()`: Solo está disponible en la sesión actual.
    - `createGlobalTempView()`: Disponible en todas las sesiones de Spark.

39. **¿Cómo se puede leer un archivo Parquet en Spark?**  
    ```python
    df = spark.read.parquet("ruta/del/archivo.parquet")
    ```

40. **¿Qué es el Optimizer Catalyst en Spark?**  
    Es el optimizador de consultas de Spark SQL, encargado de transformar y optimizar las consultas para mejorar su rendimiento.

---
## 🔀 Spark Streaming

41. **¿Qué es Spark Streaming?**  
    Es un módulo de Spark que permite el procesamiento en tiempo real de flujos de datos provenientes de fuentes como Kafka, HDFS o sockets.

42. **¿Cuál es la diferencia entre Spark Streaming y Structured Streaming?**  
    - **Spark Streaming** trabaja con microbatches.
    - **Structured Streaming** usa un enfoque basado en consultas continuas con procesamiento optimizado.

43. **¿Qué es un DStream en Spark Streaming?**  
    Es una secuencia de RDDs que representan flujos de datos en Spark Streaming.

44. **¿Cómo se puede conectar Spark Streaming con Kafka?**  
    Usando `spark.readStream.format("kafka")` para consumir mensajes desde un tópico de Kafka.

45. **¿Qué es `checkpointing` en Spark Streaming?**  
    Es una técnica para almacenar estados intermedios y permitir la recuperación en caso de fallo.

46. **¿Cómo se maneja la latencia en Spark Streaming?**  
    Ajustando el intervalo de microbatches y optimizando la paralelización.

47. **¿Cuáles son los modos de salida en Structured Streaming?**  
    - **Append:** Solo agrega nuevos registros.
    - **Complete:** Reescribe toda la tabla.
    - **Update:** Actualiza solo los registros modificados.

48. **¿Cómo se pueden gestionar eventos tardíos en Structured Streaming?**  
    Usando `watermark()` para definir un tiempo de tolerancia a retrasos.

49. **¿Qué es `watermark()` en Structured Streaming?**  
    Es un mecanismo para definir cuánto tiempo se espera eventos tardíos antes de descartarlos.

50. **¿Cómo se configura un flujo de datos en Spark Streaming?**  
    ```python
    df = spark.readStream.format("socket").option("host", "localhost").option("port", 9999).load()
    ```

---


51. **¿Qué es el Broadcast Join en Spark?**  
    Es una técnica para mejorar el rendimiento de los joins cuando una de las tablas es pequeña, transmitiéndola a todos los ejecutores para evitar el shuffle.

52. **¿Cuándo se debe usar `broadcast()` en joins?**  
    Se debe usar cuando una tabla es lo suficientemente pequeña como para caber en la memoria de cada nodo del clúster, reduciendo la sobrecarga del shuffle.

53. **¿Qué es el Shuffle en Spark?**  
    Es el proceso de redistribución de datos entre particiones, generalmente causado por operaciones como `groupBy()`, `reduceByKey()` y `join()`.

54. **¿Cómo se puede optimizar el shuffle en Spark?**  
    - Usar `reduceByKey()` en lugar de `groupByKey()`.
    - Ajustar `spark.sql.shuffle.partitions`.
    - Usar `broadcast()` para joins con tablas pequeñas.
    - Configurar `coalesce()` para reducir particiones sin shuffle.

55. **¿Qué es `spark.sql.shuffle.partitions` y cómo afecta el rendimiento?**  
    Es el número de particiones que se usan en operaciones de shuffle en Spark SQL. Un valor alto mejora la paralelización, pero un valor excesivo puede generar sobrecarga en la gestión de tareas.

56. **¿Qué es AQE (Adaptive Query Execution) en Spark?**  
    Es una funcionalidad que ajusta dinámicamente el plan de ejecución en función de la ejecución en tiempo real, optimizando el número de particiones y la estrategia de joins.

57. **¿Cómo se puede mejorar la ejecución de consultas en Spark SQL?**  
    - Usar **particionamiento adecuado** en los datos.
    - Habilitar AQE (`spark.sql.adaptive.enabled = true`).
    - Aplicar **pruning** en la consulta (`filter` antes de la agregación).
    - Usar formatos eficientes como **Parquet**.

58. **¿Cómo se puede reducir el uso de memoria en Spark?**  
    - Usar `persist(StorageLevel.DISK_ONLY)` para evitar consumir RAM.
    - Evitar `collect()` en grandes volúmenes de datos.
    - Ajustar `spark.memory.fraction` y `spark.memory.storageFraction`.

59. **¿Cómo se puede depurar un trabajo en Spark?**  
    - Revisar logs en la UI de Spark.
    - Usar `explain()` para analizar el plan de ejecución.
    - Habilitar `spark.eventLog.enabled` para registrar eventos y analizar fallos.



## 🔥 Optimización en Spark

60. **¿Qué herramientas se pueden usar para monitorear un trabajo de Spark?**  
    - **Spark UI**: Monitoreo en tiempo real del DAG y tareas.
    - **Ganglia y Prometheus**: Métricas avanzadas.
    - **Event Logs**: Registro detallado del historial de ejecución.

61. **¿Cómo manejar la concurrencia en Spark?**  
    - Ajustando `spark.sql.shuffle.partitions` y `spark.task.cpus`.

62. **¿Qué impacto tiene el Garbage Collection en Spark?**  
    - Puede ralentizar las tareas si hay demasiados objetos en memoria.

63. **¿Cómo manejar datos sesgados en Spark?**  
    - Usando técnicas como **salting** o `skew join optimization`.

64. **¿Qué es la serialización en Spark y cómo optimizarla?**  
    - Configurar `spark.serializer` para usar `KryoSerializer` en vez del predeterminado.

65. **¿Cómo configurar Spark para ejecución en Kubernetes?**  
    - Definiendo `spark.kubernetes.container.image` y `spark.kubernetes.namespace`.

66. **¿Cómo prevenir cuellos de botella en Spark?**  
    - Optimizando el paralelismo y evitando grandes acciones como `collect()`.

67. **¿Qué es un Stage en Spark?**  
    - Una unidad de ejecución de tareas generada por el DAG Scheduler.

68. **¿Cómo mejorar el rendimiento en ETLs con Spark?**  
    - Usar `coalesce()` para reducir el número de archivos pequeños.

69. **¿Cómo evitar el re-procesamiento en Structured Streaming?**  
    - Usando `checkpointing` y `watermark()`.

70. **¿Cómo optimizar joins en tablas grandes en Spark?**  
    - Usar `sort-merge join` en lugar de `broadcast join`.

71. **¿Qué es el cost-based optimizer (CBO) en Spark?**  
    - Un optimizador que mejora los planes de ejecución basado en estadísticas de los datos.

72. **¿Cómo funciona la recolección de estadísticas en Spark?**  
    - Ejecutando `ANALYZE TABLE table_name COMPUTE STATISTICS`.

73. **¿Cómo mejorar el rendimiento de un clúster de Spark?**  
    - Ajustando `spark.dynamicAllocation.enabled` y `spark.executor.instances`.

74. **¿Cómo manejar datos faltantes en Spark?**  
    - Usando `fillna()`, `dropna()` o `replace()` en DataFrames.

75. **¿Cómo mejorar la eficiencia en consultas con filtros?**  
    - Aplicando `predicate pushdown` en la lectura de archivos.

76. **¿Cómo optimizar el uso de CPU en Spark?**  
    - Ajustando `spark.task.cpus` y `spark.executor.cores`.

77. **¿Qué es `spark.memory.offHeap.enabled` y cuándo usarlo?**  
    - Permite gestionar memoria fuera del heap de JVM, útil en grandes cargas de trabajo.

78. **¿Cómo se optimiza el uso de caché en Spark?**  
    - Usando `persist()` en niveles estratégicos y evitando `cache()` innecesario.

79. **¿Cómo reducir la sobrecarga de DAG en Spark?**  
    - Usando `checkpoint()` para cortar la dependencia de linaje.

80. **¿Qué es un task en Spark?**  
    - Una unidad de ejecución individual dentro de un executor.

81. **¿Cómo ajustar `spark.default.parallelism` en Spark?**  
    - Definiéndolo manualmente en base a la capacidad del clúster.

82. **¿Cómo Spark maneja el backpressure en Structured Streaming?**  
    - Ajustando `spark.streaming.backpressure.enabled`.

83. **¿Qué es la compactación en Spark?**  
    - Un proceso que fusiona pequeños archivos en uno más grande para mejorar el rendimiento de lectura.

84. **¿Cómo manejar múltiples fuentes de datos en Spark?**  
    - Usando `union()` y `join()` para combinar datasets.

85. **¿Cómo evitar el re-procesamiento en cargas incrementales en Spark?**  
    - Aplicando `watermark()` y `checkpointing` en Structured Streaming.

86. **¿Cómo Spark maneja la recuperación ante fallos?**  
    - Mediante la re-ejecución de tareas fallidas y uso de DAG lineage.

87. **¿Cómo configurar Spark en entornos con restricciones de memoria?**  
    - Ajustando `spark.memory.fraction` y `spark.memory.storageFraction`.

88. **¿Qué es el `TaskScheduler` en Spark?**  
    - Un componente que asigna tareas a los ejecutores disponibles.

89. **¿Cómo evitar la sobrecarga de logs en Spark?**  
    - Configurando `log4j.properties` y reduciendo el nivel de logs.

90. **¿Cómo optimizar el manejo de grandes volúmenes de datos en Spark?**  
    - Usando **bucketing** y **partitioning** en almacenamiento distribuido.

91. **¿Cómo mejorar el rendimiento en consultas sobre grandes conjuntos de datos en Spark?**

    - Aplicando predicate pushdown y pruning de columnas.

91. **¿Cómo evitar la sobrecarga de shuffle en Spark?**

    - Usando técnicas como coalesce(), reduceByKey() y broadcast() en joins.

92. **¿Qué es el almacenamiento en caché en Spark y cuándo debe usarse?**

    - Permite reutilizar datos en memoria sin necesidad de recálculo, útil para consultas repetitivas.

93. **¿Cómo optimizar la ejecución de Spark en clústeres con recursos limitados?**

    - Ajustando spark.executor.memory, spark.executor.cores y activando dynamic allocation.

94. **¿Cómo se puede mejorar la escalabilidad en Spark?**

    - Ajustando la cantidad de particiones, ejecutores y recursos dinámicos.

95. **¿Qué impacto tiene el número de particiones en el rendimiento de Spark?**

    - Un número bajo de particiones reduce el paralelismo, mientras que demasiadas particiones pueden generar overhead en la gestión de tareas.

96. **¿Cómo minimizar el tiempo de ejecución en Spark?**

    - Aplicando Adaptive Query Execution (AQE) y optimizando la planificación de DAG.

97. **¿Cómo identificar cuellos de botella en Spark?**

    - Usando Spark UI, revisando Stages y Tasks y analizando los tiempos de ejecución.

98. **¿Cómo evitar la fragmentación de archivos en Spark?**

    - Ajustando el tamaño de particiones antes de escribir, usando coalesce() o repartition().

99. **¿Cómo evitar la fragmentación de archivos en Spark?**

    - Ajustando el tamaño de particiones antes de escribir, usando coalesce() o repartition().

100. **¿Cómo se gestiona la paralelización en Spark?**
    - Configurando adecuadamente el número de particiones, tareas y recursos del clúster.


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


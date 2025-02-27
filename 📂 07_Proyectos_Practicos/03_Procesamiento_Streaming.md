# 🔄 Procesamiento de Streaming en Apache Spark

## 🔥 Introducción
El **procesamiento en streaming** permite analizar datos en tiempo real a medida que llegan desde fuentes como sensores, logs, redes sociales y bases de datos. Apache **Spark Streaming** y **Structured Streaming** proporcionan una forma eficiente de procesar estos datos con latencia baja y escalabilidad.

---

## 📌 ¿Por qué usar Spark para Streaming?
✅ **Baja latencia**: Procesamiento en tiempo casi real.
✅ **Escalabilidad**: Funciona en clústeres distribuidos.
✅ **Compatibilidad**: Soporta Kafka, AWS Kinesis, Sockets, y más.
✅ **Integración con SQL y Machine Learning**.

---

## 🛠️ Configuración del Entorno
### 🔹 Inicializar SparkSession para Streaming
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("StreamingSpark") \
    .getOrCreate()
```

---

## 🔄 Lectura de Datos en Streaming
### 🔹 Leer datos desde un Socket (Ejemplo en localhost)
```python
df = spark.readStream \
    .format("socket") \
    .option("host", "localhost") \
    .option("port", 9999) \
    .load()
df.printSchema()
```

### 🔹 Leer datos desde Kafka
```python
df = spark.readStream \
    .format("kafka") \
    .option("kafka.bootstrap.servers", "localhost:9092") \
    .option("subscribe", "mi_topic") \
    .load()
df.selectExpr("CAST(value AS STRING)").show()
```

---

## 📝 Procesamiento de Datos en Streaming
### 🔹 Transformaciones en Tiempo Real
```python
from pyspark.sql.functions import split, col

df_transformed = df.withColumn("palabras", split(col("value"), " "))
df_transformed.writeStream.outputMode("append").format("console").start()
```

### 🔹 Agregaciones con Ventanas de Tiempo
```python
from pyspark.sql.functions import window, count

df_grouped = df.groupBy(window(col("timestamp"), "10 minutes")).count()
df_grouped.writeStream.outputMode("complete").format("console").start()
```

---

## 💾 Escritura de Resultados en Streaming
### 🔹 Guardar en Parquet
```python
df.writeStream \
    .format("parquet") \
    .option("path", "s3a://mi-bucket/output") \
    .option("checkpointLocation", "s3a://mi-bucket/checkpoints") \
    .start()
```

### 🔹 Guardar en Kafka
```python
df.writeStream \
    .format("kafka") \
    .option("kafka.bootstrap.servers", "localhost:9092") \
    .option("topic", "output_topic") \
    .option("checkpointLocation", "/tmp/checkpoints") \
    .start()
```

---

## ⚡ Optimización y Buenas Prácticas
✅ **Usar `checkpointLocation`** para tolerancia a fallos.
✅ **Configurar `trigger`** para optimizar la ejecución:
```python
df.writeStream.trigger(processingTime="5 seconds").start()
```
✅ **Ajustar particiones en Kafka** para mejor paralelismo.

---

## 🎯 Conclusión
Apache **Spark Streaming** permite analizar datos en tiempo real con alta eficiencia. La correcta configuración de **fuentes, transformaciones y almacenamiento** es clave para garantizar un sistema estable y escalable. 🚀


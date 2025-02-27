# ⚡ Integración de Apache Spark con Apache Kafka

## 🔥 Introducción
Apache **Spark** y Apache **Kafka** son dos herramientas clave en el ecosistema de Big Data. **Kafka** es una plataforma de mensajería en tiempo real, mientras que **Spark Streaming** permite procesar flujos de datos en tiempo real con baja latencia.

La combinación de **Spark + Kafka** es ideal para casos de uso como:
- Procesamiento de datos en tiempo real.
- Análisis de logs y métricas.
- ETL en streaming.
- Sistemas de detección de fraude y monitoreo.

---

## 📌 Requisitos Previos
Antes de integrar Spark con Kafka, asegúrate de tener:
✅ Apache Kafka en ejecución.
✅ Apache Spark con soporte para **Spark Structured Streaming**.
✅ Librerías de integración (`spark-sql-kafka-0-10`).

---

## 🛠️ Configuración de Spark para Kafka
### 🔹 Agregar Dependencias
Si usas **PySpark**, agrega la librería de Kafka al ejecutar Spark:
```bash
pyspark --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.2.1
```
Para proyectos en **Scala/Java**, agrega en `build.sbt`:
```sbt
libraryDependencies += "org.apache.spark" %% "spark-sql-kafka-0-10" % "3.2.1"
```

---

## 🔄 Consumiendo Datos desde Kafka en Spark
### 🔹 Conectarse a un Topic de Kafka
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("SparkKafkaIntegration") \
    .getOrCreate()

# Leer mensajes desde Kafka
df = spark.readStream \
    .format("kafka") \
    .option("kafka.bootstrap.servers", "localhost:9092") \
    .option("subscribe", "mi_topic") \
    .option("startingOffsets", "earliest") \
    .load()

df.selectExpr("CAST(key AS STRING)", "CAST(value AS STRING)").show()
```
✅ **Explicación:**
- `kafka.bootstrap.servers`: Servidor de Kafka.
- `subscribe`: Nombre del topic.
- `startingOffsets`: Define desde dónde leer los mensajes (`earliest`, `latest`).

---

## 📝 Escritura de Datos desde Spark a Kafka
### 🔹 Enviar Datos Procesados a Kafka
```python
query = df.selectExpr("CAST(value AS STRING) AS value") \
    .writeStream \
    .format("kafka") \
    .option("kafka.bootstrap.servers", "localhost:9092") \
    .option("topic", "output_topic") \
    .option("checkpointLocation", "/tmp/kafka-checkpoint") \
    .start()
```
✅ **Importante:** `checkpointLocation` es obligatorio para mantener el estado del streaming.

---

## ⚡ Optimización y Buenas Prácticas
✅ **Usar múltiples particiones en Kafka** para paralelizar el procesamiento.
✅ **Configurar `maxOffsetsPerTrigger`** para controlar la carga de datos.
```python
.option("maxOffsetsPerTrigger", "1000")
```
✅ **Utilizar `watermark` para manejar datos retrasados** en eventos de streaming.
```python
df.withWatermark("timestamp", "10 minutes")
```

---

## 🎯 Conclusión
Apache Spark y Kafka forman una combinación poderosa para el procesamiento de datos en tiempo real. Configurar correctamente las conexiones, offsets y particiones permite construir aplicaciones de streaming escalables y eficientes. 🚀


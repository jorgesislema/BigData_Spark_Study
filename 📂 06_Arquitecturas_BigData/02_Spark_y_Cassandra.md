# ⚡ Integración de Apache Spark con Apache Cassandra

## 🔥 Introducción
Apache **Spark** y Apache **Cassandra** forman una poderosa combinación para el procesamiento de datos distribuidos. Mientras que **Cassandra** es una base de datos NoSQL altamente escalable y tolerante a fallos, **Spark** permite realizar análisis de datos en memoria de forma eficiente.

Usar **Spark + Cassandra** es ideal para:
- Procesamiento de datos en tiempo real.
- Consultas analíticas sobre grandes volúmenes de datos.
- Integración con pipelines de Big Data.

---

## 📌 Requisitos Previos
Antes de conectar Spark con Cassandra, asegúrate de tener:
✅ Apache Cassandra instalado y ejecutándose.
✅ Apache Spark con soporte para Spark SQL.
✅ Librería `spark-cassandra-connector`.

---

## 🛠️ Configuración de Spark para Cassandra
### 🔹 Agregar Dependencias
Para conectar Spark con Cassandra, usa el conector oficial.

Si usas **PySpark**, agrega la librería al iniciar Spark:
```bash
pyspark --packages com.datastax.spark:spark-cassandra-connector_2.12:3.2.0
```
Para proyectos en **Scala/Java**, agrega en `build.sbt`:
```sbt
libraryDependencies += "com.datastax.spark" %% "spark-cassandra-connector" % "3.2.0"
```

---

## 🔄 Leer Datos desde Cassandra en Spark
### 🔹 Conectarse a una Tabla de Cassandra
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("SparkCassandraIntegration") \
    .config("spark.cassandra.connection.host", "localhost") \
    .getOrCreate()

df = spark.read \
    .format("org.apache.spark.sql.cassandra") \
    .options(table="usuarios", keyspace="mi_keyspace") \
    .load()
df.show()
```
✅ **Explicación:**
- `spark.cassandra.connection.host`: Dirección del nodo de Cassandra.
- `table`: Nombre de la tabla en Cassandra.
- `keyspace`: Keyspace de la base de datos.

---

## 📝 Escritura de Datos en Cassandra desde Spark
```python
df.write \
    .format("org.apache.spark.sql.cassandra") \
    .options(table="usuarios", keyspace="mi_keyspace") \
    .mode("append") \
    .save()
```
✅ **Modo `append`**: Inserta nuevos registros sin sobrescribir los existentes.

---

## ⚡ Optimización y Buenas Prácticas
✅ **Configurar particionamiento** para mejorar la distribución de datos.
```python
spark.conf.set("spark.sql.shuffle.partitions", "200")
```
✅ **Usar `pushdown` para optimizar consultas** en Cassandra.
```python
spark.conf.set("spark.cassandra.input.consistency.level", "LOCAL_ONE")
```
✅ **Evitar `collect()`** en grandes volúmenes de datos para prevenir problemas de memoria.
```python
df.limit(10).show()
```

---

## 🎯 Conclusión
La integración de **Apache Spark y Cassandra** permite realizar análisis en tiempo real y procesar datos de forma distribuida. Configurar correctamente la conexión y optimizar consultas ayuda a mejorar el rendimiento y escalabilidad. 🚀
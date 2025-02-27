# 🏗️ Integración de Apache Spark con Hadoop

## 🔥 Introducción
Apache **Spark** y **Hadoop** se complementan para procesar grandes volúmenes de datos de manera eficiente. **Hadoop HDFS** proporciona almacenamiento distribuido, mientras que **Spark** permite ejecutar cálculos en memoria, logrando una ejecución más rápida que MapReduce.

Usar **Spark + Hadoop** es ideal para:
- Procesamiento distribuido de grandes datasets.
- Integración con clústeres Hadoop existentes.
- Ejecución de ETL y Machine Learning a gran escala.

---

## 📌 Requisitos Previos
Antes de conectar Spark con Hadoop, asegúrate de tener:
✅ Un clúster **Hadoop HDFS** configurado y en ejecución.
✅ Apache **Spark** instalado y configurado para acceder a HDFS.
✅ Variables de entorno definidas (`HADOOP_HOME`, `SPARK_HOME`).

---

## 🛠️ Configuración de Spark para Hadoop
### 🔹 Configurar Variables de Entorno
En Linux/Mac, edita `~/.bashrc`:
```bash
export HADOOP_HOME=/usr/local/hadoop
export SPARK_HOME=/usr/local/spark
export PATH=$PATH:$HADOOP_HOME/bin:$SPARK_HOME/bin
```

### 🔹 Agregar Dependencias
Si usas **PySpark**, inicia Spark con las librerías de Hadoop:
```bash
pyspark --packages org.apache.hadoop:hadoop-client:3.2.0
```
Para proyectos en **Scala/Java**, agrega en `build.sbt`:
```sbt
libraryDependencies += "org.apache.hadoop" % "hadoop-client" % "3.2.0"
```

---

## 🔄 Leer Datos desde HDFS en Spark
### 🔹 Leer un archivo Parquet desde HDFS
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("SparkHadoop") \
    .config("spark.hadoop.fs.defaultFS", "hdfs://localhost:9000") \
    .getOrCreate()

df = spark.read.parquet("hdfs://localhost:9000/datos/output.parquet")
df.show()
```
✅ **Explicación:**
- `fs.defaultFS`: Define la dirección de HDFS.
- `hdfs://localhost:9000`: Indica la ubicación del NameNode.

### 🔹 Leer un archivo CSV desde HDFS
```python
df = spark.read.option("header", "true").csv("hdfs://localhost:9000/datos/dataset.csv")
df.show()
```

---

## 📝 Escritura de Datos en HDFS desde Spark
```python
df.write.mode("overwrite").parquet("hdfs://localhost:9000/datos/output.parquet")
```
✅ **Modo `overwrite`**: Reemplaza los archivos existentes.

---

## ⚡ Optimización y Buenas Prácticas
✅ **Usar formato Parquet en lugar de CSV** para mejorar el rendimiento.
✅ **Evitar `collect()`** en grandes volúmenes de datos para prevenir sobrecarga en el driver.
✅ **Configurar `dfs.replication`** para mejorar la tolerancia a fallos:
```bash
hdfs dfs -setrep -w 3 /datos/output.parquet
```

---

## 🎯 Conclusión
La integración de **Apache Spark y Hadoop** permite almacenar y procesar datos de manera distribuida con alto rendimiento. Configurar correctamente las conexiones y optimizar el acceso a los datos mejora la escalabilidad y eficiencia del sistema. 🚀


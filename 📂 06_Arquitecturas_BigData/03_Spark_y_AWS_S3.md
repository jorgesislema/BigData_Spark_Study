# ☁️ Integración de Apache Spark con AWS S3

## 🔥 Introducción
Apache **Spark** y **AWS S3** permiten almacenar y procesar grandes volúmenes de datos de manera escalable y eficiente. **S3** es un almacenamiento distribuido en la nube, mientras que **Spark** ofrece procesamiento paralelo para grandes datasets.

La integración de **Spark + S3** es ideal para:
- Almacenar grandes volúmenes de datos en la nube.
- Ejecutar **ETL** sobre datos en S3.
- Procesar datos sin necesidad de clústeres Hadoop tradicionales.

---

## 📌 Requisitos Previos
Antes de conectar Spark con S3, asegúrate de tener:
✅ Una cuenta de AWS con un **bucket S3** creado.
✅ Apache Spark instalado con **Hadoop AWS**.
✅ Credenciales de AWS configuradas.

---

## 🛠️ Configuración de Spark para AWS S3
### 🔹 Agregar Dependencias
Si usas **PySpark**, inicia Spark con las librerías de AWS:
```bash
pyspark --packages org.apache.hadoop:hadoop-aws:3.2.0
```
Para proyectos en **Scala/Java**, agrega en `build.sbt`:
```sbt
libraryDependencies += "org.apache.hadoop" % "hadoop-aws" % "3.2.0"
```

### 🔹 Configurar Credenciales de AWS en Spark
```python
spark = SparkSession.builder \
    .appName("SparkAWS") \
    .config("spark.hadoop.fs.s3a.access.key", "TU_ACCESS_KEY") \
    .config("spark.hadoop.fs.s3a.secret.key", "TU_SECRET_KEY") \
    .config("spark.hadoop.fs.s3a.endpoint", "s3.amazonaws.com") \
    .getOrCreate()
```
✅ **Alternativa**: Configurar credenciales en `~/.aws/credentials`.

---

## 🔄 Leer Datos desde AWS S3 en Spark
### 🔹 Leer un archivo Parquet desde S3
```python
df = spark.read.parquet("s3a://mi-bucket/datos.parquet")
df.show()
```

### 🔹 Leer un archivo CSV desde S3
```python
df = spark.read.option("header", "true").csv("s3a://mi-bucket/datos.csv")
df.show()
```

---

## 📝 Escritura de Datos en AWS S3 desde Spark
```python
df.write.mode("overwrite").parquet("s3a://mi-bucket/output.parquet")
```
✅ **Modo `overwrite`**: Reemplaza el archivo si ya existe.

---

## ⚡ Optimización y Buenas Prácticas
✅ **Usar formato Parquet o Avro** para mejorar la compresión y velocidad.
✅ **Evitar `collect()`** en grandes volúmenes de datos para prevenir sobrecarga.
✅ **Configurar `fs.s3a.multipart.size`** para mejorar rendimiento en escrituras grandes.
```python
spark.conf.set("spark.hadoop.fs.s3a.multipart.size", "104857600")  # 100 MB
```

---

## 🎯 Conclusión
La integración de **Apache Spark y AWS S3** permite el procesamiento eficiente de datos en la nube sin necesidad de clústeres tradicionales. Configurar correctamente la conexión y optimizar el acceso a los datos mejora la eficiencia del sistema. 🚀


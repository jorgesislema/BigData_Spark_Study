# 📂 Lectura y Escritura de Datos en Apache Spark

## 🔥 Introducción
Apache Spark permite leer y escribir datos en múltiples formatos como **CSV, JSON, Parquet, ORC, Avro y JDBC**. Esto facilita la integración con bases de datos, sistemas de almacenamiento y análisis de Big Data.

---

## 📌 Leer Datos en Spark
### 🔹 Leer un archivo CSV
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("LeerCSV").getOrCreate()
df = spark.read.format("csv").option("header", "true").option("inferSchema", "true").load("/ruta/datos.csv")
df.show()
```
📌 **Explicación:**
- `format("csv")`: Especifica el formato del archivo.
- `option("header", "true")`: Usa la primera fila como nombres de columnas.
- `option("inferSchema", "true")`: Detecta automáticamente los tipos de datos.

### 🔹 Leer un archivo JSON
```python
df_json = spark.read.json("/ruta/datos.json")
df_json.show()
```

### 🔹 Leer un archivo Parquet
```python
df_parquet = spark.read.parquet("/ruta/datos.parquet")
df_parquet.show()
```

### 🔹 Leer desde una Base de Datos JDBC
```python
df_jdbc = spark.read \
    .format("jdbc") \
    .option("url", "jdbc:mysql://localhost:3306/mi_bd") \
    .option("dbtable", "usuarios") \
    .option("user", "root") \
    .option("password", "password") \
    .load()
df_jdbc.show()
```

---

## 📝 Guardar Datos en Spark
### 🔹 Guardar como CSV
```python
df.write.format("csv").option("header", "true").save("/ruta/output.csv")
```

### 🔹 Guardar como JSON
```python
df.write.json("/ruta/output.json")
```

### 🔹 Guardar como Parquet
```python
df.write.parquet("/ruta/output.parquet")
```

### 🔹 Guardar en una Base de Datos JDBC
```python
df.write \
    .format("jdbc") \
    .option("url", "jdbc:mysql://localhost:3306/mi_bd") \
    .option("dbtable", "usuarios_guardados") \
    .option("user", "root") \
    .option("password", "password") \
    .save()
```

---

## 🏎️ Consideraciones de Rendimiento
✅ **Usar Parquet en lugar de CSV** para mejor compresión y velocidad.
✅ **Especificar particiones (`partitionBy`)** para grandes volúmenes de datos.
✅ **Configurar `mode`** (`overwrite`, `append`, `ignore`, `error`) al escribir datos.

Ejemplo de particionado y modo de escritura:
```python
df.write.mode("overwrite").partitionBy("categoria").parquet("/ruta/output")
```

---

## 🎯 Conclusión
Leer y guardar datos en Spark es un proceso eficiente gracias a su compatibilidad con múltiples formatos y su capacidad de optimización. Usar formatos como **Parquet** y configurar correctamente las opciones mejora el rendimiento y la escalabilidad. 🚀


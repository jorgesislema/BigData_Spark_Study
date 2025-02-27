# 🚨 Casos Reales de Errores en Apache Spark y Cómo Solucionarlos

## 🔥 Introducción
Apache Spark es una herramienta poderosa, pero su ejecución distribuida puede generar **errores difíciles de depurar**. Aquí analizamos **casos reales de errores**, su causa y la mejor forma de solucionarlos.

---

## ⚠️ 1️⃣ Error: `OutOfMemoryError`
### ❌ Problema:
El trabajo de Spark consume más memoria de la disponible en el ejecutor.

### ✅ Solución:
✔ **Ajustar la memoria de los ejecutores**:
```python
spark.conf.set("spark.executor.memory", "8g")
```
✔ **Evitar `collect()` en grandes volúmenes de datos**:
```python
df.take(10)  # En lugar de df.collect()
```
✔ **Usar `cache()` con precaución**:
```python
df.persist()
```

---

## ⚠️ 2️⃣ Error: `Task Not SerializableException`
### ❌ Problema:
Spark no puede serializar una función o variable dentro de una transformación distribuida.

### ✅ Solución:
✔ **Evitar el uso de objetos complejos en `map()`**:
```python
def transform(row):
    return row["columna"] * 2

rdd.map(transform)  # ⚠️ Esto puede fallar
```
✔ **Usar funciones lambda o `udf()` de PySpark**:
```python
from pyspark.sql.functions import udf
from pyspark.sql.types import IntegerType

def multiply_by_two(x):
    return x * 2

multiply_udf = udf(multiply_by_two, IntegerType())
df = df.withColumn("new_col", multiply_udf(df["columna"]))
```

---

## ⚠️ 3️⃣ Error: `Job Aborted due to Stage Failure`
### ❌ Problema:
Un **shuffle** excesivo o fallos en la red pueden abortar el trabajo de Spark.

### ✅ Solución:
✔ **Reducir el número de particiones en Shuffle**:
```python
spark.conf.set("spark.sql.shuffle.partitions", "200")
```
✔ **Optimizar `joins` con `broadcast()`**:
```python
from pyspark.sql.functions import broadcast

df1.join(broadcast(df2), "id").show()
```
✔ **Verificar errores en los ejecutores con**:
```python
spark.sparkContext.statusTracker.getExecutorInfos()
```

---

## ⚠️ 4️⃣ Error: `FileNotFoundException` en HDFS o S3
### ❌ Problema:
Spark no encuentra un archivo en HDFS o S3.

### ✅ Solución:
✔ **Verificar la ruta del archivo**:
```python
hdfs dfs -ls /ruta/archivo.parquet
```
✔ **Usar rutas completas y con prefijos correctos**:
```python
df = spark.read.parquet("s3a://mi-bucket/datos.parquet")
```
✔ **Revisar permisos de acceso en S3 o HDFS**:
```python
spark.conf.set("fs.s3a.access.key", "TU_ACCESS_KEY")
```

---

## 🎯 Conclusión
Detectar y corregir errores en Apache Spark requiere **conocimiento de logs, optimización y configuración**. Aplicar buenas prácticas ayuda a prevenir fallos y mejorar el rendimiento. 🚀


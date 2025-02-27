# 🔄 ETL en Apache Spark

## 🔥 Introducción
El proceso **ETL (Extract, Transform, Load)** es esencial en el mundo del **Big Data** para mover y transformar grandes volúmenes de datos. Apache **Spark** es una de las herramientas más eficientes para realizar ETL de manera distribuida y escalable.

---

## 📌 ¿Qué es ETL?
**ETL** consiste en tres fases principales:
1. **Extract (Extracción):** Obtención de datos desde múltiples fuentes.
2. **Transform (Transformación):** Limpieza, enriquecimiento y agregación de datos.
3. **Load (Carga):** Almacenamiento de los datos procesados en un destino final (Data Warehouse, Lakehouse, etc.).

---

## 🛠️ Implementación de ETL con PySpark
### 🔹 1. Inicializar SparkSession
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("ETL_Spark") \
    .getOrCreate()
```

---

### 🔹 2. Extracción de Datos
Podemos extraer datos desde varias fuentes:
#### 📂 **Desde un archivo CSV**
```python
df = spark.read.option("header", "true").csv("s3a://mi-bucket/datos.csv")
df.show()
```
#### 🗄️ **Desde una base de datos SQL**
```python
df = spark.read \
    .format("jdbc") \
    .option("url", "jdbc:mysql://localhost:3306/mi_bd") \
    .option("dbtable", "usuarios") \
    .option("user", "root") \
    .option("password", "password") \
    .load()
df.show()
```

---

### 🔹 3. Transformación de Datos
#### 🔹 **Limpieza y Filtrado**
```python
df = df.dropna()  # Elimina valores nulos
df = df.filter(df["edad"] > 18)  # Filtra mayores de 18 años
```

#### 🔹 **Agregaciones y Cálculos**
```python
from pyspark.sql.functions import col, avg

df_agg = df.groupBy("ciudad").agg(avg("salario").alias("salario_promedio"))
df_agg.show()
```

---

### 🔹 4. Carga de Datos
#### 🏛️ **Guardar en Parquet**
```python
df.write.mode("overwrite").parquet("s3a://mi-bucket/output.parquet")
```

#### 📊 **Guardar en una base de datos SQL**
```python
df.write \
    .format("jdbc") \
    .option("url", "jdbc:mysql://localhost:3306/mi_bd") \
    .option("dbtable", "usuarios_procesados") \
    .option("user", "root") \
    .option("password", "password") \
    .save()
```

---

## ⚡ Optimización en ETL con Spark
✅ **Usar formato Parquet** en lugar de CSV para mejorar la compresión y velocidad.
✅ **Ajustar el número de particiones** para optimizar el rendimiento:
```python
df = df.repartition(10)
```
✅ **Cachear datos** si se reutilizan en múltiples pasos:
```python
df.cache()
```

---

## 🎯 Conclusión
Apache **Spark** es una solución potente para procesos ETL en **Big Data**, permitiendo mover, transformar y almacenar datos de manera eficiente. Ajustar configuraciones y buenas prácticas mejora significativamente el rendimiento. 🚀


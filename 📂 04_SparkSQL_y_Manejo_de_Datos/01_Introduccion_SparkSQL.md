# 🗄️ Introducción a Spark SQL

## 🔥 ¿Qué es Spark SQL?
**Spark SQL** es un módulo de **Apache Spark** que permite procesar datos estructurados utilizando consultas **SQL**, APIs de DataFrames y **Dataset API**. Es una de las herramientas más potentes de Spark para manipular grandes volúmenes de datos con facilidad y optimización.

---

## 📌 Beneficios de Spark SQL
- ✅ **Optimización automática** con **Catalyst Optimizer**.
- ✅ **Interoperabilidad** con SQL estándar y DataFrames.
- ✅ **Soporte para múltiples fuentes de datos**: JSON, Parquet, Avro, JDBC, HDFS.
- ✅ **Integración con herramientas BI** como Tableau y Power BI.

---

## 🛠️ Creación de una SparkSession
Para usar **Spark SQL**, primero es necesario crear una **SparkSession**:
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("EjemploSparkSQL").getOrCreate()
```

---

## 📊 Creación de un DataFrame desde Datos
Podemos crear un **DataFrame** en Spark SQL a partir de una lista de datos:
```python
data = [("Alice", 25), ("Bob", 30), ("Charlie", 35)]
df = spark.createDataFrame(data, ["Nombre", "Edad"])
df.show()
```
Salida esperada:
```
+-------+----+
| Nombre|Edad|
+-------+----+
|  Alice|  25|
|    Bob|  30|
|Charlie|  35|
+-------+----+
```

---

## 🏛️ Uso de Consultas SQL en Spark SQL
### 🔹 Registrar un DataFrame como Tabla Temporal
Para ejecutar consultas SQL sobre un **DataFrame**, primero debemos registrarlo como una tabla temporal:
```python
df.createOrReplaceTempView("personas")
```

### 🔹 Ejecutar Consultas SQL
Una vez registrado, podemos ejecutar consultas SQL directamente:
```python
resultado = spark.sql("SELECT * FROM personas WHERE Edad > 25")
resultado.show()
```
Salida esperada:
```
+-------+----+
| Nombre|Edad|
+-------+----+
|    Bob|  30|
|Charlie|  35|
+-------+----+
```

---

## 📂 Lectura y Escritura de Archivos con Spark SQL
### 🔹 Leer un archivo JSON
```python
df_json = spark.read.json("/ruta/datos.json")
df_json.show()
```

### 🔹 Guardar un DataFrame en formato Parquet
```python
df.write.parquet("/ruta/output.parquet")
```

---

## ⚡ Comparación entre DataFrames y SQL en Spark
| Característica  | DataFrame API  | Spark SQL  |
|---------------|---------------|------------|
| **Sintaxis** | Python/Scala API | Consultas SQL |
| **Optimización** | Sí (Catalyst) | Sí (Catalyst) |
| **Facilidad de Uso** | Mejor para programación | Familiar para SQL users |
| **Compatibilidad** | Soporta Python, Scala, Java | Solo SQL |

---

## 🎯 Conclusión
Spark SQL combina el poder de **Apache Spark** con la facilidad de **SQL**, permitiendo trabajar con grandes volúmenes de datos de manera eficiente. Su optimización automática lo hace una excelente opción para análisis de datos a gran escala. 🚀


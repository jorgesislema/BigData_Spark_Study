# 🗄️ Operaciones sobre Tablas en Apache Spark

## 🔥 Introducción
En **Apache Spark SQL**, las **tablas** permiten manejar datos estructurados de manera eficiente. Se pueden crear, consultar, modificar y eliminar dentro de un entorno distribuido, lo que facilita la gestión de grandes volúmenes de datos.

---

## 📌 Creación de Tablas en Spark SQL
### 🔹 Crear una Tabla Temporal
Una **tabla temporal** existe solo durante la sesión de Spark y se elimina al cerrarla.
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("TablasSpark").getOrCreate()

data = [("Alice", 25), ("Bob", 30), ("Charlie", 35)]
df = spark.createDataFrame(data, ["Nombre", "Edad"])

df.createOrReplaceTempView("personas")
```
✅ Ahora podemos consultar la tabla con SQL.
```python
spark.sql("SELECT * FROM personas").show()
```

### 🔹 Crear una Tabla Permanente
Las **tablas permanentes** se almacenan en un metastore y persisten después de cerrar la sesión.
```python
spark.sql("CREATE TABLE personas_permanente (Nombre STRING, Edad INT) USING PARQUET")
```

---

## 🛠️ Consultas y Modificación de Tablas

### 🔹 Insertar Datos en una Tabla
```python
spark.sql("INSERT INTO personas_permanente VALUES ('David', 40)")
```

### 🔹 Actualizar Datos en una Tabla
Spark SQL no tiene `UPDATE`, pero podemos recrear la tabla con datos modificados.
```python
spark.sql("SELECT * FROM personas_permanente WHERE Nombre != 'David'").write.mode("overwrite").saveAsTable("personas_permanente")
```

### 🔹 Eliminar Datos en una Tabla
```python
spark.sql("DELETE FROM personas_permanente WHERE Edad < 30")
```

### 🔹 Eliminar una Tabla
```python
spark.sql("DROP TABLE IF EXISTS personas_permanente")
```

---

## 📂 Cargar Datos desde Archivos a una Tabla
### 🔹 Cargar desde CSV
```python
spark.sql("CREATE TABLE ventas USING CSV OPTIONS (path '/ruta/archivo.csv', header 'true')")
```

### 🔹 Cargar desde Parquet
```python
spark.sql("CREATE TABLE datos_parquet USING PARQUET LOCATION '/ruta/output.parquet'")
```

---

## 🏆 Comparación entre Tablas Temporales y Permanentes
| Característica | Tablas Temporales | Tablas Permanentes |
|--------------|-----------------|-----------------|
| **Duración** | Solo en la sesión | Persisten en el metastore |
| **Uso** | Análisis rápido | Almacenamiento estructurado |
| **Formato** | En memoria | Parquet, JSON, Avro, etc. |

---

## 🎯 Conclusión
Las **tablas en Apache Spark SQL** permiten gestionar datos estructurados de manera flexible. Mientras que las **tablas temporales** son útiles para análisis rápidos, las **tablas permanentes** facilitan la persistencia y reutilización de datos en múltiples sesiones. 🚀


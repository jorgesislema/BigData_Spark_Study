# 📊 Agrupaciones y Agregaciones en Apache Spark

## 🔥 Introducción
En **Apache Spark**, las operaciones de **agrupación y agregación** permiten resumir y analizar grandes volúmenes de datos de manera eficiente. Estas operaciones son ampliamente utilizadas en tareas como generación de reportes, análisis de tendencias y procesamiento de datos a gran escala.

---

## 📌 Diferencia entre Agrupaciones y Agregaciones
| Operación | Descripción |
|-----------|------------|
| **Agrupación (`groupBy`)** | Agrupa los datos en función de un campo específico, generando un conjunto de grupos. |
| **Agregación (`agg`)** | Aplica funciones de agregación (como suma, promedio, conteo) sobre los grupos de datos creados. |

---

## 🛠️ Agrupaciones en PySpark

### 🔹 `groupBy()` – Agrupar Datos
La función `groupBy()` permite agrupar un DataFrame según una o más columnas.
```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import count

spark = SparkSession.builder.appName("Agrupaciones").getOrCreate()

# Crear un DataFrame de ejemplo
data = [("Alice", "Ventas", 5000), ("Bob", "Ventas", 6000),
        ("Charlie", "IT", 7000), ("David", "IT", 8000)]
df = spark.createDataFrame(data, ["Nombre", "Departamento", "Salario"])

# Agrupar por Departamento
df_grouped = df.groupBy("Departamento").count()
df_grouped.show()
```
Salida esperada:
```
+------------+-----+
|Departamento|count|
+------------+-----+
|      Ventas|    2|
|         IT|    2|
+------------+-----+
```

---

## 📂 Agregaciones en PySpark

### 🔹 `agg()` – Aplicar Funciones de Agregación
Podemos utilizar `agg()` para realizar múltiples agregaciones en los datos agrupados.
```python
from pyspark.sql.functions import sum, avg, max, min

# Aplicar funciones de agregación
df_agg = df.groupBy("Departamento").agg(
    sum("Salario").alias("Total_Salarios"),
    avg("Salario").alias("Salario_Promedio"),
    max("Salario").alias("Salario_Max"),
    min("Salario").alias("Salario_Min")
)
df_agg.show()
```
Salida esperada:
```
+------------+--------------+---------------+------------+------------+
|Departamento|Total_Salarios|Salario_Promedio|Salario_Max|Salario_Min|
+------------+--------------+---------------+------------+------------+
|      Ventas|        11000 |         5500.0|        6000|        5000|
|         IT |        15000 |         7500.0|        8000|        7000|
+------------+--------------+---------------+------------+------------+
```

---

## ⚡ Funciones de Agregación en Spark SQL
También podemos usar **Spark SQL** para realizar agregaciones con consultas SQL.
```python
# Registrar el DataFrame como tabla temporal
df.createOrReplaceTempView("empleados")

# Ejecutar una consulta SQL con agregaciones
resultado = spark.sql("""
    SELECT Departamento, SUM(Salario) AS Total_Salarios,
           AVG(Salario) AS Salario_Promedio
    FROM empleados
    GROUP BY Departamento
""")
resultado.show()
```

---

## 🏎️ Comparación entre `groupBy()` y `reduceByKey()`
| Operación | Uso | Ventaja |
|-----------|-----|---------|
| `groupBy()` | Se usa en DataFrames | Permite aplicar múltiples funciones de agregación |
| `reduceByKey()` | Se usa en RDDs | Optimizado para agregaciones en grandes volúmenes de datos |

---

## 🎯 Conclusión
Las **agrupaciones y agregaciones en Spark** son esenciales para el procesamiento eficiente de datos. Mientras que `groupBy()` es ideal para trabajar con DataFrames y aplicar múltiples funciones de agregación, **`reduceByKey()`** sigue siendo una excelente opción en **RDDs** para cálculos optimizados. 🚀


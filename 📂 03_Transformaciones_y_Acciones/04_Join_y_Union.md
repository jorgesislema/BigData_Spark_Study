# 🔗 Joins y Uniones en Apache Spark

## 🔥 Introducción
En **Apache Spark**, las operaciones de **Join** y **Union** permiten combinar datos de diferentes **DataFrames** o **RDDs**, facilitando la integración de múltiples fuentes de datos y el análisis avanzado de información.

---

## 📌 Diferencia entre Join y Union
| Operación | Descripción |
|-----------|------------|
| **Join** | Combina filas de dos DataFrames en base a una clave común (similar a SQL JOIN). |
| **Union** | Combina filas de dos DataFrames sin claves comunes (similar a UNION en SQL). |

---

## 🛠️ Tipos de Joins en Spark
### 🔹 `inner` – Join Interno
Devuelve solo las filas que tienen coincidencia en ambas tablas.
```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import col

spark = SparkSession.builder.appName("Joins").getOrCreate()

# Crear DataFrames de ejemplo
data1 = [(1, "Alice"), (2, "Bob"), (3, "Charlie")]
data2 = [(1, "Ventas"), (2, "IT"), (4, "Marketing")]
df1 = spark.createDataFrame(data1, ["ID", "Nombre"])
df2 = spark.createDataFrame(data2, ["ID", "Departamento"])

# Join Interno
df_inner = df1.join(df2, on="ID", how="inner")
df_inner.show()
```
Salida esperada:
```
+---+------+------------+
| ID|Nombre|Departamento|
+---+------+------------+
|  1|Alice |    Ventas  |
|  2|  Bob |        IT  |
+---+------+------------+
```

### 🔹 `left` – Join Izquierdo
Devuelve todas las filas de la tabla izquierda y las coincidencias de la tabla derecha.
```python
df_left = df1.join(df2, on="ID", how="left")
df_left.show()
```
Salida esperada:
```
+---+------+------------+
| ID|Nombre|Departamento|
+---+------+------------+
|  1|Alice |    Ventas  |
|  2|  Bob |        IT  |
|  3|Charlie|      NULL  |
+---+------+------------+
```

### 🔹 `right` – Join Derecho
Devuelve todas las filas de la tabla derecha y las coincidencias de la tabla izquierda.
```python
df_right = df1.join(df2, on="ID", how="right")
df_right.show()
```

### 🔹 `full` – Join Completo (Outer Join)
Devuelve todas las filas de ambas tablas, rellenando con `NULL` cuando no hay coincidencias.
```python
df_full = df1.join(df2, on="ID", how="full")
df_full.show()
```

---

## 🔄 Operación Union en Spark
La operación **union()** combina filas de dos DataFrames con las mismas columnas.
```python
data3 = [(3, "Charlie"), (4, "David")]
df3 = spark.createDataFrame(data3, ["ID", "Nombre"])

# Union de df1 y df3
df_union = df1.union(df3)
df_union.show()
```
Salida esperada:
```
+---+-------+
| ID|Nombre |
+---+-------+
|  1| Alice |
|  2|   Bob |
|  3|Charlie|
|  3|Charlie|
|  4|  David|
+---+-------+
```

⚠️ **Nota**: Para evitar duplicados, usa `.distinct()`.
```python
df_union.distinct().show()
```

---

## 🎯 Conclusión
Las operaciones **Join** y **Union** en Apache Spark permiten combinar datos de manera eficiente. Mientras que `join()` es ideal para fusionar datos en base a claves comunes, `union()` es útil para apilar registros de DataFrames similares. 🚀


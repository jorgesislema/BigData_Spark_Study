# 🚀 Funciones Avanzadas en Apache Spark

## 🔥 Introducción
Las **funciones avanzadas en Apache Spark** permiten realizar transformaciones complejas y optimizar el procesamiento de datos. Estas incluyen funciones de ventana (*window functions*), expresiones condicionales, agregaciones personalizadas y manipulación avanzada de datos.

---

## 📌 Funciones de Ventana (*Window Functions*)
Las **funciones de ventana** permiten realizar cálculos sobre un conjunto de filas relacionadas dentro de una partición, sin reducir el número total de filas.

### 🔹 Ejemplo: Uso de `row_number()`
```python
from pyspark.sql import SparkSession
from pyspark.sql.window import Window
from pyspark.sql.functions import row_number

spark = SparkSession.builder.appName("FuncionesAvanzadas").getOrCreate()

data = [("Alice", "Ventas", 5000), ("Bob", "Ventas", 6000),
        ("Charlie", "IT", 7000), ("David", "IT", 8000), ("Eve", "Ventas", 5500)]

df = spark.createDataFrame(data, ["Nombre", "Departamento", "Salario"])

window_spec = Window.partitionBy("Departamento").orderBy(df["Salario"].desc())

df = df.withColumn("rango", row_number().over(window_spec))
df.show()
```

---

## 🛠️ Expresiones Condicionales
Podemos usar `when()` y `otherwise()` para crear condiciones dentro de un DataFrame.
```python
from pyspark.sql.functions import when

df = df.withColumn("Categoria_Salario", when(df["Salario"] > 6000, "Alto")
                                     .when(df["Salario"] > 5000, "Medio")
                                     .otherwise("Bajo"))
df.show()
```

---

## 🔄 Manipulación de Fechas y Tiempos
Spark ofrece diversas funciones para manejar fechas y tiempos de manera eficiente.
```python
from pyspark.sql.functions import current_date, date_add

df = df.withColumn("Fecha_Actual", current_date())
df = df.withColumn("Fecha_Despues_10_Dias", date_add(df["Fecha_Actual"], 10))
df.show()
```

---

## 🏆 Agregaciones Personalizadas con `agg()`
Para aplicar múltiples funciones de agregación sobre un DataFrame:
```python
from pyspark.sql.functions import sum, avg, max, min

df_agg = df.groupBy("Departamento").agg(
    sum("Salario").alias("Total_Salarios"),
    avg("Salario").alias("Salario_Promedio"),
    max("Salario").alias("Salario_Max"),
    min("Salario").alias("Salario_Min")
)
df_agg.show()
```

---

## 🔍 Búsqueda de Patrones con Expresiones Regulares
Podemos utilizar expresiones regulares con `regexp_extract()` para extraer patrones de texto.
```python
from pyspark.sql.functions import regexp_extract

df = df.withColumn("Codigo", regexp_extract(df["Nombre"], "(\w+)", 0))
df.show()
```

---

## 🎯 Conclusión
Las **funciones avanzadas en Spark** mejoran el procesamiento y análisis de datos, permitiendo realizar transformaciones más eficientes y optimizadas. 🚀


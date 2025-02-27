# 🛠️ Funciones Definidas por el Usuario (UDFs) en Spark

## 🔥 ¿Qué es una UDF en Spark?
Una **UDF (User Defined Function)** en **Apache Spark** es una función personalizada creada por el usuario para aplicar transformaciones a los datos dentro de un **DataFrame** o **RDD**. Son útiles cuando las funciones nativas de Spark no cubren casos de uso específicos.

---

## 📌 ¿Por qué usar UDFs en Spark?
✅ **Extensibilidad**: Permiten agregar lógica personalizada a las consultas.
✅ **Flexibilidad**: Se pueden escribir en Python, Scala o Java.
✅ **Compatibilidad**: Se pueden usar dentro de Spark SQL.

---

## 🛠️ Creación y Uso de UDFs en PySpark

### 🔹 Paso 1: Crear una Sesión de Spark
Antes de usar UDFs, es necesario inicializar una **SparkSession**:
```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import udf
from pyspark.sql.types import StringType

spark = SparkSession.builder.appName("EjemploUDF").getOrCreate()
```

### 🔹 Paso 2: Crear un DataFrame de Ejemplo
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

### 🔹 Paso 3: Definir una UDF en PySpark
Vamos a crear una función que agregue un prefijo a los nombres:
```python
def agregar_prefijo(nombre):
    return "Sr./Sra. " + nombre

udf_prefijo = udf(agregar_prefijo, StringType())
```

### 🔹 Paso 4: Registrar y Aplicar la UDF
Usamos `withColumn` para aplicar la UDF al DataFrame:
```python
df = df.withColumn("Nombre_Con_Prefijo", udf_prefijo(df["Nombre"]))
df.show()
```
Salida esperada:
```
+-------+----+----------------+
| Nombre|Edad|Nombre_Con_Prefijo|
+-------+----+----------------+
|  Alice|  25|   Sr./Sra. Alice|
|    Bob|  30|   Sr./Sra. Bob|
|Charlie|  35|   Sr./Sra. Charlie|
+-------+----+----------------+
```

---

## 🏛️ Uso de UDFs en Spark SQL
Las UDFs también pueden registrarse y usarse en **consultas SQL**:
```python
spark.udf.register("udf_prefijo", agregar_prefijo, StringType())
df.createOrReplaceTempView("personas")
resultado = spark.sql("SELECT Nombre, Edad, udf_prefijo(Nombre) AS Nombre_Con_Prefijo FROM personas")
resultado.show()
```

---

## ⚡ Optimización de UDFs
Las UDFs estándar pueden ser lentas porque ejecutan código Python fuera del motor de ejecución de Spark. Para mejorar el rendimiento, usa **Pandas UDFs (Vectorized UDFs)**:
```python
from pyspark.sql.functions import pandas_udf
import pandas as pd

@pandas_udf(StringType())
def agregar_prefijo_vectorizado(nombre_series: pd.Series) -> pd.Series:
    return "Sr./Sra. " + nombre_series

df = df.withColumn("Nombre_Con_Prefijo", agregar_prefijo_vectorizado(df["Nombre"]))
df.show()
```
Las **Pandas UDFs** permiten procesar datos en lotes, mejorando la eficiencia.

---

## 🎯 Conclusión
Las **UDFs en Spark** son una herramienta poderosa para personalizar transformaciones de datos. Sin embargo, deben usarse con precaución, y siempre que sea posible, se recomienda usar **Pandas UDFs** para mejorar el rendimiento. 🚀


# 🚀 Broadcast Join en Apache Spark

## 🔥 Introducción
Los **joins** en Apache Spark pueden ser costosos cuando los datos deben moverse entre nodos en un clúster. **Broadcast Join** es una técnica optimizada que evita el *shuffle* de datos distribuyendo una tabla pequeña en todos los nodos, mejorando el rendimiento en uniones.

---

## 📌 ¿Cuándo Usar Broadcast Join?
✅ Cuando una de las tablas es **pequeña** (menos de 10-100 MB).
✅ Para **evitar el shuffle**, que es costoso en términos de red y memoria.
✅ En **uniones con datos distribuidos**, cuando una tabla no cabe en memoria pero otra sí.

---

## 🛠️ Implementación de Broadcast Join en PySpark
### 🔹 Crear DataFrames de Ejemplo
```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import broadcast

spark = SparkSession.builder.appName("BroadcastJoin").getOrCreate()

# Tabla grande
data_large = [(1, "Alice"), (2, "Bob"), (3, "Charlie"), (4, "David")]
df_large = spark.createDataFrame(data_large, ["id", "nombre"])

# Tabla pequeña
data_small = [(1, "Ventas"), (2, "IT")]
df_small = spark.createDataFrame(data_small, ["id", "departamento"])
```

### 🔹 Aplicar Broadcast Join
```python
df_resultado = df_large.join(broadcast(df_small), "id", "inner")
df_resultado.show()
```
✅ **Beneficio**: La tabla pequeña se copia a todos los nodos, reduciendo la necesidad de reorganizar datos en la red.

---

## 🔍 Comparación entre Joins en Spark
| Tipo de Join | Descripción | Genera Shuffle? |
|-------------|------------|----------------|
| **Shuffle Hash Join** | Distribuye los datos de ambas tablas en todas las particiones antes de unirlas. | ✅ Sí |
| **Sort Merge Join** | Ordena y combina los datos en particiones. | ✅ Sí |
| **Broadcast Join** | Copia la tabla pequeña en todos los nodos y evita el shuffle. | ❌ No |

---

## ⚡ Configuración y Optimización
### 🔹 Ajustar el Tamaño Máximo de Broadcast
Podemos configurar el tamaño máximo para que Spark decida automáticamente si usar **broadcast**:
```python
spark.conf.set("spark.sql.autoBroadcastJoinThreshold", 50 * 1024 * 1024)  # 50 MB
```

✅ **Recomendación**: Ajustar este valor según la cantidad de memoria disponible y el tamaño de las tablas.

---

## 🎯 Conclusión
El **Broadcast Join** es una estrategia eficiente para evitar *shuffles* cuando trabajamos con una tabla pequeña y otra grande. Ajustar correctamente los umbrales de memoria y aplicarlo en los casos correctos puede mejorar significativamente el rendimiento de Spark. 🚀


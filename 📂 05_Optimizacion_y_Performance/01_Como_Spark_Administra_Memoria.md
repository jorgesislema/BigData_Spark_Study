# 🧠 ¿Cómo Apache Spark Administra la Memoria?

## 🔥 Introducción
Apache Spark utiliza un modelo de administración de memoria eficiente para manejar grandes volúmenes de datos en entornos distribuidos. Comprender su gestión de memoria es clave para optimizar el rendimiento y evitar problemas como *OutOfMemoryError*.

---

## 📌 Componentes de la Memoria en Spark
La memoria en Spark se divide en dos grandes áreas:
1. **Memoria del Driver**: Maneja la ejecución del programa y la interacción con los ejecutores.
2. **Memoria de los Ejecutores (Executors)**: Se usa para procesar datos y realizar cálculos en paralelo.

Cada **Executor** divide su memoria en:
| Área | Descripción |
|------|------------|
| **Storage Memory** | Almacena datos en caché (RDDs, DataFrames). |
| **Execution Memory** | Se usa para operaciones como `shuffle`, `sort`, `aggregation`. |
| **User Memory** | Espacio disponible para el código del usuario. |
| **Reserved Memory** | Pequeña parte reservada para Spark internamente. |

---

## 🛠️ Configuración de Memoria en Spark
La memoria de Spark se configura con parámetros clave en `spark-defaults.conf` o en la creación de una sesión:
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("AdministracionMemoria") \
    .config("spark.executor.memory", "4g") \
    .config("spark.driver.memory", "2g") \
    .config("spark.memory.fraction", "0.75") \
    .getOrCreate()
```

| Parámetro | Descripción |
|-----------|------------|
| `spark.executor.memory` | Memoria asignada a cada ejecutor. |
| `spark.driver.memory` | Memoria para el proceso principal (driver). |
| `spark.memory.fraction` | Porcentaje de memoria para Storage y Execution. |

---

## ⚡ Optimización del Uso de Memoria
### 🔹 1. **Persistencia y Caché**
Usar `cache()` y `persist()` reduce la carga en memoria al reutilizar datos en múltiples operaciones.
```python
df = spark.read.parquet("/ruta/datos.parquet").cache()
df.count()  # Activa el cache
```

### 🔹 2. **Evitar `collect()` en Grandes Volúmenes de Datos**
`collect()` trae todos los datos al driver, lo que puede causar falta de memoria.
```python
# ⚠️ Puede agotar memoria en grandes datasets
data = df.collect()
```
✅ En su lugar, usar `take()` o `show()`.
```python
df.take(10)  # Devuelve solo 10 filas
```

### 🔹 3. **Optimizar el Número de Particiones**
Ajustar las particiones ayuda a mejorar el balance de carga.
```python
df = df.repartition(10)  # Reduce número de particiones
```

---

## 🎯 Conclusión
La correcta administración de memoria en Apache Spark es fundamental para un rendimiento eficiente. Configurar parámetros adecuados y seguir buenas prácticas como *cachear datos*, *evitar collect()* y *ajustar particiones* puede mejorar significativamente la ejecución de los procesos. 🚀


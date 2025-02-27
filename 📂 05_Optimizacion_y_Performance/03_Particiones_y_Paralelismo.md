# ⚡ Particiones y Paralelismo en Apache Spark

## 🔥 Introducción
Apache Spark es un motor de procesamiento distribuido que divide los datos en **particiones** para ejecutar operaciones en paralelo. La gestión eficiente de particiones y paralelismo es clave para optimizar el rendimiento y evitar problemas de sobrecarga en la memoria o ineficiencia en la distribución de tareas.

---

## 📌 ¿Qué es una Partición en Spark?
Una **partición** es la unidad mínima de datos procesada por un **ejecutor** dentro de un clúster de Spark. Spark divide automáticamente los datos en particiones cuando se leen desde una fuente de datos como HDFS, S3 o bases de datos.

| Característica | Descripción |
|--------------|-------------|
| **Tamaño de partición** | Generalmente 128 MB por partición en HDFS |
| **Número predeterminado** | Spark elige automáticamente el número de particiones |
| **Reparticionado** | Se puede ajustar manualmente usando `repartition()` y `coalesce()` |

---

## 🛠️ Controlando el Número de Particiones
### 🔹 Ver número de particiones actuales
```python
rdd = spark.sparkContext.parallelize(range(100), 10)  # Crea un RDD con 10 particiones
print(rdd.getNumPartitions())
```
### 🔹 Cambiar el número de particiones
#### 🏎️ `repartition(n)` (Aumenta o reduce particiones con shuffle)
```python
df = df.repartition(10)  # Redistribuye los datos en 10 particiones (genera shuffle)
```

#### 🚀 `coalesce(n)` (Reduce particiones sin shuffle)
```python
df = df.coalesce(5)  # Reduce las particiones a 5 sin mover excesivos datos
```

✅ **Regla general:**
- Usa `repartition(n)` si necesitas **aumentar** o cambiar la distribución de datos.
- Usa `coalesce(n)` para **reducir** particiones de manera eficiente.

---

## ⚙️ Paralelismo en Spark
El **paralelismo** en Spark se basa en el número de **particiones** y el número de **núcleos disponibles** en el clúster. Spark ejecuta una tarea por cada partición en cada núcleo disponible.

### 🔹 Configurar el Nivel de Paralelismo
Podemos ajustar el número de tareas paralelas con:
```python
spark.conf.set("spark.default.parallelism", 200)
```

✅ **Recomendación:**
- **Para RDDs:** `spark.default.parallelism = 2 x número de núcleos`
- **Para DataFrames:** `spark.sql.shuffle.partitions = 200` (valor por defecto)

---

## 🏎️ Comparación entre `repartition()` y `coalesce()`
| Método | Uso | Genera Shuffle? |
|--------|-----|---------------|
| `repartition(n)` | Redistribuye los datos en *n* particiones | ✅ Sí |
| `coalesce(n)` | Reduce el número de particiones sin grandes movimientos de datos | ❌ No |

---

## 🎯 Conclusión
Optimizar las particiones y el paralelismo en Spark permite distribuir la carga de trabajo de manera eficiente y reducir el tiempo de ejecución de las tareas. Aplicar `repartition()` y `coalesce()` correctamente puede mejorar el rendimiento en clústeres grandes. 🚀


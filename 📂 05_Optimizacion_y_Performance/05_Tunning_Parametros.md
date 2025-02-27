# ⚙️ Tuning de Parámetros en Apache Spark

## 🔥 Introducción
El ajuste de parámetros (**tuning**) en Apache Spark es fundamental para optimizar el rendimiento de las aplicaciones de Big Data. Configurar correctamente la memoria, el paralelismo y los recursos asignados puede reducir tiempos de ejecución y mejorar la eficiencia del clúster.

---

## 📌 Principales Parámetros de Configuración
Los parámetros clave en Spark se dividen en tres categorías:
1. **Memoria y gestión de recursos**
2. **Optimización de ejecución**
3. **Configuración de shuffle y particiones**

---

## 🛠️ Configuración de Memoria y Recursos
### 🔹 Configurar Memoria para el Driver y los Ejecutores
```python
spark.conf.set("spark.driver.memory", "4g")
spark.conf.set("spark.executor.memory", "8g")
```
| Parámetro | Descripción |
|-----------|------------|
| `spark.driver.memory` | Cantidad de memoria asignada al Driver. |
| `spark.executor.memory` | Memoria para cada ejecutor en el clúster. |

✅ **Recomendación**: Ajustar estos valores según la capacidad del clúster.

### 🔹 Configurar Número de Núcleos
```python
spark.conf.set("spark.executor.cores", "4")
```
| Parámetro | Descripción |
|-----------|------------|
| `spark.executor.cores` | Número de núcleos por ejecutor. |
| `spark.task.cpus` | Núcleos requeridos por tarea individual. |

✅ **Recomendación**: Asignar un número adecuado de núcleos para balancear la carga de trabajo.

---

## 🔄 Optimización de Ejecución
### 🔹 Configurar Paralelismo
```python
spark.conf.set("spark.default.parallelism", 200)
```
| Parámetro | Descripción |
|-----------|------------|
| `spark.default.parallelism` | Número de tareas paralelas en RDDs. |
| `spark.sql.shuffle.partitions` | Número de particiones en operaciones de *shuffle*. |

✅ **Recomendación**:
- **Para RDDs**: `spark.default.parallelism = 2 x núcleos totales`
- **Para DataFrames**: `spark.sql.shuffle.partitions = 200` (ajustar según tamaño de datos)

---

## 🔀 Optimización de Shuffle y Joins
### 🔹 Ajustar el Número de Particiones en Shuffle
```python
spark.conf.set("spark.sql.shuffle.partitions", 200)
```
✅ **Beneficio**: Evita cuellos de botella en operaciones como `groupBy()` y `join()`.

### 🔹 Habilitar Broadcast Join
```python
spark.conf.set("spark.sql.autoBroadcastJoinThreshold", 100 * 1024 * 1024)  # 100 MB
```
✅ **Beneficio**: Mejora la eficiencia en **joins** cuando una tabla es pequeña.

---

## 🏎️ Comparación de Parámetros Clave
| Categoría | Parámetro | Efecto |
|-----------|----------|--------|
| **Memoria** | `spark.executor.memory` | Asigna memoria a los ejecutores |
| **Paralelismo** | `spark.default.parallelism` | Define la cantidad de tareas concurrentes |
| **Shuffle** | `spark.sql.shuffle.partitions` | Ajusta la eficiencia en operaciones de shuffle |
| **Joins** | `spark.sql.autoBroadcastJoinThreshold` | Optimiza *joins* con tablas pequeñas |

---

## 🎯 Conclusión
Ajustar los parámetros en Apache Spark es clave para mejorar el rendimiento. Configurar correctamente **la memoria, el paralelismo y la optimización de shuffle** puede reducir significativamente los tiempos de ejecución y mejorar la eficiencia del clúster. 🚀


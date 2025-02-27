# 🔥 Comandos Ocultos en Apache Spark

## 🔥 Introducción
Apache Spark tiene **comandos ocultos y funciones avanzadas** que pueden mejorar la eficiencia del desarrollo y la depuración de código. Estos comandos son útiles para **optimización, análisis de ejecución y depuración en clústeres distribuidos**.

---

## 📌 Comandos para Depuración y Optimización

### 1️⃣ **Mostrar Configuraciones de Spark en Tiempo de Ejecución**
```python
print(spark.conf.get("spark.sql.shuffle.partitions"))
print(spark.conf.get("spark.executor.memory"))
```
✅ **Beneficio:** Verifica parámetros sin acceder a archivos de configuración.

### 2️⃣ **Ver el Plan de Ejecución en Formato Completo**
```python
df.explain("extended")
```
✅ **Beneficio:** Muestra el análisis lógico y físico de la consulta.

### 3️⃣ **Habilitar `Adaptive Query Execution (AQE)`**
```python
spark.conf.set("spark.sql.adaptive.enabled", "true")
```
✅ **Beneficio:** Optimiza la ejecución de consultas en tiempo real.

---

## 🚀 Comandos Avanzados de DataFrames

### 4️⃣ **Ver los 5 DataFrames más grandes en Memoria**
```python
spark.catalog.listTables()
```
✅ **Beneficio:** Muestra qué DataFrames están almacenados en caché.

### 5️⃣ **Borrar Caché de un DataFrame**
```python
spark.catalog.clearCache()
```
✅ **Beneficio:** Libera memoria eliminando datos en caché.

### 6️⃣ **Forzar Garbage Collection**
```python
import gc
gc.collect()
```
✅ **Beneficio:** Reduce el uso de memoria liberando recursos innecesarios.

---

## 🔄 Comandos para RDDs

### 7️⃣ **Ver Particiones de un RDD**
```python
rdd.getNumPartitions()
```
✅ **Beneficio:** Verifica la distribución de datos en el clúster.

### 8️⃣ **Cambiar el Número de Particiones sin Shuffle**
```python
rdd.coalesce(5)
```
✅ **Beneficio:** Reduce el número de particiones sin generar tráfico de red.

---

## 🏎️ Comandos para Optimización de Joins

### 9️⃣ **Forzar `Broadcast Join` en una Tabla Pequeña**
```python
from pyspark.sql.functions import broadcast

df1.join(broadcast(df2), "id").show()
```
✅ **Beneficio:** Evita operaciones de shuffle en joins con tablas pequeñas.

### 🔟 **Ver el Estado de las Tareas en Tiempo Real**
```python
spark.sparkContext.statusTracker.getExecutorInfos()
```
✅ **Beneficio:** Monitorea el estado de los ejecutores en ejecución.

---

## 🎯 Conclusión
Estos **comandos ocultos y avanzados** pueden mejorar la eficiencia del desarrollo, depuración y optimización de código en Apache Spark. Usarlos correctamente permite mejorar el rendimiento y la escalabilidad del procesamiento de datos. 🚀


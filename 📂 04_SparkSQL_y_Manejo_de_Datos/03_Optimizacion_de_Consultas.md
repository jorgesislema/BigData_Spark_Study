# ⚡ Optimización de Consultas en Apache Spark

## 🔥 Introducción
Optimizar consultas en **Apache Spark** es clave para mejorar el rendimiento en el procesamiento de datos a gran escala. Spark utiliza el **Catalyst Optimizer** y el **Tungsten Engine** para optimizar consultas de manera automática, pero también existen buenas prácticas que pueden mejorar aún más la eficiencia.

---

## 📌 Estrategias para Optimización de Consultas

### 🔹 1. Usar Formatos de Archivo Optimizados
Los formatos **Parquet** y **ORC** ofrecen mayor compresión y velocidad en comparación con CSV o JSON.
```python
df.write.mode("overwrite").parquet("/ruta/output.parquet")
```
✅ **Beneficio:** Reduce el uso de almacenamiento y mejora la lectura.

### 🔹 2. Cachear DataFrames Reutilizados
Si un **DataFrame** se usa varias veces en el código, cachearlo puede mejorar el rendimiento.
```python
df.cache()
df.count()  # Fuerza la cache para evitar recalculaciones
```
✅ **Beneficio:** Evita recomputaciones innecesarias.

### 🔹 3. Reducir el Número de Particiones
Por defecto, Spark crea muchas particiones. Podemos reducirlas para optimizar consultas.
```python
df = df.repartition(10)  # Redistribuye en 10 particiones
```
✅ **Beneficio:** Menos sobrecarga en la administración de tareas.

### 🔹 4. Usar `select()` en lugar de `*`
Seleccionar solo las columnas necesarias mejora la eficiencia.
```python
df.select("columna1", "columna2").show()
```
✅ **Beneficio:** Disminuye el procesamiento de datos innecesarios.

### 🔹 5. Filtrar Datos antes de Realizar Transformaciones
Aplicar filtros lo antes posible en el pipeline evita procesar datos innecesarios.
```python
df = df.filter(df["columna"] > 100)
```
✅ **Beneficio:** Reduce la cantidad de datos procesados en transformaciones posteriores.

### 🔹 6. Uso de Broadcast Join
Para **Joins** con tablas pequeñas, `broadcast()` puede mejorar el rendimiento.
```python
from pyspark.sql.functions import broadcast

df_resultado = df1.join(broadcast(df2), "columna_comun", "inner")
```
✅ **Beneficio:** Reduce el tráfico de datos en la red y acelera los *joins*.

### 🔹 7. Configurar `spark.sql.shuffle.partitions`
El número de particiones en operaciones como `groupBy()` y `join()` puede ajustarse para mejorar el rendimiento.
```python
spark.conf.set("spark.sql.shuffle.partitions", 200)
```
✅ **Beneficio:** Evita la sobrecarga de **shuffle** en operaciones de agregación.

---

## 🏎️ Comparación de Estrategias de Optimización
| Técnica | Beneficio |
|---------|----------|
| **Usar Parquet/ORC** | Reduce tamaño y mejora lectura |
| **Cachear DataFrames** | Evita cálculos repetidos |
| **Reparticionar datos** | Mejora paralelización |
| **Select en lugar de `*`** | Reduce el procesamiento innecesario |
| **Filtrar antes de transformar** | Evita carga innecesaria |
| **Broadcast Join** | Acelera uniones con tablas pequeñas |
| **Configurar `shuffle.partitions`** | Mejora rendimiento en joins y agrupaciones |

---

## 🎯 Conclusión
Aplicar estas estrategias de **optimización en Spark** puede mejorar significativamente la eficiencia y reducir costos computacionales. 🚀


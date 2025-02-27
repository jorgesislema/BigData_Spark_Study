# 📜 Análisis de Logs con Apache Spark

## 🔥 Introducción
El análisis de **logs** es una tarea esencial en la administración de sistemas, seguridad informática y optimización de aplicaciones. Apache **Spark** permite procesar y analizar grandes volúmenes de logs de manera eficiente y en tiempo real.

---

## 📌 ¿Por qué usar Spark para Análisis de Logs?
✅ **Escalabilidad**: Puede manejar logs de múltiples fuentes distribuidas.
✅ **Velocidad**: Procesa datos en memoria y en paralelo.
✅ **Flexibilidad**: Soporta logs en múltiples formatos (JSON, CSV, texto plano, etc.).
✅ **Streaming**: Permite análisis en tiempo real con **Spark Streaming**.

---

## 🛠️ Configuración del Entorno
### 🔹 Inicializar SparkSession
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("AnalisisLogs") \
    .getOrCreate()
```

---

## 🔄 Carga de Logs en Spark
### 🔹 Leer un Archivo de Logs en Texto Plano
```python
df = spark.read.text("/ruta/logs/app.log")
df.show(truncate=False)
```

### 🔹 Leer Logs en JSON
```python
df_json = spark.read.json("/ruta/logs/logs.json")
df_json.show()
```

---

## 🔍 Procesamiento y Análisis de Logs
### 🔹 Filtrar Errores en Logs
```python
error_logs = df.filter(df["value"].contains("ERROR"))
error_logs.show(truncate=False)
```

### 🔹 Extraer Información con Expresiones Regulares
```python
from pyspark.sql.functions import regexp_extract

df = df.withColumn("timestamp", regexp_extract("value", r'(\d{4}-\d{2}-\d{2} \d{2}:\d{2}:\d{2})', 1))
df = df.withColumn("log_level", regexp_extract("value", r'(INFO|ERROR|WARN|DEBUG)', 1))
df.show()
```

### 🔹 Contar Frecuencia de Tipos de Logs
```python
from pyspark.sql.functions import count

df_count = df.groupBy("log_level").agg(count("log_level").alias("count"))
df_count.show()
```

---

## 📊 Visualización de Datos
Spark permite exportar los datos a formatos adecuados para análisis visual con herramientas de BI.
```python
df.write.mode("overwrite").parquet("/ruta/output/logs_analizados.parquet")
```

---

## ⚡ Optimización y Buenas Prácticas
✅ **Usar formato Parquet** en lugar de texto plano para optimizar almacenamiento y consultas.
✅ **Ajustar el número de particiones** para mejorar rendimiento:
```python
df = df.repartition(10)
```
✅ **Cachear DataFrames** cuando se reutilicen en múltiples consultas:
```python
df.cache()
```

---

## 🎯 Conclusión
Apache **Spark** facilita el análisis de logs a gran escala, permitiendo la detección de errores, patrones y métricas en sistemas distribuidos. Implementar optimizaciones adecuadas mejora el rendimiento y la escalabilidad del procesamiento. 🚀


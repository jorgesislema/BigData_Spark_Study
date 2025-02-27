# 📂 Comparación de Formatos de Archivo: Parquet vs JSON vs Avro

## 🔥 Introducción
Apache Spark admite múltiples formatos de almacenamiento como **Parquet, JSON y Avro**. Elegir el formato correcto puede mejorar el rendimiento y la eficiencia del procesamiento de datos en **Big Data**.

---

## 📌 Comparación General
| Característica | Parquet | JSON | Avro |
|--------------|--------|------|------|
| **Estructura** | Columnar | Basado en texto | Binario |
| **Compresión** | Alta | Baja | Alta |
| **Legibilidad** | No legible | Legible | No legible |
| **Soporte de Esquema** | Sí | No | Sí |
| **Eficiencia en Lectura** | Alta | Baja | Media |
| **Uso en Big Data** | Muy recomendable | No recomendado | Recomendado |

---

## 🛠️ Descripción y Uso de Cada Formato

### 🔹 **Parquet** (Formato Columnar)
**Ventajas:**
✅ Almacenamiento eficiente (compresión y acceso rápido).
✅ Ideal para consultas analíticas (Spark, Hive, Presto).
✅ Soporte para esquema y evolución de datos.

**Ejemplo de lectura y escritura en Parquet:**
```python
# Guardar DataFrame como Parquet
df.write.parquet("/ruta/output.parquet")

# Leer archivo Parquet
df_parquet = spark.read.parquet("/ruta/output.parquet")
df_parquet.show()
```

---

### 🔹 **JSON** (Formato Basado en Texto)
**Ventajas:**
✅ Fácil de leer y depurar.
✅ Compatible con múltiples lenguajes de programación.
✅ Flexible para datos semiestructurados.

**Desventajas:**
❌ Más pesado debido a su redundancia de texto.
❌ No optimizado para consultas en Big Data.

**Ejemplo de lectura y escritura en JSON:**
```python
# Guardar DataFrame como JSON
df.write.json("/ruta/output.json")

# Leer archivo JSON
df_json = spark.read.json("/ruta/output.json")
df_json.show()
```

---

### 🔹 **Avro** (Formato Binario)
**Ventajas:**
✅ Compacto y eficiente en almacenamiento.
✅ Soporta evolución de esquemas.
✅ Compatible con Apache Kafka y sistemas de mensajería.

**Ejemplo de lectura y escritura en Avro:**
```python
# Guardar DataFrame como Avro
df.write.format("avro").save("/ruta/output.avro")

# Leer archivo Avro
df_avro = spark.read.format("avro").load("/ruta/output.avro")
df_avro.show()
```

---

## 🏎️ ¿Cuál Formato Elegir?
| Caso de Uso | Formato Recomendado |
|------------|------------------|
| **Procesamiento en Spark** | 🏆 Parquet |
| **Intercambio de Datos en APIs** | 🏆 JSON |
| **Almacenamiento en Kafka / Big Data** | 🏆 Avro |

---

## 🎯 Conclusión
- **Parquet** es ideal para análisis de datos y consultas rápidas.
- **JSON** es útil para portabilidad y depuración de datos.
- **Avro** es eficiente para integración con sistemas de mensajería.

🚀 ¡Elegir el formato correcto mejora el rendimiento de tus aplicaciones Big Data!


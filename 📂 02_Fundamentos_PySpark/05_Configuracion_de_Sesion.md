# ⚙️ Configuración de Sesión en Apache Spark

## 🔥 Introducción
En **Apache Spark**, una **SparkSession** es el punto de entrada principal para interactuar con los datos y ejecutar operaciones. Configurar correctamente la sesión permite optimizar el rendimiento y la gestión de recursos en clústeres distribuidos.

---

## 📌 Creación de una SparkSession
Para usar **PySpark**, primero debemos crear una **SparkSession**:
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("MiAplicacion").getOrCreate()
```
**Explicación:**
- `appName("MiAplicacion")`: Define el nombre de la aplicación.
- `getOrCreate()`: Recupera una sesión existente o crea una nueva.

---

## 🛠️ Configuración Avanzada de SparkSession
Podemos agregar configuraciones adicionales para optimizar la sesión:
```python
spark = SparkSession.builder \
    .appName("Optimizada") \
    .config("spark.executor.memory", "4g") \
    .config("spark.driver.memory", "2g") \
    .config("spark.sql.shuffle.partitions", "200") \
    .getOrCreate()
```

### 🔹 Parámetros clave
| Parámetro | Descripción |
|-----------|------------|
| `spark.executor.memory` | Define la cantidad de RAM para cada executor. |
| `spark.driver.memory` | Memoria asignada al driver (proceso principal). |
| `spark.sql.shuffle.partitions` | Número de particiones en operaciones de shuffle. |

---

## 📂 Verificar Configuración de la Sesión
Para visualizar los parámetros de la sesión activa:
```python
print(spark.sparkContext.getConf().getAll())
```
Esto devuelve un listado de todas las configuraciones activas en Spark.

---

## 🏎️ Finalizar una Sesión de Spark
Para liberar los recursos correctamente después de ejecutar las tareas:
```python
spark.stop()
```
Esto es importante en entornos de producción para evitar consumo innecesario de memoria y CPU.

---

## 🎯 Conclusión
La correcta **configuración de la sesión en Spark** mejora el rendimiento y la eficiencia en el procesamiento de datos. Ajustar parámetros como la memoria y particiones permite escalar tareas en clústeres de manera efectiva. 🚀


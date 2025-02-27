# ⚡ Acciones en Apache Spark

## 🔥 Introducción
En **Apache Spark**, las **acciones** son operaciones que devuelven un resultado al controlador (driver) después de aplicar transformaciones a un **RDD** o **DataFrame**. A diferencia de las transformaciones (*lazy evaluation*), las acciones **desencadenan la ejecución real del cálculo en el clúster**.

---

## 📌 Características de las Acciones en Spark
✅ **Ejecutan transformaciones previas** y generan un resultado.
✅ **Devuelven valores al driver o guardan datos en almacenamiento**.
✅ **Pueden generar cálculos costosos** si se llaman varias veces.

---

## 🛠️ Acciones Comunes en PySpark

### 🔹 1. `collect()` – Recuperar todos los elementos
Devuelve todos los elementos de un **RDD** o **DataFrame** como una lista en el driver.
```python
rdd = spark.sparkContext.parallelize([1, 2, 3, 4, 5])
result = rdd.collect()
print(result)  # [1, 2, 3, 4, 5]
```
⚠️ **Cuidado**: No usar con grandes volúmenes de datos ya que puede agotar la memoria del driver.

### 🔹 2. `count()` – Contar elementos
Cuenta la cantidad total de elementos en un **RDD** o **DataFrame**.
```python
rdd = spark.sparkContext.parallelize([1, 2, 3, 4, 5])
print(rdd.count())  # 5
```

### 🔹 3. `first()` – Obtener el primer elemento
Devuelve el primer elemento del conjunto de datos.
```python
rdd = spark.sparkContext.parallelize([10, 20, 30])
print(rdd.first())  # 10
```

### 🔹 4. `take(n)` – Obtener los primeros *n* elementos
Devuelve una lista con los primeros *n* elementos.
```python
rdd = spark.sparkContext.parallelize([10, 20, 30, 40, 50])
print(rdd.take(3))  # [10, 20, 30]
```

### 🔹 5. `reduce()` – Reducir elementos a un solo valor
Aplica una función de agregación para reducir los datos.
```python
rdd = spark.sparkContext.parallelize([1, 2, 3, 4])
result = rdd.reduce(lambda a, b: a + b)
print(result)  # 10 (1+2+3+4)
```

### 🔹 6. `foreach()` – Aplicar una función a cada elemento
Ejecuta una función en cada elemento, útil para escribir en bases de datos o almacenamiento.
```python
def imprimir_elemento(x):
    print(x)

rdd = spark.sparkContext.parallelize(["A", "B", "C"])
rdd.foreach(imprimir_elemento)
```

### 🔹 7. `saveAsTextFile()` – Guardar datos en archivos
Guarda el resultado en un archivo de texto dentro de un directorio.
```python
rdd = spark.sparkContext.parallelize(["Hola", "Mundo", "Spark"])
rdd.saveAsTextFile("/ruta/salida")
```

---

## 🏎️ Comparación entre `collect()` y `take()`
| Acción | Uso | Desventaja |
|--------|-----|------------|
| `collect()` | Devuelve todos los datos al driver | Puede agotar la memoria en grandes datasets |
| `take(n)` | Devuelve solo los primeros *n* elementos | Menos costoso que `collect()` |

---

## 🎯 Conclusión
Las **acciones en Spark** permiten obtener resultados y desencadenar la ejecución de transformaciones. Es importante elegir la acción adecuada para evitar sobrecarga en el **driver** y mejorar el rendimiento en entornos distribuidos. 🚀


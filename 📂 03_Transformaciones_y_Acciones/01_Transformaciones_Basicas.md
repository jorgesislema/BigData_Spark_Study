# 🔄 Transformaciones Básicas en Apache Spark

## 🔥 Introducción
Las **transformaciones** en Apache Spark son operaciones que se aplican sobre **RDDs (Resilient Distributed Datasets) o DataFrames** para generar nuevos conjuntos de datos sin modificar los originales. Son **perezosas** (*lazy evaluation*), lo que significa que no se ejecutan hasta que se invoca una **acción**.

---

## 📌 Tipos de Transformaciones en Spark
En Spark, las transformaciones pueden ser de dos tipos:
- **Narrow Transformations** (Transformaciones estrechas): Cada partición del RDD hijo depende de una única partición del RDD padre. Ejemplo: `map()`, `filter()`.
- **Wide Transformations** (Transformaciones amplias): Requieren una reorganización de datos entre nodos, generando una fase de *shuffle*. Ejemplo: `groupBy()`, `reduceByKey()`.

---

## 🛠️ Transformaciones Comunes en PySpark
### 🔹 1. `map()` – Aplicar una función a cada elemento
Transforma cada elemento del RDD aplicando una función dada.
```python
rdd = spark.sparkContext.parallelize([1, 2, 3, 4, 5])
result = rdd.map(lambda x: x * 2)
print(result.collect())  # [2, 4, 6, 8, 10]
```

### 🔹 2. `filter()` – Filtrar elementos de un RDD
Devuelve solo los elementos que cumplen una condición.
```python
rdd = spark.sparkContext.parallelize([1, 2, 3, 4, 5])
result = rdd.filter(lambda x: x % 2 == 0)
print(result.collect())  # [2, 4]
```

### 🔹 3. `flatMap()` – Transformación con división de elementos
Similar a `map()`, pero cada elemento puede producir múltiples valores.
```python
rdd = spark.sparkContext.parallelize(["Hola mundo", "Apache Spark"])
result = rdd.flatMap(lambda x: x.split(" "))
print(result.collect())  # ['Hola', 'mundo', 'Apache', 'Spark']
```

### 🔹 4. `distinct()` – Eliminar duplicados
Elimina elementos repetidos dentro del RDD.
```python
rdd = spark.sparkContext.parallelize([1, 2, 2, 3, 3, 3])
result = rdd.distinct()
print(result.collect())  # [1, 2, 3]
```

### 🔹 5. `groupByKey()` – Agrupar por clave
Agrupa elementos con la misma clave, sin reducirlos.
```python
rdd = spark.sparkContext.parallelize([("a", 1), ("b", 2), ("a", 3)])
result = rdd.groupByKey()
print([(x, list(y)) for x, y in result.collect()])  # [('a', [1, 3]), ('b', [2])]
```

### 🔹 6. `reduceByKey()` – Reducir valores por clave
Similar a `groupByKey()`, pero aplica una función de reducción.
```python
rdd = spark.sparkContext.parallelize([("a", 1), ("b", 2), ("a", 3)])
result = rdd.reduceByKey(lambda x, y: x + y)
print(result.collect())  # [('a', 4), ('b', 2)]
```

---

## 🏎️ Comparación entre `groupByKey()` y `reduceByKey()`
| Transformación | Uso | Desventaja |
|--------------|----|------------|
| `groupByKey()` | Agrupa valores por clave en una lista | Puede consumir más memoria |
| `reduceByKey()` | Aplica reducción sin crear listas intermedias | Solo para operaciones reducibles |

---

## 🎯 Conclusión
Las transformaciones en Spark permiten manipular grandes volúmenes de datos de forma eficiente. Comprender cuándo usar **`map()`**, **`filter()`**, **`groupByKey()`** y otras transformaciones básicas es clave para optimizar el rendimiento de procesamiento en **Big Data**. 🚀


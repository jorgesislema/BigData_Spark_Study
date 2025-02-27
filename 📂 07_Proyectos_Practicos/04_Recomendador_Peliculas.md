# 🎬 Sistema de Recomendación de Películas con Apache Spark

## 🔥 Introducción
Los **sistemas de recomendación** son una de las aplicaciones más populares en el campo de **Big Data** y **Machine Learning**. Apache **Spark MLlib** proporciona herramientas para construir un **motor de recomendación escalable y eficiente** basado en **filtrado colaborativo**.

---

## 📌 ¿Qué es el Filtrado Colaborativo?
El **filtrado colaborativo** utiliza el comportamiento de los usuarios para recomendar productos similares. Se basa en dos enfoques principales:
1. **Basado en usuarios:** Encuentra usuarios con preferencias similares.
2. **Basado en ítems:** Recomienda productos similares a los que el usuario ha calificado.

Spark utiliza el algoritmo **ALS (Alternating Least Squares)** para entrenar modelos de recomendación en grandes volúmenes de datos.

---

## 🛠️ Implementación en PySpark
### 🔹 1. Inicializar SparkSession
```python
from pyspark.sql import SparkSession
from pyspark.ml.recommendation import ALS

spark = SparkSession.builder \
    .appName("RecomendadorPeliculas") \
    .getOrCreate()
```

---

### 🔹 2. Cargar Datos de Calificaciones
```python
df = spark.read.csv("/ruta/dataset/ratings.csv", header=True, inferSchema=True)
df.show()
```
✅ **Formato del dataset:**
```
+--------+---------+------+----------+
| userId | movieId | rating | timestamp |
+--------+---------+------+----------+
|    1   |   31    |  4.0  |  964982703|
|    2   |   102   |  5.0  |  964982224|
+--------+---------+------+----------+
```

---

### 🔹 3. Entrenar el Modelo con ALS
```python
als = ALS(userCol="userId", itemCol="movieId", ratingCol="rating",
          coldStartStrategy="drop")
modelo = als.fit(df)
```
✅ **Cold Start Strategy:** Evita problemas con datos no vistos en validación.

---

### 🔹 4. Generar Recomendaciones para Usuarios
```python
recomendaciones = modelo.recommendForAllUsers(5)
recomendaciones.show(truncate=False)
```
✅ **Salida esperada:**
```
+------+------------------------------------------------+
|userId|recommendations                                 |
+------+------------------------------------------------+
|   1  |[(50, 4.8), (34, 4.7), (78, 4.6), (2, 4.5), ...]|
+------+------------------------------------------------+
```

---

### 🔹 5. Evaluar el Modelo
```python
from pyspark.ml.evaluation import RegressionEvaluator

evaluator = RegressionEvaluator(metricName="rmse", labelCol="rating", predictionCol="prediction")
predicciones = modelo.transform(df)
rmse = evaluator.evaluate(predicciones)
print(f"Error RMSE: {rmse}")
```
✅ **RMSE (Root Mean Squared Error)** mide la precisión del modelo.

---

## ⚡ Optimización y Buenas Prácticas
✅ **Ajustar hiperparámetros:**
```python
als = ALS(rank=10, maxIter=20, regParam=0.1, userCol="userId", itemCol="movieId", ratingCol="rating")
```
✅ **Filtrar datos con pocas calificaciones para evitar sesgos.**
✅ **Utilizar particionamiento adecuado para distribuir la carga en el clúster.**

---

## 🎯 Conclusión
Apache **Spark MLlib** permite construir sistemas de recomendación escalables en grandes volúmenes de datos. Ajustando los hiperparámetros y aplicando optimizaciones adecuadas, se pueden obtener recomendaciones personalizadas con alta eficiencia. 🚀


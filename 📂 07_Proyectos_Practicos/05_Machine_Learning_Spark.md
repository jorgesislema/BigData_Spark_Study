# 🤖 Machine Learning en Apache Spark

## 🔥 Introducción
Apache **Spark MLlib** es la biblioteca de **Machine Learning** de Spark, diseñada para entrenar modelos a gran escala con procesamiento distribuido. Soporta algoritmos de clasificación, regresión, clustering y reducción de dimensionalidad.

---

## 📌 Ventajas de Spark MLlib
✅ **Escalabilidad**: Funciona en clústeres grandes con procesamiento paralelo.
✅ **Compatibilidad**: Soporta múltiples formatos de datos.
✅ **Integración con Pipelines**: Permite estructurar el flujo de entrenamiento.
✅ **Optimización en Memoria**: Usa estructuras distribuidas para mejorar el rendimiento.

---

## 🛠️ Configuración del Entorno
### 🔹 Inicializar SparkSession
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("ML_Spark") \
    .getOrCreate()
```

---

## 🔄 Carga y Preprocesamiento de Datos
### 🔹 Cargar Datos desde un CSV
```python
from pyspark.sql.functions import col

df = spark.read.csv("/ruta/dataset.csv", header=True, inferSchema=True)
df = df.select(col("feature1"), col("feature2"), col("label"))
df.show()
```

### 🔹 Transformar Datos con `VectorAssembler`
```python
from pyspark.ml.feature import VectorAssembler

assembler = VectorAssembler(inputCols=["feature1", "feature2"], outputCol="features")
df = assembler.transform(df).select("features", "label")
```

---

## 🤖 Entrenamiento de Modelos
### 🔹 Regresión Logística
```python
from pyspark.ml.classification import LogisticRegression

lr = LogisticRegression(featuresCol="features", labelCol="label")
modelo = lr.fit(df)
```

### 🔹 Árboles de Decisión
```python
from pyspark.ml.classification import DecisionTreeClassifier

dt = DecisionTreeClassifier(featuresCol="features", labelCol="label")
modelo_dt = dt.fit(df)
```

### 🔹 Clustering con K-Means
```python
from pyspark.ml.clustering import KMeans

kmeans = KMeans(featuresCol="features", k=3)
modelo_km = kmeans.fit(df)
```

---

## 📊 Evaluación de Modelos
### 🔹 Calcular Métricas de Precisión
```python
from pyspark.ml.evaluation import MulticlassClassificationEvaluator

evaluator = MulticlassClassificationEvaluator(labelCol="label", metricName="accuracy")
precision = evaluator.evaluate(modelo.transform(df))
print(f"Precisión del modelo: {precision}")
```

---

## ⚡ Optimización y Buenas Prácticas
✅ **Usar Pipelines** para simplificar el flujo de ML:
```python
from pyspark.ml import Pipeline
pipeline = Pipeline(stages=[assembler, lr])
modelo_pipeline = pipeline.fit(df)
```
✅ **Hiperparámetros con Cross Validation**:
```python
from pyspark.ml.tuning import ParamGridBuilder, CrossValidator
paramGrid = ParamGridBuilder().addGrid(lr.regParam, [0.1, 0.01]).build()
```

---

## 🎯 Conclusión
Apache **Spark MLlib** permite entrenar modelos de **Machine Learning** en grandes volúmenes de datos de manera distribuida. Su integración con Pipelines y herramientas de optimización lo convierte en una excelente opción para escalar modelos predictivos. 🚀


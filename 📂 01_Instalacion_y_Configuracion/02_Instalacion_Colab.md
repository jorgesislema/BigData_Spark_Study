# 🚀 Instalación de Apache Spark en Google Colab

## 🔥 Introducción
Google Colab es una plataforma en la nube que permite ejecutar código en Python sin necesidad de configuraciones locales. Sin embargo, no incluye Apache Spark por defecto, por lo que es necesario instalarlo manualmente.

---

## 📌 Requisitos Previos
- Cuenta en Google ([https://colab.research.google.com](https://colab.research.google.com)).
- Conocimientos básicos de Python y Jupyter Notebooks.

---

## 🛠️ Instalación de Apache Spark en Colab
Como Google Colab no incluye Apache Spark, debemos instalarlo desde cero usando los siguientes pasos.

### 🔹 Paso 1: Descargar e Instalar Apache Spark
Ejecuta el siguiente código en una celda de Colab para instalar Spark y sus dependencias:
```python
!apt-get install openjdk-8-jdk-headless -qq > /dev/null
!wget -q https://downloads.apache.org/spark/spark-3.2.1/spark-3.2.1-bin-hadoop3.2.tgz
!tar xf spark-3.2.1-bin-hadoop3.2.tgz
!pip install -q findspark
```

### 🔹 Paso 2: Configurar Variables de Entorno
Configura las variables de entorno necesarias para ejecutar Spark:
```python
import os
os.environ["JAVA_HOME"] = "/usr/lib/jvm/java-8-openjdk-amd64"
os.environ["SPARK_HOME"] = "/content/spark-3.2.1-bin-hadoop3.2"
```

### 🔹 Paso 3: Iniciar PySpark en Colab
Ejecuta el siguiente código para iniciar PySpark:
```python
import findspark
findspark.init()
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("Colab_Spark").getOrCreate()
print("Apache Spark en Colab ha sido configurado correctamente.")
```
Si el proceso es exitoso, verás el mensaje de confirmación.

---

## 🏎️ Verificación de Instalación
Para asegurarte de que Spark está funcionando, ejecuta:
```python
df = spark.createDataFrame([("Alice", 25), ("Bob", 30), ("Charlie", 35)], ["Nombre", "Edad"])
df.show()
```
Si ves una tabla con nombres y edades, significa que Spark está corriendo correctamente en Colab.

---

## 🎯 Conclusión
Ahora tienes Apache Spark funcionando en **Google Colab**. Esto te permite aprovechar la infraestructura en la nube sin necesidad de configuraciones complejas. Puedes comenzar a trabajar con **PySpark** para análisis de datos y machine learning en grandes volúmenes de información. 🚀


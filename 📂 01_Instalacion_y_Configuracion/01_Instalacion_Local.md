# 🖥️ Instalación de Apache Spark en Local

## 🔥 Introducción
Apache Spark se puede ejecutar en entornos locales sin necesidad de un clúster distribuido. Esta instalación es ideal para desarrollo, pruebas y aprendizaje antes de trabajar en entornos de producción.

---

## 🛠️ Requisitos Previos
Antes de instalar Spark, asegúrate de tener lo siguiente:
- **Java JDK 8 o superior**: Spark requiere Java para ejecutarse.
- **Python 3.6 o superior**: Para usar PySpark.
- **Apache Spark**: Descarga e instala la versión estable.
- **Hadoop (opcional)**: Para utilizar HDFS y gestionar almacenamiento distribuido.

### 📌 Verificar Instalaciones
Ejecuta los siguientes comandos en la terminal para comprobar las versiones instaladas:
```bash
java -version
python --version
```
Si no están instalados, descárgalos desde:
- Java: [https://www.oracle.com/java/](https://www.oracle.com/java/)
- Python: [https://www.python.org/](https://www.python.org/)

---

## 📥 Instalación de Apache Spark

### 🔹 Paso 1: Descargar Apache Spark
Descarga la última versión estable desde el sitio oficial:  
➡️ [https://spark.apache.org/downloads.html](https://spark.apache.org/downloads.html)  
Selecciona **Pre-built for Apache Hadoop** para evitar compilaciones manuales.

### 🔹 Paso 2: Extraer y Configurar Variables de Entorno
Una vez descargado el archivo, extráelo en el directorio deseado y configura las variables de entorno:
```bash
mkdir ~/spark
cd ~/spark
tar -xvzf ~/Descargas/spark-3.x.x-bin-hadoop3.tgz
```
Edita el archivo `.bashrc` o `.zshrc` para agregar las variables de entorno:
```bash
echo 'export SPARK_HOME=~/spark/spark-3.x.x-bin-hadoop3' >> ~/.bashrc
echo 'export PATH=$SPARK_HOME/bin:$PATH' >> ~/.bashrc
echo 'export PYSPARK_PYTHON=python3' >> ~/.bashrc
source ~/.bashrc
```

### 🔹 Paso 3: Verificar la Instalación
Para comprobar que Spark está funcionando correctamente, ejecuta:
```bash
spark-shell
```
Si todo está correcto, verás la consola interactiva de Spark con Scala.

---

## 🐍 Uso de PySpark en Local
Si deseas ejecutar Spark con Python, usa:
```bash
pyspark
```
Para probar un pequeño script en PySpark:
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("EjemploLocal").getOrCreate()
data = [("Alice", 25), ("Bob", 30), ("Charlie", 35)]
df = spark.createDataFrame(data, ["Nombre", "Edad"])
df.show()
```

---

## 🚀 Conclusión
Con esta configuración, tienes Apache Spark funcionando en tu máquina local. Puedes empezar a desarrollar y probar código en PySpark sin necesidad de un clúster distribuido. ¡A explorar el poder de Spark! 🔥


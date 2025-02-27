# ☁️ Configurar Apache Spark en AWS

## 🔥 Introducción
Apache Spark es una herramienta poderosa para el procesamiento de datos a gran escala. En **AWS (Amazon Web Services)**, podemos configurar Spark en EC2 o utilizar **Amazon EMR (Elastic MapReduce)**, que ofrece una solución optimizada para el análisis de datos en clústeres.

---

## 📌 Requisitos Previos
Antes de configurar Spark en AWS, necesitas:
- ✅ Una cuenta en AWS ([https://aws.amazon.com/](https://aws.amazon.com/)).
- ✅ Conocimientos básicos de AWS EC2 y EMR.
- ✅ Tener configurado AWS CLI en tu máquina local.
- ✅ Un par de claves SSH para acceder a las instancias EC2.

---

## 🛠️ Opción 1: Instalar Spark en una instancia EC2

### 🔹 Paso 1: Crear una instancia EC2
1. Inicia sesión en **AWS Console**.
2. Dirígete a **EC2 > Instancias** y haz clic en "**Launch Instance**".
3. Selecciona una AMI (Amazon Machine Image), como `Ubuntu 20.04` o `Amazon Linux 2`.
4. Escoge el tipo de instancia (**t2.medium** o superior para mejor rendimiento).
5. Configura el almacenamiento y la seguridad (puerto 22 abierto para SSH).
6. Genera o usa una clave SSH existente y lanza la instancia.

### 🔹 Paso 2: Conectar a la instancia y actualizar paquetes
Conéctate a la instancia desde tu terminal:
```bash
ssh -i "tu-clave.pem" ubuntu@tu-ip-publica
```
Luego, actualiza los paquetes del sistema:
```bash
sudo apt update && sudo apt upgrade -y
```

### 🔹 Paso 3: Instalar Java y Apache Spark
```bash
sudo apt install openjdk-8-jdk -y
wget https://downloads.apache.org/spark/spark-3.2.1/spark-3.2.1-bin-hadoop3.2.tgz
tar -xvzf spark-3.2.1-bin-hadoop3.2.tgz
mv spark-3.2.1-bin-hadoop3.2 spark
```

### 🔹 Paso 4: Configurar Variables de Entorno
```bash
echo 'export SPARK_HOME=~/spark' >> ~/.bashrc
echo 'export PATH=$SPARK_HOME/bin:$PATH' >> ~/.bashrc
echo 'export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64' >> ~/.bashrc
source ~/.bashrc
```

### 🔹 Paso 5: Verificar instalación de Spark
```bash
spark-shell
```
Si la consola de Spark inicia correctamente, la instalación fue exitosa.

---

## 🏆 Opción 2: Configurar Apache Spark en Amazon EMR

Si no quieres configurar manualmente un clúster EC2, **Amazon EMR** permite crear un clúster con Apache Spark preconfigurado.

### 🔹 Paso 1: Crear un clúster EMR
1. Inicia sesión en **AWS Console**.
2. Ve a **Amazon EMR > Create Cluster**.
3. Selecciona el modo **Cluster estándar**.
4. En la sección **Software Configuration**, elige **Apache Spark**.
5. Configura el tamaño del clúster (mínimo `m5.xlarge` para rendimiento óptimo).
6. Configura las claves SSH y reglas de acceso.
7. Lanza el clúster y espera a que el estado sea **Waiting**.

### 🔹 Paso 2: Conectar y ejecutar Spark en EMR
Conéctate a la instancia **Master Node** con SSH:
```bash
ssh -i "tu-clave.pem" hadoop@tu-ip-master
```
Para ejecutar Spark desde EMR, usa:
```bash
spark-shell
```
Si deseas trabajar con PySpark:
```bash
pyspark
```

---

## 🎯 Conclusión
Dependiendo de tu caso de uso, puedes instalar Spark manualmente en **EC2** o usar **Amazon EMR** para un despliegue más sencillo. EMR es recomendable para proyectos grandes con integración en el ecosistema de AWS. 🚀


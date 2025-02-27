# 🐳 Configuración de Apache Spark con Docker

## 🔥 Introducción
Docker permite ejecutar **Apache Spark** en un entorno aislado sin necesidad de instalaciones complejas en el sistema operativo anfitrión. Con Docker, puedes desplegar Spark en contenedores, facilitando la escalabilidad y la portabilidad de los proyectos de Big Data.

---

## 📌 Requisitos Previos
Antes de comenzar, asegúrate de tener instalado:
- **Docker** ([https://www.docker.com/get-started](https://www.docker.com/get-started))
- **Docker Compose** (opcional para clústeres más complejos)

Para verificar la instalación, ejecuta:
```bash
docker --version
docker-compose --version
```
Si Docker no está instalado, sigue la guía oficial en su sitio web.

---

## 🛠️ Instalación y Configuración de Apache Spark en Docker
### 🔹 Paso 1: Descargar la Imagen Oficial de Apache Spark
Ejecuta el siguiente comando para obtener la imagen oficial de Spark:
```bash
docker pull bitnami/spark:latest
```
Este contenedor incluye Apache Spark preconfigurado.

### 🔹 Paso 2: Ejecutar un Contenedor con Spark Standalone
Para iniciar un contenedor con **Spark Standalone**, usa:
```bash
docker run -it --rm \
  --name spark-master \
  -p 8080:8080 -p 7077:7077 \
  bitnami/spark:latest spark-class org.apache.spark.deploy.master.Master
```
Este comando inicia un **Master Node** y expone los puertos 8080 (interfaz web) y 7077 (comunicación con Workers).

Para verificar que Spark está corriendo, accede a la interfaz web en:  
➡️ [http://localhost:8080](http://localhost:8080)

### 🔹 Paso 3: Añadir un Nodo Worker
Ejecuta el siguiente comando en una nueva terminal:
```bash
docker run -it --rm \
  --name spark-worker \
  --link spark-master \
  bitnami/spark:latest spark-class org.apache.spark.deploy.worker.Worker spark://spark-master:7077
```
Este nodo Worker se conectará automáticamente al Master Node.

Para ver el estado del Worker, revisa la interfaz web en [http://localhost:8080](http://localhost:8080).

---

## 📂 Usar Docker Compose para un Clúster Completo
Si deseas automatizar la configuración, crea un archivo `docker-compose.yml` con la siguiente configuración:
```yaml
version: '3'
services:
  spark-master:
    image: bitnami/spark:latest
    container_name: spark-master
    ports:
      - "8080:8080"
      - "7077:7077"
    command: spark-class org.apache.spark.deploy.master.Master
  
  spark-worker:
    image: bitnami/spark:latest
    container_name: spark-worker
    depends_on:
      - spark-master
    command: spark-class org.apache.spark.deploy.worker.Worker spark://spark-master:7077
```

Para iniciar el clúster, usa:
```bash
docker-compose up -d
```
Y para detenerlo:
```bash
docker-compose down
```

---

## 🎯 Conclusión
Docker simplifica la instalación y administración de Apache Spark al eliminar dependencias y configuraciones manuales. Con un solo comando, puedes iniciar un entorno de Big Data listo para el desarrollo y la experimentación. 🚀


# Google Cloud Vertex AI

```markdown
# Uso de Google Cloud Vertex AI para Desarrollo y Despliegue de Modelos de Machine Learning

En este proyecto, utilizaremos Google Cloud Vertex AI para crear y desplegar modelos de Machine Learning a gran escala. A continuación, se presenta un ejemplo básico de cómo realizar este proceso.

## Creación de un Modelo con Google Cloud Vertex AI

Primero, configuramos nuestro entorno de desarrollo y creamos un modelo con la siguiente secuencia de comandos utilizando Google Cloud SDK:

```bash
gcloud ai models create NOMBRE_MODELO \
  --region=REGION
```

Reemplazamos `NOMBRE_MODELO` con el nombre deseado para nuestro modelo y `REGION` con la región de Google Cloud que queremos utilizar.

## Entrenamiento del Modelo

A continuación, iniciamos el entrenamiento de nuestro modelo utilizando un conjunto de datos de ejemplo:

```bash
gcloud ai models versions create VERSION \
  --model=NOMBRE_MODELO \
  --origin=gs://RUTA_DATOS_ENTRENAMIENTO \
  --framework=SCIKIT_LEARN \
  --python-version=3.7 \
  --runtime-version=2.1 \
  --region=REGION
```

Reemplazamos `VERSION` con el número de versión que queremos asignar a nuestro modelo y `RUTA_DATOS_ENTRENAMIENTO` con la ruta al conjunto de datos de entrenamiento en Google Cloud Storage.

## Despliegue del Modelo

Desplegamos nuestro modelo para que esté listo para recibir predicciones:

```bash
gcloud ai endpoints create NOMBRE_ENDPOINT \
  --region=REGION

gcloud ai endpoints deploy-model NOMBRE_ENDPOINT \
  --region=REGION \
  --model=NOMBRE_MODELO \
  --version=VERSION
```

Reemplazamos `NOMBRE_ENDPOINT` con el nombre que queremos para nuestro endpoint y `VERSION` con la versión del modelo que queremos desplegar.

## Realización de Predicciones

Una vez que el modelo está desplegado, podemos realizar predicciones con el siguiente comando:

```bash
gcloud ai endpoints predict NOMBRE_ENDPOINT \
  --region=REGION \
  --json-request=archivo_solicitud.json
```

Reemplazamos `archivo_solicitud.json` con el archivo que contiene la solicitud de predicción en formato JSON.

## Monitoreo y Evaluación

Google Cloud Vertex AI proporciona herramientas para monitorear y evaluar el rendimiento de nuestros modelos desplegados. Podemos utilizar la consola de Google Cloud o las API correspondientes para realizar un seguimiento de las métricas y el comportamiento del modelo en producción.

## Limpieza de Recursos

Finalmente, para evitar costos innecesarios, podemos limpiar los recursos creados utilizando los siguientes comandos:

```bash
gcloud ai endpoints delete NOMBRE_ENDPOINT --region=REGION

gcloud ai models delete NOMBRE_MODELO --region=REGION
```

Reemplazamos `NOMBRE_ENDPOINT` y `NOMBRE_MODELO` con los nombres de nuestro endpoint y modelo, respectivamente.

```

Este ejemplo básico muestra cómo crear, entrenar y desplegar un modelo de Machine Learning utilizando Google Cloud Vertex AI. Puedes personalizar estos comandos según los detalles específicos de tu proyecto, como el tipo de modelo, los datos de entrenamiento y las métricas de evaluación.
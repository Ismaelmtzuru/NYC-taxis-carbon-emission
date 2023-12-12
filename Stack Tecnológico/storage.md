# Google Cloud Storage

```markdown
# Uso de Google Cloud Storage para Almacenamiento Eficiente de Datos

Google Cloud Storage es un servicio de almacenamiento en la nube que permite almacenar y recuperar datos de manera escalable y segura. A continuación, se presenta un ejemplo básico de cómo utilizar Google Cloud Storage para el almacenamiento eficiente de datos.

## Configuración Inicial

Antes de utilizar Google Cloud Storage, asegúrate de tener una cuenta de Google Cloud y haber creado un proyecto. A continuación, se describen los pasos iniciales:

1. **Habilitar la API de Cloud Storage:**
   - Ve a la consola de Google Cloud.
   - Selecciona tu proyecto.
   - Habilita la API de Cloud Storage desde el panel de servicios.

2. **Configurar Credenciales:**
   - Crea credenciales de cuenta de servicio con permisos de almacenamiento.
   - Descarga el archivo JSON de las credenciales.

3. **Instalar la Biblioteca Cliente de Google Cloud Storage:**
   - Instala la biblioteca cliente de Google Cloud Storage en tu entorno de desarrollo:

   ```bash
   pip install google-cloud-storage
   ```

## Subir Archivos a Cloud Storage

Para subir archivos a Cloud Storage, utiliza el siguiente código en Python:

```python
from google.cloud import storage

def upload_blob(bucket_name, source_file_name, destination_blob_name):
    """Cargar un archivo a Cloud Storage."""
    storage_client = storage.Client()
    bucket = storage_client.bucket(bucket_name)
    blob = bucket.blob(destination_blob_name)

    blob.upload_from_filename(source_file_name)

    print(f"Archivo {source_file_name} subido a {destination_blob_name} en el bucket {bucket_name}.")

# Ejemplo de uso
upload_blob("mi_bucket", "archivo_local.txt", "ruta_en_cloud/archivo_remoto.txt")
```

Reemplaza `"mi_bucket"`, `"archivo_local.txt"`, `"ruta_en_cloud/archivo_remoto.txt"` con tus propios valores.

## Descargar Archivos desde Cloud Storage

Para descargar archivos desde Cloud Storage, utiliza el siguiente código en Python:

```python
def download_blob(bucket_name, source_blob_name, destination_file_name):
    """Descargar un archivo de Cloud Storage."""
    storage_client = storage.Client()
    bucket = storage_client.bucket(bucket_name)
    blob = bucket.blob(source_blob_name)

    blob.download_to_filename(destination_file_name)

    print(f"Archivo {source_blob_name} descargado a {destination_file_name}.")

# Ejemplo de uso
download_blob("mi_bucket", "ruta_en_cloud/archivo_remoto.txt", "archivo_local.txt")
```

Reemplaza `"mi_bucket"`, `"ruta_en_cloud/archivo_remoto.txt"`, `"archivo_local.txt"` con tus propios valores.

## Listar Archivos en un Bucket

Para obtener la lista de archivos en un bucket, utiliza el siguiente código en Python:

```python
def list_blobs(bucket_name):
    """Listar todos los archivos en un bucket."""
    storage_client = storage.Client()
    blobs = storage_client.list_blobs(bucket_name)

    print("Archivos en el bucket:")
    for blob in blobs:
        print(blob.name)

# Ejemplo de uso
list_blobs("mi_bucket")
```

Reemplaza `"mi_bucket"` con tu propio valor.

## Eliminar Archivos de Cloud Storage

Para eliminar un archivo de Cloud Storage, utiliza el siguiente código en Python:

```python
def delete_blob(bucket_name, blob_name):
    """Eliminar un archivo de Cloud Storage."""
    storage_client = storage.Client()
    bucket = storage_client.bucket(bucket_name)
    blob = bucket.blob(blob_name)

    blob.delete()

    print(f"Archivo {blob_name} eliminado del bucket {bucket_name}.")

# Ejemplo de uso
delete_blob("mi_bucket", "ruta_en_cloud/archivo_remoto.txt")
```

Reemplaza `"mi_bucket"`, `"ruta_en_cloud/archivo_remoto.txt"` con tus propios valores.

```

Este ejemplo básico muestra cómo utilizar Google Cloud Storage para el almacenamiento eficiente de datos. Personaliza los ejemplos según las necesidades de tu proyecto y aprovecha las capacidades de escalabilidad y seguridad de Cloud Storage.
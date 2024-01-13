### Pipeline ETL Automatizado:

Para automatizar el proceso ETL, puedes utilizar un script de Python que maneje las tareas de extracción, transformación y carga de datos. Aquí proporciono un ejemplo simple que podrías adaptar según tus necesidades y entorno.

```python
import os
import sqlite3
import pandas as pd
from bs4 import BeautifulSoup
import requests
import urllib.parse
import math

# Definir rutas
url = "https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page"
output_directory = 'C:\\Users\\ISMAEL\\Desktop\\scrapping\\raw'
ruta_limpia = 'C:\\Users\\ISMAEL\\Desktop\\scrapping\\clean'
ruta_bd = 'C:\\Users\\ISMAEL\\Desktop\\scrapping\\data_warehouse\\bd.db'

def descargar_archivo(link_url, output_directory):
    file_name = os.path.basename(link_url)
    file_path = os.path.join(output_directory, file_name)

    response_file = requests.get(link_url)

    if response_file.status_code == 200:
        with open(file_path, 'wb') as file:
            file.write(response_file.content)
        print(f'Archivo descargado: {file_path}')
        return file_name
    else:
        print(f'Error al descargar el archivo desde {link_url}. Código de estado: {response_file.status_code}')
        return None

def limpiar_y_guardar(archivo, output_directory, ruta_limpia):
    archivo_ruta = os.path.join(output_directory, archivo)
    archivo_ruta_limpia = os.path.join(ruta_limpia, archivo)

    if os.path.exists(archivo_ruta_limpia):
        # Obtener el año y mes del archivo en la carpeta limpia
        parts = archivo.split('_')
        if len(parts) >= 4:
            year, month = map(int, parts[-2].split('-'))
        else:
            print(f'Error al procesar el nombre del archivo: {archivo}')
            return

        # Obtener el año y mes del archivo en la carpeta limpia
        parts_clean = archivo_ruta_limpia.split('_')
        if len(parts_clean) >= 4:
            clean_year, clean_month = map(int, parts_clean[-2].split('-'))
        else:
            print(f'Error al procesar el nombre del archivo limpio: {archivo_ruta_limpia}')
            return

        if year == clean_year and month == clean_month:
            print(f'El archivo {archivo} ya existe, se procede con el siguiente.')
            return
    else:
        print(f'Limpiando y guardando en la carpeta limpia: {archivo}')

    # ... (Operaciones de limpieza y transformación según el tipo de archivo)

    # Guardar en la carpeta "clean"
    df.to_parquet(os.path.join(ruta_limpia, archivo), index=False)

    # ... (Cargar a la base de datos)

# Continuar con el código del scraping y ETL...
```

Este script realiza la descarga y la limpieza de cada archivo, evitando descargarlos nuevamente si ya existen en la carpeta limpia. 


 Ahora agregaremos funciones para la creación de tablas y la carga de datos en la base de datos SQLite.

```python
import sqlite3



def crear_tabla(nombre_tabla, cursor):
    if 'green' in nombre_tabla:
        sql_command = """
        CREATE TABLE IF NOT EXISTS green (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            VendorID INTEGER NOT NULL,
            lpep_pickup_datetime DATETIME,
            lpep_dropoff_datetime DATETIME,
            store_and_fwd_flag VARCHAR(4),
            RatecodeID INTEGER,
            PULocationID INTEGER,
            DOLocationID INTEGER,
            passenger_count INTEGER,
            trip_distance FLOAT,
            fare_amount FLOAT,
            extra FLOAT,
            mta_tax FLOAT,
            tip_amount FLOAT,
            tolls_amount FLOAT,
            improvement_surcharge FLOAT,
            total_amount FLOAT,
            payment_type INTEGER,
            trip_type INTEGER,
            congestion_surcharge FLOAT
        )
        """
    # ... (Añadir otras tablas según sea necesario)

    cursor.execute(sql_command)

def carga_sqlite(nombre_tabla, comando_sql, ruta_limpia, archivo):
    ruta_bd = 'C:\\Users\\ISMAEL\\Desktop\\scrapping\\data_warehouse\\bd.db'
    with sqlite3.connect(ruta_bd) as conn:
        cursor = conn.cursor()

        # Crear la tabla si no existe
        crear_tabla(nombre_tabla, cursor)

        # Cargar datos en la tabla SQLite
        df = pd.read_parquet(os.path.join(ruta_limpia, archivo))
        df.to_sql(nombre_tabla, conn, if_exists='append', index=False)

# ... (Código anterior)

# Iterar sobre los archivos descargados para limpiar y guardar en otra carpeta
for archivo in descargados:
    # ... (Código anterior)

    # Obtener tipo de archivo
    tipo_archivo = archivo.split('_')[0].lower()

    # Se realiza la limpieza según el tipo de archivo (green, yellow, fhv, fhvhv)
    if 'green' == tipo_archivo:
        nombre_tabla = 'green'
        # ... (Operaciones de limpieza y transformación para green)
        carga_sqlite(nombre_tabla, None, ruta_limpia, archivo)
    elif 'yellow' == tipo_archivo:
        nombre_tabla = 'yellow'
        # ... (Operaciones de limpieza y transformación para yellow)
        carga_sqlite(nombre_tabla, None, ruta_limpia, archivo)
    # ... (Agregar casos para 'fhv' y 'fhvhv')

# ... (Código posterior)
```

Este código asume que los datos se cargarán en la misma base de datos SQLite. Si prefieres utilizar un servicio diferente para el almacenamiento, el código puede necesitar ajustes. Además, ten en cuenta que las operaciones de limpieza y transformación deben completarse según los requisitos de tus datos.




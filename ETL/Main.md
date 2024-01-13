
### ETL Completo:

El ETL (Extract, Transform, Load) es un proceso esencial en el flujo de trabajo de cualquier proyecto de análisis de datos. Aquí hay un esquema básico para el ETL completo:

#### 1. Extracción de Datos:

```python
# Ejemplo de Extracción de Datos desde Archivos Parquet
import os
import urllib.parse
import requests
import pandas as pd

url = "https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page"
output_directory = 'C:\\Users\\ISMAEL\\Desktop\\scrappng\\raw'
response = requests.get(url)

# Validar si la solicitud fue exitosa (código de estado 200)
if response.status_code == 200:
    soup = BeautifulSoup(response.text, "html.parser")
    year_section = soup.find('div', {'id': 'faq2023'})

    if year_section:
        links = year_section.find_all('a')
        for link in links:
            link_url = urllib.parse.urljoin(url, link.get('href'))
            file_name = os.path.basename(link_url)
            file_path = os.path.join(output_directory, file_name)
            
            response_file = requests.get(link_url)
            if response_file.status_code == 200:
                with open(file_path, 'wb') as file:
                    file.write(response_file.content)
                print(f'Archivo descargado: {file_path}')
            else:
                print(f'Error al descargar el archivo desde {link_url}. Código de estado: {response_file.status_code}')
```

Esto descargará los archivos de la URL proporcionada y los almacenará en el directorio especificado (`output_directory`).

#### 2. Transformación de Datos:

En el código que proporcionaste ya tienes algunas transformaciones para los archivos `green`, `yellow`, `fhv`, y `fhvhv`. Estas transformaciones se encargan de limpiar los datos, manejar valores nulos y ajustar los tipos de datos. Puedes seguir mejorando estas transformaciones según tus necesidades específicas.

```python
# (Continuación del código)
# Iterar sobre los archivos descargados para limpiar y guardar en otra carpeta
for archivo in descargados:
    archivo_ruta = os.path.join(output_directory, archivo)
    archivo_ruta_limpia = os.path.join(ruta_limpia, archivo)
    
    # Se verifica si el archivo existe para no volver a descargar
    if os.path.exists(archivo_ruta_limpia):
        # Obtener el año y mes del archivo
        parts = archivo.split('_')
        if len(parts) >= 4:
            year, month = map(int, parts[-2].split('-'))
        else:
            print(f'Error al procesar el nombre del archivo: {archivo}')
            continue

        # Obtener el año y mes del archivo en la carpeta limpia
        parts_clean = archivo_ruta_limpia.split('_')
        if len(parts_clean) >= 4:
            clean_year, clean_month = map(int, parts_clean[-2].split('-'))
        else:
            print(f'Error al procesar el nombre del archivo limpio: {archivo_ruta_limpia}')
            continue

        if year == clean_year and month == clean_month:
            print(f'El archivo {archivo} ya existe, se procede con el siguiente.')
            continue
    else:
        # El archivo no existe en la carpeta limpia, proceder con la limpieza
        print(f'Limpiando y guardando en la carpeta limpia: {archivo}')

    # (Aquí sigue el código de limpieza y transformación que ya proporcionaste)
    # ...
```

Este bloque de código verifica si el archivo ya existe en la carpeta limpia (`ruta_limpia`). Si existe, se omite y pasa al siguiente archivo; de lo contrario, se procede con la limpieza y transformación.

#### 3. Carga de Datos:

El código también incluye la carga de datos en SQLite después de la transformación. Se utiliza una función `carga_sqlite` para este propósito.

```python
# (Continuación del código)
# se carga el esquema dependiendo del nombre
nombre_tabla = 'green'  # o 'yellow', 'fhv', 'fhvhv' según el archivo
sql_esquema = sql_esquema_tabla(nombre_tabla)

# se carga a la base de datos
carga_sqlite(nombre_tabla, sql_esquema, ruta_limpia, archivo)
```

Este fragmento llama a la función `carga_sqlite` que toma el nombre de la tabla, el comando SQL y el archivo limpio, y carga los datos en SQLite.


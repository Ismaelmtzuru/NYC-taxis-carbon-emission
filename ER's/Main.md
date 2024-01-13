### Estructura de Datos Implementada:

Para estructurar los datos, se pueden utilizar varios elementos. Aquí propongo una estructura simple con un Data Lake y un Data Warehouse:

#### 1. Data Lake (Raw):

En el Data Lake se almacenarían los datos crudos sin procesar, descargados directamente de la fuente. Esto permite preservar la integridad de los datos originales.

```
data_lake/
|-- raw/
|   |-- green_tripdata_2023-01.parquet
|   |-- yellow_tripdata_2023-01.parquet
|   |-- fhv_tripdata_2023-01.parquet
|   |-- fhvhv_tripdata_2023-01.parquet
```

En este directorio, cada archivo parquet representa un conjunto de datos descargado.

#### 2. Data Lake (Clean):

Después del proceso de limpieza y transformación, los datos se almacenan en una carpeta diferente para mantener una copia limpia y procesada.

```
data_lake/
|-- clean/
|   |-- green_tripdata_2023-01.parquet
|   |-- yellow_tripdata_2023-01.parquet
|   |-- fhv_tripdata_2023-01.parquet
|   |-- fhvhv_tripdata_2023-01.parquet
```

Aquí, los archivos parquet son versiones limpias de los datos originales.

#### 3. Data Warehouse:

El Data Warehouse almacena datos listos para el análisis y consultas. Puedes usar SQLite como base de datos, pero para implementaciones más avanzadas, considera bases de datos como PostgreSQL, MySQL o soluciones en la nube como Google BigQuery o Amazon Redshift.

```
data_warehouse/
|-- bd.db
```

En este caso, `bd.db` es la base de datos SQLite que contiene las tablas estructuradas.

Con esta estructura, se mantiene una separación clara entre los datos brutos y procesados. 


Claro, continuemos. Ahora vamos a definir el modelo ER y crear pipelines para alimentar el Data Warehouse. Dado que en este caso estamos utilizando SQLite y asumiendo un esquema simplificado, no se necesitarán estructuras complejas de Data Warehouse ni ETL exhaustivo. Vamos a mantenerlo simple y directo.

### Modelo ER (Diagrama de Entidad-Relación)

Asumiendo que tienes las siguientes entidades:

1. `GreenTrips`
2. `YellowTrips`
3. `FHVHVTrips`
4. `FHTrips`

Y cada una de estas entidades tiene atributos que se corresponden con las columnas en las tablas de la base de datos SQLite, el modelo ER podría verse así:

```
+--------------+           +------------------------+
| GreenTrips   |<--------->| YellowTrips            |
|--------------|           |------------------------|
| id           |           | id                     |
| VendorID     |           | VendorID               |
| ...          |           | ...                    |
+--------------+           +------------------------+
        |
        |
+--------------+
| FHVHVTrips   |
|--------------|
| id           |
| hvfhs_license_num  |
| ...          |
+--------------+
        |
        |
+--------------+
| FHTrips      |
|--------------|
| id           |
| dispatching_base_num |
| ...          |
+--------------+
```

### Pipelines para alimentar el Data Warehouse

Dado que estamos utilizando SQLite y asumiendo que todas las tablas están en la misma base de datos, el proceso de carga en el Data Warehouse puede simplificarse. Puedes ejecutar consultas SQL para extraer datos de las tablas limpias y cargarlos en tablas específicas del Data Warehouse.

Aquí hay un ejemplo de cómo podrías hacer esto:

```python
import sqlite3

def cargar_en_data_warehouse(tabla_fuente, tabla_destino, conn):
    cursor = conn.cursor()
    query = f"INSERT INTO {tabla_destino} SELECT * FROM {tabla_fuente}"
    cursor.execute(query)
    conn.commit()

# ... (Código anterior)

# Iterar sobre los archivos descargados para cargar en Data Warehouse
for archivo in descargados:
    # ... (Código anterior)

    # Obtener tipo de archivo
    tipo_archivo = archivo.split('_')[0].lower()

    # Se realiza la limpieza según el tipo de archivo (green, yellow, fhv, fhvhv)
    if 'green' == tipo_archivo:
        nombre_tabla = 'green'
        # ... (Operaciones de limpieza y transformación para green)
        carga_sqlite(nombre_tabla, None, ruta_limpia, archivo)
        cargar_en_data_warehouse('green', 'GreenTrips', conn)
    elif 'yellow' == tipo_archivo:
        nombre_tabla = 'yellow'
        # ... (Operaciones de limpieza y transformación para yellow)
        carga_sqlite(nombre_tabla, None, ruta_limpia, archivo)
        cargar_en_data_warehouse('yellow', 'YellowTrips', conn)
    # ... (Agregar casos para 'fhv' y 'fhvhv')

# ... (Código posterior)
```

Este código simplemente ejecuta una consulta SQL para insertar los datos desde las tablas limpias en las tablas correspondientes del Data Warehouse.




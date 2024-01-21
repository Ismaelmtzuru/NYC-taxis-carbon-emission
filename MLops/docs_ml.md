# Time Series 📊

**Descripción general:**
Este script implementa un modelo de series temporales utilizando la biblioteca Pycaret. El conjunto de datos proviene de los viajes de taxis en enero de 2023 y se carga desde un archivo Parquet. El objetivo es predecir la variable 'driver_pay' (pago al conductor) en función de la fecha de los viajes.

**Pasos de preprocesamiento de datos:**
1. **Carga de datos:**
   - Se utiliza la función 'pd.read_parquet' para cargar los datos desde el archivo Parquet 'fhvhv_tripdata_2023-01.parquet'.
2. **Creación de la columna de fecha:**
   - Se crea una nueva columna 'date' extrayendo la fecha de la columna 'pickup_datetime'.
3. **Selección de columnas relevantes:**
   - Se seleccionan las columnas 'dates' y 'driver_pay' para el análisis y lo necesario para el modelo de time series.
4. **Eliminación de valores nulos y duplicados:**
   - Se eliminan filas que contienen valores nulos y duplicados en el DataFrame resultante.
5. **Agrupación por fecha y suma de 'driver_pay':**
   - Se agrupa el DataFrame por la columna 'date' y se suma la columna 'driver_pay' para obtener un DataFrame consolidado.
6. **Conversión de 'date' a tipo Datetime:**
   - Se convierte la columna 'date' a tipo datetime para facilitar su manipulación y visualización.

**Configuración del modelo con Pycaret:**
1. **Configuración del entorno Pycaret:**
   - Se utiliza la función 'setup' de Pycaret para configurar el entorno de trabajo.
   - Se especifica el DataFrame agrupado como entrada.
   - Se establece un horizonte de predicción 'fh' de 3 periodos.
   - Se utiliza un esquema de validación cruzada con 5 pliegues 'fold'.
2. **Comparación de modelos:**
   - Se emplea la función 'compare_models' para comparar varios modelos de series temporales.
   - Se evalúan los modelos según diferentes métricas, como MASE, RMSSE, MAE, RMSE, MAPE, SMAPE, R2.
3. **Visualización de resultados:**
   - Se utiliza la función 'plot_model' para visualizar los resultados del mejor modelo seleccionado.
   - Se muestran gráficos de pronóstico, diagnóstico y resultado de la muestra.
4. **Finalización del modelo:**
   - Se finaliza el mejor modelo seleccionado utilizando la función 'finalize_model'.
5. **Predicción con el modelo entrenado:**
   - Se utiliza la función 'predict_model' para realizar predicciones en una ventana de tiempo futura ('h=2').

**Observaciones y conclusiones:**
   - El modelo seleccionado se basa en la comparación de varios modelos utilizando Pycaret.
   - Se han evaluado métricas de rendimiento específicas de series temporales para seleccionar el mejor modelo.
   - Las visualizaciones proporcionan información sobre los pronósticos, diagnósticos y resultados en la muestra.
   - Se ha finalizado el mejor modelo y se han realizado predicciones para un horizonte de tiempo futuro.

**Notas finales:**
Este documento proporciona una descripción general del proceso de implementación del modelo de series temporales utilizando Pycaret. Es recomendable ajustar y mejorar el script según las necesidades específicas del problema. 🚀






























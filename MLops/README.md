# Time Series con PyCaret [notebook](ML_pago_conductor.ipynb)

Este script utiliza PyCaret para desarrollar un modelo de series temporales con el objetivo de predecir 'driver_pay' en los viajes de taxis de 2023, empleando datos cargados desde un archivo Parquet. Los pasos incluyen la carga y preprocesamiento de datos, la agrupación por fecha y la configuración del modelo con PyCaret. Se realiza una comparación de modelos, seguida de visualizaciones y la finalización del mejor modelo para futuras predicciones. Se evalúan métricas de rendimiento específicas de series temporales, y las visualizaciones proporcionan información sobre pronósticos y diagnósticos. Este documento brinda una visión general concisa del proceso, recomendando ajustes según las necesidades específicas del problema. 🚀

## Gráficas generadas con el modelo Time Series

#### Gráfico de pronóstico
![1](img/1.png)

<br>
<br>
<br>
<br>
<br>

#### Gráfico de diagnóstico

![2](img/2.png)
<br>
<br>
<br>
<br>
<br>

#### Gráfico de resultados en la muestra

![3](img/3.png)


# Predicción de costo de viaje a través de Machine learning
En el siguiente [repositorio](https://github.com/Ismaelmtzuru/ml_deploy) se encuentra un *segundo* modelo de machine learning el cual puede ser consumido por un usuario que desee predecir el costo de un viaje en la ciudad de Nueva York (NYC).
[App del modelo](https://ml-deploy-9c4d57010124.herokuapp.com/)



# Documentación
<br>

[Documentación del modelo consumible 'predicción de costo de viaje'](https://github.com/Ismaelmtzuru/ml_deploy/blob/master/ml_consumible.ipynb) <br>
[Documentación del modelo 'ganancias de conductor'](docs_ml.md)

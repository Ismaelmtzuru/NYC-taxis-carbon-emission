# PYCARET

```markdown
# Uso de PyCaret para Análisis Previo al EDA y Selección de Modelos de Machine Learning

Para un uso antes del EDA y ver los features importantes para algún modelo de machine learning, el cual la misma librería nos va a recomendar. Se implementaría de la siguiente forma:

```python
from pycaret.datasets import get_data
data = get_data("diabetes")
```

donde en la variable `data`, se guarda el dataset el cual se va a analizar, en este ejemplo se obtienen los datos de la misma librería.

Para iniciar la configuración, se importan todas las clasificaciones:

```python
from pycaret.classification import *
s = setup(data, target="Class variable", session_id=123)
```

Donde `data` es el dataset, `target` es "Class variable" para analizar todas las variables en los modelos. `session_id` es igual a un random state. Esto va a arrojar información del trabajo que ha realizado al configurar el dataset original en la nueva variable.

| Description               | Value               |
|---------------------------|---------------------|
| Session id                | 123                 |
| Target                    | Class variable      |
| Target type               | Binary              |
| Original data shape       | (768, 9)            |
| Transformed data shape     | (768, 9)            |
| Transformed train set shape| (537, 9)            |
| Transformed test set shape | (231, 9)            |
| Numeric features          | 8                   |
| Preprocess                | True                |
| Imputation type           | simple              |
| Numeric imputation        | mean                |
| Categorical imputation    | mode                |
| Fold Generator            | StratifiedKFold     |
| Fold Number               | 10                  |
| CPU Jobs                  | -1                  |
| Use GPU                   | False               |
| Log Experiment            | False               |
| Experiment Name           | clf-default-name    |
| USI                       | d3df                |

Lo más relevante de esta info es que el shape original es de (768,9) y como este dataset no tiene valores nulos o NaN, sigue de la misma forma. Si fuera caso contrario, se imputarían con el valor medio estos valores nulos. Se puede ver que está indicado en `numeric imputation`.

Para manejar los valores faltantes, sean string o numéricos, se usa lo siguiente:

- `imputation_type`: es string, por default = "simple". Puede ser simple o iterative. Si es none, no se imputarán los valores faltantes.

- `numeric_imputation`: int, float, or string, default = "mean". Es un parámetro que determina la estrategia de imputación a utilizar para las columnas numéricas en el conjunto de datos, cuando `imputation_type` es "simple". Se pueden dar los siguientes valores:

  - `drop`: Elimina toda la fila que contenga por lo menos un valor faltante en alguna columna.
  - `mean`: Se rellenarán los valores faltantes con el promedio de la columna.
  - `median`: Imputará los faltantes en las columnas numéricas utilizando la mediana de la columna.
  - `mode`: Se imputarán los valores faltantes con columnas numéricas con el valor más frecuente (moda) de la columna.
  - `knn`: Se hará la imputación utilizando un enfoque de vecinos más cercanos (k-nearest neighbors). El algoritmo KNN utilizará los valores conocidos más cercanos a un valor faltante para estimar su valor.
  - `int` o `float`: Aquí se puede establecer un número en específico proporcionado por el usuario para rellenar los valores faltantes.

También se puede dar el parámetro `remove_outliers` al momento de hacer la configuración, en este caso en la variable `s`.

- `remove_outliers`: bool, default = False. Cuando se indica True, los outliers son eliminados usando Isolation Forest.
- `outliers_method`: str, default = "iforest". Es el método con el cual se van a eliminar los outliers. Es ignorado si `remove_outliers = False`. Los métodos que se pueden utilizar son:
  - `iforest`: usa sklearn Isolation Forest.
  - `ee`: usa sklearn EllipticEnvelope.
  - `lof`: Usa sklearn LocalOutlierFactor.
- `outliers_threshold`: float, default = 0.05. Es el porcentaje de outliers que se van a eliminar del dataset. Este es ignorado si `remove_outliers = False`.

Para continuar con la comparación, usamos el siguiente código y nos arrojó datos concretos.

```python
best = s.compare_models()
```

A la variable `s`, que es donde está la configuración, se pasa la función `compare_models` para que haga la comparación.

Aquí un ejemplo de su comparación:

| Model                       | Accuracy | AUC    | Recall | Precision | F1     | Kappa | MCC    | TT (Sec) |
|-----------------------------|----------|--------|--------|-----------|--------|-------|--------|----------|
| lr Logistic Regression      | 0.7689   | 0.8047 | 0.5602 | 0.7208    | 0.6279 | 0.4641| 0.4736 | 0.8230   |
| ridge Ridge Classifier      | 0.7670   | 0.0000 | 0.5497 | 0.7235    | 0.6221 | 0.4581| 0.4690 | 0.0170   |
| lda Linear Discriminant Ana | 0.7670   | 0.8055 | 0.5550 | 0.7202    | 0.6243 | 0.4594| 0.4695 | 0.0300   |
| rf Random Forest Classifier | 0.7485   | 0.7911 | 0.5284 | 0.6811    | 0.5924 | 0.4150| 0.4238 | 0.1170   |
| nb Naive Bayes              | 0.7427   | 0.7955 | 0.5702 | 0.6543    | 0.6043 | 0.4156| 0.4215 | 0.0220   |

Y para obtener el modelo que más se adapta a estos datos se usa el código siguiente:

```python
print(best)
```

el cual da el modelo de Logistic Regression.

Para evaluar este modelo se usa lo siguiente:

```python
s.evaluate_model(best)
```

El cual nos va a dar varias pestañas que nos dan indicaciones sobre cómo se ha realizado este modelo y una explicación del dataframe. En feature selection, podemos ver un gráfico del ```markdown
## Evaluación del Modelo

Para evaluar este modelo se utiliza lo siguiente:

```python
s.evaluate_model(best)
```

Esto nos dará varias pestañas que nos dan indicaciones sobre cómo se ha realizado este modelo y una explicación del dataframe. En **Feature Selection**, podemos ver un gráfico del método del codo, donde se observa que se han elegido 4 columnas relevantes. En **Feature Importance**, podemos ver cuáles son esas columnas y así poder tomar decisiones sobre las otras columnas que no son necesarias para este modelo.

En **Confusion Matrix**, se puede observar:

|                | Predicted Positive | Predicted Negative |
|----------------|-------------------|--------------------|
| Actual Positive| Verdaderos Positivos (True Positives)   | Falsos Negativos (False Negatives)   |
| Actual Negative| Falsos Positivos (False Positives)   | Verdaderos Negativos (True Negatives)   |

Esto se lee desde arriba y de izquierda a derecha.
```
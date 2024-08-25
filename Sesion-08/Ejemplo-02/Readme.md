🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 08**](../Readme.md) ➡️ / 📝 `Ejemplo 02: Regresión logística para clasificación supervisada`

## 🎯 Objetivo

Aplicar el algoritmo de **Regresión Logística** para clasificar registros en diferentes grupos basados en características específicas. Utilizaremos un dataset de pacientes para predecir la presencia o ausencia de una enfermedad cardíaca basándonos en factores como edad, presión arterial y nivel de colesterol.

---

## 🚀 Comencemos

La **Regresión Logística** es un algoritmo de clasificación supervisada utilizado para predecir la probabilidad de que una observación pertenezca a una de las dos clases posibles. Es ampliamente utilizado cuando la variable de respuesta es categórica binaria. En este ejemplo, utilizaremos un dataset de pacientes para analizar cómo la Regresión Logística puede ayudar a predecir la presencia de una enfermedad cardíaca basada en la edad, presión arterial en reposo y nivel de colesterol. Utilizaremos el archivo [Ejemplo_02_Heart_Disease_Data.csv](../../Datasets/S08/Ejemplo_02_Heart_Disease_Data.csv).

---

### 🛠️ **Aplicación de la regresión logística**

Sigue los siguientes pasos para aplicar la Regresión Logística al dataset de pacientes:

1. **Instalación de las bibliotecas necesarias:** Asegúrate de tener instaladas las bibliotecas necesarias para realizar el análisis. Si no las tienes, instálalas con el siguiente comando:

    ```bash
    !pip install pandas numpy scikit-learn matplotlib seaborn
    ```

2. **Importación de las bibliotecas:** Importa las bibliotecas que vas a utilizar:

    ```python
    from sklearn.model_selection import train_test_split
    from sklearn.linear_model import LogisticRegression
    import pandas as pd
    import numpy as np
    ```

3. **Carga y exploración del conjunto de datos:** Carga el dataset de detección de enfermedades cardíacas y explora las primeras filas para familiarizarte con los datos:

    ```python
    # Cargar el conjunto de datos
    df = pd.read_csv('../S08/Ejemplo_02_Heart_Disease_Data.csv') # Cambia la ruta al archivo, de acuerdo a tu entorno de trabajo.

    # Mostrar las primeras filas del DataFrame
    df.head()
    ```

4. **Preprocesamiento de datos:** Antes de aplicar la regresión logística, es necesario preprocesar los datos para manejar valores nulos y seleccionar las columnas relevantes para el análisis:

    ```python
    # Verificar y eliminar filas con valores nulos en las columnas relevantes
    # (edad, presión arterial, colesterol y variable objetivo)
    df_cleaned = df.dropna(subset=['age', 'trestbps', 'chol', 'target'])

    # Seleccionar solo las columnas relevantes para el análisis
    X = df_cleaned[['age', 'trestbps', 'chol']]
    y = df_cleaned['target']
    ```

5. **División del conjunto de datos:** Divide el conjunto de datos en conjuntos de entrenamiento y prueba:

    ```python
    # Dividir los datos en entrenamiento y prueba (80% entrenamiento, 20% prueba)
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
    ```

    - **`train_test_split(X, y, test_size=0.2, random_state=42)`**: Divide el conjunto de datos en conjuntos de entrenamiento y prueba.
    - **`X`**: Características independientes.
    - **`y`**: Variable objetivo.
    - **`test_size=0.2`**: Usa el 20% de los datos para pruebas y el 80% para entrenamiento.
    - **`random_state=42`**: Fija la semilla para obtener resultados reproducibles.

    - **`X_train` y `y_train`**: Datos de entrenamiento (80% del total).
    - **`X_test` y `y_test`**: Datos de prueba (20% del total).

    <br>

6. **Aplicación de la regresión logística:** Aplica el algoritmo de regresión logística a los datos de entrenamiento:

    ```python
    # Inicializar el modelo de Regresión Logística
    logreg = LogisticRegression()

    # Ajustar el modelo a los datos de entrenamiento
    logreg.fit(X_train, y_train)

    # Realizar predicciones con el conjunto de prueba
    y_pred = logreg.predict(X_test)

    # Obtener el score del modelo en los datos de prueba
    score = logreg.score(X_test, y_test)
    print(f"Precisión del modelo: {score:.2f}")
    ```
    
    ```
    Precisión del modelo: 0.64
    ```

    - **`logreg = LogisticRegression()`**: Inicializa el modelo de regresión logística.
    - **`logreg.fit(X_train, y_train)`**: Entrena el modelo usando los datos de entrenamiento (`X_train`, `y_train`).
    - **`y_pred = logreg.predict(X_test)`**: Realiza predicciones usando los datos de prueba (`X_test`).
    - **`score = logreg.score(X_test, y_test)`**: Calcula la precisión del modelo en los datos de prueba comparando las predicciones (`y_pred`) con las etiquetas verdaderas (`y_test`). El score varía entre 0 y 1, donde 1 indica una predicción perfecta.

---

### 📉 **Interpretación de los resultados**

El score del modelo obtenido en los datos de prueba proporciona una medida general de la precisión del modelo en la predicción de la presencia de enfermedades cardíacas basado en las características seleccionadas (edad, presión arterial y nivel de colesterol).

En este caso el nivel precisión del modelo fue de 0.64, lo que indica que el modelo acierta en un 64% de los casos. Este valor puede variar dependiendo de la semilla aleatoria utilizada para dividir los datos en entrenamiento y prueba, así como de la selección de características y otros factores.

---

### 💡 **¿Sabías que?...**

La Regresión Logística es sensible a las características escaladas, por lo que a menudo es útil normalizar los datos antes de aplicar el modelo. Además, como en K-Medias, el parámetro `random_state` es importante para garantizar la reproducibilidad de los resultados.

Otro aspecto a considerar es la regularización en la regresión logística. La regularización ayuda a prevenir el sobreajuste penalizando los coeficientes de la función de pérdida. Puedes ajustar el parámetro `C` en `LogisticRegression` para controlar la fuerza de la regularización. Un valor pequeño de `C` indica una mayor regularización.

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Reto-02/Readme.md) ➡️
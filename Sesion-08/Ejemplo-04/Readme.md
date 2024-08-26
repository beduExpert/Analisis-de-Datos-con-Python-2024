🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 08**](../Readme.md) ➡️ / 📝 `Ejemplo 03: Curva ROC y AUC para evaluación de modelos`

## 🎯 Objetivo

Aprender a utilizar la **Curva ROC** y el **Área Bajo la Curva (AUC)** para evaluar el rendimiento de un modelo de clasificación. En este caso, utilizaremos un dataset de transacciones de tarjetas de crédito para predecir si una transacción es fraudulenta o no, y analizaremos la capacidad del modelo para distinguir entre clases utilizando la curva ROC y el AUC.

---

## 🚀 Comencemos

La **Curva ROC (Receiver Operating Characteristic)** es una herramienta utilizada para evaluar el rendimiento de un modelo de clasificación binaria, mostrando la relación entre la tasa de verdaderos positivos (TPR) y la tasa de falsos positivos (FPR) para diferentes umbrales de decisión. El **Área Bajo la Curva (AUC)** mide la capacidad del modelo para distinguir entre las clases. En este ejemplo, utilizaremos un dataset de transacciones de tarjetas de crédito para analizar cómo estas métricas pueden ayudar a evaluar el desempeño del modelo de regresión logística en la detección de fraudes. Utilizaremos el archivo [Ejemplo_03_Credit_Card_Fraud_Dataset.csv](../../Datasets/S08/Ejemplo_03_Credit_Card_Fraud_Dataset.csv).

---

### 🛠️ **Aplicación de la Curva ROC y AUC para la evaluación de modelos**

Sigue los siguientes pasos para calcular la curva ROC y AUC para el dataset de detección de fraudes:

1. **Instalación de las bibliotecas necesarias:** Asegúrate de tener instaladas las bibliotecas necesarias para realizar el análisis. Si no las tienes, instálalas con el siguiente comando:

    ```bash
    pip install pandas numpy scikit-learn matplotlib seaborn
    ```

2. **Importación de las bibliotecas:** Importa las bibliotecas que vas a utilizar:

    ```python
    from sklearn.model_selection import train_test_split
    from sklearn.linear_model import LogisticRegression
    from sklearn.metrics import roc_curve, roc_auc_score, RocCurveDisplay
    import matplotlib.pyplot as plt
    import pandas as pd
    import numpy as np
    ```

3. **Carga y exploración del conjunto de datos:** Carga el dataset de detección de fraudes y explora las primeras filas para familiarizarte con los datos:

    ```python
    # Cargar el conjunto de datos
    df = pd.read_csv('Ejemplo_03_Credit_Card_Fraud_Dataset.csv')  # Ajusta la ruta al archivo según tu entorno de trabajo.

    # Mostrar las primeras filas del DataFrame
    df.head()
    ```

4. **Preprocesamiento de datos:** Selecciona las columnas relevantes para el análisis:

    ```python
    # Seleccionar las columnas relevantes para el análisis
    X = df[['Transaction Amount', 'Transaction Month', 'Transaction Year', 'Transaction Day', 
            'Transaction Hour', 'Transaction Minute', 'Transaction Second', 'Merchant ID']]
    y = df['Fraudulent Flag']
    ```

5. **División del conjunto de datos:** Divide el conjunto de datos en conjuntos de entrenamiento y prueba:

    ```python
    # Dividir los datos en entrenamiento y prueba (80% entrenamiento, 20% prueba)
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
    ```

6. **Aplicación de la regresión logística:** Aplica el algoritmo de regresión logística a los datos de entrenamiento:

    ```python
    # Inicializar el modelo de Regresión Logística
    logreg = LogisticRegression(max_iter=1000)

    # Ajustar el modelo a los datos de entrenamiento
    logreg.fit(X_train, y_train)

    # Predecir las probabilidades en el conjunto de prueba
    y_prob = logreg.predict_proba(X_test)[:, 1]
    ```

7. **Generar y visualizar la curva ROC:** Utiliza la curva ROC para evaluar el rendimiento del modelo:

    ```python
    # Calcular la curva ROC y el AUC
    fpr, tpr, thresholds = roc_curve(y_test, y_prob)
    auc = roc_auc_score(y_test, y_prob)

    # Visualizar la curva ROC
    plt.figure(figsize=(10, 8))
    plt.plot(fpr, tpr, label=f'ROC curve (AUC = {auc:.2f})')
    plt.plot([0, 1], [0, 1], linestyle='--', color='gray')
    plt.xlabel('Tasa de Falsos Positivos (FPR)')
    plt.ylabel('Tasa de Verdaderos Positivos (TPR)')
    plt.title('Curva ROC - Regresión Logística')
    plt.legend()
    plt.show()
    ```

    <details>
        <summary><b>✨Haz clic aquí para ver la imagen✨</b></summary>
        <div align="center">
            <img src="../Imagenes/Ejemplo_03_Imagen_02.png" alt="Curva ROC" width="50%">
        </div>
    </details>

    <br>

8. **Interpretación de los resultados de la Curva ROC y AUC**:

    - **Curva ROC:** Muestra el rendimiento del modelo para todos los umbrales posibles. Una curva más cercana a la esquina superior izquierda indica un mejor rendimiento.
    - **AUC (Área Bajo la Curva):** Es un valor entre 0 y 1 que mide la capacidad del modelo para distinguir entre clases. Un AUC de 0.5 indica un modelo que no es mejor que el azar, mientras que un AUC de 1.0 indica un modelo perfecto.

### 📉 **Interpretación de los resultados**

- **Curva ROC:** La curva ROC muestra la relación entre la tasa de verdaderos positivos y la tasa de falsos positivos para diferentes umbrales de decisión. Cuanto más se acerque la curva a la esquina superior izquierda, mejor será el rendimiento del modelo.
- **AUC (Área Bajo la Curva):** El AUC proporciona un solo número que resume el rendimiento del modelo. Un AUC más alto indica una mejor capacidad del modelo para discriminar entre clases. Por ejemplo, un AUC de 0.85 significa que hay un 85% de probabilidad de que el modelo clasifique correctamente una observación positiva sobre una negativa.

---

🏆 ¡Bien hecho! Ahora estás listo para evaluar tus modelos de clasificación utilizando la curva ROC y AUC. ¡Mucho éxito en tu análisis!

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Reto-03/Readme.md) ➡️
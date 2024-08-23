🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 05**](../Readme.md) ➡️ / 📝 `Ejemplo 04: Métodos de validación cruzada`


## 🎯 Objetivo 
El objetivo es comprender y aplicar técnicas de validación cruzada para evaluar la capacidad de generalización y rendimiento de los modelos predictivos, utilizando métodos como K-Fold Cross-Validation, Leave-One-Out Cross-Validation (LOOCV), y Stratified K-Fold Cross-Validation. También se busca aprender a implementar estos métodos de manera efectiva, asegurando que la evaluación del modelo sea robusta y representativa.

---

## 🚀 Comencemos
**La validación cruzada** es una técnica para evaluar el rendimiento y capacidad de generalización de un modelo predictivo, dividiendo los datos en subconjuntos para entrenar y probar el modelo en diferentes combinaciones. Esto ayuda a prevenir el overfitting y asegura un buen desempeño en datos no vistos.

**Métodos de validación cruzada:**

- **K-Fold Cross-Validation:** Divide el dataset en K partes. El modelo se entrena K veces, usando K-1 partes para entrenamiento y 1 para prueba. Los resultados se promedian para una estimación precisa.

- **Leave-One-Out Cross-Validation (LOOCV):** Un caso especial de K-Fold donde K es igual al número de muestras. Cada muestra se usa una vez como prueba, ofreciendo una evaluación muy precisa, pero con alto costo computacional.

- **Stratified K-Fold Cross-Validation:** Variante de K-Fold que mantiene la proporción original de clases en cada fold, ideal para problemas de clasificación con clases desbalanceadas.

---

### 🛠️ **Ejecución de técnicas de validación cruzada**
Antes de aplicar técnicas como `K-Fold`, `LOOCV`, y `Stratified K-Fold`, es crucial entender la necesidad de evaluar un modelo de múltiples formas. Dividir los datos en entrenamiento y prueba una sola vez puede no ser representativo debido a la variabilidad de los datos. La validación cruzada ofrece una evaluación más robusta al promediar resultados de diferentes divisiones, proporcionando una estimación más precisa del rendimiento del modelo.

Vamos a ejecutar `K-Fold`, `LOOCV`, y `Stratified K-Fold` utilizando el ejemplo del químico interesado en modelado y simulación [Ejemplo_03_04_Dataset_Quimico.csv](../../Datasets/S05/Ejemplo_03_04_Dataset_Quimico.csv)

1. **Pasos iniciales:** ¿Los recuerdas? Instalar (en caso de que no las tengamos) e importar las librerías, cargar y preparar el dataset. 

    ```python
    !pip install pandas scikit-learn
    ```
    ```python
    import pandas as pd
    from sklearn.model_selection import train_test_split

    # Cargar el dataset
    df = pd.read_csv('../Ejemplo_03_04_Dataset_Quimico.csv') # Cambiar la ruta del archivo si es necesario

    # Definir características (X) y la etiqueta objetivo (y)
    X = df.drop('Eficacia_Reaccion', axis=1)  # Características
    y = df['Eficacia_Reaccion']  # Etiqueta objetivo

    # Convertir las variables categóricas en variables dummy si es necesario
    X = pd.get_dummies(X, drop_first=True)
    ```

2. **K-Fold Cross-Validation:** Implementamos K-Fold Cross-Validation usando Scikit-learn.

    ```python
    from sklearn.model_selection import cross_val_score, KFold
    from sklearn.tree import DecisionTreeClassifier

    # Crear el modelo
    model = DecisionTreeClassifier(random_state=42)

    # Implementar K-Fold Cross-Validation
    kf = KFold(n_splits=5, shuffle=True, random_state=42)  # 5-Folds
    scores = cross_val_score(model, X, y, cv=kf, scoring='accuracy')

    # Mostrar los resultados
    print(f"K-Fold Cross-Validation Scores: {scores}")
    print(f"Promedio de las puntuaciones: {scores.mean():.2f}")
    ```
    - `KFold(n_splits=5)`: Divide los datos en 5 partes.
    - `cross_val_score`: Calcula la precisión del modelo en cada fold.
    - `scores.mean()`: Promedia los resultados para obtener una medida más robusta.

  <br>

3.  **Leave-One-Out Cross-Validation (LOOCV):** Implementamos LOOCV, que es más intensivo computacionalmente.
    ```python
    from sklearn.model_selection import LeaveOneOut

    # Crear el modelo
    model = DecisionTreeClassifier(random_state=42)

    # Implementar LOOCV
    loo = LeaveOneOut()
    scores = cross_val_score(model, X, y, cv=loo, scoring='accuracy')

    # Mostrar los resultados
    print(f"LOOCV Mean Score: {scores.mean():.2f}")
    ```
    - `LeaveOneOut()`: Deja una muestra fuera en cada iteración.
    - `cross_val_score`: Calcula la precisión para cada iteración y luego promedia los resultados.

  <br>

4.  **Stratified K-Fold Cross-Validation:** Implementamos Stratified K-Fold Cross-Validation para asegurar que cada fold tenga una distribución equilibrada de clases.

    ```python
    from sklearn.model_selection import StratifiedKFold

    # Crear el modelo
    model = DecisionTreeClassifier(random_state=42)

    # Implementar Stratified K-Fold Cross-Validation
    skf = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
    scores = cross_val_score(model, X, y, cv=skf, scoring='accuracy')

    # Mostrar los resultados
    print(f"Stratified K-Fold Cross-Validation Scores: {scores}")
    print(f"Promedio de las puntuaciones: {scores.mean():.2f}")
    ```
    - `StratifiedKFold(n_splits=5)`: Divide los datos en 5 partes, manteniendo la proporción de clases en cada fold.
    - `cross_val_score`: Calcula la precisión en cada fold y luego promedia los resultados.

    Al utilizar K-Fold, LOOCV, y Stratified K-Fold, obtienes una visión completa del rendimiento del modelo en diferentes escenarios, lo que te ayuda a elegir el mejor modelo para tus datos.

---

### 📉 **Interpretación de la distribución muestral**
Para evaluar los métodos de validación cruzada revisados es importante considerar varios criterios que te ayudarán a determinar cuál es el más adecuado para tu problema y cómo interpretar sus resultados.

<div align="center">
<h4>K-Fold Cross-Validation, criterios:</h4>
</div>

| Variabilidad de los Scores | Promedio de los Scores | Número de Folds (K) |
|----------------------------|------------------------|---------------------|
| Evalúa cómo varían los puntajes de precisión, recall, F1-score, etc., entre los diferentes folds. | El promedio de los puntajes te da una idea del rendimiento general del modelo. | Aumentar el número de folds generalmente da una estimación más precisa, pero a costa de más tiempo de cómputo. |
| **Baja variabilidad:** Indica que el modelo es estable y que su rendimiento no depende mucho de cómo se dividen los datos. | **Alto promedio:** Sugiere que el modelo es eficaz en general. | **K más alto (10 o más):** Proporciona una mejor estimación, pero aumenta el tiempo de procesamiento. |
| **Alta variabilidad:** Sugiere que el modelo puede estar sobreajustado (overfitting) o que los datos son ruidosos. | **Bajo promedio:** Indica que el modelo tiene dificultades para predecir correctamente. | **K bajo (5):** Reduce el tiempo de cómputo, pero puede dar una estimación menos estable. |

---

<div align="center">
<h4>Leave-One-Out Cross-Validation (LOOCV), criterios:</h4>
</div>

| Exactitud de la estimación                                                                 | Costo computacional                                                                 | Variabilidad en los Scores                                                                                     |
|--------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| LOOCV es útil cuando necesitas una estimación muy precisa del rendimiento del modelo porque utiliza casi todos los datos disponibles para entrenar en cada iteración. | LOOCV puede ser computacionalmente costoso, especialmente en datasets grandes, porque entrena y prueba el modelo tantas veces como muestras haya. | Dado que solo se deja una muestra fuera en cada iteración, el rendimiento puede fluctuar más si los datos son ruidosos o contienen outliers. |
| **Alta exactitud:** Buen método si el dataset es pequeño y cada muestra es valiosa.        | **Apropiado para datasets pequeños:** Se recomienda cuando el dataset no es muy grande |                                                                                                                |
| **Bajo rendimiento:** Puede ocurrir si el modelo es muy sensible a pequeñas variaciones en los datos. | **Costoso para datasets grandes:** Puede ser ineficiente y lento                                                  |                                                                                                                |

---

<div align="center">
<h4>Stratified K-Fold Cross-Validation, criterios:</h4>
</div>

| Representatividad de las clases                                                                 | Consistencia de los Scores                                                                 | Variabilidad en los Scores                                                                                                            |
|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| Este método es ideal para problemas de clasificación con clases desbalanceadas, ya que asegura que cada fold tenga una proporción similar de cada clase. | Evaluar cómo de consistentes son los puntajes entre los folds. En un problema de clasificación desbalanceado, este método debería proporcionar puntajes más consistentes. | Al igual que en K-Fold, el promedio de los scores proporciona una estimación del rendimiento general del modelo, pero con la ventaja de que las clases están equilibradas en cada fold. |
| **Buena representatividad:** Si las clases están desbalanceadas, este método es más confiable para evaluar el rendimiento del modelo. | **Alta consistencia:** Indica que el modelo maneja bien las clases desbalanceadas.                                                 |                                                                                                                                      |
| **Mala representatividad:** Si no se usa este método en problemas desbalanceados, los resultados pueden ser engañosos.              | **Baja consistencia:** Sugiere que el modelo podría estar sesgado hacia la clase mayoritaria.                                       |                                                                                                                                      |

---

**En nuestro ejemplo, los resultados fueron:**

**• K-Fold Cross-Validation**  
- 📝 **Scores:** [0.5, 0.25, 0.6, 0.7, 0.45]  
  Las precisiones varían significativamente entre los 5 folds, con un mínimo de 0.25 y un máximo de 0.70.
- 📊 **Promedio de las puntuaciones:** 0.50  
  El modelo acierta en un 50% de las veces, sugiriendo un rendimiento mediocre y posible sensibilidad a la división de los datos, lo que podría indicar overfitting o underfitting.

**• LOOCV**  
- 📉 **Mean Score:** 0.45  
  El modelo acertó en el 45% de los casos, ligeramente inferior al promedio de K-Fold, lo que sugiere dificultades para generalizar.

**• Stratified K-Fold Cross-Validation**  
- 📊 **Scores:** [0.45, 0.4, 0.55, 0.55, 0.55]  
  Los puntajes son más consistentes, oscilando entre 0.40 y 0.55.
- 📈 **Promedio de las puntuaciones:** 0.50  
  Al igual que con K-Fold, el promedio es 0.50, mostrando rendimiento promedio cuando las clases están equilibradas en cada fold.

**🔍 En resumen…**  
Tenemos un rendimiento global **Moderado/Bajo**, con una precisión promedio alrededor del 50% en todos los métodos de validación cruzada, lo que indica dificultades para hacer predicciones precisas y confiables.

---
### 💡 **¿Sabías que?...**

El **overfitting** ocurre cuando un modelo se ajusta demasiado a los datos de entrenamiento, capturando incluso el ruido y las irregularidades, lo que lo hace menos efectivo para predecir nuevos datos. Esto es como aprenderse un libro de memoria en lugar de entender su contenido. 

Por otro lado, el **underfitting** sucede cuando un modelo es demasiado simple para captar los patrones importantes de los datos, fallando tanto en los datos de entrenamiento como en los nuevos. Es como estudiar solo los resúmenes de un libro y no entenderlo realmente.

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../../Sesion-06/Readme.md) ➡️
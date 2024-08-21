🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 05**](../Readme.md) ➡️ / 📝 `Ejemplo 03: Técnicas de evaluación de modelos`


## 🎯 Objetivo 
Comprender y aplicar técnicas de evaluación de modelos predictivos usando métricas como precisión, recall y F1-score. También aprenderás a dividir datos en conjuntos de entrenamiento y prueba para evaluar el modelo de manera justa y mejorar la toma de decisiones basada en datos.

---

## 🚀 Comencemos

Antes de evaluar modelos, es crucial entender la división de datos:

- **Un dataset de entrenamiento** es un subconjunto de datos que se utiliza para entrenar un modelo predictivo, es decir, el modelo aprende de estos datos para identificar patrones y relaciones entre las variables.  Se utiliza para ajustar el modelo y aprender de los datos.

- **Un dataset de prueba** es otro subconjunto que se utiliza para evaluar el rendimiento del modelo una vez que ha sido entrenado. Este conjunto de prueba contiene datos que el modelo no ha visto antes, permitiendo medir su capacidad de generalización y asegurando que las predicciones no están sesgadas hacia los datos de entrenamiento. Se utiliza para evaluar el modelo y comprobar su rendimiento en datos no vistos.


Dividir los datos en entrenamiento y prueba asegura que el modelo generalice correctamente, evitando el sobreajuste y proporcionando una evaluación más realista de su rendimiento en situaciones reales. Evaluar con un conjunto de prueba independiente ayuda a identificar problemas y medir cómo se comportará el modelo en la práctica.

---

### 🛠️ **Creación de un dataset de entrenamiento y prueba**
Supongamos que eres un químico interesado en modelado y simulación, y tienes un dataset con diferentes compuestos químicos y su eficacia en una reacción particular. Vamos a dividir este dataset en conjuntos de entrenamiento y prueba para entrenar un modelo predictivo y luego evaluar su rendimiento. Utilizaremos el dataset [Ejemplo_03_04_Dataset_Quimico.csv](../../Datasets/S05/Ejemplo_03_04_Dataset_Quimico.csv) 

1. **Dividir el dataset en entrenamiento y prueba**

    ```python
    from sklearn.model_selection import train_test_split
    import pandas as pd

    # Cargar el dataset
    df = pd.read_csv('../Ejemplo_03_04_Dataset_Quimico.csv') # Cambiar la ruta del archivo si es necesario

    # Definir características (X) y la etiqueta objetivo (y)
    X = df.drop('Eficacia_Reaccion', axis=1)  # Características
    y = df['Eficacia_Reaccion']  # Etiqueta objetivo

    # Dividir los datos en conjunto de entrenamiento (70%) y prueba (30%)
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42, stratify=y)

    # Mostrar la forma de los conjuntos para confirmar la división
    print(f"Conjunto de Entrenamiento: {X_train.shape}, {y_train.shape}")
    print(f"Conjunto de Prueba: {X_test.shape}, {y_test.shape}")
    ```

    - **Cargar el dataset**: El dataset simulado se carga desde un archivo CSV.
    - Definir características y etiqueta: Se separan las columnas del dataset en X (las características) y y (la etiqueta o el objetivo que queremos predecir).
    - **Dividir el dataset**: Usamos train_test_split de scikit-learn para dividir el dataset en un conjunto de entrenamiento y otro de prueba, manteniendo el 70% de los datos para entrenar el modelo y el 30% para evaluarlo. La opción stratify=y asegura que se mantenga la proporción original de la etiqueta en ambos conjuntos.
    - **Confirmar la división**: Finalmente, se imprimen las formas de los conjuntos de entrenamiento y prueba para confirmar que la división se realizó correctamente.

---

🌟 **Técnicas de evaluación de modelos predictivos:** 
Las técnicas y métricas de evaluación son herramientas clave para medir el rendimiento de un modelo predictivo. Entre las métricas más comunes están:

- 🔍 **Precisión:** Proporción de predicciones positivas correctas.
- 🎯 **Recall:** Capacidad del modelo para identificar todas las instancias positivas.
- ⚖️ **F1-Score:** Media armónica entre precisión y recall, balanceando ambas métricas.

La elección de técnicas de evaluación depende del tipo de problema (clasificación, regresión, clustering, etc.). En el ejemplo que revisaremos, usaremos un **Árbol de Decisión**, un modelo que se estructura como un árbol donde cada nodo representa una pregunta sobre una característica del dataset. No te preocupes por entender el árbol de decisión ahora, nos centraremos en la evaluación.

---

### 🛠️ **Aplicación de técnicas de evaluación de modelos predictivos**
Vamos a implementar estas métricas utilizando el dataset `Ejemplo_03_04_Dataset_Quimico` que usamos anteriormente. Entrenaremos un modelo y luego mediremos su rendimiento usando precisión, recall y F1-score.

1. **Cargar y preparar el dataset:** Como siempre, asegúrate de tener tus bibliotecas importadas y tu dataset cargado correctamente. Ahora también dividiremos los datos en conjunto de entrenamiento `(70%)` y prueba `(30%)` como lo aprendimos anteriormente.

    ```python
    import pandas as pd
    from sklearn.model_selection import train_test_split
    from sklearn.tree import DecisionTreeClassifier
    from sklearn.metrics import precision_score, recall_score, f1_score
    ```
    Utilizaremos:
    - pandas para manejar y procesar datos estructurados.
    - train_test_split de Scikit-learn para dividir datos en conjuntos de entrenamiento y prueba.
    - DecisionTreeClassifier de Scikit-learn para crear y entrenar modelos de árboles de decisión.
    - precision_score, recall_score, y f1_score de Scikit-learn para evaluar el rendimiento de modelos de clasificación.

        
    ```python
    # Cargar el dataset
    df = pd.read_csv('../Ejemplo_03_04_Dataset_Quimico .csv') # Cambiar la ruta del archivo si es necesario

    # Definir características (X) y la etiqueta objetivo (y)
    X = df.drop('Eficacia_Reaccion', axis=1) # Características
    y = df['Eficacia_Reaccion'] # Etiqueta objetivo

    # Dividir los datos en conjunto de entrenamiento (70%) y prueba (30%)
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42, stratify=y)
    ```
2.  **Entrenar un modelo:** Usaremos un árbol de decisión como modelo, aunque puedes experimentar con otros modelos también.

    ```python
    # Crear y entrenar el modelo
    model = DecisionTreeClassifier(random_state=42)
    model.fit(X_train, y_train)
    ```
    - **Crear y entrenar un modelo:** Creamos un modelo de árbol de decisión y lo entrenamos con los datos de entrenamiento.

3.  **Realizar predicciones y evaluar el modelo:** Después de entrenar el modelo, realizaremos predicciones en el conjunto de prueba y luego calcularemos las métricas de evaluación.
    ```python
    # Realizar predicciones en el conjunto de prueba
    y_pred = model.predict(X_test)

    # Calcular las métricas
    precision = precision_score(y_test, y_pred)
    recall = recall_score(y_test, y_pred)
    f1 = f1_score(y_test, y_pred)

    # Mostrar los resultados
    print(f'Precisión: {precision:.2f}')
    print(f'Recall: {recall:.2f}')
    print(f'F1-Score: {f1:.2f}')
    ```
    Dependiendo de los resultados, podrías decidir ajustar el modelo, cambiar de algoritmo o recopilar más datos para mejorar el rendimiento. Este proceso te ayuda a crear un modelo que no solo funcione bien en datos conocidos, sino que también sea capaz de hacer predicciones precisas en nuevos escenarios.

---

### 📉 **Interpretación de la distribución muestral**
Para hacer la interpretación a nuestro resultados, los niveles de aceptación o criterios comunes para las métricas de Precisión, Recall y F1-score son:


| Precisión (Precision) | Recall (Sensibilidad) | F1-Score |
|----------------|-----------------------|-----------------------|
| **> 0.90 (90%):** Alta precisión. El modelo rara vez comete falsos positivos. | **> 0.90 (90%):** Alto recall. El modelo casi siempre captura los verdaderos positivos. | **> 0.90 (90%):** Excelente balance entre precisión y recall. El modelo es altamente confiable en general. |
| **0.80 - 0.90 (80% - 90%):** Buena precisión. El modelo es confiable, pero todavía hay algunos falsos positivos. | **0.80 - 0.90 (80% - 90%):** Buen recall. El modelo identifica correctamente la mayoría de los casos positivos. | **0.80 - 0.90 (80% - 90%):** Buen balance, el modelo maneja bien tanto la precisión como el recall. |
| **0.60 - 0.79 (60% - 79%):** Precisión aceptable, pero puede haber un número significativo de falsos positivos. | **0.60 - 0.79 (60% - 79%):** Recall aceptable, pero podría estar perdiendo un número considerable de verdaderos positivos. | **0.60 - 0.79 (60% - 79%):** F1-score aceptable, pero el modelo puede necesitar ajustes para mejorar en precisión o recall. |
| **< 0.60 (60%):** Baja precisión. El modelo a menudo predice incorrectamente como positivo algo que no lo es. | **< 0.60 (60%):** Bajo recall. El modelo no logra identificar muchos de los casos positivos. | **< 0.60 (60%):** Bajo F1-score. El modelo probablemente necesita mejoras significativas. |


🔄 **Los valores pueden variar según el contexto, pero los criterios mencionados son un buen punto de partida.**

Al ejecutar el código, obtuvimos:

- 🎯 **Precisión: 0.50**  
El modelo tiene un 50% de precisión en predicciones positivas, lo que indica una alta cantidad de falsos positivos. En la mitad de los casos, predice éxitos que en realidad no lo son.

- 🔍 **Recall: 0.58**  
El modelo identifica correctamente solo el 58% de los éxitos reales, perdiendo el 42% de las reacciones exitosas (falsos negativos).

- ⚖️ **F1-Score: 0.54**  
Este valor refleja un desequilibrio entre precisión y recall, señalando un rendimiento general bajo.

📉 **En resumen, el modelo tiene problemas para hacer predicciones precisas y completas, con errores significativos tanto en falsos positivos como en falsos negativos.**

💡 **¿Qué podemos hacer?**

1. 🛠️ **Mejorar la calidad de los datos:** Revisar outliers, variables irrelevantes o características que necesiten transformación.
2. ➕ **Recopilar más datos:** Si el dataset es pequeño, más datos podrían ayudar al modelo a aprender mejor.

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Reto-02/Readme.md) ➡️
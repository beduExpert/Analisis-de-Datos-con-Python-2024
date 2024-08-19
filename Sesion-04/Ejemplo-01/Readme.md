🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 04**](../Readme.md) ➡️ / 📝 `Ejemplo 01: Coeficiente de correlación de Pearson`

## 🎯 Objetivo

Comprender y aplicar el coeficiente de correlación de Pearson para evaluar y determinar la fuerza y dirección de la relación lineal entre variables cuantitativas, interpretando los resultados y considerando la visualización de datos y el impacto de valores atípicos.

---

## 🚀 Comencemos

El coeficiente de correlación de Pearson busca cuantificar la relación lineal entre dos variables cuantitativas. Valorar numéricamente esta correlación puede ser complejo, ya que no es sencillo determinar qué par de variables está más correlacionado. El objetivo es asignar un valor específico a esta relación, facilitando así la comparación entre diferentes pares de variables. Este índice varía entre `-1` y `+1`, incluyendo ambos extremos.

---
### 🛠️ **Calculo del coeficiente de correlación de Pearson**

Antes de realizar el cálculo hay que considerar lo siguiente.

**Condiciones:**

- La relación que se quiere estudiar es de tipo lineal (de lo contrario, el coeficiente de Pearson no la puede detectar).
- Las dos variables deben de ser numéricas.
- Normalidad: ambas variables se tienen que distribuir de forma normal. En la práctica, se suele considerar válido aun cuando se alejan moderadamente de la normalidad.
- Homocedasticidad: la varianza de Y debe ser constante a lo largo de la variable `X`. Esto se puede contrastar si en un scatterplot los valores de `Y` mantienen la misma dispersión en las distintas zonas de la variable `X`.


En este ejemplo, aprenderás a calcular el coeficiente de correlación de Pearson utilizando Python y la biblioteca scipy, aplicado a un caso del campo de la psicología. Analizaremos la relación entre el nivel de estrés de los pacientes y la cantidad de horas de sueño que reportan.

Aplica los siguientes pasos:

1. **Instalación de las bibliotecas necesarias:** Asegúrate de tener instaladas las bibliotecas necesarias. Si aún no las tienes, puedes instalarlas utilizando el siguiente comando:

    ```python
    !pip install numpy pandas scipy
    ```

2. **Importa las bibliotecas necesarias:** Importa las bibliotecas que vas a utilizar en tu análisis.
   
    ```python
    from scipy.stats import pearsonr
    import numpy as np
    import pandas as pd
    ```
    - `numpy` y `pandas` para el manejo de datos.
    - `pearsonr` de `scipy.stats` para calcular el coeficiente de correlación de Pearson.


3. **Creación del conjunto de datos:** Imagina que estás investigando cómo el nivel de estrés afecta la cantidad de horas de sueño en un grupo de pacientes. Crearemos un conjunto de datos ficticio para simular esta situación.

    ```python
    # Crear un dicionario con los datos de nivel de estrés y horas de sueño.
    data = {
        'Nivel_de_estres': [7, 6, 8, 5, 9, 4, 7, 3, 10, 2],
        'Horas_de_sueño': [5, 6, 4, 7, 3, 8, 5, 9, 2, 10]
    }

    # Crear un DataFrame con los datos.
    df = pd.DataFrame(data)

    # Mostrar el DataFrame.
    df.head()
    ```
    Este DataFrame contiene dos columnas:
    - `Nivel_de_estres:` Representa el nivel de estrés auto-reportado por los pacientes en una escala de 1 a 10.
    - `Horas_de_sueño:` Muestra la cantidad de horas de sueño que los pacientes reportan.

4. **Cálculo del coeficiente de correlación de Pearson:** Utiliza la función `pearsonr` de `scipy.stats` para calcular el coeficiente de correlación de Pearson.

    ```python
    # Calcular el coeficiente de correlación de Pearson
    pearson_corr, _ = pearsonr(df['Nivel_de_estres'], df['Horas_de_sueño'])
    print(f"Coeficiente de correlación de Pearson: {pearson_corr}")
    ```
    
   ```plaintext
   🛍️ Coeficiente de correlación de Pearson: -0.9999999999999999
   ```
---

### 📉 **Interpretación del coeficiente de correlación de Pearson**
El coeficiente de correlación de Pearson varía entre `-1` y `1`. En este contexto:

- Un valor cercano a `1` indicaría una correlación positiva, lo que implicaría que un mayor nivel de estrés está asociado con más horas de sueño (lo cual sería poco intuitivo en este caso).
- Un valor cercano a `-1` indicaría una correlación negativa, lo que sugeriría que un mayor nivel de estrés está asociado con menos horas de sueño, lo que sería más consistente con lo esperado en psicología.
- Un valor cercano a `0` indicaría que no hay una relación lineal entre el nivel de estrés y las horas de sueño.


En este caso, probablemente encuentres un coeficiente de correlación negativo, lo que indicaría que a medida que aumenta el nivel de estrés, disminuyen las horas de sueño. Sin embargo, el valor exacto del coeficiente de correlación de Pearson dependerá de los datos que utilices.

---

### 💡 **¿Sabías que?...**

El coeficiente de correlación de Pearson: 
- Es independiente de las escalas en las que se midan las variables.
- No varía si se aplican transformaciones a las variables.
- No tiene en consideración que las variables sean dependientes o independientes.
- El coeficiente de correlación de Pearson no equivale a la pendiente de la recta de regresión.
- Es sensible a outliers, por lo que se recomienda, en caso de poder justificarlos, excluirlos antes de realizar el cálculo.

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Ejemplo-02/Readme.md) ➡️
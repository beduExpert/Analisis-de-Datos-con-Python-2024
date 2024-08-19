🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 04**](../Readme.md) ➡️ / 📝 `Ejemplo 02: Matriz de correlaciones y mapa de calor`

## 🎯 Objetivo

El objetivo es analizar la relación entre múltiples variables cuantitativas, como el nivel de estrés y la cantidad de horas de sueño reportadas por los pacientes, utilizando una matriz de correlaciones y un mapa de calor. Estos métodos te permiten visualizar fácilmente cómo se correlacionan las variables entre sí y detectar patrones de relación que pueden no ser evidentes a simple vista.

---

## 🚀 Comencemos

La matriz de correlaciones es una tabla que muestra los coeficientes de correlación entre varias variables. Cada celda de la matriz contiene el valor de correlación entre dos variables diferentes, facilitando la comparación y análisis de múltiples relaciones al mismo tiempo. A su vez, el mapa de calor (también llamado heatmap) es una representación gráfica de la matriz de correlaciones. Los valores de correlación se representan mediante colores, donde el color indica la fuerza y la dirección de la correlación. Este tipo de visualización es útil para identificar rápidamente relaciones fuertes, débiles, positivas o negativas entre las variables.

---

### 🛠️ **Creación de una matriz de correlaciones y un mapa de calor**

Aplica los siguientes pasos:

1. **Instalación de las bibliotecas necesarias:** Primero, asegúrate de tener instaladas las bibliotecas necesarias. Si no las tienes, instala seaborn, una biblioteca que facilita la creación de mapas de calor, además de numpy, pandas, y matplotlib:
    
    ```python
    !pip install numpy pandas seaborn matplotlib
    ```
2. **Importación de las bibliotecas:** Importa las bibliotecas que vas a utilizar:
    
    ```python
    import numpy as np
    import pandas as pd
    import matplotlib.pyplot as plt
    import seaborn as sns
    ```
    - `numpy` y `pandas` para el manejo de datos.
    - `matplotlib ` y `seaborn ` para la visualización de los datos, incluyendo los mapas de calor.

3. **Creación del conjunto de datos:** Utiliza un conjunto de datos que represente la relación entre el nivel de estrés y las horas de sueño, junto con cualquier otra variable que desees analizar:

    ```python
    # Crear un diccionario con los datos de nivel de estrés, horas de sueño y horas de ejercicio.
    data = {
        'Nivel_de_estres': [7, 6, 8, 5, 9, 4, 7, 3, 10, 2],
        'Horas_de_sueño': [5, 6, 4, 7, 3, 8, 5, 9, 2, 10],
        'Horas_de_ejercicio': [1, 2, 1, 3, 0, 4, 1, 3, 0, 5]
    }

    # Crear un DataFrame con los datos.
    df = pd.DataFrame(data)

    # Mostrar el DataFrame.
    df.head()
    ```


4. **Cálculo de la matriz de correlaciones:** Calcula la matriz de correlaciones entre las variables del dataframe:
    ```python
    # Calcular la matriz de correlaciones
    correlation_matrix = df.corr()

    # Mostrar la matriz de correlaciones
    correlation_matrix.head()
    ```
    - `df.corr()`: calcula el coeficiente de correlación de Pearson entre todas las variables del dataframe. El resultado es una matriz donde cada celda muestra la correlación entre dos variables, con valores que van de -1 a 1.


    |                 | Nivel_de_estres | Horas_de_sueño | Horas_de_ejercicio |
    |-----------------|-----------------|----------------|--------------------|
    | Nivel_de_estres | 1.000000        | -1.000000      | -0.954967          |
    | Horas_de_sueño  | -1.000000       | 1.000000       | 0.954967           |
    | Horas_de_ejercicio | -0.954967    | 0.954967       | 1.000000           |

5. **Creación de un mapa de calor:** Ahora, visualiza la matriz de correlaciones utilizando un mapa de calor:
    ```python
    # Crear el mapa de calor
    plt.figure(figsize=(8, 6))
    sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', linewidths=0.5)

    # Personalizar el gráfico
    plt.title('Mapa de Calor de la Matriz de Correlaciones')
    plt.show()
    ```

    - sns.heatmap() genera el mapa de calor basado en la matriz de correlaciones.
        - `annot=True` muestra los valores de correlación en cada celda.
        - `cmap='coolwarm'` define el esquema de colores a utilizar.
        - `linewidths=0.5` agrega líneas entre las celdas para mejorar la visualización.
    - plt.figure(figsize=(8, 6)) ajusta el tamaño del mapa de calor para que sea más legible.


---
### 📉 **Interpretación del mapa de calor**

<div align="center">
    <img src="../Imagenes/Matriz_Ccp.png" alt="Mapa de calor" width="40%">
</div>

El mapa de calor te permite ver rápidamente como se relacionan las variables entre sí:
- Los colores mas cercanos al rojo indican correlaciones positivas fuertes.
- Los colores mas cercanos al azul indican correlaciones negativas fuertes
- Los colores cercanos al blanco o neutros indican poca o ninguna correlación.

Por ejemplo, si en el mapa de calor ves que Nivel_de_estres tiene un color rojo oscuro con respecto a Horas_de_sueño, esto indicaría que a medida que aumenta el nivel de estrés, las horas de sueño disminuyen, sugiriendo una fuerte correlación negativa.


---

### 💡 **¿Sabías que?...**

Es posible agregar un ligero formato de colores a la tabla de correlaciones para hacerla más fácil de leer. Para ello, puedes utilizar el siguiente código:

```python
# Formatear la matriz de correlaciones con colores
correlation_matrix.style.background_gradient(cmap='coolwarm')
```

1. **`style`**: El método `style` es una función de Pandas que te permite aplicar estilos personalizados a los dataframes. No cambia los datos, solo afecta cómo se muestran.

2. **`background_gradient(cmap='coolwarm')`**: Esta función aplica un gradiente de color al fondo de las celdas en función de los valores de la matriz. El parámetro `cmap='coolwarm'` especifica que se utilice la paleta de colores "coolwarm", que va de colores fríos (generalmente azules) para valores bajos a colores cálidos (generalmente rojos) para valores altos.

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Ejemplo-03/Readme.md) ➡️
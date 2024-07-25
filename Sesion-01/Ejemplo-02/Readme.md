🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 01**](../Readme.md) ➡️ / 📝 `Ejemplo 02: Valores atípicos y estimados de variabilidad`

## 🎯 Objetivo

Entender y aplicar técnicas para identificar valores atípicos y calcular estimados de variabilidad, como el rango, la varianza y la desviación estándar, utilizando datos estructurados en Python.

---

## 🚀 Comencemos

En ocasiones, los datos pueden contener valores atípicos que afectan la interpretación de los resultados, por ejemplo la distribución de riqueza en un país y los diferentes estratos sociales, por lo que es importante identificarlos y analizarlos adecuadamente. Así mismo también es importante entender la variabilidad de los datos y que tan dispersos están los datos en torno a la media o promedio de los datos.

---

## 📊 **Valores atípicos y estimados de variabilidad** 📈

### **Valores atípicos (outliers)**

Los valores atípicos son observaciones que se encuentran significativamente alejadas de la mayoría de los datos en un conjunto. Pueden indicar errores de medición, datos anómalos o eventos inusuales que pueden afectar considerablemente los resultados del análisis.

#### 🛠️ **¿Cómo identificamos los valores atípicos?**

- **Visualización de datos**: Diagramas de caja y bigotes, histogramas, gráficos de dispersión.
- **Métodos estadísticos**: Criterios basados en la desviación estándar, percentiles, rango intercuartílico.
- **Modelos de aprendizaje automático**: Algoritmos de detección de anomalías.

#### 🛠️**Causas de valores atípicos**

- **Errores en la recopilación de datos**: Errores humanos o de instrumentos.
- **Variabilidad natural**: Diferencias naturales en la población o muestras.
- **Efectos transitorios**: Eventos temporales que afectan los datos.

---

### 📐 **Estimados de variabilidad**

Primero comenzaremos por calcular la varianza y la desviación estándar de la tarifa de los pasajeros en el Titanic, y luego calcularemos el rango de la edad de los pasajeros.

```python
# Importar librerías
import pandas as pd

# Cargar el dataset
df = pd.read_csv('../../Datasets/Titanic_Dataset.csv') # Modifica la ruta de acuerdo a tu entorno de trabajo

# Mostrar las primeras filas del dataset
df.head()
```

Los estimados de variabilidad miden la dispersión, variabilidad o separación de los datos en un conjunto. Algunos de los estimados más comunes son la varianza y la desviación estándar.

#### 📊 **Varianza**

La varianza mide la dispersión de los datos respecto a la media, elevando al cuadrado las desviaciones.
```python
# Calcular la varianza de la tarifa
varianza_fare = df['Fare'].var()
print(f'La varianza de la tarifa de los pasajeros en el Titanic es: {varianza_fare:,.2f}')

# Nota: Este valor representa el valor de tarifa elevado al cuadrado, por lo que no tiene unidades monetarias.
```

#### 📉 **Desviación estándar**

La desviación estándar es la raíz cuadrada de la varianza y proporciona una medida de dispersión en las mismas unidades que los datos originales.

```python
# Calcular la desviación estándar de la tarifa
desviacion_estandar_fare = df['Fare'].std()
print(f'La desviación estándar de la tarifa de los pasajeros en el Titanic es: ${desviacion_estandar_fare:,.2f}')
```

<!-- Rango -->
#### 📊 **Rango**
El rango es una medida de dispersión que representa la diferencia entre el valor máximo y el valor mínimo de un conjunto de datos.

```python
# Calcular el rango de la edad
edad_max = df['Age'].max()
edad_min = df['Age'].min()
rango_edad = edad_max - edad_min
print(f'El rango de la edad de los pasajeros en el Titanic es: {rango_edad}')
```

<!-- Interpretación de los datos -->
**Interpretación de los datos:**

- **Varianza**: La varianza de la tarifa de los pasajeros en el Titanic es $\$3,125.66$. Esto indica que las tarifas pagadas por los pasajeros varían significativamente alrededor de la media. La alta varianza sugiere que hay una gran variabilidad en las tarifas pagadas, con algunas tarifas muy bajas y otras muy altas.

- **Desviación Estándar**: La desviación estándar de la tarifa es $\$55.91$. Esto significa que, en promedio, las tarifas de los pasajeros se desvían en $\$55.91$ unidades monetarias de la media. Una desviación estándar alta indica que las tarifas están muy dispersas respecto a la media, podría decirse la mayoría de las tarifas pagadas se encuentran en un rango de $\$55.91$ de la media.

- **Rango**: El rango de la edad de los pasajeros en el Titanic es de $79.58$. Esto indica que la edad de los pasajeros varía en un rango de $79.58$ años, desde $0.42$ años hasta $80$ años.

---

### 💡 **¿Sabías que?...**

La **media truncada** es un estimado de locación más robusto que el promedio y la mediana. Esto significa que es menos sensible a valores atípicos. La media truncada se obtiene de la siguiente manera:

1. **Ordenar**: Primero, ordena tu conjunto de datos de manera ascendente.
2. **Determinar el porcentaje a truncar**: Decide qué porcentaje de tus datos vas a truncar. Los valores más comunes suelen variar entre 5% y 25%.
3. **Truncar datos**: Divide el porcentaje acordado entre dos y elimina esa fracción de tus datos del inicio y del final de tu secuencia. Por ejemplo, si decides truncar un 5%, elimina el 2.5% de tus datos del inicio y el otro 2.5% del final de tu secuencia.
4. **Calcular la media**: Obtén el promedio de los valores restantes.

Afortunadamente, no tenemos que hacer esto manualmente. La librería `scipy` ofrece un método para obtener la media truncada fácilmente:

```python
from scipy import stats
import pandas as pd

# Eliminar valores NaN en la columna 'Age'
edad_sin_nan = df['Age'].dropna()

# Calcular la media truncada
media_truncada_edad = stats.trim_mean(edad_sin_nan, 0.05)
print(f'La media truncada de la edad de los pasajeros en el Titanic es: {media_truncada_edad:.2f}')
```

**Salida esperada**:

```plaintext
La media truncada de la edad de los pasajeros en el Titanic es: 30.02
```
---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Reto-02/Readme.md) ➡️
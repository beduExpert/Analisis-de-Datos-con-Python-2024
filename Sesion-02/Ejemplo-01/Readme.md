🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 02**](../Readme.md) ➡️ / 📝 `Ejemplo 01: Creación y análisis de tablas de frecuencias`

## 🎯 Objetivo

Entender y aplicar las tablas de frecuencias para resumir datos categóricos o discretos, construyendo tablas mediante la organización de datos en categorías, el conteo de frecuencias y su representación estructurada. Además de interpretar los resultados, identificando patrones y tendencias como la moda y la distribución general de la información.

---

## 🚀 Comencemos

Las tablas de frecuencias son una forma de organizar y resumir datos cuantitativos o cualitativos en intervalos o categorías, y nos permiten entender la distribución de los datos y la frecuencia con la que aparecen en cada categoría, por ejemplo, la distribución de edades en una población de acuerdo a un rango de edades en particular.

---

### 📚 **Definición y conceptos**

Las tablas de frecuencia generalmente utilizan ciertos términos para describir los datos:

| **Término**                            | **Descripción**                                            |
|----------------------------------------|------------------------------------------------------------|
| **Intervalo de clase**                 | Rango de valores agrupados en una clase.                   |
| **Marca de clase**                     | Valor central de cada intervalo de clase.                  |
| **Frecuencia absoluta (fi)**           | Conteo total de ocurrencias por cada clase.                |
| **Frecuencia absoluta acumulada (Fi)** | Suma acumulada de frecuencias absolutas hasta cierta clase.|
| **Frecuencia relativa (fi/n)**         | Proporción de ocurrencias respecto al total de datos.      |
| **Frecuencia relativa acumulada (Fi/n)**| Suma acumulada de frecuencias relativas.                  |



---

### 🛠️ **Construcción de tabla de frecuencias**

Para construir una tabla de frecuencias, se deben considerar dos aspectos importantes:

1. **Valores numéricos:** Al trabajar con datos numéricos, es posible agruparlos en intervalos y marcas de clase para representar el rango de valores, posteriormente se realiza el conteo de frecuencias absolutas y relativas.

2. **Datos categóricos:** En el caso de datos categóricos, se agrupan en categorías y se realiza el conteo de frecuencias absolutas y relativas.

📂 **Carga el dataset**: Vamos a trabajar con el archivo [Laptops_Dataset.csv](../../Datasets/Laptops_Dataset.csv), con el fin de realizar dos ejemplos en diferentes columnas generando los pasos necesarios, para datos numéricos y categóricos.

1. **Datos numéricos**: Vamos a trabajar con la columna `price` del dataset, para ello, vamos a realizar los siguientes pasos:

```python
import pandas as pd

# 1.- Cargar el dataset
df = pd.read_csv('../../Datasets/Laptops_Dataset.csv') # Modifica la ruta de acuerdo a tu entorno de trabajo

# 2.- Determinar el Rango de los datos.
rango = df['price'].max() - df['price'].min()

# 3.- Determinar el número de clases.
n_clases = 1 + 3.322 * (df['price'].count() ** (1/3)) # Fórmula de Sturges.

# 4.- Determinar la amplitud o tamaño de las clases.
amplitud = rango / n_clases

# 5.- Definir los limites de los intervalos de clase.
limites = [df['price'].min() + i * amplitud for i in range(int(n_clases) + 1)]

# 6.- Definir las marcas de clase (puntos medios).
marcas = [(limites[i] + limites[i + 1]) / 2 for i in range(int(n_clases))]

# 7.- Crear la tabla de frecuencias con datos numéricos para la columna 'price'.
tabla_frecuencias_num = pd.DataFrame({
    'Intervalo_de_clase': [f'({round(limites[i], 2)} - {round(limites[i + 1], 2)}]' for i in range(int(n_clases))],
    'Marca_de_clase': [round(marcas[i], 2) for i in range(int(n_clases))],
    'Frecuencia_absoluta': [((df['price'] >= limites[i]) & (df['price'] < limites[i + 1])).sum() for i in range(int(n_clases))],
    'Frecuencia_relativa': [((df['price'] >= limites[i]) & (df['price'] < limites[i + 1])).sum() / df['price'].count() for i in range(int(n_clases))]
})

# 8.- Mostrar la tabla de frecuencias.
tabla_frecuencias_num.head().sort_values(by='Frecuencia_absoluta', ascending=False)
```

2. **Datos categóricos**: Vamos a trabajar con la columna `brand` del dataset, para ello, vamos a realizar los siguientes pasos:

```python
# Crear la tabla de frecuencias con datos categóricos para la columna 'brand'.
tabla_frecuencias_cat = pd.DataFrame({
    'Categoría': df['brand'].unique(),
    'Frecuencia_absoluta': [df['brand'].value_counts()[i] for i in range(df['brand'].nunique())],
    'Frecuencia_relativa': [df['brand'].value_counts(normalize=True)[i] for i in range(df['brand'].nunique())]
})

# Mostrar la tabla de frecuencias.
tabla_frecuencias_cat.head().sort_values(by='Frecuencia_absoluta', ascending=False)
```

---

### 🎨 **Interpretación de las tablas de frecuencia**

Una vez construida las tablas de frecuencias, es importante interpretar los resultados obtenidos, para ello, se pueden realizar las siguientes acciones:

1. **Identificar la moda:** La moda es el valor que más se repite en un conjunto de datos, y se puede identificar en la tabla de frecuencias como la clase con mayor frecuencia absoluta.

```python
# Localizamos la moda de la frecuencias absoluta, para los datos numéricos.
moda_num = tabla_frecuencias_num.loc[tabla_frecuencias_num['Frecuencia_absoluta'] == tabla_frecuencias_num['Frecuencia_absoluta'].max()]
moda_num.head()
```

```python
# Localizamos la moda de la frecuencias absoluta, para los datos categóricos.
moda_cat = tabla_frecuencias_cat.loc[tabla_frecuencias_cat['Frecuencia_absoluta'] == tabla_frecuencias_cat['Frecuencia_absoluta'].max()]
moda_cat.head()
```

🤔 **¿Qué puedes interpretar de los datos obtenidos?**

Comparte tus resultados con tus compañeros y discutan sobre las conclusiones obtenidas.

---

### 💡 **¿Sabías que?...**

Si requieres agregar las frecuencias acumuladas, puedes realizarlo de la siguiente manera:

```python
# Agregar las frecuencias acumuladas al dataframe de datos numéricos.
tabla_frecuencias_num['Frecuencia_absoluta_acumulada'] = tabla_frecuencias_num['Frecuencia_absoluta'].cumsum()
tabla_frecuencias_num['Frecuencia_relativa_acumulada'] = tabla_frecuencias_num['Frecuencia_relativa'].cumsum()

# Mostrar la tabla de frecuencias con las frecuencias acumuladas.
tabla_frecuencias_num.head(50)
```

```python
# Agregar las frecuencias acumuladas al dataframe de datos categóricos.
tabla_frecuencias_cat['Frecuencia_absoluta_acumulada'] = tabla_frecuencias_cat['Frecuencia_absoluta'].cumsum()
tabla_frecuencias_cat['Frecuencia_relativa_acumulada'] = tabla_frecuencias_cat['Frecuencia_relativa'].cumsum()

# Mostrar la tabla de frecuencias con las frecuencias acumuladas.
tabla_frecuencias_cat.head(50)
```

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Ejemplo-02/Readme.md) ➡️
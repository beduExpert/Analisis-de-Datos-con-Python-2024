🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 01**](../Readme.md) ➡️ / 📝 `Ejemplo 03: Cuartiles y Percentiles`

## 🎯 Objetivo

Entender y aplicar técnicas para calcular cuartiles y percentiles, utilizando datos estructurados en Python. Estos estimados nos ayudan a entender la distribución y la posición relativa de los datos dentro de un conjunto.

---

## 🚀 Comencemos

Los cuartiles y percentiles son medidas estadísticas que dividen los datos en partes iguales. Nos permiten entender cómo se distribuyen los datos e identificar la posición de un valor dentro de la distribución.

---

## 📊 **Cuartiles y percentiles** 📈

### **Cuartiles**

Los cuartiles dividen un conjunto de datos en cuatro partes iguales, cada una representando un cuarto de los datos. Los cuartiles principales son:

- **Primer cuartil (Q1)**: Representa el 25% inferior de los datos.
- **Segundo cuartil (Q2)**: Representa la mediana o el 50% de los datos.
- **Tercer cuartil (Q3)**: Representa el 75% inferior de los datos.



Vamos a calcular los cuartiles de la tarifa (`Fare`) de los pasajeros en el Titanic.

```python
# Importar librerías
import pandas as pd

# Cargar el dataset
df = pd.read_csv('../../Datasets/Titanic_Dataset.csv') # Modifica la ruta de acuerdo a tu entorno de trabajo

# Calcular los cuartiles de la tarifa
Q1_fare = df['Fare'].quantile(0.25)
Q2_fare = df['Fare'].quantile(0.50)
Q3_fare = df['Fare'].quantile(0.75)

print(f'Primer cuartil (Q1) de la tarifa: ${Q1_fare:.2f}')
print(f'Segundo cuartil (Q2) de la tarifa (mediana): ${Q2_fare:.2f}')
print(f'Tercer cuartil (Q3) de la tarifa: ${Q3_fare:.2f}')
```

---

### **Percentiles**

Los percentiles dividen un conjunto de datos en cien partes iguales. Por ejemplo, el percentil 90 indica que el 90% de los datos son menores o iguales a ese valor.

Vamos a calcular el percentil 90 de la edad (`Age`) de los pasajeros en el Titanic.

```python
# Eliminar valores NaN en la columna 'Age'
edad_sin_nan = df['Age'].dropna()

# Calcular el percentil 90 de la edad
percentil_90_edad = edad_sin_nan.quantile(0.90)

print(f'El percentil 90 de la edad de los pasajeros en el Titanic es: {percentil_90_edad:.2f} años')
```

---

### **Interpretación de los datos**

- **Primer Cuartil (Q1)**: El primer cuartil de la tarifa es \$7.90. Esto indica que el 25% de los pasajeros pagaron una tarifa de \$7.90 o menos.
- **Segundo Cuartil (Q2)**: El segundo cuartil, o mediana, de la tarifa es \$14.45. Esto significa que el 50% de los pasajeros pagaron una tarifa de \$14.45 o menos.
- **Tercer Cuartil (Q3)**: El tercer cuartil de la tarifa es \$31.50. Esto indica que el 75% de los pasajeros pagaron una tarifa de \$31.50 o menos.
- **Percentil 90**: El percentil 90 de la edad es 50.00 años. Esto significa que el 90% de los pasajeros tienen 50 años o menos.

---

### 💡 **¿Sabías que?...**

El análisis de cuartiles y percentiles es ampliamente utilizado en estadísticas y data science para entender la distribución de los datos y detectar valores extremos o atípicos. Estos estimados son particularmente útiles en estudios de población, análisis de rendimiento académico y estudios de mercado.

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Reto-03/Readme.md) ➡️
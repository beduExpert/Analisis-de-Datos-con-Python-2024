🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 01**](../Readme.md) ➡️ / 📝 `Ejemplo 01: Datos estructurados y estimados de locación`

## 🎯 Objetivo

Entender y aplicar técnicas para calcular y analizar estimados de locación, como la media, mediana y moda, utilizando datos estructurados en Python.

---

## 🚀 Comencemos

El módulo anterior se enfoco en procesar nuestros datasets para dejarlos limpios y ordenados. La principal razón fue para para extraer información útil de ellos. En este módulo aprendemos qué información podemos analizar e interpretar y cómo nos puede ser de utilidad.

Lo primero que veremos son estimados de locación y variabilidad. Pero para entender la razón por la que son útiles, primero necesitamos echar un vistazo a los tipos de datos estructurados con los que podemos trabajar.

---

## 📊 **Datos estructurados y estimados de locación** 📈

### **¿Qué son los datos estructurados?**

| Tipo de dato | Subtipo    | Descripción                                                                                                                                               |
|--------------|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Numéricos (cuantitativos) | Discretos  | Datos que sólo pueden tomar el valor de un número entero, como conteos o edades de personas.                                                 |
|              | Continuos  | Datos que pueden tomar cualquier valor dentro de un intervalo específico, como la temperatura o el salario.                                               |
| Categóricos (Cualitativos) | Binarios   | Datos categóricos que sólo tienen dos categorías posibles.                                                                                  |
|              | Nominales  | Datos categóricos que no tienen un orden explícito, como colores (rojo, azul, verde) o estado civil.                                                      |
|              | Ordinales  | Datos categóricos que tienen un orden explícito, como rankings de restaurantes.                                                                              |

---

### 📊 **Estimados de locación**

Los estimados de locación son medidas estadísticas que proporcionan información sobre el centro o la ubicación típica de un conjunto de datos. Los más comunes son la **media, mediana y moda**.



Que les parece si trabajamos con un dataset muy popular en el mundo de la programación, Titanic. Vamos a calcular la media, mediana y moda de la edad de los pasajeros.

Para realizar este análisis, primero necesitamos cargar el dataset a nuestra carpeta en google drive, para poder acceder desde nuestro entorno de trabajo en Google Colab.

**1. Descarga el archivo [Titanic_Dataset.csv](../../Datasets/Titanic_Dataset.csv) y súbelo a tu Google Drive.**

```python
# Importar librerías
import pandas as pd

# Cargar el dataset
df = pd.read_csv('../../Datasets/Titanic_Dataset.csv') # Modifica la ruta de acuerdo a tu entorno de trabajo

# Mostrar las primeras filas del dataset
df.head()
```

**2. Calculamos la media, mediana y moda de la edad de los pasajeros.**

```python
# Calcular la media
promedio_edad = df['Age'].mean()
print(f'El promedio de edad de los pasajeros en el Titanic fue: {promedio_edad}')

# Calcular la mediana
mediana_edad = df['Age'].median()
print(f'El valor central de la edad de los pasajeros en el Titanic fue: {mediana_edad}')

# Calcular la moda
moda_edad = df['Age'].mode()[0]
print(f'La edad más común de los pasajeros en el Titanic fue: {moda_edad}')
```

Hasta este momento ya hemos calculado la media, mediana y moda de la edad de los pasajeros del Titanic. Este tipo de análisis nos permite entender mejor como están distribuidos de los datos y nos da una idea de cómo se comportan.

Podemos inferir que la edad promedio de los pasajeros era de 29.7 años, la edad central fue de 28 años y la edad más común fue de 24 años.

---

### 💡 **¿Sabías que?...**

### 🔍 **Detección de fraudes y anomalías**

Las empresas financieras y de comercio electrónico usan la media, la mediana y la moda para identificar actividades fraudulentas en transacciones financieras.

**Caso real:**

Una compañía de tarjetas de crédito monitorea transacciones calculando la media, mediana y moda del gasto diario de un usuario.

1. **📊 Media**: Proporciona una idea general del gasto, pero es sensible a valores atípicos. Una transacción alta puede elevar la media significativamente.
2. **📈 Mediana**: Menos sensible a valores atípicos. Si media y mediana difieren mucho, puede haber transacciones anómalas.
3. **🔢 Moda**: Identifica patrones comunes. Si las transacciones habituales son pequeñas y aparece una grande, puede ser una señal de alarma.

### 🛡️ **Curiosidad**

Los analistas combinan estas medidas para crear un perfil de gasto normal. Si una transacción se desvía significativamente (por ejemplo, una transacción mucho mayor que la mediana y la moda, elevando la media), el sistema la marca como potencialmente fraudulenta, activando una revisión manual.

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Reto-01/Readme.md) ➡️
🏠 [**Inicio**](../Readme.md) ➡️ / 📖 `Sesión 05`

<div align="center">
    <img src="Imagenes/S05_Bedu.png" alt="Sesion_05">
</div>

## 🎯 Objetivo

⚒️ Comprender y aplicar distribuciones muestrales y técnicas de Bootstrap para estimar la precisión de las estadísticas de la muestra, calcular errores estándar y entender su importancia en la inferencia estadística, determinar intervalos de confianza para evaluar la precisión de las estimaciones, y aplicar técnicas de validación cruzada para evaluar la efectividad de los modelos predictivos.

---

📘 Material del prework: Antes de comenzar con los ejercicios de esta sesión, recordemos que en el material de prework hemos cubierto los fundamentos teóricos que aplicaremos hoy. A lo largo de esta sesión, pondremos en práctica estos conceptos mediante una serie de ejercicios y retos diseñados para reforzar y validar nuestro entendimiento. 🔥¡Vamos a comenzar!🔥

---

## 📂 Temas de la sesión...


### 📖 Error estándar e intervalos de confianza
El error estándar es una medida de la variabilidad o dispersión de una estadística muestral, como la media, con relación a la verdadera media poblacional. Se utiliza para cuantificar la precisión de la estimación de la estadística de muestra y se calcula como la desviación estándar de la distribución muestral.

El intervalo de confianza da una aproximación de los valores entre los cuales se encuentra el valor de un parámetro poblacional con un determinado nivel de confianza. Los intervalos de confianza más habituales tienen un nivel de confianza del 95% o del 99%.

#### 📜 **[Ejemplo 01: Error estándar e intervalos de confianza](Ejemplo-01/Readme.md)**

---

### 📖 Distribuciones muestrales y Bootstrap
También llamada distribución de muestreo describe la variabilidad de una estadística de muestra, como la media o la proporción, a través de múltiples muestras tomadas de la misma población. 

El método Bootstrap es una técnica de remuestreo que te permite estimar la precisión de las estadísticas de muestra, como la media o la mediana, sin hacer suposiciones sobre la distribución de la población.

#### 📜 **[Ejemplo 02: Distribuciones muestrales y Bootstrap](Ejemplo-02/Readme.md)**
#### 🔥 **[Reto 01:  Análisis de la distribución de recursos naturales](Reto-01/Readme.md)**

---

### 📖 Técnicas de evaluación de modelos
La evaluación de modelos predictivos es el proceso de medir y analizar el rendimiento de un modelo para asegurarse de que sus predicciones sean precisas y confiables. Esto quiere decir que el modelo es preciso, no sesgado y capaz de generalizar bien a datos nuevos.

**Precisión:** Proporción de verdaderos positivos sobre el total de predicciones positivas. Indica cuán exactas son las predicciones positivas del modelo.

**Recall (Sensibilidad):** Proporción de verdaderos positivos sobre el total de positivos reales. Mide la capacidad del modelo para identificar correctamente todas las instancias positivas. 

**F1 – score:** Media armónica de precisión y recall.  Ofrece un balance entre ambas métricas, siendo útil cuando necesitas considerar tanto la precisión como la sensibilidad del modelo

#### 📜 **[Ejemplo 03: Técnicas de evaluación de modelos](Ejemplo-03/Readme.md)**
#### 🔥 **[Reto 02:  Evaluación de modelos de predicción de recursos hídricos](Reto-02/Readme.md)**

---

### 📖 Validación cruzada
Es una técnica utilizada para evaluar la capacidad predictiva de un modelo y evitar el sobreajuste. Los métodos más comunes de validación cruzada son:

**K-Fold Cross-Validation:** Divide los datos en k subconjuntos (folds) de tamaño aproximadamente igual. El modelo se entrena k veces, cada vez utilizando k-1 folds para el entrenamiento y el fold restante para la evaluación.

**Leave-One-Out Cross-Validation (LOOCV):** Cada observación se utiliza una vez como conjunto de prueba mientras que el resto se utiliza como conjunto de entrenamiento. Esto resulta en tantas iteraciones como observaciones en el conjunto de datos.

**Stratified K-Fold Cross-Validation:** Similar a k-fold cross-validation, pero se asegura de que cada fold tenga la misma proporción de clases que el conjunto de datos original.

#### 📜 **[Ejemplo 04: Métodos de validación cruzada](Ejemplo-04/Readme.md)**

---

⬅️ [**Anterior**](../Sesion-04/Readme.md) | [**Siguiente**](../Sesion-06/Readme.md)➡️
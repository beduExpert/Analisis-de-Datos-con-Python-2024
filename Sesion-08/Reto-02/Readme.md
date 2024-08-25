🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 08**](../Readme.md) ➡️ / ⚡`Reto 02: Predicción de inseguridad futura en los estudios`

## 🎯 Objetivo

Aplicar el algoritmo de **regresión logística** para predecir la inseguridad futura de los estudiantes basada en variables relacionadas con la salud mental, como la depresión, ansiedad y aislamiento. Utilizarás la **matriz de confusión** y otras métricas de evaluación para analizar el rendimiento del modelo y entender mejor los factores que contribuyen a la inseguridad.

---

## 📝 Instrucciones

Tu tarea es analizar un dataset que contiene información sobre la salud mental de los estudiantes, incluyendo variables como la depresión, ansiedad y aislamiento, y cómo estas pueden predecir su inseguridad sobre el futuro. Implementarás el algoritmo de regresión logística para predecir la inseguridad futura y utilizarás herramientas de evaluación como la **matriz de confusión** para medir la efectividad del modelo. Utiliza el archivo [Reto_02_Mental_Health_Survey.csv](../../Datasets/S08/Reto_02_Mental_Health_Survey.csv).

Asegúrate de tener instaladas las librerías necesarias:

```bash
pip install pandas numpy scikit-learn matplotlib seaborn
```

**Tu reto es:**

1. **Preprocesamiento de datos**: 
   - Carga el dataset y selecciona las columnas relevantes para el análisis: `depression`, `anxiety`, `isolation` y `future_insecurity`.
   - Convierte la variable `future_insecurity` en binaria para su uso en la regresión logística, donde `1` indica alta inseguridad y `0` indica baja inseguridad o ausencia de inseguridad.

2. **Aplicación de la regresión logística**:
   - Implementa el algoritmo de regresión logística para predecir `future_insecurity` basada en las variables seleccionadas (`depression`, `anxiety`, `isolation`).
   - Divide los datos en conjuntos de entrenamiento y prueba para entrenar el modelo y validar su rendimiento.
   - Ajusta el modelo a los datos de entrenamiento y realiza predicciones en el conjunto de prueba.

3. **Evaluación del modelo**:
   - 📉 Calcula la **precisión** del modelo en el conjunto de prueba.
   - 📊 Genera una **matriz de confusión** para visualizar el rendimiento del modelo en términos de predicciones correctas e incorrectas.
   - 📑 Crea un **informe de clasificación** para evaluar métricas clave como precisión (precision), sensibilidad (recall) y F1 score, lo cual te ayudará a entender mejor cómo está funcionando el modelo en diferentes clases.

4. **Interpretación de los resultados**:
   - 📝 Analiza los resultados del modelo e interpreta qué tan bien predice la inseguridad futura basada en las variables de salud mental. Observa especialmente las métricas de la matriz de confusión para ver dónde el modelo tiene más aciertos y errores.
   - 🔍 Discute posibles intervenciones o enfoques que podrían ser útiles para los estudiantes con alta inseguridad futura basándote en los hallazgos del modelo. Considera estrategias de apoyo psicológico o programas de bienestar que aborden directamente los factores de salud mental más relevantes.

---

🏆 Nos vemos en el siguiente reto, ¡mucho éxito!

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Ejemplo-04/Readme.md) ➡️
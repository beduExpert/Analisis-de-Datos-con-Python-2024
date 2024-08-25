🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 08**](../Readme.md) ➡️ / ⚡`Reto 01: Segmentación de clientes por K-Medias`

## 🎯 Objetivo

Aplicar el algoritmo de **agrupamiento por K-Medias** para segmentar a los clientes en diferentes grupos basados en sus ingresos anuales y puntaje de gasto. Utilizarás visualizaciones para identificar patrones de comportamiento de los clientes que puedan ser útiles para estrategias de marketing más efectivas.

---

## 📝 Instrucciones

Tu tarea es analizar un dataset que contiene información sobre los clientes de un centro comercial, incluyendo sus ingresos anuales y puntaje de gasto. Utilizarás el algoritmo de K-Medias para agrupar a los clientes en segmentos basados en estos atributos y crearás visualizaciones para explorar los grupos formados. Utiliza el archivo [Reto_01_Mall_Customers.csv](../../Datasets/S08/Reto_01_Mall_Customers.csv).

Asegúrate de tener instaladas las librerías necesarias:

```python
!pip install pandas numpy scikit-learn matplotlib seaborn
```

**Tu reto es:**

1. **Preprocesamiento de datos**: Carga el dataset y selecciona las columnas relevantes para el análisis: `Annual Income (k$)` y `Spending Score (1-100)`. Asegúrate de que no hay valores nulos en estas columnas.

2. **Aplicación del K-Medias**: Implementa el algoritmo de K-Medias para segmentar a los clientes en 5 grupos. Ajusta el modelo a los datos seleccionados y asigna las etiquetas de los clusters a cada registro en el DataFrame.

3. **Visualización de los clusters**:
   - 🖼️ Crea un **scatterplot** que muestre los clientes agrupados según sus ingresos anuales y puntaje de gasto. Utiliza diferentes colores para representar cada uno de los clusters.
   - 📍 Añade los **centroides** de los clusters al gráfico para visualizar los puntos centrales de cada grupo.

4. **Interpretación de los resultados**:
   - 📝 Analiza los clusters formados e interpreta qué tipo de clientes representa cada grupo basándote en los ingresos y el puntaje de gasto.
   - 🔍 Discute posibles estrategias de marketing que podrían ser efectivas para cada segmento de clientes identificado.

---

🏆 Nos vemos en el siguiente reto, ¡mucho éxito!

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Ejemplo-02/Readme.md) ➡️
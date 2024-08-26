🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 07**](../Readme.md) ➡️ / 📝 `Ejemplo 03: Procesamiento de lenguaje natural (NLP)`

## 🎯 Objetivo

El objetivo es comprender cómo las computadoras pueden interactuar y entender el lenguaje humano de manera eficiente. A medida que aumenta la cantidad de datos textuales generados por la comunicación digital, como las reseñas de productos o comentarios en redes sociales, se hace necesario convertir estos textos en datos estructurados que se puedan analizar.

---

## 🚀 Comencemos

El **procesamiento de lenguaje natural (NLP)** es una rama de la inteligencia artificial que permite a las computadoras entender y interactuar con el lenguaje humano, convirtiendo textos en datos estructurados que pueden ser analizados para extraer información valiosa. Con el creciente volumen de datos textuales en plataformas digitales, el NLP facilita el análisis de opiniones, la clasificación de correos electrónicos, la traducción de idiomas, la extracción de información y la creación de chatbots, mejorando la eficiencia en procesos que dependen del lenguaje y permitiendo automatizar tareas repetitivas.

---

### 🛠️ **Text y FreqDist de NLTKr**

**NLTK (Natural Language Toolkit)** es una biblioteca de Python para procesamiento de lenguaje natural, que ofrece herramientas para analizar y manipular texto. 
- **Text** permite trabajar con texto tokenizado, facilitando tareas como búsqueda de palabras en contexto, análisis de frecuencia, y visualización de patrones en el lenguaje. 
- **FreqDist** se utiliza para calcular la distribución de frecuencias de los elementos en una lista, como palabras en un texto. Facilita tareas como el análisis de frecuencia de palabras, identificación de las palabras más comunes, y exploración de la diversidad léxica en el lenguaje.

Para aplicar esto, utilizaremos el archivo [Ejemplo_01_03_Amazon_Sales_Dataset.csv](../../Datasets/S07/Ejemplo_01_03_Amazon_Sales_Dataset.csv) que utilizamos en el ejemplo 01. Hagamos los siguientes pasos:

1. **Instalar NLTK:** Si no lo tienes instalado, puedes hacerlo ejecutando.
    ```python
    # Instalar NLTK
    !pip install nltk

    # Descargar los recursos necesarios
    nltk.download('punkt')
    ```

2. **Cargar los datos y preprocesar:**

    ```python
    # Asegúrate de tener nltk instalado y descarga los recursos necesarios
    import nltk
    nltk.download('punkt')

    import pandas as pd
    import string
    from nltk.text import Text
    from nltk import FreqDist
    from nltk.tokenize import word_tokenize

    # Cargar el archivo CSV
    df = pd.read_csv('/Datos_ejemplo01y03_WorkS07_amazon_sales_dataset.csv')

    # Preprocesamiento: Convertir a minúsculas y eliminar signos de puntuación
    df['Review_clean'] = df['Review'].str.lower().str.translate(str.maketrans('', '', string.punctuation))
    ```

    **df:**
    - Función **.str.lower():** convierte todo el texto de la columna "Review" a minúsculas, lo que ayuda a unificar el texto y evitar que palabras como "Producto" y "producto" se traten como diferentes.
    - Función **.str.translate(str.maketrans('', '', string.punctuation)):** elimina todos los signos de puntuación del texto, como comas, puntos, signos de interrogación, etc. Esto se hace para limpiar el texto y facilitar su análisis, eliminando caracteres que no son necesarios para la mayoría de las tareas de procesamiento de lenguaje natural.

    <br>

3. **Tokenización:**

    ```python
    # Tokenizar las reseñas
    tokens = word_tokenize(' '.join(df['Review_clean'].dropna()))
    ```

    - **word_tokenize:** es una función de la biblioteca NLTK que divide un texto en palabras individuales o "tokens". Esta técnica se llama Tokenización.
    - **df['Review_clean'].dropna():** Este comando toma la columna Review_clean del DataFrame df y elimina cualquier valor nulo que pueda existir.
    - **' '.join(df['Review_clean'].dropna()):** Une todas las reseñas limpias en una sola cadena de texto grande, separando cada reseña con un espacio.
    - **word_tokenize(...):** Aplica la tokenización al texto unido, dividiendo esta gran cadena en una lista de palabras individuales (tokens).

    <br>

4. **Crear un objeto Text y calcular la distribución de frecuencias:**

    ```python
    # Crear un objeto Text de NLTK
    text_nltk = Text(tokens)

    # Funcionalidades de Text
    # 1. Buscar palabras en contexto
    text_nltk.concordance('wonderful')

    # 2. Buscar palabras similares
    text_nltk.similar('product')

    # 3. Generar dispersión de palabras
    # Nota: Esta línea produce un gráfico que se mostrará en tu entorno local
    text_nltk.dispersion_plot(['product', 'quality', 'recommend', 'value'])

    # 4. Contar el total de palabras y la cantidad de palabras únicas
    total_tokens = len(text_nltk)
    unique_tokens = len(set(text_nltk))
    print(f"Total de tokens: {total_tokens}")
    print(f"Cantidad de tokens únicos: {unique_tokens}")
    ```

    **Con Text, tenemos varias funcionalidades, algunas de ellas son:**
    - **Buscar palabras en contexto**
    text_nltk.concordance('palabra'): Muestra las ocurrencias de una palabra en el texto junto con su contexto, lo que es útil para entender cómo se utiliza esa palabra.

    - **Buscar palabras similares**
    text_nltk.similar('palabra'): Encuentra palabras que aparecen en contextos similares a la palabra especificada, lo que puede ayudar a descubrir sinónimos o términos relacionados en el texto.

    - **Generar dispersión de palabras**
    text_nltk.dispersion_plot(['palabra1', 'palabra2']): Crea un gráfico de dispersión que muestra las posiciones de las palabras en el texto, útil para analizar la distribución de términos clave a lo largo de un documento.

    - **Contar el total de palabras y la cantidad de palabras únicas**
    len(text_nltk): Devuelve el número total de tokens en el texto, útil para medir el tamaño del corpus.
    len(set(text_nltk)): Calcula el número de palabras únicas en el texto, lo que da una idea de la diversidad léxica.

    <br>

5. **Crear un objeto FreqDist y funcionalidades:**

    ```python
    #FreqDisq y funcionalidades

    # Crear un objeto FreqDist para análisis de frecuencia de palabras
    fdist = FreqDist(text_nltk)

    # Funcionalidades de FreqDist
    # 1. Mostrar todas las palabras únicas
    unique_words = list(fdist.keys())
    print(f"Palabras únicas (muestra): {unique_words[:10]}")  # Muestra solo las primeras 10 palabras únicas

    # 2. Filtrar palabras según su frecuencia (hapaxes)
    hapaxes = fdist.hapaxes()
    print(f"Hapaxes (muestra): {hapaxes[:10]}")  # Muestra solo las primeras 10 hapaxes

    # 3. Gráfico de palabras más comunes
    # Nota: Esta línea produce un gráfico que se mostrará en tu entorno local
    fdist.plot(30, cumulative=False)

    # 4. Acceder a la frecuencia de una palabra específica
    frequency_of_product = fdist['product']
    print(f"Frecuencia de la palabra 'product': {frequency_of_product}")
    ```

    **Con FreqDist, tenemos varias funcionalidades, algunas de ellas son:**
    - **Mostrar todas las palabras únicas**
    fdist.keys(): Devuelve todas las palabras únicas encontradas en el texto.

    - **Filtrar palabras según su frecuencia**
    fdist.hapaxes(): Devuelve una lista de palabras que solo aparecen una vez en el texto, conocidas como "hapax legomena".
    fdist.plot(30, cumulative=False): Genera un gráfico de las 30 palabras más comunes y su frecuencia, lo que ayuda a visualizar la distribución de palabras.

    - **Acceder a la frecuencia de una palabra específica**
    fdist['palabra']: Proporciona la frecuencia de una palabra específica en el texto, lo que es útil para análisis más detallados.


---

### 💡 **¿Sabías que?...**

El **procesamiento de lenguaje natural (NLP)** es una disciplina que combina la lingüística, la informática y la inteligencia artificial para permitir a las computadoras entender, interpretar y generar lenguaje humano de manera eficiente. Algunas aplicaciones comunes de NLP incluyen:

- **Análisis de sentimientos:** Identificar emociones y opiniones en textos, como reseñas de productos o comentarios en redes sociales.
- **Extracción de información:** Identificar y extraer información relevante de textos, como nombres de personas, fechas o lugares.
- **Traducción automática:** Convertir texto de un idioma a otro, facilitando la comunicación entre personas que hablan diferentes idiomas.
- **Generación de texto:** Crear contenido de manera automática, como resúmenes de texto, respuestas a preguntas o diálogos de chatbots.

Prácticamente es la base de los LLMs (Large Language Models) como GPT-3, BERT, entre otros.

---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Reto-03/Readme.md) ➡️
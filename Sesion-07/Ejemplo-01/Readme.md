🏠 [**Inicio**](../../Readme.md) ➡️ / 📖 [**Sesión 07**](../Readme.md) ➡️ / 📝 `Ejemplo 01: Expresiones regulares`

## 🎯 Objetivo

Desarrollar habilidades para utilizar expresiones regulares en Python, permitiendo la extracción y manipulación eficiente de patrones específicos en textos, como direcciones de correo electrónico, números de teléfono o fechas, facilitando el análisis de grandes volúmenes de datos textuales.

---

## 🚀 Comencemos

Las **expresiones regulares** permiten identificar y manipular patrones en textos, automatizando tareas complejas y mejorando el análisis de grandes volúmenes de datos textuales de manera rápida y precisa.

Algunos ejemplos sencillos son:
- Buscar URLs en un texto: Extraer todas las direcciones web (URLs) de un documento o un correo electrónico.
- Filtrar hashtags en redes sociales: Identificar y extraer hashtags específicos en publicaciones de redes sociales.
- Validar números de teléfono: Comprobar que los números de teléfono ingresados en un formulario siguen un formato correcto.


---

### 🛠️ **Sintaxis básica de expresiones regulares**
Para poder hacer uso de Regex en Python es necesario:

1.  **Importar el Módulo re**: Python tiene un módulo integrado llamado re que se utiliza para trabajar con expresiones regulares. También usaremos Pandas y cargaremos el dataset [Ejemplo_01_03_Amazon_Sales_Dataset.csv](../../Datasets/S07/Ejemplo_01_03_Amazon_Sales_Dataset.csv)

    ```python
    import pandas as pd
    import re

    # Cargar el dataset
    df = pd.read_csv('./Ejemplo_01_03_Amazon_Sales_Dataset.csv') # Modifica la ruta de acuerdo a tu entorno de trabajo
    
    # Mostrar las primeras filas del dataset
    df.head()
    ```

2. **Entender la sintaxis básica de las expresiones regulares:** Estas las revisamos en el Prework, ¿las recuerdas?

    | Tipo | Función | Ejemplo |
    |------|---------|---------|
    | `^` / `$` | Indican el inicio (`^`) y el final (`$`) de una línea en un texto. | `^Hola` busca la palabra "Hola" solo si está al principio de una línea. |
    | `.` | Representa cualquier carácter, excepto una nueva línea. | `h.t` coincidirá con "hat", "hit", "hot", etc. |
    | `\s` / `\S` | `\s` representa un espacio en blanco (como espacios, tabulaciones), mientras que `\S` representa cualquier carácter que no sea un espacio en blanco. | `\sHola` buscaría "Hola" solo si está precedida por un espacio. |
    | `*` | Indica la repetición de un carácter cero o más veces. | `ho*la` coincidiría con "hla", "hola", "hoooola", etc. |
    | `+` | Indica la repetición de un carácter una o más veces. | `ho+la` coincidirá con "hola", "hoola", "hoooola", pero no con "hla". |
    | `?` | Hace que el carácter anterior sea opcional, coincidiendo con cero o una vez. | `colou?r` coincidirá con "color" y "colour". |
    | `[ ]` | Indican un conjunto de caracteres, cualquiera de los cuales puede coincidir. | `[abc]` coincidirá con "a", "b" o "c". |
    | `( )` | Agrupan partes de un patrón, permitiendo realizar coincidencias complejas o capturar subcadenas. | `(abc)+` coincidirá con "abc", "abcabc", etc. |

    <br>

3.  **Usar funciones del módulo re:** Estas también las revisamos en el Prework. 
    - re.findall(): Encuentra todas las ocurrencias de un patrón en una cadena y las devuelve como una lista.

    - re.search(): Busca la primera ocurrencia de un patrón en una cadena.

    - re.split(): Divide una cadena en partes utilizando un patrón como delimitador.

    <br>

4.  **Practicar diversas expresiones regulares:**

    **Ejemplos con re.findall**

    - Buscar direcciones de correo electrónico
        - La función `find_gmail_emails()` devuelve `True` si se encuentra al menos una coincidencia (es decir, si el correo electrónico pertenece a Gmail), o `False` si no se encuentra ninguna coincidencia.
        - La función `apply()` se usa para aplicar find_gmail_emails() a cada elemento en la columna `Customer Email`.
        - Los resultados booleanos `(True o False)` se utilizan para filtrar el DataFrame, seleccionando solo las filas donde la función devuelve True.
        - df_result contendrá solo los registros que tienen correos electrónicos de Gmail.


---

⬅️ [**Anterior**](../Readme.md) | [**Siguiente**](../Ejemplo-02/Readme.md) ➡️

páginas de referencia usadas: 

-- Para el uso de la API --
https://www.kaggle.com/docs/api
https://www.youtube.com/watch?v=hzcV0hDkfzs
https://www.youtube.com/watch?v=u2Ms34GE14U
https://medium.com/%40vinaychavda.de/a-guide-to-extracting-data-from-kaggle-for-your-data-science-projects-e15ef8ffc054
https://lerner.co.il/2018/07/24/avoiding-windows-backslash-problems-with-pythons-raw-strings/ #problema con API para leer dónde dejar el archivo

-- Ítem 3.1 --
cheatsheet pandas en Python del curso
https://www.youtube.com/watch?v=4YI9z1qUpew
https://datascientest.com/es/que-es-un-dataframe #datos faltantes
https://learn.microsoft.com/es-es/dotnet/api/system.data.dataset.merge?view=netframework-4.8 
https://www.youtube.com/watch?v=yAo6QlSRXjA
https://interactivechaos.com/es/manual/tutorial-de-pandas/dataframes-la-funcion-merge

Pregunta a ChatGPT: "En el contexto de reemplazar una columna de una base de datos, llamémosla A, con la información de otra base datos, llamémosla B, siendo A y B archivos .csv, si se utiliza la función de pandas merge(), ¿Queda la información de las columnas B en el lugar original de A o se abre otra columna "al final" de la base de datos? Toma en cuenta que el archivo B tiene dos columnas, la primera teniendo un número y la segunda un nombre asociado, y la idea es cambiar los números de la columna A correspondiente a los nombres de la segunda columna B." Respuesta: "Gracias por el contexto, está muy claro. Vamos a analizarlo paso a paso.

---

### ? Objetivo:

Quieres reemplazar en el archivo **A** una columna que contiene **números**, con los **nombres asociados** que se encuentran en el archivo **B**, que actúa como una tabla de equivalencias (diccionario).

Supongamos:

#### Archivo A (`A.csv`):

| ID | Valor | Código |
| -- | ----- | ------ |
| 1  | 10    | 101    |
| 2  | 15    | 102    |
| 3  | 20    | 103    |

#### Archivo B (`B.csv`):

| Código | Nombre     |
| ------ | ---------- |
| 101    | Producto A |
| 102    | Producto B |
| 103    | Producto C |

Quieres que la columna `Código` de A (que tiene números) sea reemplazada por la columna `Nombre` de B (texto).

---

### ?? ¿Qué hace `merge()`?

La función `pandas.merge()` **añade columnas** a la tabla resultante, no reemplaza directamente. Pero tú puedes controlar qué columnas se conservan y cuáles se eliminan después del `merge`.

---

### ??? Ejemplo práctico:

```python
import pandas as pd

# Cargar los archivos
df_a = pd.read_csv("A.csv")
df_b = pd.read_csv("B.csv")

# Hacemos el merge entre df_a y df_b usando la columna 'Código'
df_merged = pd.merge(df_a, df_b, on="Código", how="left")

# Opcional: eliminar la columna 'Código' si ya no la necesitas
df_merged.drop(columns=["Código"], inplace=True)

# Renombrar la columna 'Nombre' como 'Código' si quieres mantener el mismo nombre
df_merged.rename(columns={"Nombre": "Código"}, inplace=True)
```

---

### ?? Resultado:

| ID | Valor | Código     |
| -- | ----- | ---------- |
| 1  | 10    | Producto A |
| 2  | 15    | Producto B |
| 3  | 20    | Producto C |

---

### ? Conclusión:

* `merge()` **agrega** columnas; **no reemplaza en el mismo lugar automáticamente**.
* Si quieres reemplazar, debes **eliminar la columna original** y **renombrar** la nueva, como en el ejemplo.
* Esto te permite transformar fácilmente identificadores por descripciones o nombres, como es tu caso.

¿Quieres que te ayude a generar el script completo según tus nombres de archivo y columnas reales?"
- BIBLIOGRAFIA -

Fuentes extras usadas no correspondientes a ninguna carpeta del curso.

-> Para el uso de la API:
https://www.kaggle.com/docs/api
https://www.youtube.com/watch?v=hzcV0hDkfzs
https://www.youtube.com/watch?v=u2Ms34GE14U
https://medium.com/%40vinaychavda.de/a-guide-to-extracting-data-from-kaggle-for-your-data-science-projects-e15ef8ffc054
https://lerner.co.il/2018/07/24/avoiding-windows-backslash-problems-with-pythons-raw-strings/

-> Item 3.1
https://www.youtube.com/watch?v=4YI9z1qUpew
https://datascientest.com/es/que-es-un-dataframe
https://learn.microsoft.com/es-es/dotnet/api/system.data.dataset.merge?view=netframework-4.8 
https://www.youtube.com/watch?v=yAo6QlSRXjA
https://interactivechaos.com/es/manual/tutorial-de-pandas/dataframes-la-funcion-merge

Pregunta a ChatGPT: "En el contexto de reemplazar una columna de una base de datos, llamemosla A, 
con la informacion de otra base datos, llamemosla B, siendo A y B archivos .csv, si se utiliza la 
funcion de pandas merge(), queda la informacion de las columnas B en el lugar original de A o se 
abre otra columna "al final" de la base de datos? Toma en cuenta que el archivo B tiene dos
columnas, la primera teniendo un numero y la segunda un nombre asociado, y la idea es cambiar los
numeros de la columna A correspondiente a los nombres de la segunda columna B." 

Respuesta: "Gracias por el contexto, est� muy claro. Vamos a analizarlo paso a paso.

---

### ? Objetivo:

Quieres reemplazar en el archivo **A** una columna que contiene **n�meros**, con los **nombres asociados** que se encuentran en el archivo **B**, que act�a como una tabla de equivalencias (diccionario).

Supongamos:

#### Archivo A (`A.csv`):

| ID | Valor | C�digo |
| -- | ----- | ------ |
| 1  | 10    | 101    |
| 2  | 15    | 102    |
| 3  | 20    | 103    |

#### Archivo B (`B.csv`):

| C�digo | Nombre     |
| ------ | ---------- |
| 101    | Producto A |
| 102    | Producto B |
| 103    | Producto C |

Quieres que la columna `C�digo` de A (que tiene n�meros) sea reemplazada por la columna `Nombre` de B (texto).

---

### ?? �Qu� hace `merge()`?

La funci�n `pandas.merge()` **a�ade columnas** a la tabla resultante, no reemplaza directamente. Pero t� puedes controlar qu� columnas se conservan y cu�les se eliminan despu�s del `merge`.

---

### ??? Ejemplo pr�ctico:

```python
import pandas as pd

# Cargar los archivos
df_a = pd.read_csv("A.csv")
df_b = pd.read_csv("B.csv")

# Hacemos el merge entre df_a y df_b usando la columna 'C�digo'
df_merged = pd.merge(df_a, df_b, on="C�digo", how="left")

# Opcional: eliminar la columna 'C�digo' si ya no la necesitas
df_merged.drop(columns=["C�digo"], inplace=True)

# Renombrar la columna 'Nombre' como 'C�digo' si quieres mantener el mismo nombre
df_merged.rename(columns={"Nombre": "C�digo"}, inplace=True)
```

---

### ?? Resultado:

| ID | Valor | C�digo     |
| -- | ----- | ---------- |
| 1  | 10    | Producto A |
| 2  | 15    | Producto B |
| 3  | 20    | Producto C |

---

### ? Conclusi�n:

* `merge()` **agrega** columnas; **no reemplaza en el mismo lugar autom�ticamente**.
* Si quieres reemplazar, debes **eliminar la columna original** y **renombrar** la nueva, como en el ejemplo.
* Esto te permite transformar f�cilmente identificadores por descripciones o nombres, como es tu caso.

�Quieres que te ayude a generar el script completo seg�n tus nombres de archivo y columnas reales?"

-> Item 3.2:
https://www.britishmuseum.org/blog/top-10-historical-board-games
https://en.wikipedia.org/wiki/Senet
Crist, Walter. "Debunking the Diffusion of Senet." Board Game Studies Journal, 2021.
https://stackoverflow.com/questions/13187778/convert-pandas-dataframe-to-numpy-array
https://docs.vultr.com/python/third-party/numpy/ptp
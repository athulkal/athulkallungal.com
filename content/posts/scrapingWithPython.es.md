+++
title = 'Cómo extraer tablas de la web'
date = 2023-10-13T02:20:06+01:00
draft = false
categories = ["Python"]
showReadingTime = true
ShowShareButtons = true
+++

¿Cómo extraer datos de una tabla?

Este artículo es una guía definitiva para extraer datos de tablas de sitios web utilizando Python. Para empezar, necesitas tener Python instalado, y también algunos paquetes, concretamente `BeautifulSoup` y `Pandas` .

BeautifulSoup es una librería popular para el web scraping y el análisis de documentos HTML o XML.
Pandas es una librería muy utilizada en Python para la manipulación y análisis de datos.

Puedes instalar ambos paquetes usando el comando `pip install`. Ejecutando `pip install bs4` y `pip install pandas` debería ser suficiente. Si surge algún problema durante la instalación, tendrás que buscar información en internet sobre cómo solucionarlo.

Si lo necesitas, también puedes instalar Jupyter Notebook, ya que al trabajar con pandas facilita la visualización de los datos, aunque no es obligatorio. Puedes seguir el tutorial con un editor de código como VS Code o cualquier otro.

Primero necesitamos importar BeautifulSoup desde el módulo bs4. Y, si aún no lo tienes instalado, también debes instalar requests con `pip install requests`

```
from bs4 import BeautifulSoup
import requests

```

Para este ejemplo, voy a usar la base de datos de Pokémon como la tabla que vamos a extraer. Puedes verla [**aquí**](https://pokemondb.net/pokedex/all).

```
page = requests.get('https://pokemondb.net/pokedex/all')
soup = BeautifulSoup(page.text,'html')

```

A continuación, hacemos una petición GET a la página donde se encuentra la tabla que contiene los datos. Después, analizamos el contenido HTML de la página y lo convertimos en un objeto BeautifulSoup que podremos manipular más adelante.

El siguiente paso es inspeccionar la página haciendo clic derecho y seleccionando “Inspeccionar elemento”.

En esta tabla concreta, hay un atributo `id`, lo que facilita seleccionar el elemento. Si hubiera una clase, tampoco sería un problema; aunque en algunos casos varias filas pueden compartir el mismo nombre de clase, en cuyo caso usaríamos el método `find_all` y accederíamos mediante índices.

`titles = table.find_all('th')`

Si imprimimos esto, veremos una salida como la siguiente:

```
[<th class="sorting" data-sort="int"><div class="sortwrap">#</div></th>,
 <th class="sorting" data-sort="string"><div class="sortwrap">Name</div></th>,
 <th><div class="sortwrap">Type</div></th>,
 <th class="sorting" data-sort="int"><div class="sortwrap">Total</div></th>,
 <th class="sorting" data-sort="int"><div class="sortwrap">HP</div></th>,
 <th class="sorting" data-sort="int"><div class="sortwrap">Attack</div></th>,
 <th class="sorting" data-sort="int"><div class="sortwrap">Defense</div></th>,
 <th class="sorting" data-sort="int"><div class="sortwrap">Sp. Atk</div></th>,
 <th class="sorting" data-sort="int"><div class="sortwrap">Sp. Def</div></th>,
 <th class="sorting" data-sort="int"><div class="sortwrap">Speed</div></th>]

```

Esto es una lista y contiene todos los encabezados de las columnas. Podemos obtenerlos recorriéndolos en un bucle y accediendo a su propiedad `.text`.

```
table_titles = []
for title in titles:
    table_titles.append(title.text.strip())

```

Recorremos la lista y añadimos cada elemento a la lista `table_titles`. Usamos el método `strip()` para eliminar los saltos de línea y espacios innecesarios.

Si imprimimos `table_titles`, veremos algo como:

```
['#',
 'Name',
 'Type',
 'Total',
 'HP',
 'Attack',
 'Defense',
 'Sp. Atk',
 'Sp. Def',
 'Speed']

```

Ahora tenemos los nombres de las columnas.

El siguiente paso es crear un DataFrame. Para ello, importamos la librería pandas:

```
import pandas as pd
df = pd.DataFrame(columns = table_titles)

```

Esta línea crea un DataFrame con los encabezados de columna que definimos anteriormente.

Ahora viene la parte más complicada: obtener las filas de datos. Si inspeccionas la página en Chrome DevTools, verás que cada fila está representada por una etiqueta `tr` (table row), y dentro de cada una hay etiquetas `td` (table data), que contienen la información que necesitamos. Vamos a dos niveles de profundidad.

`column_data = table.find_all('tr')`

Esto devuelve todas las filas de la tabla como una lista. Ahora debemos recorrer cada una y extraer los datos.

```
for row in column_data[1:]:
    row_data = row.find_all('td')
    individual_row_data = [data.text.strip() for data in row_data]
    length = len(df)
    df.loc[length] = individual_row_data

```

Vamos línea por línea:

- El bucle empieza recorriendo las filas, ignorando la primera porque parece estar vacía o no contiene datos útiles.
- Luego encontramos todos los elementos `td` dentro de cada fila `tr`.
- Usamos una comprensión de listas para limpiar el texto y almacenarlo.
- Finalmente, insertamos cada fila en el DataFrame usando `df.loc`, utilizando la longitud actual del DataFrame como índice.

Después de todas las iteraciones, tendremos una tabla completa lista para usar.

Si quieres exportarla a CSV, puedes hacerlo así:

`df.to_csv('ruta/del/archivo.csv', index=False)`

Debes especificar la ruta donde quieres guardar el archivo. Usamos `index=False` porque no queremos incluir la columna de índices en el archivo final.

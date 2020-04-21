`Estadistica-Programacion-con-R` > [`Programacion con R`] > [`Sesion-03`] > [`Actividad-05`] 

### OBJETIVO
- Tomar datos de url(tablas) y archivos xml y .json (fetch) desde Rstudio.

#### REQUISITOS
1. Contar con R studio.
1. Usar la carpeta de trabajo `Sesion03/Ejemplo-05`

#### DESARROLLO

### Leer archivos JSON en R

Para obtener archivos JSON en R, primero debes instalar o cargar el paquete rjson. 

Una vez hecho esto, puedes usar la función fromJSON(). Aquí tienes dos opciones:

- Tu archivo JSON se almacena en tu directorio de trabajo:
```{r}
# Activate `rjson`
library(rjson)

# Import data from json file
JsonData <- fromJSON(file= "<filename.json>" )
````
- Tu archivo JSON está disponible a través de una URL:
```{r}
# Activate `rjson`
library(rjson)

# Import data from json file
JsonData <- fromJSON(file= "<URL to your JSON file>" )
````
#### Leer datos XML en R
Si deseas obtener datos XML en R, una de las formas más fáciles es mediante el uso del paquete XML. Primero, asegúrate de instalar y cargar el paquete XML en tu espacio de trabajo, tal como se demostró anteriormente. Luego, puedes usar xmlTreeParse() para analizar el archivo XML directamente desde la web:

```{r}
# Activate the `XML` library
library(XML)

# Parse the XML file
xmlfile <- xmlTreeParse("<Your URL to the XML data>")
```
Notarás que los datos se presentan de forma extraña al imprimir el xmlfilevector. Esto se debe a que el archivo XML sigue siendo un documento XML real en R en este momento. Para poner los datos en un marco de datos, primero debes extraer los valores XML. Puedes usar la xmlSApply()función para hacer esto:

```{r}
topxml <- xmlSApply(topxml,
                    function(x) xmlSApply(x, xmlValue))
```         
El primer argumento de esta función será topxml, ya que es el nodo superior en cuyos hijos desea realizar una determinada función. Luego, enumera la función que desea aplicar a cada nodo secundario. En este caso, desea extraer el contenido de un nodo XML hoja. Esto, en combinación con el primer argumento topxml, asegurará que hagas esto para cada nodo XML.
¡Finalmente, pones los valores en un marco de datos!

```{r}
xml_df <- data.frame(t(topxml),
                     row.names=NULL)
````

Si crees que los pasos anteriores son demasiado complicados, simplemente haz lo siguiente:
```{r}
url <- "<a URL with XML data>"
data_df <- xmlToDataFrame(url)
````

### Importar datos de tablas HTML a R
De las tablas HTML a R es bastante sencillo:

```{r}
# Assign your URL to `url`
url <- "<a URL>"

# Read the HTML table
data_df <- readHTMLTable(url,
                         which=3)
````
Ten en cuenta que which te permite especificar qué tablas devolver desde dentro del documento.

Si esto te da un error en la naturaleza de "no se pudo cargar la entidad externa", no te preocupes: este error ha sido señalado por muchas personas y ha sido confirmado por el autor del paquete.

Puedes solucionar esto utilizando RCurl  en combinación con el paquete XML para leer sus datos:

```{r}
# Activate the libraries
library(XML)
library(RCurl)

# Assign your URL to `url`
url <- "YourURL"

# Get the data
urldata <- getURL(url)

# Read the HTML table
data <- readHTMLTable(urldata,
                      stringsAsFactors = FALSE)
````
¡Ten en cuenta que no deseas que las cadenas se registren como factores o variables categóricas! También puedes usar el paquete httr para lograr exactamente lo mismo, excepto por el hecho de que querrás convertir los objetos sin procesar del contenido de la URL en caracteres mediante el rawToChar argumento:

```{r}
# Activate `httr`
library(httr)

# Get the URL data
urldata <- GET(url)

# Read the HTML table
data <- readHTMLTable(rawToChar(urldata$content),
                      stringsAsFactors = FALSE)
````


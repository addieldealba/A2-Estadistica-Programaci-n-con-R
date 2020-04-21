`Estadistica-Programacion-con-R` > [`Programacion con R`] > [`Sesion-03`] > [`Actividad-02`] 

### OBJETIVO
- Utilizar dplyr y DBI para hacer queries a MySQL.

#### REQUISITOS
1. Contar con R studio.
1. Usar la carpeta de trabajo `Sesion03/Ejemplo-02`

#### DESARROLLO

#### Utilizar dplyr y DBI para hacer queries a MySQL

Hay cuatro paquetes que necesita en esta serie de artículos. Aquí están las instrucciones de instalación, para que su código funcione sin problemas:

```{r}
# get shiny, DBI, dplyr and dbplyr from CRAN
install.packages("shiny")
install.packages("DBI")
install.packages("dplyr")
install.packages("dbplyr")

# get pool from GitHub, since it's not yet on CRAN
devtools::install_github("rstudio/pool")
```
#### Visión general

A medida que las aplicaciones Shiny crecen y se vuelven más complejas, un problema recurrente ha sido el de integrar una base de datos externa en una aplicación. Si bien esto ya es posible, hasta ahora depende principalmente de los autores de la aplicación averiguar el controlador de base de datos apropiado para R y cómo administrar las conexiones de la base de datos dentro de la propia aplicación. 

En particular, cubriremos:

- Cómo usar el paquete dplyr para leer datos de una base de datos externa;

- Cómo usar el paquete DBI para conectar a una base de datos externa;

- Cómo prevenir inyecciones SQL;

- Cómo administrar las conexiones, evitar fugas y garantizar el mejor rendimiento con el poolpaquete;

- Cómo integrar el poolpaquete con dplyr.

Tenga en cuenta que no siempre es ideal vincular a una base de datos externa, ya que puede romperse y ciertamente es más costoso desde el punto de vista computacional que tratar con datos locales. Para citar a Hadley sobre cuándo usar dplyrcon bases de datos frente a datos en memoria :

Además de trabajar con datos locales en memoria almacenados en marcos de datos, dplyr también trabaja con datos remotos en disco almacenados en bases de datos. Esto es particularmente útil en dos escenarios:

Sus datos ya están en una base de datos.
Tiene tantos datos que no caben todos en la memoria simultáneamente y necesita usar algún motor de almacenamiento externo.
(Si sus datos encajan en la memoria, no hay ninguna ventaja en ponerlos en una base de datos: solo será más lento y más frustrante).

La forma más fácil de conectarse a una base de datos externa desde su aplicación es utilizarla dplyr. 

La motivación para admitir bases de datos en dplyr es que nunca extrae el subconjunto o agregado correcto de la base de datos la primera vez, y generalmente debe iterar entre R y SQL muchas veces antes de obtener el conjunto de datos perfecto. Cambiar entre idiomas es un desafío cognitivo (especialmente porque R y SQL son muy similares), por lo que dplyr le permite escribir código R que se traduce automáticamente a SQL. El objetivo de dplyr no es reemplazar todas las funciones SQL con una función R: eso sería difícil y propenso a errores. En cambio, dplyr solo genera sentencias SELECT, el SQL que escribe con mayor frecuencia como analista.

Aquí le mostramos cómo leer las primeras cinco filas de una tabla desde una base de datos remota:

```{r}
library(pool)
library(dplyr)

my_db <- dbPool(
  RMySQL::MySQL(), 
  dbname = "shinydemo",
  host = "shiny-demo.csa7qlmguqrf.us-east-1.rds.amazonaws.com",
  username = "guest",
  password = "guest"
)

# get the first 5 rows:
my_db %>% tbl("City") %>% head(5)
## # Source:   lazy query [?? x 5]
## # Database: mysql 10.0.17-MariaDB [guest@shiny-demo.csa7qlmguqrf.us-east-1.rds.amazonaws.com:/shinydemo]
##      ID           Name CountryCode      District Population
##   <dbl>          <chr>       <chr>         <chr>      <dbl>
## 1     1          Kabul         AFG         Kabol    1780000
## 2     2       Qandahar         AFG      Qandahar     237500
## 3     3          Herat         AFG         Herat     186800
## 4     4 Mazar-e-Sharif         AFG         Balkh     127800
## 5     5      Amsterdam         NLD Noord-Holland     731200

```
Como puede ver, es bastante sencillo.

Paquete DBI

Si necesita hacer algo más elaborado que SELECT consultas bastante simples , dplyr no podrá ayudarlo. En ese caso, le recomendamos encarecidamente que utilice DBIpara conectarse a su base de datos si hay un controlador adecuado. Aquí hay un dato sobre DBI de su página de github :

El paquete DBI define una interfaz común entre R y los sistemas de gestión de bases de datos (DBMS). La interfaz define un pequeño conjunto de clases y métodos similares en espíritu al DBI de Perl, JDBC de Java, DB-API de Python y ODBC de Microsoft. Define un conjunto de clases y métodos define qué operaciones son posibles y cómo se realizan:

conectar / desconectar al DBMS
crear y ejecutar declaraciones en el DBMS
extraer resultados / resultados de declaraciones
manejo de errores / excepciones
información (metadatos) de los objetos de la base de datos
gestión de transacciones (opcional)

Aquí hay un ejemplo de uso básico que destaca algunas de las capacidades DBI más comunes: establecemos una conexión a una base de datos, la consultamos, buscamos el conjunto de resultados, cerramos el conjunto de resultados y nos desconectamos cuando terminamos:

```{r}
library(DBI)
conn <- dbConnect(
    drv = RMySQL::MySQL(),
    dbname = "shinydemo",
    host = "shiny-demo.csa7qlmguqrf.us-east-1.rds.amazonaws.com",
    username = "guest",
    password = "guest")
rs <- dbSendQuery(conn, "SELECT * FROM City LIMIT 5;")
dbFetch(rs)
##   ID           Name CountryCode      District Population
## 1  1          Kabul         AFG         Kabol    1780000
## 2  2       Qandahar         AFG      Qandahar     237500
## 3  3          Herat         AFG         Herat     186800
## 4  4 Mazar-e-Sharif         AFG         Balkh     127800
## 5  5      Amsterdam         NLD Noord-Holland     731200
dbClearResult(rs)
dbDisconnect(conn)
```



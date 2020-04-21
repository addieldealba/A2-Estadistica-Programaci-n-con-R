`Estadistica-Programacion-con-R` > [`Programacion con R`] > [`Sesion-03`] > [`Actividad-02`] 

### OBJETIVO
- Integrar Rstudio con BDs mediante librerías, drivers (odbc drivers).

#### REQUISITOS
1. Contar con R studio.
1. Usar la carpeta de trabajo `Sesion03/Ejemplo-02`

#### DESARROLLO

#### MySQL

Hay dos opciones para conectarse a una base de datos MySQL:

- Usar el odbc package en R.
- Usando el RMariaDB package en R.

#### Usando el odbc package.

El odbc package, proporciona soporte DBI  y una conexión ODBC.

### Opciones de driver 

- MySQL : el sitio web oficial de MySQL proporciona un controlador ODBC descargable para MySQL: MySQL Connector

- MariaDB : MariaDB es una base de datos relacional de código abierto creada por los desarrolladores originales de MySQL. MariaDB proporciona un conector ODBC que se puede usar como reemplazo directo para un conector ODBC MySQL: conector MariaDB

- Controladores RStudio Professional : los usuarios de RStudio Server Pro, RStudio Connect o Shiny Server Pro pueden descargar y usar los controladores RStudio Professional sin costo adicional. Estos controladores incluyen un conector ODBC para bases de datos MySQL. RStudio ofrece controladores ODBC profesionales basados en estándares, compatibles. Utilice los Controladores RStudio Professional cuando ejecute R o Shiny con sus sistemas de producción. Consulte los Controladores RStudio Professional para obtener más información

#### CONFIGURACIONES DE CONEXIÓN

Hay 5 configuraciones necesarias para hacer una conexión:

devtools::install_github("r-dbi/odbc")

install.packages("shiny")
install.packages("DBI")
install.packages("dplyr")
install.packages("dbplyr")

Driver : consulte la sección previa de controladores para obtener información sobre la configuración
Server : una ruta de red al servidor de la base de datos
UID : nombre de usuario utilizado para acceder al servidor MySQL
PWD : la contraseña correspondiente al UID proporcionado
Port : debe establecerse en 3306

```{r}
# get DBI, dplyr and dbplyr from CRAN
devtools::install_github("r-dbi/odbc")
install.packages("shiny")
install.packages("DBI")
install.packages("dplyr")
install.packages("dbplyr")

con <- DBI::dbConnect(odbc::odbc(),
                      Driver   = "[your driver's name]",
                      Server   = "[your server's path]",
                      UID      = rstudioapi::askForPassword("Database user"),
                      PWD      = rstudioapi::askForPassword("Database password"),
                      Port     = 3306)
}
```
Usando el RMariaDB package


RMariaDB es una interfaz de base de datos y un controlador MariaDB para R. Esta versión tiene como objetivo el pleno cumplimiento de la especificación DBI , como reemplazo del RMySQL package anterior. Para obtener más información, visite RMariaDB el sitio oficial de: rmariadb.r-dbi.org

Para instalar desde CRAN:

```{r}
install.packages("RMariaDB")
The development version from github:
```
Para instalar la versión de desarrollo:

```{r}
# install.packages("remotes")
remotes::install_github("r-dbi/DBI")
remotes::install_github("r-dbi/RMariaDB")
```

Para conectar:
```{r}
library(DBI)
# Connect to my-db as defined in ~/.my.cnf
con <- dbConnect(RMariaDB::MariaDB(), group = "my-db")
```


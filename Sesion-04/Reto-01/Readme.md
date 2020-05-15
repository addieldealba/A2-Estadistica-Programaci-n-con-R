`Estadistica-Programacion-con-R` > [`Programacion con R`] > [`Sesion-04`] > [`Reto-01`] 

### OBJETIVO
- Aplicar los conocimientos adquiridos en las actividades para conectarnos a un repositorio propio y Base de Datos MySQL.
- Conectar a tu propio repositorio en git Gub y almacenar un archivo csv con datos de una BD propia.

#### REQUISITOS
1. Contar con RStudio.
1. Usar la carpeta de trabajo `Sesion04/Reto-01`

#### DESARROLLO

### Para este reto tienes que lograr los siguientes milestones.

1. Crea tu repostiorio de trabajo para este curso, si ya lo tienes ubica el URL.
2. Configura Git Hub para este repositorio en RStudio Desktop de la forma en que lo hicimos para RStudio Cloud.
3. Conectate a la BD de prueba que proporcionamos en los Ejemplos, si no la recuerdas aquí estan los datos de conexión.

```{r}
    con <- dbConnect(
      drv = RMySQL::MySQL(),
      dbname = "shinydemo",
      host = "shiny-demo.csa7qlmguqrf.us-east-1.rds.amazonaws.com",
      username = "guest",
      password = "guest")
```
4. Importa la tabla que esta accesible gratuitamente a un data.frame, después exportalo a .csv

Por ejemplo con la Tabla City,

```{r}
DataDB = dbGetQuery(con, "select * from City")
```

5. El archivo csv. guardalo en tu repositorio mediante un Push desde Git Hub Terminal o Git Hub Desktop.
       

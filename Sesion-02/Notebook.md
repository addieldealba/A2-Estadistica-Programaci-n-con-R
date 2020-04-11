[`Estadística con R`]> `General Notebooks: Estadística y Programacion con R`

## Work: Scripts con R

### OBJETIVOS DE LA SESIÓN

- Entender el concepto de script en R
- Utilizar un script para análisis de archivos
- Tomar un data set real y hacer preguntas interesantes sobre los datos
- Programar funciones para tareas comunes de lectura, escritura  de archivos con loops en R
- Saber como revisar (debug) un script en R paso a paso
- Utilizar funciones matemáticas en R 

#### ORGANIZACION DE LA SESIÓN

- Creación de un script en R con funciones y argumentos 
	- [Ejemplo 01](Ejemplo-01)

- Funciones append, completecases, rbind, list.files, vector, tipos de acceso a valores en dataframes
	- [Ejemplo 02](Ejemplo-02)
	- [Reto 02](Reto-02)

### OBJETIVO EJEMPLO 2
- Generar un script en R con tareas complejas implementadas mediante funciones

#### REQUISITOS EJEMPLO 2
1. Contar con R studio.
1. Usar la carpeta de trabajo `Sesion02/Ejemplo-02`

#### DESARROLLO EJEMPLO 2
En esta sección vamos a crear varias funciones con tareas de programación intermedia.

Limpiamos el workspace como buena práctica de programación:
```{r}
rm(list=ls())
```

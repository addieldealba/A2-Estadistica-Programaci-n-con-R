`Data Science` > [`Programacion con R`]
## Scripts con R

### OBJETIVO
- Generar un script en R con tareas complejas implementadas mediante funciones

#### REQUISITOS
1. Contar con R studio.
1. Usar la carpeta de trabajo `Sesion02/Ejemplo-02`

#### DESARROLLO

Limpiamos el workspace como buena práctica de programación:
```{r}
rm(list=ls())
```
Como ya conocemos, así es como se define una función en R:
```{r}
function_name <- function(arg1, arg2)
{
#	Manipular argumentos arg1 y arg2 de cierta forma
# y regresar un valor
}
```
Crea una funcion sencilla que regrese el valor del argumento:  
```{r}
boring_function <- function(x) {
  x
}
```
Si desea ver el código fuente de cualquier función, solo escriba el nombre de la función sin argumentos ni paréntesis. Probemos esto con la función que acaba de crear. Teclea: boring_function para ver su código fuente.
```{r}
boring_function
```

Vamos a usar la informacion de mtcars, ya disponible en R 
```{r}

```

Creamos la variable mtcars para poder hacer operaciones sobre esos datos 
```{r}
mtcars <- mtcars 
```

Selecciona las variables nombre del carro, millas por galon y horse power 
```{r}
select(mtcars, 'nombre carro', mpg, hp) 
```
Usamos las comillas para que detecte que es una palabra compuesta 


Filtra por aquellos vehiculos que tengan hp mayor a 200 y su nombre contenga la letra "a" 
```{r}
filter(mtcars, grepl("a", 'nombre carro') & hp > 200 )
```

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
#	Manipular argumentos arg1 y arg2 de cierta forma y regresar un valor
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

### Ahora hagamos un Script con R

Para esto hay que abrir el editor de scripts con un script nuevo:
![RScript](../images/RScript.png)

Ahora vamos a replicar la funcionalidad de la funcion mean(), creando nuestra propia función que haga lo mismo que mean()
```{r}
my_mean <- function(my_vector) {
  sum(my_vector)/length(my_vector)
  # Recuerda: la ultima expresion evaluada es lo que regresa R en sus funciones
}
```

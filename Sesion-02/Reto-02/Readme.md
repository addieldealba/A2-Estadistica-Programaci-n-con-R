`Estadistica-Programacion-con-R` > [`Programacion con R`] > [`Sesion-02`] > [`Reto-02`] 
### OBJETIVO RETO 2
- Generar un script en R con tareas complejas implementadas mediante funciones

#### REQUISITOS RETO 2
1. Contar con R studio.
1. Usar la carpeta de trabajo `Sesion02/Ejemplo-02`

#### DESARROLLO RETO 2
En esta sección vamos a crear varias funciones con tareas de programación intermedia.

Para esto hay que abrir el editor de scripts con un script nuevo:
![RScript](../images/RScript.png)

Limpiamos el workspace como buena práctica de programación:
```{r}
rm(list=ls())
```
Termine la definición de la función a continuación para que si una función se pasa alargumento "func" y algunos datos (como un vector) se pasan al argumento dat la función evaluate() devolverá el resultado de que se haya pasado como argumento para func.

Sugerencias: Este ejercicio es un poco complicado, así que daré algunos ejemplos de cómo evaluate () debe actuar:
1. evaluate(sum, c(2, 4, 6)) debe evaluar a 12
2. evaluate(median, c(7, 40, 9)) debe evaluar a 9
3. evaluate(floor, 11.1) debe evaluar a 11

Recuerda hacerlo en un script!

```{r}
evaluate <- función (func, dat) {
  # ¡Escribe tu código aquí!
  # Recuerde: ¡se devolverá la última expresión evaluada!
}
```
¡Hagamos girar su nueva función de evaluate()!. Utilice evaluate para encontrar la desviación estándar del vector c (1.4, 3.6, 7.9, 8.8).

Escriba el siguiente comando y luego discutiremos cómo funciona: evalúe (function (x) {x + 1}, 6)

[`Estadística con R`](../Readme.md) > `Sesión 07: Regresión Lineal`

## Modelo de Regresión Lineal

### OBJETIVO

Al final de el `Ejemplo-01` serás capaz de:
- Comprender el concepto de modelo Regresión Lineal 

### REQUISITOS

1. Completar el prework
2. R versión 3.6.2 o mayor
3. R Studio versión 1.2.5033 o mayor 
4. Git Bash


A. Que es Regresión Lineal ? : ´Una regresión lineal es una aproximación lineal de una relación causal entre dos o más variables´ 


Proceso para implementar un modelo de regresión lineal:
1. Obtener datos de un sampleo del origen de la población
2. Diseñar un modelo que funcione para ese dataset
3. Hacer predicciónes para toda la población
4. Tomar en cuenta la variable independiente que llamarémos Y y las independientes: x1,x2,x3,.....,xk

```r
library(tidyr)
library(ggplot2)

# Leer datos
breast.cancer <- read.csv('breast_cancer.csv')
```

B.

```r
# Contar el número de renglones del dataframe
nrow.df <- nrow(breast.cancer)
```
.

```r
# Sacar muestra sin reemplazo de los índices del 20% de todo el dataframe
idx.sample <- sample(nrow(breast.cancer), size = as.integer(nrow.df*0.2))

# Traer las observaciones del dataframe de los índices que salieron en la muestra
sample.df <- breast.cancer[idx.sample,]
```

C.

```r
# Vemos estructura del dataframe de los índices que salieron en la muestra
str(sample.df)
sample.df <- sample.df[,-c(1,2,3)]
```
